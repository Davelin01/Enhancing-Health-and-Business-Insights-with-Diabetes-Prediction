**Overview**

Diabetes is one of the most prevalent chronic diseases globally, including in the United States,
and it poses a significant economic burden. With the number of cases continuing to rise,
addressing diabetes requires a multifaceted approach that includes prevention, effective
management, and targeted support for those affected.
Our analysis highlights actionable strategies for health insurance companies to design
specialized plans tailored to high-risk individuals. By addressing the unique healthcare needs of
this demographic, insurers can provide better support while enhancing profitability.
Targeted insurance products not only help mitigate diabetes risk through preventive care but
also create a sustainable financial model for addressing this growing health challenge. This
dual-focused approach ensures improved health outcomes for individuals and optimized
business growth for insurers

**About the dataset**

The dataset we chose is a Diabetes Health Indicators Dataset. This dataset contains 253,680
survey responses to the CDC's BRFSS2015. The Behavioral Risk Factor Surveillance System
(BRFSS) is a health-related telephone survey that is collected annually by the CDC. Each year, the
survey collects responses from over 400,000 Americans on health-related risk behaviors,
chronic health conditions, and the use of preventative services. It has been conducted every
year since 1984. Data resource from:
https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset/data

**Exploratory Data Analysis & Modeling approaches**

First, we observed that the original dataset's Diabetes_binary column contains 22,000 instances
of 0 and 35,000 instances of 1, indicating a highly imbalanced dataset. To address this, we
conducted our analysis using three different training datasets (split as 80% for training and 20%
for testing): the original training dataset(1), the oversampled training dataset(1a), and the
undersampled training dataset(1b).

Additionally, the Education column was imbalanced in categories 1, 2, and 3, so we combined
these into a single category labeled as 0 and adjusted the original categories 4, 5, and 6 to 1, 2,
and 3, respectively. We removed the Age and Income columns due to missing descriptions and
excluded the GenHlth column because it consistently caused issues in previous assignments.
Second, we identified the top 7 variables most predictive of diabetes using the Classification
Trees approach. Cross-validation was performed to ensure an optimal model, and we found the
best tree complexity parameter (cp) to be 0.0022. The top 7 variables identified were HighBP,
BMI, HighChol, DiffWalk, PhysHlth, HeartDiseaseorAttack.
Third, we utilized the Random Forest algorithm and determined that setting ntree=20 was
sufficient, based on testing with ntree=50. Using the Out-of-Bag (OOB) Error, we identified the
optimal value for mtry as 3 instead 4.
After that, we used the Mean Decrease in Gini metric to evaluate variable importance and
establish a ranking of key predictors. The most important variables identified were HighBP, BMI,
HighChol, DiffWalk, PhysHlth, and HeartDiseaseorAttack.
And then, we checked the relationship between variables and diabetes using grouped
proportion tables. Fortunately, all the binary variables show a strong positive relationship with
diabetes. On the other hand, the continuous variables have a light positive relationship with
diabetes.

Fourth, we used the variables identified in the previous model and added two additional
variables of interest: CholCheck, Stroke, and Smoker intending to test their significance using a
Logistic Regression Model. However, after applying the Logistic Regression Model on the
original dataset, the Smoker variable was removed due to its high p-value, indicating low
statistical significance. All remaining variables in the model were found to be statistically
significant.

The AUC scores for the original training dataset (0.7908), the oversampled training dataset
(0.7918), and the undersampled training dataset (0.7916) demonstrated consistent model
performance across different class distribution techniques.
Finally, we applied the Hierarchical Clustering to analyze five clusters, focusing on the top three
factors with the most significant mean changes. This approach allowed us to identify the key
factors with the greatest impact in distinguishing between diabetes patients and non-patients.
Based on the percentage changes across the clusters, the top three factors with the highest
variation were Stroke, High Blood Pressure, and Heart Disease.
(All detailed code and results are provided in the appendix.)

**Results**
Logistic regression analysis using the original training dataset (marked as 1), the oversampling
dataset (marked as 1a), and the undersampling dataset (marked as 1b) identified the following
significant predictors of diabetes:
HighBP:
● 1: Odds Ratio = 2.85. Odds of diabetes for individuals with high blood pressure are
multiplied by 2.85, meaning their odds are 185% higher compared to those without high
blood pressure.
● 1a: Odds Ratio = 2.85. Odds of diabetes for individuals with high blood pressure are
multiplied by 2.85, meaning their odds are 185% higher compared to those without high
blood pressure.
● 1b: Odds Ratio = 2.84. Odds of diabetes for individuals with high blood pressure are
multiplied by 2.84, meaning their odds are 184% higher compared to those without high
blood pressure.
BMI:
● 1: Odds Ratio = 1.06. Odds of diabetes are multiplied by 1.06 for each additional unit
increase in BMI, translating to a 6% increase in odds for every additional unit of BMI.
● 1a: Odds Ratio = 1.07. Odds of diabetes are multiplied by 1.07 for each additional unit
increase in BMI, translating to a 7% increase in odds for every additional unit of BMI.
● 1b: Odds Ratio = 1.07. Odds of diabetes are multiplied by 1.07 for each additional unit
increase in BMI, translating to a 7% increase in odds for every additional unit of BMI.
HighChol:
● 1: Odds Ratio = 2.00. Odds of diabetes for individuals with high cholesterol are
multiplied by 2.00, indicating a 100% increase in odds compared to those without high
cholesterol.
● 1a: Odds Ratio = 2.03. Odds of diabetes for individuals with high cholesterol are
multiplied by 2.03, indicating a 103% increase in odds compared to those without high
cholesterol.
● 1b: Odds Ratio = 2.06. Odds of diabetes for individuals with high cholesterol are
multiplied by 2.06, indicating a 106% increase in odds compared to those without high
cholesterol.
DiffWalk:
● 1: Odds Ratio = 1.65. Odds of diabetes for individuals with difficulty walking are
multiplied by 1.65, meaning their odds are 65% higher compared to those without
walking difficulties.
● 1a: Odds Ratio = 1.65. Odds of diabetes for individuals with difficulty walking are
multiplied by 1.65, meaning their odds are 65% higher compared to those without
walking difficulties.
● 1b: Odds Ratio = 1.68. Odds of diabetes for individuals with difficulty walking are
multiplied by 1.68, meaning their odds are 68% higher compared to those without
walking difficulties.
PhysHlth:
● 1: Odds Ratio = 1.01. Odds of diabetes are multiplied by 1.01 for each additional unit of
poor physical health, representing a slight 1% increase in odds.
● 1a: Odds Ratio = 1.02. Odds of diabetes are multiplied by 1.02 for each additional unit of
poor physical health, representing a slight 2% increase in odds.
● 1b: Odds Ratio = 1.01. Odds of diabetes are multiplied by 1.01 for each additional unit of
poor physical health, representing a slight 1% increase in odds.
HeartDiseaseorAttack:
● 1: Odds Ratio = 1.74. Odds of diabetes for individuals with a history of heart disease or
heart attack are multiplied by 1.74, representing a 74% increase in odds compared to
those without such a history.
● 1a: Odds Ratio = 1.88. Odds of diabetes for individuals with a history of heart disease or
heart attack are multiplied by 1.88, representing an 88% increase in odds compared to
those without such a history.
● 1b: Odds Ratio = 1.84. Odds of diabetes for individuals with a history of heart disease or
heart attack are multiplied by 1.84, representing an 84% increase in odds compared to
those without such a history.
CholCheck:
● 1: Odds Ratio = 3.86. Odds of diabetes for individuals who have had a cholesterol check
are multiplied by 3.86, indicating a 286% increase in odds, potentially reflecting
heightened awareness or diagnosis among those being checked.
● 1a: Odds Ratio = 3.79. Odds of diabetes for individuals who have had a cholesterol check
are multiplied by 3.79, indicating a 279% increase in odds, potentially reflecting
heightened awareness or diagnosis among those being checked.
● 1b: Odds Ratio = 4.09. Odds of diabetes for individuals who have had a cholesterol check
are multiplied by 4.09, indicating a 309% increase in odds, potentially reflecting
increased health awareness or diagnosis rates.
PhysActivity:
● 1: Odds Ratio = 0.82. Odds of diabetes for individuals engaging in physical activity are
multiplied by 0.82, indicating an 18% reduction in odds compared to those who do not
engage in physical activity.
● 1a: Odds Ratio = 0.81. Odds of diabetes for individuals engaging in physical activity are
multiplied by 0.81, indicating a 19% reduction in odds compared to those who do not
engage in physical activity.
● 1b: Odds Ratio = 0.81. Odds of diabetes for individuals engaging in physical activity are
multiplied by 0.81, indicating a 19% reduction in odds compared to those who do not
engage in physical activity.
Stroke:
● 1: Odds Ratio = 1.36. Odds of diabetes for individuals with a history of stroke are
multiplied by 1.36, indicating a 36% increase in odds compared to those without a stroke
history.
● 1a: Odds Ratio = 1.44. Odds of diabetes for individuals with a history of stroke are
multiplied by 1.44, indicating a 44% increase in odds compared to those without a stroke
history.
● 1b: Odds Ratio = 1.46. Odds of diabetes for individuals with a history of stroke are
multiplied by 1.46, indicating a 46% increase in odds compared to those without a stroke
history.

**Logistic Regression Models Performance (Confusion Matrix)**

We decided to set the cutoff at 0.5 (based on best models performance) and used the original
testing dataset to generate the confusion matrix.
Original Training Dataset
Accuracy: 0.8635
Sensitivity (True Positive Rate): 0.11306
Specificity (True Negative Rate): 0.98493
Positive Predictive Value (Precision): 0.54839
Negative Predictive Value: 0.87281
With the original dataset, this model performs well in identifying negative cases, demonstrating
high specificity and a strong ability to detect negative cases. However, it struggles significantly
to identify positive cases, reflecting low sensitivity and a limited ability to detect positive cases.
While the model's high specificity and overall accuracy may seem promising, they are
misleading due to the imbalanced nature of the dataset.

**Oversampled Training Dataset**

Accuracy: 0.7238
Sensitivity (True Positive Rate): 0.70652
Specificity (True Negative Rate) : 0.72658
Positive Predictive Value (Precision): 0.29487
Negative Predictive Value: 0.93864
With oversampling, the model's sensitivity improves dramatically, leading to a more balanced
ability to detect both positive and negative cases. This results in a significant improvement in
detecting positive cases. However, the precision remains relatively low, highlighting the
presence of many false positives.

**Undersampled Training Dataset**

Accuracy: 0.7198
Sensitivity(True Positive Rate) : 0.71261
Specificity (True Negative Rate): 0.72092
Positive Predictive Value(Precision): 0.29240
Negative Predictive Value: 0.93940
With undersampling, this model performs similarly to its oversampling counterpart, achieving a
good balance between sensitivity and specificity. While precision remains low, it demonstrates
further improvement in detecting positive cases compared to the original dataset, thereby
enhancing its overall performance.

**Conclusions**

People with high blood pressure, high BMI, high cholesterol, heart disease, or a history of stroke
are at greater risk of developing diabetes. These individuals should regularly monitor these
health conditions and work on managing them through healthy lifestyle changes or medications
as recommended by their doctors.
Additionally, individuals who have had their cholesterol levels checked within the past five years
should be reminded to continue monitoring their levels regularly. This is particularly important,
as elevated cholesterol levels are strongly linked to an increased risk of diabetes.
By implementing these two strategies, we believe that individuals can significantly reduce their
risk of developing diabetes.
On the other hand, to increase revenue, we recommend that insurance companies design
specialized products targeting individuals at high risk, particularly those exhibiting all these
traits. Tailoring insurance products for this high-risk demographic can effectively
