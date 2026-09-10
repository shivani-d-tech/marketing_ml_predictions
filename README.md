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

To view the data understanding notebook, click [here](./1_notebooks/01_data_inspection.ipynb).

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

Find the full EDA notebook [here](./1_notebooks/2_eda/ipynb).

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
* *SMOTE()* = Used for class imbalance and prevention of model bias.

Find the preprocessing notebook [here](./1_notebooks/03_preprocessing.ipynb).

## 🤖 Models Implemented

| Model | Type | Hyperparameter Tuning? |
|-------|------|------------------------|
| Logistic Regression | Baseline | No |
| Random Forest Model | Advanced | Yes |
| XGBoost | Advanced | Yes |

## 📈 Model Comparison and Selection

| Model | Precision (yes) | Recall (yes) | F1 (yes) | Accuracy |
|-------|-----------------|--------------|----------|----------|
| Logistic Regression | 0.28 | 0.62 | 0.39 | 0.76 |
| Random Forest | 0.46 | 0.43 | 0.45 | 0.87 |
| XGBoost | 0.70 | 0.20 | 0.31 | 0.89 |

**Model Selection: *Logistic Regression***

* Has the best overall balance when predicting the “yes” class.
* Whilst logistic regression and XGBoost excel in one evaluation metric each, neither has the balance needed for effective targeting.
* The Random Forest Model is an example of a balanced trade-off – precision, recall, and F1 are all important to goal, therefore need a model that performs consistently across all metrics.
* Although precision, recall, and F1-score is below 0.55 for the “yes” class – this is expected for severely imbalanced classification problems.
* Random Forest is the model that is the most dependable for identifying likely responders and supporting targeted marketing decisions.

Find the baseline model notebook [here](./1_notebooks/04_baseline_models_logistic.ipynb).

Find the advanced models and their comparison [here](./1_notebooks/05_advanced_models.ipynb).

Find the final model notebook [here](./1_notebooks/06_final_model.ipynb).

## Explainability

Techniques used:
* Feature Importance
* LIME
  
Example:

**Feature Importance:**

<p align="center">
  <img src="https://github.com/user-attachments/assets/81f1c533-4cb4-46cc-afc8-945f9c16c8a5" width="800" />

* The model focuses primarily on balance_log, age, and poutcome_success. This suggests that financial stability, demographic factors, and past campaign outcomes are the driving power behind predictions.
* Contact_type, previous_log, and month_may also matter, suggesting that communication strategy and timing influence the model’s decisions more than job or marital status.



**LIME - correctly predicted case:**

<p align="center">
  <img src="https://github.com/user-attachments/assets/2286b850-9fe5-4156-b0c4-f846dbcc66a9" width="800" />

* The model shows a 65% confidence in its positive prediction.
* Features, such as the last contact month of July and days since contact, are main drivers in swaying the prediction of the model.

**LIME - False Negative case:**

<p align="center">
  <img src="https://github.com/user-attachments/assets/2286b850-9fe5-4156-b0c4-f846dbcc66a9" width="800" />

* The model is 99% confident in its decision. This suggests that the model is highly over-confident.
* There are big contributions from features, such as cat_month_aug, that push for a positive prediction. However, the model seems to begin with a very strong internal bias towards class 0 for this customer, and the positive contributions are not large enough to overcome this.

## 💼 Future Work

* Try other class imbalance techniques. Although this project uses SMOTE, techniques, such as random undertraining, might improve evaluation metrics.
* Calibrate the model confidence – The model shows overconfidence and this could be improved through calibration curves and adjusting the decision threshold.
* Feature engineering – create features to create stronger signals.
* Try more advanced models (e.g. LightGBM) to improve evaluation metrics.










