# Diabetes Health Indicators Analysis
📋 Overview

Diabetes is one of the most prevalent chronic diseases worldwide and poses a significant economic burden. With cases on the rise, combating diabetes requires prevention, effective management, and targeted support. This analysis presents actionable strategies for health insurance companies to create specialized plans tailored to high-risk individuals.

These targeted products help mitigate diabetes risks through preventive care while also supporting sustainable business growth. This dual-focused approach improves individual health outcomes and enhances insurer profitability.

📊 About the Dataset

We used the Diabetes Health Indicators Dataset from Kaggle, which contains 253,680 survey responses from the CDC’s Behavioral Risk Factor Surveillance System (BRFSS 2015). This annual telephone survey collects health-related data such as:

Risk behaviors

Chronic health conditions

Use of preventive services

🔍 Exploratory Data Analysis & Modeling

⚠️ Imbalanced Data

The target variable Diabetes_binary has 22,000 (0s) and 35,000 (1s)

We created 3 versions of the training dataset:

Original (1)

Oversampled (1a)

Undersampled (1b)

🧹 Data Cleaning

Merged categories 1, 2, 3 in the Education column into one.

Removed Age, Income (due to missing descriptions).

Removed GenHlth (inconsistent behavior in previous assignments).

🌳 Modeling Approaches

1. Classification Tree
Performed cross-validation.

Best complexity parameter (cp) = 0.0022.

Top 7 variables:
HighBP, BMI, HighChol, DiffWalk, PhysHlth, HeartDiseaseorAttack.

2. Random Forest
Best ntree = 20; best mtry = 3 (based on Out-of-Bag error).

Variable importance (Mean Decrease in Gini) confirmed same top predictors.

3. Logistic Regression
Added CholCheck, Stroke, and Smoker.

Smoker was removed due to high p-value (not statistically significant).

Consistent performance across all dataset variations:

AUC (Original): 0.7908

AUC (Oversampled): 0.7918

AUC (Undersampled): 0.7916

4. Hierarchical Clustering
Identified 5 clusters.

Top 3 varying features:
Stroke, HighBP, HeartDiseaseorAttack.

🔢 Logistic Regression Results


📈 Model Performance (Cutoff = 0.5)
✅ Original Dataset
Accuracy: 0.8635

Sensitivity: 0.1131

Specificity: 0.9849

Precision: 0.5484

Note: High specificity, but very poor sensitivity due to class imbalance.

🔁 Oversampled Dataset
Accuracy: 0.7238

Sensitivity: 0.7065

Specificity: 0.7266

Precision: 0.2949

Note: Improved detection of positive cases (diabetes), but precision drops.

🔁 Undersampled Dataset
Accuracy: 0.7198

Sensitivity: 0.7126

Specificity: 0.7209

Precision: 0.2924

Note: Very similar to oversampled. Balanced sensitivity/specificity trade-off.

📌 Key Takeaways
Top risk factors: HighBP, HighChol, BMI, HeartDiseaseorAttack, DiffWalk, Stroke.

Individuals with these conditions should monitor them regularly and adopt lifestyle changes or treatment.

CholCheck likely reflects increased diagnosis awareness—not necessarily causal.

PhysActivity is protective—encouraging regular exercise is key.

💡 Recommendation for Insurance Companies
Insurance providers should design specialized products targeting high-risk individuals—those with multiple predictive traits:

Higher premiums with tailored preventive care

Incentives for maintaining healthy behaviors (e.g., gym reimbursements)

Better risk prediction → sustainable financial outcomes

By offering targeted support, insurers can reduce long-term costs while delivering better outcomes.
