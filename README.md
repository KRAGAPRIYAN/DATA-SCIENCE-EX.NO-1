#EX.NO:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

## Date: 22/05/2026
## Roll.No:212225040323

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

## Program

```
import pandas as pd
import numpy as np
from scipy import stats

# STEP 1: Read the given Data

df = pd.read_csv("Loan_data.csv")

print("Original Dataset")
print(df.head())

# STEP 2: Get information

print("\nDataset Information")
print(df.info())

print("\nMissing Values")
print(df.isnull().sum())

# STEP 3: Remove null values

df['Gender'] = df['Gender'].fillna(df['Gender'].mode()[0])
df['Dependents'] = df['Dependents'].fillna(df['Dependents'].mode()[0])
df['Self_Employed'] = df['Self_Employed'].fillna(df['Self_Employed'].mode()[0])
df['LoanAmount'] = df['LoanAmount'].fillna(df['LoanAmount'].median())
df['Loan_Amount_Term'] = df['Loan_Amount_Term'].fillna(df['Loan_Amount_Term'].median())
df['Credit_History'] = df['Credit_History'].fillna(df['Credit_History'].mode()[0])

# Remove duplicates
df = df.drop_duplicates()

print("\nCleaned Dataset")
print(df.head())

print("\nMissing Values After Cleaning")
print(df.isnull().sum())

# STEP 4: Save cleaned data

df.to_csv("Cleaned_Loan_data.csv", index=False)

print("\nCleaned data saved successfully")

# STEP 5: Remove Outliers using IQR

data = pd.read_csv("heights.csv")

print("\nHeights Dataset")
print(data)

Q1 = data['height'].quantile(0.25)
Q3 = data['height'].quantile(0.75)
IQR = Q3 - Q1

lower_limit = Q1 - 1.5 * IQR
upper_limit = Q3 + 1.5 * IQR

print("\nLower Limit =", lower_limit)
print("Upper Limit =", upper_limit)

# Detect outliers
iqr_outliers = data[
    (data['height'] < lower_limit) |
    (data['height'] > upper_limit)
]

print("\nOutliers using IQR")
print(iqr_outliers)

# Remove IQR outliers
iqr_clean = data[
    (data['height'] >= lower_limit) &
    (data['height'] <= upper_limit)
]

print("\nDataset after IQR Removal")
print(iqr_clean)

# STEP 6: Remove Outliers using Z-score

z = np.abs(stats.zscore(iqr_clean['height']))

zscore_clean = iqr_clean[z < 3]

print("\nDataset after Z-score Removal")
print(zscore_clean)
```

## Output

![alt text](<Screenshot 2026-05-26 085456.png>)
![alt text](<Screenshot 2026-05-26 085648.png>)
![alt text](<Screenshot 2026-05-26 085709.png>)
![alt text](<Screenshot 2026-05-26 085728.png>)

# Result

Thus the given dataset was read successfully, null values and duplicate values were removed, and the cleaned data was saved successfully. Outliers were detected and removed using both IQR and Z-score methods using Python.
