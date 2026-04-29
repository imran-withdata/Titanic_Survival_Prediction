# Titanic_Survival_Prediction


This project aims to analyze the famous Titanic dataset to understand the factors that influenced the survival of passengers and prepare the data for building a predictive model.

## Table of Contents
1.  [Introduction](#introduction)
2.  [Dataset](#dataset)
3.  [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
4.  [Feature Engineering](#feature-engineering)
5.  [Data Cleaning and Transformation](#data-cleaning-and-transformation)
6.  [Conclusion & Next Steps](#conclusion--next-steps)
7.  [Libraries Used](#libraries-used)

## Introduction
The sinking of the RMS Titanic is one of the most infamous shipwrecks in history. On April 15, 1912, during her maiden voyage, the Titanic sank after colliding with an iceberg, resulting in the deaths of 1502 out of 2224 passengers and crew. This project delves into the dataset of Titanic passengers to uncover patterns and relationships that might explain who survived and who perished.

## Dataset
The dataset used is `taitanic.csv`, which contains various information about each passenger, including:
*   `PassengerId`: A unique ID for each passenger.
*   `Survived`: Survival status (0 = No, 1 = Yes).
*   `Pclass`: Ticket class (1 = 1st, 2 = 2nd, 3 = 3rd).
*   `Name`: Passenger's name.
*   `Sex`: Passenger's sex (male/female).
*   `Age`: Age in years.
*   `SibSp`: Number of siblings/spouses aboard the Titanic.
*   `Parch`: Number of parents/children aboard the Titanic.
*   `Ticket`: Ticket number.
*   `Fare`: Passenger fare.
*   `Cabin`: Cabin number.
*   `Embarked`: Port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton).

## Exploratory Data Analysis (EDA)
Through various visualizations and statistical analyses, the following key insights were observed:

*   **Survival Rate**: Approximately 38% of the passengers survived.
*   **Sex**: Women had a significantly higher survival rate (around 74%) compared to men (around 19%). This highlights the "women and children first" protocol.
*   **Pclass**: Passengers in 1st class had the highest survival rates, followed by 2nd and 3rd class. This indicates that socio-economic status played a crucial role.
*   **Age**: Children (especially those under 10) had better survival chances. A high number of deaths occurred in the 30-40 age group. Missing age values were identified.
*   **Embarked**: Passengers embarking from Cherbourg (C) had a higher survival rate than those from Southampton (S) or Queenstown (Q).
*   **Family Size (SibSp & Parch)**: Passengers traveling alone or in very large families had lower survival chances compared to those with small to medium-sized families (1-4 members).
*   **Fare**: Higher fares were generally associated with higher survival rates, correlating with Pclass.

## Feature Engineering
To enhance the predictive power of our model, several new features were engineered:

*   **`Initial`**: Extracted titles (Mr, Mrs, Miss, Master, Other) from the `Name` feature to better represent social status and gender, and to aid in filling missing `Age` values.
*   **`Age_band`**: Continuous `Age` values were binned into 5 categories (0-16, 17-32, 33-48, 49-64, >64) to convert it into a categorical feature.
*   **`Family_Size`**: Created by summing `SibSp` and `Parch`, indicating the total number of family members aboard.
*   **`Alone`**: A binary feature indicating whether a passenger was traveling alone (1) or with family (0).
*   **`Fare_cat`**: `Fare` values were binned into 4 categories using `pd.qcut` to convert the continuous fare into an ordinal feature.

## Data Cleaning and Transformation

*   **Handling Missing Values**:
    *   `Age`: Missing `Age` values were imputed based on the mean age of their respective `Initial` (title) group.
    *   `Embarked`: The 2 missing `Embarked` values were filled with the most frequent port, 'S' (Southampton).
    *   `Cabin`: This feature had a large number of missing values and was deemed unhelpful for direct modeling, so it was dropped.
*   **Categorical to Numerical Conversion**: Features like `Sex`, `Embarked`, and `Initial` were converted into numerical representations (e.g., male=0, female=1) as machine learning models typically require numerical input.
*   **Dropping Redundant Features**: Original `Name`, `Age`, `Ticket`, `Fare`, `Cabin`, `Fare_Range`, and `PassengerId` columns were dropped as either their information was captured in new features or they were deemed irrelevant/too sparse.

## Conclusion & Next Steps
At this stage, the data has been thoroughly explored, engineered, and cleaned. It is now in a suitable format for building various machine learning models to predict survival on the Titanic. The next steps would involve:

1.  Splitting the data into training and testing sets.
2.  Applying various classification algorithms (e.g., Logistic Regression, SVM, Decision Trees, Random Forest, K-Nearest Neighbors).
3.  Evaluating model performance using metrics like accuracy, precision, reca
