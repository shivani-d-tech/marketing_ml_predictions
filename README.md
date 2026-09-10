# Bank Marketing Prediction Model
A supervised learning machine learning project which predicts whether a client will respond to a marketing campaign for a bank and subscribe to a term deposit.

## 🎯Project Overview
This goal of this project predicts whether a customer will respond to a bank's marketing campaign and subscribe to a term deposit. A supervised machine learning approach was used and several classification algorithms were compared and evaluated.

## 📂 Repository Structure

```
marketing_ml_project_3/
├── 1_notebooks/
│ ├── 01_data_inspection.ipynb
│ └── 02_eda.ipynb
│ └── 03_preprocessing.ipynb
│ └── 04_baseline_models_logistic.ipynb
│ └── 05_advanced_models.ipynb
│ └── 06_final_model.ipynb
├── 2_reports/
│ └── project_report.pptx
└── README.md
```
## ℹ️ Dataset Information
**Name:** Bank Marketing

**Source:** UCI Machine Learning Repository

**Citation:** Moro S., Cortez P., & Rita P. (2014). A Data-Driven Approach to Predict the Success of Bank Telemarketing. Decision Support Systems, 62, 22–31.

**DOI:** https://doi.org/10.24432/C5K306

**License:** CC BY 4.0

**Description:**

* *Number of records:* 45,211
* *Number of features:* 17
* *Target variable:* If the client subscribed to term deposit ('y')

To view the data understanding notebook, click [here](./1_notebooks/01_data_inspection.ipynb)

**Key Features:**

| Feature | Description |
|---------|-------------|
| Age | Age of customer. |
| job | Type of job customer holds. |
| marital | marital status of customer. |
| educaion | Level of education of customer. |
| default | If customer has got credit in default. |
| balance | Average yearly balance. |
| housing | If customer has a housing loan. |
| loan | If customer has a personal loan. |
| contact | How customer has been contacted |
| day_of_week | The last day of the week the customer was contacted. |
| month | The last contact month of the year the customer was contacted. |
| duration | The duration of the last contact in seconds. Possible cause of data leakage. |
| campaign | Number of times the customer has been contacted during the campaign. |
| pdays | Number of days that passed since the last contact with the customer. |
| previous | Number of times a customers was contacted before this campaign. |
| poutcome | The outcome of the previous marketing campagin. |
| **p** | **If the customer subscribed to a term deposit.** |

## 🔍 Exploratory Data Analysis (EDA)

**Key Findings:**

* Numeric features (e.g. balance, duration) are heavily right-skewed with valid but extreme outliers.
* Categorical variables are unevenly distributed, with certain groups dominating.
* The target is highly imbalanced (more 'no' than 'yes').
* Duration strongly separates the target classes and should be removed due to data leakage.

**Key Visualisations:**

<p align="center">
  <img src="https://github.com/user-attachments/assets/ea110394-bfbd-494a-a800-b7b9277ad234" width="400" />
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/e7977730-05e2-4cfe-a9e7-93a1f5769bd8" width="400" />
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/bbd93c79-6beb-4761-9dbe-a1769074890b" width="400" />
</p>

## ⚙️ Data Preprocessing and Feature Engineering

**Data Cleaning Steps:**

* Removed 'duration' column to prevent data leakage.
* After removal of 'duration' column, 16 duplicates were found and removed to stop distortion of dataset.
* Log transformed skewed numeric columns.
  

**Feature Engineering:**

Columns added:
* *‘contacted_before’* = converted pdays column into a binary feature (-1 = not previously contacted; 0 = no previous contact; 1 = contacted)
* *‘age_bucket’* =  ‘young’, ‘middle’, ‘senior’
* *‘balance_positive’* = balance is bigger than 0 => 1
* *‘long_campaign’* = for number of contacts longer than 15 days. The original 'campaign' feature was removed after analysis showed a negligable correlation with the target variable (-0.0073).

**Preprocessing Pipeline:**

<p align="center">
  <img src="https://github.com/user-attachments/assets/b56283a3-038a-41eb-9d39-e09c7d80c131" width="700" />

* *StandardScaler()* = As columns are normally distributed or log-transformed, ready for scaling.
* *OneHotEncoder()* = To transform categorical data into binary columns, that is digestible by the models.
* *SMOTE()* = Used for class imbalance and prevent model bias.

Find the preprocessing notebook [here](./1_notebooks/03_preprocessing.ipynb)

## 🤖 Models Implemented

| Model | Type | Hyperparameter Tuning? |
|-------|------|------------------------|
| Logistic Regression | Baseline | No |
| Random Forest Model | Advanced | Yes |
| XGBoost | Advanced | Yes |







