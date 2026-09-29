# 🚀 Spaceship Titanic — CatBoost Solution

This was my third Kaggle Machine Learning project.

The goal was to predict whether a passenger of the Spaceship Titanic was transported to another dimension during the incident.

**Kaggle Score: 0.80032**

---

## 🎯 Goal

In this project I wanted to continue improving my classification workflow and start making more decisions based on the data itself instead of applying standard preprocessing automatically.

One of the main things I focused on was understanding the missing values and looking for relationships between different columns before deciding how to fill them.

I also used **CatBoost for the first time** in this project.

---

## 🔍 Exploratory Data Analysis

I started with a basic data audit:

* dataset size and structure;
* data types;
* missing values;
* categorical features;
* numerical features;
* target distribution;
* relationships between features.

I used visualizations during the process to check my assumptions and better understand the data.

---

## 🧩 Missing Values

This became one of the most interesting parts of the project for me.

Instead of simply replacing missing values with the mean, median or most common category, I tried to look at the relationships between columns and understand what the missing value could represent.

For example, some features contained information that could help explain another feature with missing values.

This changed the way I think about missing data:

> A missing value is not always just a technical problem that needs to be filled. Sometimes the other features can help explain why it is missing or what value is more reasonable.

I also had to pay attention to data types and debugging during preprocessing, because some transformations did not work as expected at first.

---

## 🛠️ Feature Engineering

I experimented with features based on the structure of the dataset and the relationships I found during EDA.

The main idea was to create features that could make useful information more explicit for the model.

I tried to avoid creating features just for the sake of increasing the score.

---

## 🤖 Models

I compared different classification approaches and eventually used **CatBoost** as the main model.

This was my first practical experience with CatBoost.

One of the reasons I wanted to try it was its ability to work well with categorical data and reduce the amount of manual preprocessing required for some features.

---

## 📊 Evaluation

The competition uses **Accuracy** as the main evaluation metric.

Final Kaggle score:

**0.80032**

I also used validation during the development process to compare changes before making the final submission.

---

## 🧪 Experiments

The main experiments in this project were related to:

* missing-value handling;
* feature engineering;
* categorical features;
* preprocessing;
* model comparison;
* CatBoost parameters.

The general approach was:

```text
Hypothesis
   ↓
```
