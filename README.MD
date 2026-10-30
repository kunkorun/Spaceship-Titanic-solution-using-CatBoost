# 🚀 Spaceship Titanic — CatBoost Solution

This was my third Kaggle Machine Learning project.

The goal was to predict whether a passenger of the Spaceship Titanic was transported to another dimension during the incident.

**Kaggle Score: 0.80032**

---

## 🎯 Goal

In this project, I wanted to improve my classification workflow and make more data-driven decisions instead of applying standard preprocessing automatically.

I focused on understanding missing values, exploring relationships between features, and testing different preprocessing and modeling approaches.

I also used **CatBoost for the first time** in a practical classification task.

---

## 🔍 Exploratory Data Analysis

I started with an initial data audit:

- dataset size and structure;
- data types and missing values;
- categorical and numerical features;
- target distribution;
- relationships between features and the target.

I also explored passenger characteristics and spending patterns to identify relationships that could be useful during preprocessing and feature engineering.

---

## 🧩 Missing Values

Missing-value handling was one of the main parts of this project.

Instead of filling all missing values with a single statistical value, I tried to use relationships between features to make more reasonable decisions.

For example:

- **CryoSleep and spending features:** passengers in CryoSleep were expected to have no spending. I used this relationship when handling missing values in spending columns.
- **Spending features:** for passengers not in CryoSleep, missing spending values were filled using medians calculated from the corresponding group.
- **CryoSleep:** I used the available spending information to infer some missing values.
- **Cabin:** I split the original feature into `Deck`, `CabinNumber`, and `Side`, then handled missing values in these new columns separately.
- **HomePlanet:** for some missing values, I used information from the passenger's deck.

I also handled missing values in other numerical and categorical features using appropriate strategies.

This helped me understand that missing values are not always just a technical problem. Sometimes other features can provide useful information about what a missing value might represent.

---

## 🛠️ Feature Engineering

I created additional features to make potentially useful information more explicit for the models.

Some of the features included:

- `HasSpend` — indicates whether a passenger had any spending.
- `Deck` — extracted from the original `Cabin` feature.
- `CabinNumber` — extracted cabin number.
- `Side` — extracted cabin side.
- `CabinNumberMissing` — indicates whether the cabin number was missing.

I also explored different ways of using the available features and checked whether additional information improved model performance.

---

## 🤖 Models

I compared several classification approaches:

- **Logistic Regression** — used as an initial baseline.
- **Random Forest** — tested as a more flexible model and tuned using `RandomizedSearchCV`.
- **CatBoost** — used for the final Kaggle submission.

The Random Forest experiments showed that hyperparameter tuning could improve validation performance.

CatBoost was particularly interesting to explore because of its ability to work with categorical features and its usefulness for tabular classification tasks.

---

## 📊 Evaluation

I used a stratified train-validation split to evaluate the models and compare their performance.

For Random Forest, I also used cross-validation and hyperparameter tuning.

The main evaluation metric was **Accuracy**, which is also the metric used in the Kaggle competition.

**Final Kaggle score: 0.80032**

---

## 🧪 Experiments

The main experiments focused on:

- different missing-value handling strategies;
- relationships between `CryoSleep` and spending features;
- feature engineering;
- comparing Logistic Regression and Random Forest;
- Random Forest hyperparameter tuning;
- trying CatBoost for the final submission.

My general workflow was:

```text
Hypothesis
   ↓
Data exploration
   ↓
Preprocessing / Feature Engineering
   ↓
Model training
   ↓
Validation
   ↓
Evaluation and comparison
```

I tried to evaluate changes using validation results rather than assuming that every new feature or preprocessing step would improve the model.

---

## 💡 Key Learnings

This project helped me develop a more thoughtful approach to preprocessing and feature engineering.

The main things I learned:

- Missing values can sometimes be better understood through relationships between features.
- Domain knowledge and data exploration can help guide preprocessing decisions.
- Feature engineering should be evaluated rather than added automatically.
- Cross-validation and validation results are important when comparing models.
- CatBoost is another useful approach to explore when working with tabular data.

It was also a good opportunity to practice debugging and handling data types during preprocessing.

---

## 🔮 Possible Improvements

If I return to this project, I would like to:

- make preprocessing fully consistent across validation and training stages;
- explore additional feature engineering ideas;
- perform more systematic hyperparameter tuning;
- investigate model errors in more detail;
- compare CatBoost with other gradient boosting approaches.

---

## ⚙️ How to Run

1. Clone the repository.
2. Install the required libraries:

```bash
pip install -r requirements.txt
```

3. Download the Spaceship Titanic dataset from Kaggle.
4. Place the dataset files in the appropriate directory.
5. Open and run the notebook.

---

## 🔗 Links

- [Kaggle Competition — Spaceship Titanic](https://www.kaggle.com/competitions/spaceship-titanic)
