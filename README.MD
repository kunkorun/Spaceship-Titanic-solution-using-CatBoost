# Spaceship Titanic — CatBoost Solution

In this project, I tackle the quirky and fun [Kaggle Spaceship Titanic](https://www.kaggle.com/competitions/spaceship-titanic) competition. The goal is to predict which passengers were transported to an alternate dimension during the spaceship's collision with a spacetime anomaly.

While the premise is sci-fi, the data challenges are very real: messy categorical features, complex missing value patterns, and the need for robust feature engineering. I used this project to deeply explore gradient boosting on decision trees (specifically CatBoost) and to practice debugging real-world ML pipeline issues.

---

## Problem

This is a binary classification problem. The target variable is `Transported` (True/False), and the challenge lies in extracting meaningful signals from a mix of numerical, categorical, and heavily structured string features (like `Cabin` and `PassengerId`).

## Dataset

The project relies on the official Kaggle competition data. The repository contains the main project notebook and a dedicated `data/` directory for the raw CSV files.

## Workflow

To keep the experimentation structured, I followed a complete end-to-end machine learning pipeline:

1. Data Loading & Initial Audit
2. Data Cleaning & Missing Value Imputation
3. Exploratory Data Analysis (EDA)
4. Feature Engineering
5. Model Comparison (Baselines vs Advanced)
6. Hyperparameter Tuning
7. Final Model Selection
8. Kaggle Submission Generation

## Data Preprocessing

Handling missing values in this dataset required logical, domain-based reasoning rather than just blindly filling with medians. 

One of the key insights I used during preprocessing was the relationship between `CryoSleep` and onboard service spending: if a passenger is in cryosleep, they logically cannot spend money on RoomService, FoodCourt, ShoppingDeck, etc. Therefore, for passengers in cryosleep, I imputed missing spending values with `0`.

I also spent time fixing column types and ensuring strict train/test feature alignment, which is critical when working with strict libraries like CatBoost.

## Feature Engineering

Some of the most important features were hidden inside string columns. I拆解 (parsed) the `Cabin` feature to expose its internal spatial structure, creating three new distinct features:

- `Deck`
- `CabinNumber`
- `Side` (Port vs Starboard)

I also explored mapping `Deck` information to `HomePlanet` based on the strong conditional probabilities I observed during the EDA phase.

## Why CatBoost?

I tested several algorithms, but **CatBoost** emerged as the clear winner. It performed exceptionally well right out-of-the-box, handling the complex categorical features natively with minimal hyperparameter tuning.

However, integrating it smoothly required addressing a few specific implementation details:
- explicitly converting all categorical columns to `string` types to prevent silent type-casting errors
- utilizing `catboost.Pool` for both training and prediction to maintain categorical metadata
- strictly enforcing feature order alignment between the train and test sets

## Results

I tracked the performance of several models to establish a solid baseline before moving to complex algorithms.

| Model | Public Score | Notes |
|---|---|---|
| Logistic Regression | ~0.780 | Solid baseline model |
| Random Forest | ~0.800 | Noticeable improvement over the baseline |
| Tuned Random Forest | ~0.790 | Hyperparameter tuning actually degraded performance (overfitting) |
| **CatBoost** | **0.80032** | **Selected final model** |
| Tuned CatBoost | ~0.800 | No meaningful improvement over the default CatBoost parameters |

The final reported Kaggle score is **0.80032**. Interestingly, extensive tuning didn't beat the well-engineered baseline CatBoost, reinforcing the principle that feature engineering often beats hyperparameter tweaking.

## Bugs and Debugging

Real-world ML is messy, and I ran into several implementation hurdles that taught me a lot about pipeline robustness:

- **Pandas `FutureWarning`**: I encountered a warning related to implicit downcasting after using `fillna()`. I resolved this by explicitly converting the affected boolean columns using `.astype(bool)` to ensure type safety.
- **CatBoost Categorical Error**: CatBoost threw an error when it encountered the letter `"G"` in a column, mistakenly trying to parse it as a numerical value. I fixed this by strictly casting all categorical features to strings and wrapping the data in `catboost.Pool`.
- **Train/Test Column Mismatch**: After dropping or creating features, the train and test sets occasionally fell out of sync. I implemented explicit column alignment steps before passing the test set to the model for final predictions.

## Key Takeaways

This project reinforced several crucial lessons for my ML workflow:

- **Logic beats defaults**: Domain-based reasoning (like the CryoSleep spending logic) is vastly superior to blind imputation for missing values.
- **Feature Engineering is king**: Parsing structured strings (like `Cabin`) can expose hidden signals that drastically boost model performance.
- **Tuning isn't a silver bullet**: More complex hyperparameter searches don't guarantee better results; a strong baseline with good features often wins.
- **Type safety matters**: Debugging data types and enforcing strict train/test alignment is a non-negotiable part of a reproducible ML pipeline.

## Possible Improvements

If I were to iterate on this project further, I would explore:

- extracting group size and family information from the `PassengerId` column
- creating a aggregated `TotalSpend` feature across all luxury services
- experimenting with advanced ensemble methods (Stacking/Blending)
- using `Optuna` for a more systematic, Bayesian hyperparameter optimization
- testing neural network approaches to see if they can capture the spatial anomaly patterns differently

## Repository Structure

```text
Spaceship-Titanic-solution-using-CatBoost/
├── README.md
├── project.ipynb
└── data/
```

## How to Run

1. Install the main dependencies:

```bash
pip install pandas numpy catboost scikit-learn matplotlib
```

2. Open `project.ipynb` in Jupyter or Kaggle.
3. Run the notebook cells sequentially from top to bottom to reproduce the analysis and generate the final submission.

## Tech Stack

- Python
- Jupyter Notebook
- pandas
- NumPy
- matplotlib
- scikit-learn
- CatBoost
- Kaggle

## Conclusion

For me, this project was an excellent exercise in executing a complete binary classification workflow under realistic constraints. It pushed me to look beyond basic model fitting and focus on the unglamorous but critical parts of data science: logical data cleaning, rigorous debugging of data types, and understanding when to stop tuning and trust the features.