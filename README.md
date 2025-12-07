# Predicting Voter Turnout  
### Machine Learning Analysis using European Social Survey (ESS10)

This repository contains the R code and documentation for a project predicting **voter turnout** using microdata from the **European Social Survey (Round 10)**.  
The aim of the project is to build both **theory-driven** and **data-driven** models to understand which demographic, political, social, economic, religious, and attitudinal factors best predict whether an individual voted.

The project is structured as a fully reproducible data-science workflow:  
- Data import and cleaning  
- Extensive preprocessing and recoding  
- Class rebalancing using **ROSE**  
- Machine learning models  
- Model evaluation using confusion matrices  

---

## Repository Structure

```
Predicting_Voter_Turnout/
│
├── Code.R # Main R analysis script (data cleaning, ML models)
├── Voter Turnout Analysis.pdf # Final project report
└── ESS10 codebook.html # Original ESS10 codebook (variable documentation)
```

---
## Project Overview

### **Goal**
Predict whether respondents voted in the last national election using ESS10 microdata.

### **Dependent Variable**
- `vote` — recoded as a binary factor  
  - 1 = did not vote  
  - 2 = voted  

### **Feature Groups Included**

- **Demographic**: age, gender, education, country, marital status, household children, health  
- **Institutional trust**: trust in parliament, police, courts, politicians, parties, EU institutions  
- **Political engagement**: political interest, party closeness, satisfaction with democracy, left–right scale, news consumption  
- **Social factors**: social gatherings, trust in people, happiness, life satisfaction, discrimination  
- **Economic factors**: income, employment status, economic perceptions, working hours  
- **Religion**: affiliation, prayer frequency, denomination  
- **Immigration attitudes**: cultural/economic perceptions of immigration  
- **Discrimination indicators**

All variables are cleaned from ESS non-response codes (77, 88, 99, etc.) and converted to factors where appropriate.

---

## Methods and Workflow

### **1. Data Cleaning & Preprocessing**
- Import ESS10  
- Recode categorical variables  
- Filter invalid entries  
- Print summaries for each variable group  

### **2. Train–Test Split**
Using `caret::createDataPartition`, 70% training and 30% test.

### **3. Class Balancing**
Voting is imbalanced in the dataset.  
Balanced training data are generated using **ROSE** (Random Over-Sampling Examples).

### **4. Models Implemented**

#### ✔ **Theory-Driven Logistic Regression**
Includes predictors well-established in political science:
- Age  
- Gender  
- Education  
- Income  
- News consumption  
- Political interest  
- Party closeness  
- Country fixed effects  

#### ✔ **Data-Driven Logistic Regression**
Uses **all** variables after cleaning.

#### ✔ **Random Forest**
- 500 trees  
- `mtry = 3`  
- Includes variable importance metrics  

#### ✔ **Gradient Boosting (GBM)**
- Bernoulli distribution  
- 500 trees  
- 5-fold cross-validation  

### **5. Evaluation**
Each model outputs:
- Predicted classes  
- Confusion matrix  
- Accuracy  
- Misclassification rate  

---

## Project Report

The file **“Voter Turnout Analysis.pdf”** contains:
- Research background  
- Data description  
- Model specifications  
- Results & discussion  
- Limitations and future work  

---

## Requirements (R Packages)

```r
library(tidyverse)
library(caret)
library(ROSE)
library(randomForest)
library(gbm)
library(xgboost)
library(e1071)
library(tree)
