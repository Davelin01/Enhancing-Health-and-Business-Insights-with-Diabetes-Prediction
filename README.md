# 🚀 Enhancing Health and Business Insights with Diabetes Prediction

## 📊 Overview

This project applies data mining and machine learning to understand key diabetes risk factors using the CDC's BRFSS2015 dataset. Our aim is twofold:  
- **Advance public health insights** by identifying high-impact predictors of diabetes.  
- **Guide health insurers** in designing specialized, data-driven plans for high-risk individuals, supporting prevention and improved management while optimizing business growth.

---

## 🗂️ Dataset

- **Source**: [Kaggle - Diabetes Health Indicators Dataset](https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset/data)
- **Description**: 253,680 survey responses from the CDC's 2015 Behavioral Risk Factor Surveillance System (BRFSS), covering health behaviors, chronic conditions, and preventive services.
- **Variables**: Features include binary, categorical, and continuous health and lifestyle indicators (see "Data Description" below).

---

## 📋 Data Description

| Variable                | Type        | Description                                                                                  |
|-------------------------|-------------|----------------------------------------------------------------------------------------------|
| Diabetes_binary         | Binary      | 0 = no diabetes, 1 = (pre)diabetes                                                          |
| HighBP                  | Binary      | 0 = no high BP, 1 = high BP                                                                  |
| HighChol                | Binary      | 0 = no high cholesterol, 1 = high cholesterol                                                |
| CholCheck               | Binary      | 0 = no cholesterol check in 5 years, 1 = yes                                                 |
| BMI                     | Continuous  | Body Mass Index                                                                              |
| Smoker                  | Binary      | 0 = never smoked 100 cigarettes, 1 = yes                                                     |
| Stroke                  | Binary      | 0 = never had a stroke, 1 = yes                                                              |
| HeartDiseaseorAttack    | Binary      | 0 = no CHD/MI, 1 = CHD/MI                                                                    |
| PhysActivity            | Binary      | 0 = no physical activity (past 30 days), 1 = yes                                             |
| Fruits                  | Binary      | 0 = no fruit daily, 1 = yes                                                                  |
| Veggies                 | Binary      | 0 = no veggies daily, 1 = yes                                                                |
| HvyAlcoholConsump       | Binary      | 0 = not heavy drinker, 1 = heavy drinker                                                     |
| AnyHealthcare           | Binary      | 0 = no coverage, 1 = has health coverage                                                     |
| NoDocbcCost             | Binary      | 0 = did not skip doctor due to cost, 1 = did                                                 |
| MentHlth                | Continuous  | Days poor mental health (0-30)                                                               |
| PhysHlth                | Continuous  | Days poor physical health (0-30)                                                             |
| DiffWalk                | Binary      | 0 = no walking difficulty, 1 = yes                                                           |
| Sex                     | Binary      | 0 = female, 1 = male                                                                         |
| Education               | Categorical | 0 = <HS grad, 1 = HS grad, 2 = some college, 3 = college grad                                |

---

## 🛠️ Analytical Approach

### 1️⃣ Data Preprocessing

- **Class Imbalance**: Created three training sets: original, oversampled, and undersampled to address the imbalance in diabetes status.
- ![image](https://github.com/user-attachments/assets/c66f6d84-19de-4326-a545-5c2c86518a8f)
  ```r
  # Oversampling the minority class in the training set
  train.df1.oversampled1 <- ovun.sample(Diabetes_binary ~ ., data = train.df1, method = "over", N = 340000)$data

  # Undersampling the majority class in the training set
  train.df1.undersampled1 <- ovun.sample(Diabetes_binary ~ ., data = train.df1, method = "under", N = 58000)$data
  ```
  
  ```r
  # Visualize the class imbalance before and after sampling
  barplot(table(train.df1$Diabetes_binary), main = "Original Class Distribution")
  barplot(table(train.df1.oversampled1$Diabetes_binary), main = "Oversampled Class Distribution")
  barplot(table(train.df1.undersampled1$Diabetes_binary), main = "Undersampled Class Distribution")
  ```
![image](https://github.com/user-attachments/assets/c2b1cd58-2321-4a43-890a-83bb4b1a7bf3)

---

### 3️⃣ Predictive Modeling

#### Classification Tree

```r
library(rpart)
library(rpart.plot)
tree_cv2 <- rpart(Diabetes_binary ~ ., data = train.df1, 
                  method = "class", minbucket = 30, cp = 0.0022)
rpart.plot(tree_cv2, digits = -2)
```

#### Random Forest Variable

```r
library(randomForest)
set.seed(123, sample.kind = "Rejection")
rf_final1 <- randomForest(Diabetes_binary ~ ., data = train.df1, 
                          ntree = 20, nodesize = 50, mtry = 3)
varImpPlot(rf_final1)
```

#### Logistic Regression

```r
# Logistic Regression Model by using training dataset
logreg1 <- glm(Diabetes_binary ~ HighBP + BMI + HighChol + DiffWalk + PhysHlth +
               HeartDiseaseorAttack + PhysActivity + Stroke,
               data = train.df1, family = "binomial")
summary(logreg1)
exp(coef(logreg1)) # Odds ratios

# Logistic Regression Model by using oversampled training dataset
logreg1a <- glm(Diabetes_binary ~ HighBP + BMI + HighChol + DiffWalk + PhysHlth +
                HeartDiseaseorAttack + PhysActivity + Stroke,
                data = train.df1.oversampled1, family = "binomial")
summary(logreg1a)
exp(coef(logreg1a)) # Odds ratios

# Logistic Regression Model by using undersampled training dataset
logreg1b <- glm(Diabetes_binary ~ HighBP + BMI + HighChol + DiffWalk + PhysHlth +
                HeartDiseaseorAttack + PhysActivity + Stroke,
                data = train.df1.undersampled1, family = "binomial")
summary(logreg1b)
exp(coef(logreg1b)) # Odds ratios
```

---

### 📉 ROC Curve

![ROC Curve](https://github.com/user-attachments/assets/5e429e10-e709-4228-99cd-ea9e66bed3d2)
*ROC curve for the logistic regression model by different sampled way dataset, AUC ~0.79.*

---

### 🧮 Confusion Matrix 

**Original**, **Oversampled**, **Undersampled**

![Confusion Matrix](https://github.com/user-attachments/assets/55719cf4-370d-426f-8b31-e338e81722e4)

---

### ⚖️ Odds Ratios (Logistic Regression)

![image](https://github.com/user-attachments/assets/849db828-6b84-4cd8-bd63-3d962f3ca3ef)

---

### 🔗 Hierarchical Clustering

![Hierarchical Clustering](https://github.com/user-attachments/assets/198a14d6-a6b1-4e73-8add-fd5eb7af7d17)

Top 3 factors that show the highest changes are stroke, high blood pressure, and heart disease.

---

## 🏆 Key Results

- **Top predictors**: HighBP, BMI, HighChol, DiffWalk, PhysHlth, HeartDiseaseorAttack, Stroke, PhysActivity.
- **Odds Ratios**: HighBP increases odds by 2.85x； physical activity reduces odds by ~0.82x.
- **Model Insights**:
  - Original data: High specificity, low sensitivity (misses positives).
  - Oversampled/Undersampled: Balanced sensitivity/specificity, lower overall accuracy.
- **Recommendations**:
  - Individuals with elevated blood pressure, cholesterol, BMI, heart disease, or stroke history should monitor these closely.
  - Insurers should target high-risk groups to improve care and business outcomes.

---
