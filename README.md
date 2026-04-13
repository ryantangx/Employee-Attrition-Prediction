# Predicting Employee Turnover to Drive HR Retention Strategies

![Python](https://img.shields.io/badge/Python-3.9-3776AB?logo=python)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?logo=scikitlearn)
![Status](https://img.shields.io/badge/Status-Completed-success)
[![View Notebook](https://img.shields.io/badge/Jupyter-View_Notebook-F37626?logo=jupyter&style=flat)](employee_attrition_random_forest.ipynb)

## 📌 Abstract
Salifort Motors, a global consulting firm, is currently experiencing an unusually high rate of employee turnover. This attrition significantly impacts the company's bottom line through increased recruitment costs, lost productivity, and diminished team morale. This project utilizes the **PACE (Plan, Analyze, Construct, Execute) framework** to transition HR from a reactive replacement approach to a proactive retention strategy.

By developing a **Random Forest Classifier**, this analysis identifies employees at high risk of leaving and uncovers the core drivers of turnover. The final model achieved an **Accuracy of 99% and a Precision of 99%**. The results indicate that turnover is primarily driven by satisfaction levels, extreme workload imbalances, and a critical 3–5 year tenure window.

---

## 📂 Data & Preprocessing
The dataset consists of 14,999 employee records with 10 variables, including satisfaction levels, performance evaluations, and workload metrics.

### Preprocessing Pipeline
* **Data Cleaning**: Identified and removed **3,008 duplicated rows** to prevent biased predictions and overweighting specific profiles.
* **Standardization**: Renamed columns to standardized `snake_case` (e.g., `time_spend_company` was renamed to `tenure`).
* **Feature Engineering**: Converted categorical features (`department` and `salary`) into numeric formats using **One-Hot Encoding**.
* **Data Splitting**: Split the data into a 75/25 Train-Test set. Stratification was used to ensure the ~16.6% turnover class imbalance was maintained in both sets.

---

## 📈 Exploratory Data Analysis (EDA)
Extensive visualization was conducted to map the relationships between workload, performance, and attrition.

### 1. Risk Segmentation (Satisfaction vs. Evaluation)
![Satisfaction vs Evaluation](satisfaction_eval_scatter.png)
*Figure 1: Employee Clusters: Satisfaction Level vs. Last Evaluation*

**Insight:** The data reveals three highly distinct "flight risk" clusters. **The Burned Out** (top performers with low satisfaction), **The Underperformers** (struggling with both metrics), and **The Ambitious** (top-tier employees with high satisfaction who likely leave for better growth opportunities elsewhere).

### 2. Workload Imbalances (Monthly Hours vs. Projects)
![Workload Distribution](workload_distribution.png)
*Figure 2: Workload Distribution: Avg Monthly Hours vs. Number of Projects*

**Insight:** There is a clear "sweet spot" for retention at **3 to 4 projects**. Employees falling outside this range are at high risk: those with only 2 projects are significantly underutilized, while those with 6–7 projects are consistently overworked, often exceeding 250–300 monthly hours.

### 3. Tenure & Salary Trends
![Turnover by Salary](turnover_by_salary.png)
*Figure 3: Turnover Proportion by Salary Level*

![Attrition by Tenure](attrition_by_tenure.png)
*Figure 4: Employee Attrition by Years at Company*

**Insight:** While "low" salary earners quit at the highest rate, compensation is not the only factor. A dramatic spike in turnover occurs specifically at the **3, 4, and 5-year marks**, suggesting a systemic issue with mid-level career progression and long-term engagement.

---

## 🧠 Model Architecture
Because the EDA revealed non-linear relationships, a **Random Forest Classifier** was selected for its robustness and ability to provide feature importance metrics.

* **Model**: Scikit-Learn `RandomForestClassifier`.
* **Optimization**: `GridSearchCV` was used to test 36 combinations of hyperparameters.
* **Refit Metric**: **F1-Score** (0.944 on training set) to minimize both false positives and false negatives.
* **Best Parameters**: `max_depth: 15`, `min_samples_leaf: 1`, `min_samples_split: 10`.

---

## 📊 Results & Performance
The model demonstrated exceptional predictive power on the unseen test set, providing HR with a highly reliable deployment tool.

| Metric | Score |
| :--- | :--- |
| **Accuracy** | **0.99** |
| **Precision** | **0.99** |
| **Recall** | **0.92** |
| **F1-Score** | **0.96** |

### Confusion Matrix & Feature Importance
The confusion matrix confirms that the model produced only **4 false positives** across 3,000 cases. Feature importance metrics show **satisfaction_level** as the primary driver, followed by project count and tenure.

![Confusion Matrix](confusion_matrix.png)
*Figure 5: Random Forest Confusion Matrix*

![Feature Importances](feature_importances.png)
*Figure 6: Feature Importance Analysis*

---

## 🎯 Strategic Business Roadmap & Implementation
To solve the turnover crisis, Salifort Motors must move beyond reactive hiring and implement the following data-driven interventions:

### 1. High-Precision Retention Outreach
* **Model Deployment**: Implement the Random Forest model as a monthly automated pipeline.
* **Prioritize High-Risk Flags**: Because the model has a **99% precision rate**, HR should immediately prioritize outreach to flagged individuals, as they are almost certain to leave without intervention.

### 2. Workload & Operational Boundaries
* **Cap Active Projects**: Managers should enforce a limit of 5 projects per employee to prevent burnout.
* **Automated Alerts**: Establish a system that alerts HR when an employee's monthly hours breach the 250-hour mark or project counts fall below 3, indicating underutilization.

### 3. Structural Engagement Overhaul
* **Quarterly "Pulse Checks"**: Transition from annual reviews to quarterly satisfaction checks to catch dipping sentiment early, particularly for top-tier "Ambitious" and "Burned Out" clusters.
* **Mid-Level Tenure Pathways**: Design specific retention tracks (leadership training, sabbaticals, or title promotions) specifically for employees entering their **third year of service**.

### 4. Quantifying Business Impact (Next Steps)
* **ROI Calculation**: Conduct a financial analysis by multiplying the 460 successfully identified flight risks by the average cost of replacement (recruitment + onboarding).
* **Qualitative Deep-Dive**: Use the model's findings to lead targeted focus groups to understand the specific qualitative reasons why top-performing employees feel their satisfaction is dropping.

---
*© 2026 Ryan Tang.*
