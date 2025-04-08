# handson-10-MachineLearning-with-MLlib.

#  Customer Churn Prediction with MLlib

This project uses Apache Spark MLlib to predict customer churn based on structured customer data. You will preprocess data, train classification models, perform feature selection, and tune hyperparameters using cross-validation.

---



Build and compare machine learning models using PySpark to predict whether a customer will churn based on their service usage and subscription features.

---

##  Dataset

The dataset used is `customer_churn.csv`, which includes features like:

- `gender`, `SeniorCitizen`, `tenure`, `PhoneService`, `InternetService`, `MonthlyCharges`, `TotalCharges`, `Churn` (label), etc.

---

##  Tasks

### Task 1: Data Preprocessing and Feature Engineering

**Objective:**  
Clean the dataset and prepare features for ML algorithms.

**Steps:**
1. Fill missing values in `TotalCharges` with 0.
2. Encode categorical features using `StringIndexer` and `OneHotEncoder`.
3. Assemble numeric and encoded features into a single feature vector with `VectorAssembler`.

**Code Output:**

===== Task 1: Features with ChurnIndex =====
+--------------------+----------+
|            features|ChurnIndex|
+--------------------+----------+
|[1.0,1.0,1.0,0.0,...|       0.0|
|[1.0,1.0,0.0,1.0,...|       0.0|
|[1.0,1.0,0.0,1.0,...|       1.0|
|[1.0,1.0,1.0,0.0,...|       0.0|
|[0.0,1.0,1.0,0.0,...|       0.0|
+--------------------+----------+
```
---

### Task 2: Train and Evaluate Logistic Regression Model

**Objective:**  
Train a logistic regression model and evaluate it using AUC (Area Under ROC Curve).

**Steps:**
1. Split dataset into training and test sets (80/20).
2. Train a logistic regression model.
3. Use `BinaryClassificationEvaluator` to evaluate.

**Code Output Example:**
```
===== Logistic Regression AUC =====
AUC: 0.7235


---

###  Task 3: Feature Selection using Chi-Square Test

**Objective:**  
Select the top 5 most important features using Chi-Square feature selection.

**Steps:**
1. Use `ChiSqSelector` to rank and select top 5 features.
2. Print the selected feature vectors.

**Code Output Example:**
```
===== Top 5 Selected Features =====
+--------------------+----------+
|    selectedFeatures|ChurnIndex|
+--------------------+----------+
|[1.0,1.0,0.0,41.0...|       0.0|
|[1.0,0.0,1.0,1.0,...|       0.0|
|[1.0,0.0,1.0,16.0...|       1.0|
|[1.0,1.0,0.0,63.0...|       0.0|
|[1.0,1.0,0.0,54.0...|       0.0|
+--------------------+----------+

```

---

### Task 4: Hyperparameter Tuning and Model Comparison

**Objective:**  
Use CrossValidator to tune models and compare their AUC performance.

**Models Used:**
- Logistic Regression
- Decision Tree Classifier
- Random Forest Classifier
- Gradient Boosted Trees (GBT)

**Steps:**
1. Define models and parameter grids.
2. Use `CrossValidator` for 5-fold cross-validation.
3. Evaluate and print best model results.

**Code Output Example:**
```
===== Cross-Validation Model Comparison =====

Tuning LogisticRegression...
LogisticRegression Best Model Accuracy (AUC): 0.72
Best Params for LogisticRegression: regParam=0.0, maxIter=100

Tuning DecisionTree...
DecisionTree Best Model Accuracy (AUC): 0.74
Best Params for DecisionTree: maxDepth=5

Tuning RandomForest...
RandomForest Best Model Accuracy (AUC): 0.78
Best Params for RandomForest: maxDepth=5, numTrees=20

Tuning GBT...
GBT Best Model Accuracy (AUC): 0.73
Best Params for GBT: maxDepth=5, maxIter=20

```
---

##  Execution Instructions

### 1. Prerequisites

- Apache Spark installed
- Python environment with `pyspark` installed
- `customer_churn.csv` placed in the project directory

### 2. Run the Project


spark-submit churn_prediction.py
```

