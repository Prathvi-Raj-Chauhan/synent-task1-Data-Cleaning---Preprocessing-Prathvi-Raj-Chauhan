# Titanic Dataset Data Cleaning and Preprocessing

## Problem Statement

The objective of this project is to clean and preprocess the Titanic dataset by handling missing values, removing irrelevant features, correcting data types, and preparing the dataset for further exploratory analysis or machine learning tasks.

Data preprocessing is a crucial step in the data science workflow, ensuring that the dataset is complete, consistent, and suitable for analysis.

---

## Dataset Details

**Dataset:** Titanic Passenger Dataset

**Source:** Titanic Survival Dataset

### Dataset Overview

* Total Records: **891**
* Total Features (Before Cleaning): **12**
* Total Features (After Cleaning): **11**
* Target Variable: **Survived**

### Features

| Feature     | Description                       |
| ----------- | --------------------------------- |
| PassengerId | Unique passenger identifier       |
| Survived    | Survival status (0 = No, 1 = Yes) |
| Pclass      | Passenger class (1st, 2nd, 3rd)   |
| Name        | Passenger name                    |
| Sex         | Gender                            |
| Age         | Passenger age                     |
| SibSp       | Number of siblings/spouses aboard |
| Parch       | Number of parents/children aboard |
| Ticket      | Ticket number                     |
| Fare        | Ticket fare                       |
| Cabin       | Cabin number                      |
| Embarked    | Port of embarkation               |

---

## Initial Dataset Inspection

The dataset contained:

* 891 passenger records
* Numerical and categorical features
* Several missing values requiring preprocessing

### Missing Values Before Cleaning

| Column   | Missing Values |
| -------- | -------------- |
| Age      | 177            |
| Cabin    | 687            |
| Embarked | 2              |

The remaining columns contained no missing values.

---

## Data Cleaning Process

### 1. Handling Missing Values in Age

The `Age` column contained 177 missing values.

To preserve the dataset size and avoid dropping records, missing values were replaced with the mean age of passengers.

```python id="tbh71e"
df['Age'] = df['Age'].fillna(df['Age'].mean())
```

### Reason

* Age is an important feature.
* Mean imputation is a common strategy for numerical variables.
* Prevents loss of valuable passenger records.

---

### 2. Handling Missing Values in Cabin

The `Cabin` column contained 687 missing values out of 891 records.

Since more than 75% of the values were missing, the column was removed.

```python id="p6q8yl"
df.drop('Cabin', axis=1, inplace=True)
```

### Reason

* Excessive missing data.
* Imputation would be unreliable.
* Cabin information contributes little when most entries are absent.

---

### 3. Handling Missing Values in Embarked

The `Embarked` column contained only 2 missing values.

Missing values were replaced using the most frequent embarkation port (mode).

```python id="2f6lqf"
df['Embarked'] = df['Embarked'].fillna(
    df['Embarked'].mode()[0]
)
```

### Reason

* Only a small number of values were missing.
* Mode imputation preserves the categorical distribution.

---

## Verification of Missing Values

After preprocessing:

```python id="7a7l7u"
print(df.isnull().sum())
```

### Result

| Column      | Missing Values |
| ----------- | -------------- |
| All Columns | 0              |

The dataset became completely free of missing values.

---

## Feature Renaming

The passenger class column was renamed for improved readability.

### Before

```text id="m4zj8m"
Pclass
```

### After

```text id="qv7h1m"
PassangerClass
```

Implementation:

```python id="h8lf0g"
df.rename(
    columns={'Pclass':'PassangerClass'},
    inplace=True
)
```

---

## Data Type Conversion

The Age column originally had a floating-point data type because mean imputation introduced decimal values.

The column was converted to integer format:

```python id="e4yt0d"
df['Age'] = df['Age'].astype(int)
```

### Reason

* Passenger age is typically represented as a whole number.
* Simplifies interpretation and analysis.

---

## Dataset After Cleaning

### Final Features

| Feature        |
| -------------- |
| PassengerId    |
| Survived       |
| PassangerClass |
| Name           |
| Sex            |
| Age            |
| SibSp          |
| Parch          |
| Ticket         |
| Fare           |
| Embarked       |

### Dataset Characteristics

* Missing values removed
* Unnecessary column removed
* Improved feature naming
* Corrected data types
* Ready for visualization and machine learning

---

## Summary of Changes

| Operation               | Action Taken             |
| ----------------------- | ------------------------ |
| Missing Age Values      | Replaced with mean age   |
| Missing Cabin Values    | Dropped Cabin column     |
| Missing Embarked Values | Replaced with mode       |
| Column Renaming         | Pclass → PassangerClass  |
| Data Type Conversion    | Age converted to integer |

---

## Results

### Before Cleaning

* Total Features: 12
* Missing Age Values: 177
* Missing Cabin Values: 687
* Missing Embarked Values: 2

### After Cleaning

* Total Features: 11
* Missing Values: 0
* Dataset Ready for Analysis: Yes

---

## Conclusion

This project successfully cleaned and preprocessed the Titanic dataset by addressing missing values, removing highly incomplete features, renaming columns for clarity, and correcting data types.

The preprocessing workflow improved data quality while preserving the majority of available information. The resulting dataset is complete, consistent, and suitable for exploratory data analysis, visualization, statistical modeling, and machine learning applications such as Titanic survival prediction.

## Future Work

Possible next steps include:

* Exploratory Data Analysis (EDA)
* Survival rate analysis by gender and passenger class
* Feature engineering
* Data visualization
* Classification models for survival prediction
* Feature importance analysis
* Model evaluation and comparison
