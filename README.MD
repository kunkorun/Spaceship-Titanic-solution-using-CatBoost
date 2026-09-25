\# Spaceship Titanic - My First Real ML Project!



\## Hi there!



Hey! This is my third data science project and I'm super excited to share it with you! I've been learning Python and machine learning for about 6 months now, and this is my first Kaggle competition submission!



The goal is to predict which passengers were transported to another dimension during the Spaceship Titanic disaster. It sounds like sci-fi but it's actually a really cool binary classification problem!



\*\*My score: 0.80032\*\* (I know it's not amazing but I'm still learning!)



\## What's in this project



This project has two main parts:



\### 1. Main Analysis (`main\_part`)

This is where I explored the data and tried different models. I learned so much here! I used:

\- \*\*Logistic Regression\*\* - my first model, pretty simple but it works!

\- \*\*Random Forest\*\* - much better! I learned about ensemble methods here

\- \*\*CatBoost\*\* - the winner!



I also made lots of visualizations with matplotlib to understand the data better. There are histograms, bar charts, correlation matrices... maybe too many charts honestly



\### 2. Final Submission (`final\_part`)

This is the cleaned-up version that makes the actual predictions. It's standalone so you can run it by itself! It does all the data preprocessing and trains the final CatBoost model.



\## How to run it



First, install the requirements:

```bash

pip install pandas numpy catboost scikit-learn matplotlib

```



Then you can either:

\- Open the notebook in Kaggle (easiest way!)

\- Or run `final\_part` locally if you have the data files



The script is smart enough to find the data whether you're on Kaggle or running locally!



\## What I learned



This project taught me SO much! Here are the key things:



\### Data Preprocessing is 80% of the work

I spent way more time cleaning data than building models! The missing values were tricky:

\- If a passenger was in `CryoSleep`, they probably didn't spend money on services

\- If they spent money, they definitely weren't in cryo sleep

\- I used this logic to fill missing values smartly!



\### Feature Engineering matters a lot

I created new features from the `Cabin` column:

\- `Deck` (A, B, C, D, E, F, G)

\- `CabinNumber` (the number part)

\- `Side` (P or S)



I also mapped decks to home planets because I noticed a pattern in the data!



\### CatBoost is amazing

I tried different models and CatBoost gave the best results with the least tuning. I didn't even need to tune the hyperparameters much - the default settings worked great!



\## My Results



| Model | Score | Notes |

|-------|-------|-------|

| Logistic Regression | \~0.78 | Good baseline! |

| Random Forest | \~0.80 | Better! |

| Tuned Random Forest | \~0.79 | Tuning didn't help much |

| \*\*CatBoost\*\* | \*\*0.80032\*\* | \*\*Winner!\*\* |

| Tuned CatBoost | \~0.80 | Same as baseline |



I learned that sometimes simpler is better! The tuned models didn't improve much, so I stuck with the baseline CatBoost.



\## Bugs I encountered (and fixed!)



\### 1. Pandas FutureWarning

```

FutureWarning: Downcasting object dtype arrays on .fillna() is deprecated

```

\*\*Solution:\*\* I added `.astype(bool)` after filling missing values. This explicitly tells pandas what type the column should be!



\### 2. CatBoost Error

```

CatBoostError: Cannot convert 'G' to float

```

\*\*Solution:\*\* This was tricky! I had to:

\- Convert categorical columns to `str` type (not `category`)

\- Use `catboost.Pool` for training and prediction

\- Make sure column order is the same in train and test



\### 3. Column mismatch

Sometimes test data had different columns than train data. I fixed it with:

```python

X\_test\_cat = X\_test\_cat\[X\_full\_cat.columns]

```

This one line saved me hours of debugging!



\## What I would do next



If I had more time (and energy), I would try:

\- \[ ] Extract group information from `PassengerId` (like group size)

\- \[ ] Create a `TotalSpend` feature (sum of all spending)

\- \[ ] Try ensemble methods (combine multiple models)

\- \[ ] Use Optuna for better hyperparameter tuning

\- \[ ] Try neural networks (though that might be overkill)



\## Acknowledgments



\- Thanks to Kaggle for this competition and the free GPU access!

\- Thanks to all the YouTube tutorials that helped me understand CatBoost

\- Thanks to Stack Overflow for answering all my questions

\- Thanks to my cat for keeping me company during late-night coding sessions



\## Resources that helped me



\- Kaggle Learn courses (especially Pandas and Intro to Machine Learning)

\- "Hands-On Machine Learning" book (still reading it!)

\- Various YouTube channels (StatQuest is amazing!)

\- The Kaggle discussion forums (so many helpful people!)



\## Questions?



I'm still learning, so if you see something in my code that could be better, please let me know! I'd love to get feedback and improve.



You can reach me at... actually, I'm not sure yet. Maybe I'll add my contact info later when I figure out how professionals do this



\## If you found this helpful



Please give it a star! It would mean a lot to me as a beginner!



\---



\*\*P.S.\*\* If you're also a beginner, don't be discouraged by the leaderboard scores. Everyone starts somewhere! The important thing is to keep learning and building projects. You got this!

