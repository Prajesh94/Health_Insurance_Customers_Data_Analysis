# Health_Insurance_Customers_Data_Analysis
Capstone Project Final Submission

Health Insurance Customers Data Analysis
Health Insurance Customers Data Analysis_
PROJECT TITLE: Health Insurance Customers Data Analysis
Project Goals
The main goal of this project is to perform Exploratory Data Analysis (EDA) on health insurance customer data to identify meaningful patterns, trends, and insights.

Exploratory Data Analysis (EDA): Explore the health insurance dataset to understand its structure, characteristics, and patterns.

Customer and Policy-Wise Analysis: Analyze customer information and insurance policy details to understand customer profiles and policy distribution.

Statistical Analysis: Apply statistical methods to summarize customer demographics, insurance coverage, hospital expenses, and claim amounts.

Data Visualization: Use Matplotlib and Seaborn to create charts and graphs for clear and effective data presentation.

Customer Demographic Analysis: Analyze customers based on age, gender, location, occupation, and other demographic characteristics.

Policy and Coverage Analysis: Examine policy types, sum insured, and available policy-related information to understand coverage patterns.

Claim Analysis: Analyze claim amounts, claim-related information, and claim frequency to identify trends in insurance claims.

Insight Generation: Generate meaningful insights from the data to support better understanding of customer behavior, insurance coverage, healthcare expenses, and claim patterns.

Project Objectives
Understand the structure and characteristics of the health insurance dataset.

Identify and handle duplicate records and missing values appropriately.

Analyze customer demographics, including age, gender, and location where available.

Examine policy details, premiums, and coverage information.

Explore claim amounts, claim status, and other claim-related variables.

Use descriptive statistics and data visualizations to identify patterns and outliers.

Generate meaningful insights from the available health insurance data.


[103]
0s
# ==============================================================================
# IMPORT LIBRARIES & ENVIRONMENT SETUP
# ==============================================================================

# Data manipulation and analysis
import pandas as pd
import numpy as np

# Data visualization
import matplotlib.pyplot as plt
import seaborn as sns

# Interactive visualizations
import plotly.express as px

# Report formatting
from tabulate import tabulate

# Configure pandas options for display
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', 100)
pd.set_option('display.width', 1000)

print("Libraries imported and environment configured successfully!")
Libraries imported and environment configured successfully!

[104]
1s

Drive already mounted at /content/drive; to attempt to forcibly remount, call drive.mount("/content/drive", force_remount=True).
Google Drive mounted successfully!

[105]

📊 Dataset Description Summary
Dataset Name: Health Insurance Customer Dataset
Source: Google Colab Drive Link
Initial Records: 8,000 rows
Total Columns: 38
🔹 Float Columns: 9
🔹 Integer Columns: 7
🔹 Object Columns: 22
Duplicate Records Removed: 5
Final Records: 7,995 rows
Features List – Health Insurance Customer Dataset
Data loading and initial inspection of the dataset.
Data cleaning, including handling missing values, duplicate records, and inconsistent values.
Data type conversion and preprocessing.
Outlier detection and investigation using the IQR method.
Exploratory Data Analysis (EDA) using summary statistics.
Customer demographic analysis based on age, gender, and location.
Health condition analysis based on BMI, diabetes, hypertension, and other available health indicators.
Customer income and financial profile analysis.
Insurance policy-wise analysis.
Premium and coverage amount analysis.
Policy start date and claim date analysis.
Claim amount and claim status analysis.
Hospital bill amount and total claim amount analysis.
Hospitalization analysis based on ICU days and length of stay.
Statistical analysis of numerical variables.
Correlation analysis between relevant numerical variables.
Data visualization using Matplotlib and Seaborn.
Comparison of customer demographics, policy details, and claim trends.
Analysis of relationships between customer health conditions, insurance claims, hospital expenses, and other relevant variables.
Identification and investigation of unusual values and potential data quality issues.
Identification of key insights, patterns, and findings from the analysis.

[106]
0s
df


[107]
0s
df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 8000 entries, 0 to 7999
Data columns (total 38 columns):
 #   Column                        Non-Null Count  Dtype  
---  ------                        --------------  -----  
 0   policy_id                     8000 non-null   object 
 1   customer_name                 8000 non-null   object 
 2   gender                        8000 non-null   object 
 3   age                           8000 non-null   int64  
 4   marital_status                8000 non-null   object 
 5   state                         8000 non-null   object 
 6   city                          8000 non-null   object 
 7   pincode                       8000 non-null   int64  
 8   aadhaar_masked                8000 non-null   object 
 9   occupation_type               8000 non-null   object 
 10  annual_income_inr             7437 non-null   object 
 11  bmi                           7440 non-null   float64
 12  tobacco_usage                 8000 non-null   object 
 13  alcohol_units_per_week        8000 non-null   int64  
 14  physical_activity_level       8000 non-null   object 
 15  diet_type                     8000 non-null   object 
 16  has_diabetes                  7617 non-null   float64
 17  has_hypertension              7609 non-null   float64
 18  family_history_cardiac        8000 non-null   int64  
 19  stress_level_score            7440 non-null   float64
 20  policy_type                   8000 non-null   object 
 21  sum_insured                   8000 non-null   int64  
 22  policy_start_date             8000 non-null   object 
 23  claim_date                    8000 non-null   object 
 24  hospital_name                 8000 non-null   object 
 25  hospital_tier                 8000 non-null   object 
 26  room_category                 8000 non-null   object 
 27  icu_days                      8000 non-null   int64  
 28  length_of_stay                8000 non-null   int64  
 29  cashless_claim                8000 non-null   object 
 30  agent_channel                 7999 non-null   object 
 31  hospital_bill_amount          8000 non-null   object 
 32  pre_hospitalization_expense   8000 non-null   float64
 33  post_hospitalization_expense  7999 non-null   float64
 34  non_payable_items             8000 non-null   float64
 35  deductible_amount             8000 non-null   float64
 36  co_pay_amount                 7998 non-null   float64
 37  total_claim_amount            8000 non-null   object 
dtypes: float64(9), int64(7), object(22)
memory usage: 2.3+ MB

[108]
0s
df.head()


[109]
0s
df.tail()


[110]
0s
df.shape
(8000, 38)

[111]
0s
df.columns
Index(['policy_id', 'customer_name', 'gender', 'age', 'marital_status', 'state', 'city', 'pincode', 'aadhaar_masked', 'occupation_type', 'annual_income_inr', 'bmi', 'tobacco_usage', 'alcohol_units_per_week', 'physical_activity_level', 'diet_type', 'has_diabetes', 'has_hypertension', 'family_history_cardiac', 'stress_level_score', 'policy_type', 'sum_insured', 'policy_start_date', 'claim_date', 'hospital_name', 'hospital_tier', 'room_category', 'icu_days', 'length_of_stay', 'cashless_claim', 'agent_channel', 'hospital_bill_amount', 'pre_hospitalization_expense', 'post_hospitalization_expense', 'non_payable_items', 'deductible_amount', 'co_pay_amount', 'total_claim_amount'], dtype='object')

[112]
0s
df.dtypes


[113]
0s
df.describe()


[114]
0s
df.isnull().sum()


[115]
0s
df.duplicated().sum()
np.int64(5)
Data Cleaning
Checking the dataset structure, column names, and data types.
Identifying missing values in each column.
Detecting duplicate records.
Converting columns to appropriate data types.
Converting date columns into the correct date format.
Correcting inconsistent values in categorical columns.
Cleaning numerical columns and handling invalid values.
Checking for invalid values in age, BMI, income, and medical expenses.
Validating policy start dates and claim dates.
Checking consistency between ICU days and hospital length of stay.
Handling missing values using appropriate methods.
Removing duplicate records.
Detecting and investigating outliers using the IQR method.
Verifying data quality after cleaning.
Performing final checks for missing values and duplicates.
Preparing the cleaned dataset for Exploratory Data Analysis (EDA).
Step 1: Checking dataset structure, column names, and data types

[116]
0s
# Step 1: Initial dataset inspection

print("Dataset Shape:", df.shape)
print("\nColumn Names:")
print(df.columns.tolist())

print("\nDataset Information:")
df.info()

print("\nData Types:")
display(df.dtypes.to_frame(name="Data Type"))

Step 2: Identifying missing values in each column

[117]
0s
# Step 2: Check missing values

missing_report = pd.DataFrame({
    "Missing Values": df.isnull().sum(),
    "Missing Percentage": (df.isnull().mean() * 100).round(2)
})

display(missing_report.sort_values(
    by="Missing Values", ascending=False
))

print("Total Missing Values:", df.isnull().sum().sum())

Step 3: Detecting duplicate records

[118]
0s


Step 4: Converting columns to appropriate data types

[119]
0s
# Step 4: Review column data types

print("Current Data Types:")
display(df.dtypes.to_frame(name="Data Type"))

# Identify numerical and categorical columns
numerical_columns = df.select_dtypes(
    include="number"
).columns.tolist()

categorical_columns = df.select_dtypes(
    include=["object", "category", "bool"]
).columns.tolist()

print("\nNumerical Columns:", numerical_columns)
print("\nCategorical Columns:", categorical_columns)

Step 5: Converting date columns into the correct date format

[120]
0s
# Step 5: Convert date columns

date_columns = ["policystartdate", "claimdate"]

for col in date_columns:
    if col in df.columns:
        df[col] = pd.to_datetime(df[col], errors="coerce")

print("Date conversion completed.")

for col in date_columns:
    if col in df.columns:
        print(col, ":", df[col].dtype)
        print("Missing or invalid dates:", df[col].isna().sum())
Date conversion completed.
Step 6. Correct inconsistent values in categorical columns

[121]
0s

# Step 6: Remove unnecessary spaces from text columns

categorical_columns = df.select_dtypes(
    include=["object", "category"]
).columns.tolist()

for col in categorical_columns:
    df[col] = df[col].apply(
        lambda x: x.strip() if isinstance(x, str) else x
    )

print("Unnecessary spaces removed.")

# Inspect category values
for col in categorical_columns:
    print(f"\n{col}:")
    print(df[col].value_counts(dropna=False).head(10))

Unnecessary spaces removed.

policy_id:
policy_id
IND107279    4
IND102340    3
IND101868    1
IND103872    1
IND107119    1
IND101700    1
IND107107    1
IND106519    1
IND105081    1
IND105435    1
Name: count, dtype: int64

customer_name:
customer_name
Christopher Sur        4
Nakul Raghavan         3
Laksh Dewan            2
Kashish Edwin          2
Sanaya Som             2
Unni Kothari           2
Yashoda Rau            2
Meera Garde            2
Rachana Ranganathan    2
Rudra Sridhar          2
Name: count, dtype: int64

gender:
gender
female    1362
F         1350
Male      1335
male      1334
Female    1328
M         1291
Name: count, dtype: int64

marital_status:
marital_status
Widowed     1681
married     1633
Married     1571
Single      1559
Divorced    1556
Name: count, dtype: int64

state:
state
Uttar Pradesh    1424
Tamil Nadu       1384
West Bengal      1320
Karnataka        1297
Delhi            1288
Maharashtra      1287
Name: count, dtype: int64

city:
city
Kolkata       1320
New Delhi     1288
Chennai        704
Coimbatore     680
Bengaluru      654
Mysuru         643
Noida          496
Kanpur         495
Mumbai         441
Lucknow        433
Name: count, dtype: int64

aadhaar_masked:
aadhaar_masked
XXXX-XXXX-4379    5
XXXX-XXXX-7897    5
XXXX-XXXX-5317    5
XXXX-XXXX-7202    5
XXXX-XXXX-9743    5
XXXX-XXXX-4106    5
XXXX-XXXX-8679    5
XXXX-XXXX-1644    5
XXXX-XXXX-3527    5
XXXX-XXXX-8273    5
Name: count, dtype: int64

occupation_type:
occupation_type
Unemployed       1406
Student          1388
Self-employed    1324
Salaried         1320
Business         1288
Retired          1274
Name: count, dtype: int64

annual_income_inr:
annual_income_inr
NaN         563
6.3 LPA      17
4.5 LPA      12
5.4 LPA      12
6.1 LPA      12
6.2 LPA      11
3.9 LPA      10
10.2 LPA     10
7.0 LPA      10
4.8 LPA       9
Name: count, dtype: int64

tobacco_usage:
tobacco_usage
none       4424
smoking    1985
chewing    1193
both        398
Name: count, dtype: int64

physical_activity_level:
physical_activity_level
low         3243
moderate    3204
high        1553
Name: count, dtype: int64

diet_type:
diet_type
vegan         2023
non-veg       2016
eggetarian    1997
veg           1964
Name: count, dtype: int64

policy_type:
policy_type
individual        3902
family_floater    2843
senior_citizen    1255
Name: count, dtype: int64

policy_start_date:
policy_start_date
10-08-2020    12
11-05-2020    11
13-03-2020    11
13-06-2021    11
01-11-2022    10
27-05-2022    10
06-04-2021    10
01-06-2020    10
17-01-2022    10
04-12-2022    10
Name: count, dtype: int64

claim_date:
claim_date
30-06-2024    10
08-03-2024    10
31-05-2023    10
05-01-2024    10
04-04-2023    10
22-09-2022     9
10-09-2023     9
28-10-2022     9
02-10-2024     9
20-02-2024     9
Name: count, dtype: int64

hospital_name:
hospital_name
Kaul Group Hospital       6
Wali Ltd Hospital         5
Dhar and Sons Hospital    5
Kala Inc Hospital         5
Mani Inc Hospital         5
Master Ltd Hospital       4
Saha LLC Hospital         4
Joshi PLC Hospital        4
Kapadia Inc Hospital      4
Buch Ltd Hospital         4
Name: count, dtype: int64

hospital_tier:
hospital_tier
private_corporate    4038
private_small        2766
govt                 1196
Name: count, dtype: int64

room_category:
room_category
private         2039
deluxe          1993
semi-private    1985
general         1983
Name: count, dtype: int64

cashless_claim:
cashless_claim
yes    5573
no     2427
Name: count, dtype: int64

agent_channel:
agent_channel
aggregator       2063
bancassurance    1990
online           1976
agent            1970
NaN                 1
Name: count, dtype: int64

hospital_bill_amount:
hospital_bill_amount
5000          10
82792.92       4
53122.25       3
173995.15      2
â‚¹119,068     2
â‚¹67,443      2
â‚¹172,012     2
â‚¹45,901      2
30894.1        1
204298.85      1
Name: count, dtype: int64

total_claim_amount:
total_claim_amount
5000          9
78465.72      4
59218.94      3
â‚¹68,492     2
5,000         2
99182.94      2
72,449        2
â‚¹67,312     1
29949.94      1
â‚¹102,063    1
Name: count, dtype: int64
Step 7. Clean numerical columns and identify invalid values

[122]
0s

# Step 7: Identify numerical columns

numerical_columns = df.select_dtypes(
    include="number"
).columns.tolist()

print("Numerical Columns:")
print(numerical_columns)

# Display numerical summary
display(df[numerical_columns].describe().T)


Step 8. Check invalid values in age, BMI, income, and medical expenses

[123]
0s

# Step 8: Identify potentially invalid values

validation_rules = {
    "age": lambda s: (s < 0) | (s > 120),
    "bmi": lambda s: (s < 10) | (s > 80),
    "annualincomeinr": lambda s: s < 0,
    "hospitalbillamount": lambda s: s < 0,
    "totalclaimamount": lambda s: s < 0,
    "icudays": lambda s: s < 0,
    "lengthofstay": lambda s: s < 0,
    "alcoholunitsperweek": lambda s: s < 0
}

for col, rule in validation_rules.items():
    if col in df.columns:
        invalid_rows = df[rule(df[col])]

        print(f"\n{col}: {len(invalid_rows)} potentially invalid records")
        display(invalid_rows.head(5))


Step 9. Validate policy start dates and claim dates

[124]

# Step 9: Check policy and claim dates

for col in ["policystartdate", "claimdate"]:
    if col in df.columns:
        print(f"{col} missing dates:", df[col].isna().sum())

if {"policystartdate", "claimdate"}.issubset(df.columns):

    invalid_dates = df[
        df["claimdate"].notna()
        & df["policystartdate"].notna()
        & (df["claimdate"] < df["policystartdate"])
    ]

    print(
        "\nClaims dated before policy start:",
        len(invalid_dates)
    )

    display(invalid_dates.head(10))

Step 10: Check consistency between ICU days and hospital stay

[125]
0s

# Step 10: Validate hospital stay duration

if {"icudays", "lengthofstay"}.issubset(df.columns):

    invalid_stay = df[
        df["icudays"].notna()
        & df["lengthofstay"].notna()
        & (df["icudays"] > df["lengthofstay"])
    ]

    print(
        "Records where ICU days exceed hospital stay:",
        len(invalid_stay)
    )

    display(invalid_stay.head(10))
else:
    print("Required columns are not available.")

Required columns are not available.
Step 11. Handle missing values using appropriate methods

[126]
0s

# Step 11: Handle missing values

# Selected numerical columns
numeric_to_fill = [
    "bmi",
    "stresslevelscore",
    "annualincomeinr",
    "hospitalbillamount",
    "totalclaimamount"
]

for col in numeric_to_fill:
    if col in df.columns:
        df[col] = pd.to_numeric(df[col], errors="coerce")

        if df[col].notna().any():
            df[col] = df[col].fillna(df[col].median())

# Selected categorical columns
categorical_to_fill = [
    "hasdiabetes",
    "hashypertension"
]

for col in categorical_to_fill:
    if col in df.columns:
        mode_values = df[col].mode(dropna=True)

        if not mode_values.empty:
            df[col] = df[col].fillna(mode_values[0])

print("Missing value treatment completed.")
print("\nRemaining Missing Values:")
display(df.isnull().sum()[df.isnull().sum() > 0])


Step 12. Remove duplicate records

[127]
0s

# Step 12: Remove exact duplicate rows

duplicates_before = df.duplicated().sum()

df = df.drop_duplicates().copy()

duplicates_after = df.duplicated().sum()

print("Duplicates Before Removal:", duplicates_before)
print("Duplicates After Removal:", duplicates_after)
print("Dataset Shape After Removal:", df.shape)

Duplicates Before Removal: 5
Duplicates After Removal: 0
Dataset Shape After Removal: (7995, 38)
Step 13. Detect and investigate outliers using the IQR method

[128]
0s

# Step 13: Detect outliers using IQR

numerical_columns = df.select_dtypes(
    include="number"
).columns.tolist()

outlier_results = []

for col in numerical_columns:

    values = df[col].dropna()

    if values.empty:
        continue

    Q1 = values.quantile(0.25)
    Q3 = values.quantile(0.75)
    IQR = Q3 - Q1

    lower_limit = Q1 - 1.5 * IQR
    upper_limit = Q3 + 1.5 * IQR

    outlier_count = (
        (values < lower_limit) |
        (values > upper_limit)
    ).sum()

    outlier_results.append({
        "Column": col,
        "Q1": Q1,
        "Q3": Q3,
        "IQR": IQR,
        "Lower Limit": lower_limit,
        "Upper Limit": upper_limit,
        "Outlier Count": outlier_count
    })

outlier_table = pd.DataFrame(outlier_results)

display(outlier_table)


Step 14. Verify data quality after cleaning

[129]
0s

# Step 14: Review cleaned dataset

print("Dataset Shape:", df.shape)
print("Duplicate Records:", df.duplicated().sum())
print("Total Missing Values:", df.isnull().sum().sum())

print("\nDataset Information:")
df.info()

Dataset Shape: (7995, 38)
Duplicate Records: 0
Total Missing Values: 1898

Dataset Information:
<class 'pandas.core.frame.DataFrame'>
Index: 7995 entries, 0 to 7999
Data columns (total 38 columns):
 #   Column                        Non-Null Count  Dtype  
---  ------                        --------------  -----  
 0   policy_id                     7995 non-null   object 
 1   customer_name                 7995 non-null   object 
 2   gender                        7995 non-null   object 
 3   age                           7995 non-null   int64  
 4   marital_status                7995 non-null   object 
 5   state                         7995 non-null   object 
 6   city                          7995 non-null   object 
 7   pincode                       7995 non-null   int64  
 8   aadhaar_masked                7995 non-null   object 
 9   occupation_type               7995 non-null   object 
 10  annual_income_inr             7435 non-null   object 
 11  bmi                           7995 non-null   float64
 12  tobacco_usage                 7995 non-null   object 
 13  alcohol_units_per_week        7995 non-null   int64  
 14  physical_activity_level       7995 non-null   object 
 15  diet_type                     7995 non-null   object 
 16  has_diabetes                  7612 non-null   float64
 17  has_hypertension              7604 non-null   float64
 18  family_history_cardiac        7995 non-null   int64  
 19  stress_level_score            7435 non-null   float64
 20  policy_type                   7995 non-null   object 
 21  sum_insured                   7995 non-null   int64  
 22  policy_start_date             7995 non-null   object 
 23  claim_date                    7995 non-null   object 
 24  hospital_name                 7995 non-null   object 
 25  hospital_tier                 7995 non-null   object 
 26  room_category                 7995 non-null   object 
 27  icu_days                      7995 non-null   int64  
 28  length_of_stay                7995 non-null   int64  
 29  cashless_claim                7995 non-null   object 
 30  agent_channel                 7994 non-null   object 
 31  hospital_bill_amount          7995 non-null   object 
 32  pre_hospitalization_expense   7995 non-null   float64
 33  post_hospitalization_expense  7994 non-null   float64
 34  non_payable_items             7995 non-null   float64
 35  deductible_amount             7995 non-null   float64
 36  co_pay_amount                 7993 non-null   float64
 37  total_claim_amount            7995 non-null   object 
dtypes: float64(9), int64(7), object(22)
memory usage: 2.4+ MB
Step 15. Perform final checks for missing values and duplicates

[130]
0s

# Step 15: Final data quality report

final_report = pd.DataFrame({
    "Data Type": df.dtypes.astype(str),
    "Missing Values": df.isnull().sum(),
    "Missing Percentage": (
        df.isnull().mean() * 100
    ).round(2),
    "Unique Values": df.nunique()
})

display(final_report)

print("\nFinal Number of Rows:", df.shape[0])
print("Final Number of Columns:", df.shape[1])
print("Final Duplicate Records:", df.duplicated().sum())


Step 16. Prepare the cleaned dataset for EDA

[131]
0s

# Step 16: Save the cleaned dataset

cleaned_file = "health_insurance_cleaned.csv"

df.to_csv(cleaned_file, index=False)

print("Cleaned dataset saved successfully.")
print("Final Dataset Shape:", df.shape)

# Download the cleaned CSV file
from google.colab import files
files.download(cleaned_file)


Exploratory Data Analysis (EDA)
Exploratory Data Analysis (EDA) was performed on the cleaned Health Insurance Customer Dataset to understand customer demographics, health conditions, insurance policies, and claim-related information. Descriptive statistics were used to summarize numerical variables and identify unusual values. Data visualizations were created using Matplotlib and Seaborn to identify patterns, trends, distributions, and relationships between variables.
The analysis included customer age and BMI distributions, income patterns, health conditions, hospital expenses, claim amounts, and hospitalization details. Correlation analysis was used to examine relationships between numerical variables. The findings help provide a better understanding of customer characteristics, healthcare expenses, and insurance claim patterns.
Step 1: Import libraries and load the dataset

[139]
0s
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files
import os

file_path = "/content/Health Insurance Customers Data Analysis.csv"

if os.path.exists(file_path):
    a = pd.read_csv(file_path)
else:
    uploaded = files.upload()
    file_path = next(iter(uploaded))
    a = pd.read_csv(file_path)

print("Dataset loaded successfully!")
print("Initial shape:", a.shape)
display(a.head())

Step 2: Dataset overview

[140]
0s
print("COLUMN NAMES")
print(a.columns.tolist())

print("\nDATASET INFORMATION")
a.info()

print("\nMISSING VALUES IN EACH COLUMN")
display(a.isnull().sum().to_frame("Missing Values"))

print("\nDUPLICATE RECORDS")
print(a.duplicated().sum())

print("\nSTATISTICAL SUMMARY")
display(a.describe(include="all").T)

Step 3 — Clean the dataset

[141]
0s
# Standardize column-name spacing and capitalization
a.columns = a.columns.str.strip().str.lower()

# Remove duplicate records
a = a.drop_duplicates().copy()

print("Shape after removing duplicates:", a.shape)
print("Remaining duplicates:", a.duplicated().sum())

# Check missing values before treatment
print("\nMissing values before treatment:")
display(a.isnull().sum().to_frame("Missing Values"))

# Check data types
print("\nData types:")
display(a.dtypes.to_frame("Data Type"))

Step 4 — Correct data types

[142]
0s
# Convert date columns only if present
date_cols = ["policy_start_date", "claim_date"]

for col in date_cols:
    if col in a.columns:
        a[col] = pd.to_datetime(a[col], errors="coerce")

# Convert numeric fields that may have been read as text
numeric_candidates = [
    "age",
    "bmi",
    "stress_level_score",
    "annual_income_inr",
    "hospital_bill_amount",
    "total_claim_amount",
    "sum_insured",
    "premium_amount",
    "alcohol_units_per_week",
    "icu_days",
    "length_of_stay"
]

for col in numeric_candidates:
    if col in a.columns:
        a[col] = pd.to_numeric(a[col], errors="coerce")

print("Data types after conversion:")
display(a.dtypes.to_frame("Data Type"))

Step 5 — Handle missing values carefully

[143]
0s
# Fill selected numeric columns with their median
median_cols = [
    "bmi",
    "stress_level_score",
    "annual_income_inr"
]

for col in median_cols:
    if col in a.columns and a[col].notna().any():
        a[col] = a[col].fillna(a[col].median())

# Fill missing agent channel only if the column exists
if "agent_channel" in a.columns:
    a["agent_channel"] = a["agent_channel"].fillna("Unknown")

print("Missing values after selected treatments:")
display(a.isnull().sum().to_frame("Remaining Missing Values"))

Step 6 — Numerical data analysis

[144]
0s
numeric_cols = a.select_dtypes(include=np.number).columns.tolist()

print("Numerical columns:")
print(numeric_cols)

if numeric_cols:
    print("\nMean")
    display(a[numeric_cols].mean().to_frame("Mean"))

    print("\nMedian")
    display(a[numeric_cols].median().to_frame("Median"))

    print("\nMinimum")
    display(a[numeric_cols].min().to_frame("Minimum"))

    print("\nMaximum")
    display(a[numeric_cols].max().to_frame("Maximum"))

    print("\nStandard Deviation")
    display(a[numeric_cols].std().to_frame("Standard Deviation"))

    print("\nComplete Statistical Summary")
    display(a[numeric_cols].describe().T)

Step 7 — Categorical data analysis

[145]
0s
categorical_cols = a.select_dtypes(
    include=["object", "category", "bool"]
).columns.tolist()

print("Categorical columns:")
print(categorical_cols)

for col in categorical_cols:
    print(f"\nCategory Analysis: {col}")

    counts = a[col].value_counts(dropna=False)
    percentages = (
        a[col].value_counts(dropna=False, normalize=True) * 100
    ).round(2)

    result = pd.concat(
        [
            counts.rename("Count"),
            percentages.rename("Percentage (%)")
        ],
        axis=1
    )

    display(result)

Step 8 — Most common categories

[146]
0s
for col in categorical_cols:
    print(f"\nMost Common Category: {col}")

    modes = a[col].mode(dropna=True)
    print("Mode:", modes.tolist())

    display(a[col].value_counts(dropna=False).head(5))

Step 9 — Customer demographic analysis

[147]
0s
demographic_cols = [
    "age", "gender", "city", "state",
    "bmi", "annual_income_inr"
]

for col in demographic_cols:
    if col in a.columns:
        print(f"\nDemographic Analysis: {col}")

        if pd.api.types.is_numeric_dtype(a[col]):
            display(a[col].describe().to_frame())
        else:
            display(a[col].value_counts(dropna=False).to_frame("Count"))

Step 10 — Policy and premium analysis

[148]
0s
policy_cols = [
    "policy_type", "sum_insured", "premium_amount",
    "policy_start_date"
]

for col in policy_cols:
    if col in a.columns:
        print(f"\nPolicy Analysis: {col}")

        if pd.api.types.is_numeric_dtype(a[col]):
            display(a[col].describe().to_frame())
        else:
            display(a[col].value_counts(dropna=False).to_frame("Count"))

# Average premium by policy type
if {"policy_type", "premium_amount"}.issubset(a.columns):
    print("\nAverage Premium by Policy Type:")

    display(
        a.groupby("policy_type", dropna=False)["premium_amount"]
        .agg(["count", "mean", "median", "min", "max"])
        .round(2)
    )

# Sum insured by policy type
if {"policy_type", "sum_insured"}.issubset(a.columns):
    print("\nAverage Sum Insured by Policy Type:")

    display(
        a.groupby("policy_type", dropna=False)["sum_insured"]
        .mean()
        .sort_values(ascending=False)
        .to_frame("Average Sum Insured")
    )

Step 11 — Claim analysis

[149]
0s
claim_cols = [
    "claim_status",
    "claim_date",
    "hospital_bill_amount",
    "total_claim_amount",
    "icu_days",
    "length_of_stay"
]

for col in claim_cols:
    if col in a.columns:
        print(f"\nClaim Analysis: {col}")

        if pd.api.types.is_numeric_dtype(a[col]):
            display(a[col].describe().to_frame())
        else:
            display(a[col].value_counts(dropna=False).to_frame("Count"))

# Average claim amount by claim status
if {"claim_status", "total_claim_amount"}.issubset(a.columns):
    print("\nClaim Amount by Claim Status:")

    display(
        a.groupby("claim_status", dropna=False)["total_claim_amount"]
        .agg(["count", "mean", "median", "sum"])
        .round(2)
    )

# Average hospital bill by claim status
if {"claim_status", "hospital_bill_amount"}.issubset(a.columns):
    print("\nHospital Bill by Claim Status:")

    display(
        a.groupby("claim_status", dropna=False)["hospital_bill_amount"]
        .agg(["count", "mean", "median"])
        .round(2)
    )

Step 12 — Percentage analysis

[150]
0s
percentage_candidates = [
    "gender",
    "policy_type",
    "claim_status",
    "has_diabetes",
    "has_hypertension",
    "smoking_status",
    "agent_channel"
]

for col in percentage_candidates:
    if col in a.columns:
        print(f"\nPercentage Distribution: {col}")

        percentages = (
            a[col].value_counts(normalize=True, dropna=False) * 100
        ).round(2)

        display(percentages.to_frame("Percentage (%)"))

STEP 13: DISTRIBUTION ANALYSIS – STATISTICAL DETAILS & SUMMARY

[158]
import pandas as pd
import numpy as np
import re

# Helper function to clean text/currency into floats
def clean_numeric_col(val):
    if pd.isna(val): return np.nan
    s = re.sub(r'[^\d.]', '', str(val))
    return float(s) if s else np.nan

# Select key numerical columns for distribution analysis
numerical_columns = [
    'age', 'annual_income_inr', 'bmi', 'icu_days',
    'length_of_stay', 'stress_level_score', 'total_claim_clean'
]

# Ensure all target columns are converted to clean floats before calculation
for col in numerical_columns:
    if col in df.columns:
        if df[col].dtype == 'object':
            df[col] = df[col].apply(clean_numeric_col)

valid_num_cols = [col for col in numerical_columns if col in df.columns]

print("=" * 60)
print("DISTRIBUTION ANALYSIS – STATISTICAL SUMMARY")
print("=" * 60)

print("\n--- Mean ---")
print(df[valid_num_cols].mean().round(2))

print("\n--- Median ---")
print(df[valid_num_cols].median().round(2))

print("\n--- Minimum ---")
print(df[valid_num_cols].min())

print("\n--- Maximum ---")
print(df[valid_num_cols].max())

print("\n--- Standard Deviation ---")
print(df[valid_num_cols].std().round(2))

print("\n--- Full Descriptive Statistics (df.describe()) ---")
display(df[valid_num_cols].describe().round(2))

Step 14 — Correlation analysis

[160]
0s
# Select numerical columns for correlation matrix
numeric_df = df.select_dtypes(include='number')

# Calculate correlation coefficients (-1 to +1)
correlation_matrix = numeric_df.corr()

print("=" * 60)
print("CORRELATION ANALYSIS (NUMERICAL FEATURES)")
print("=" * 60)
display(correlation_matrix.round(4))

Step 15 — Outlier analysis using IQR

[153]
0s
outlier_results = []

for col in numeric_cols:
    values = a[col].dropna()

    if len(values) > 0:
        q1 = values.quantile(0.25)
        q3 = values.quantile(0.75)
        iqr = q3 - q1

        lower = q1 - 1.5 * iqr
        upper = q3 + 1.5 * iqr

        outlier_count = (
            (values < lower) | (values > upper)
        ).sum()

        outlier_results.append({
            "Column": col,
            "Q1": q1,
            "Q3": q3,
            "Lower Limit": lower,
            "Upper Limit": upper,
            "Outlier Count": int(outlier_count)
        })

display(pd.DataFrame(outlier_results))

Step 16 — Data validation

[154]
0s
# Check potential invalid values
validation_rules = {
    "age": lambda s: s.lt(0),
    "bmi": lambda s: s.le(0),
    "annual_income_inr": lambda s: s.lt(0),
    "hospital_bill_amount": lambda s: s.lt(0),
    "total_claim_amount": lambda s: s.lt(0),
    "sum_insured": lambda s: s.lt(0),
    "premium_amount": lambda s: s.lt(0),
    "icu_days": lambda s: s.lt(0),
    "length_of_stay": lambda s: s.lt(0)
}

for col, rule in validation_rules.items():
    if col in a.columns:
        invalid = rule(a[col].dropna())
        print(f"{col}: {int(invalid.sum())} potential invalid values")

# Check claim date before policy start date
if {"policy_start_date", "claim_date"}.issubset(a.columns):
    invalid_dates = (
        a["claim_date"].notna()
        & a["policy_start_date"].notna()
        & (a["claim_date"] < a["policy_start_date"])
    )

    print(
        "Claims dated before policy start:",
        int(invalid_dates.sum())
    )

# Check ICU days greater than length of stay
if {"icu_days", "length_of_stay"}.issubset(a.columns):
    invalid_icu = (
        a["icu_days"].notna()
        & a["length_of_stay"].notna()
        & (a["icu_days"] > a["length_of_stay"])
    )

    print(
        "Records where ICU days exceed length of stay:",
        int(invalid_icu.sum())
    )
age: 0 potential invalid values
bmi: 0 potential invalid values
annual_income_inr: 0 potential invalid values
hospital_bill_amount: 0 potential invalid values
total_claim_amount: 0 potential invalid values
sum_insured: 0 potential invalid values
icu_days: 0 potential invalid values
length_of_stay: 0 potential invalid values
Claims dated before policy start: 0
Records where ICU days exceed length of stay: 0
Step 17 — Final EDA summary

[155]
0s
print("=" * 55)
print("HEALTH INSURANCE CUSTOMER DATA - EDA SUMMARY")
print("=" * 55)

print("Total Records:", a.shape[0])
print("Total Columns:", a.shape[1])
print("Duplicate Records:", a.duplicated().sum())
print("Total Missing Values:", int(a.isnull().sum().sum()))
print("Numerical Columns:", len(a.select_dtypes(include=np.number).columns))
print(
    "Categorical Columns:",
    len(a.select_dtypes(include=["object", "category", "bool"]).columns)
)

print("\nMissing Values by Column:")
display(a.isnull().sum().to_frame("Missing Values"))

print("\nDataset Preview:")
display(a.head())

print("\nEDA Analysis Completed!")

Data Visualization
In this section, we create informative visual representations using Matplotlib, Seaborn, and Plotly to uncover hidden patterns in customer demographics, medical expenses, and insurance claims.

[165]
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import plotly.express as px
import seaborn as sns

# Assume 'df' is loaded and preprocessed Health Insurance Customer Dataset
# Setting design style
sns.set_theme(style="whitegrid")
plt.rcParams["font.sans-serif"] = "DejaVu Sans"
1. Bar Chart – Policy Type Distribution
Goal: To identify the most and least popular policy types among customers.
Categories used: policy_type and the count of policies in each category.

[166]
0s
# Code
df["policy_type"].value_counts().plot(kind="bar", color="#1f77b4")
plt.title("Policy Type Distribution")
plt.xlabel("Policy Type")
plt.ylabel("Number of Customers")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()

Output explanation: The height of each bar represents the total number of customers enrolled in each policy type, allowing quick visual comparison across options.
Insight: Individual policies account for 48.80%, Family Floater policies account for 35.56%, and Senior Citizen policies account for 15.64% of all coverage plans.
2. Line Chart – Monthly Claim Trends
Goal: To track fluctuations and seasonality in insurance claim submissions over the calendar year.
Categories used: claim_month and the number of claims recorded in each month.

[167]
0s
# Code
months = [
    "January",
    "February",
    "March",
    "April",
    "May",
    "June",
    "July",
    "August",
    "September",
    "October",
    "November",
    "December",
]

df["claim_month"] = pd.to_datetime(
    df["claim_date"], format="%d-%m-%Y", errors="coerce"
).dt.month_name()
monthly_claims = (
    df["claim_month"].value_counts().reindex(months, fill_value=0)
)

monthly_claims.plot(kind="line", marker="o", color="#2ca02c", linewidth=2)

plt.title("Monthly Claim Trends")
plt.xlabel("Month")
plt.ylabel("Number of Claims")
plt.xticks(range(12), months, rotation=45)
plt.grid(True, linestyle="--", alpha=0.6)
plt.tight_layout()
plt.show()

Output explanation: The continuous line plot highlights peaks and troughs in claim frequency across the twelve months.
Insight: Claim filings display steady volume throughout the year with subtle peaks during monsoon and winter months due to heightened seasonal illnesses.
3. Histogram – Customer Age Distribution
Goal: To identify the age brackets containing the highest and lowest concentration of policyholders.
Categories used: age, grouped into continuous numerical bins.

[168]
0s
# Code
plt.hist(df["age"], bins=10, color="#4c72b0", edgecolor="black")
plt.title("Customer Age Distribution")
plt.xlabel("Age (Years)")
plt.ylabel("Number of Customers")
plt.tight_layout()
plt.show()

Output explanation: Each vertical bar represents a specific age group interval, with the height showing how many customers belong to that bracket.
Insight: The average customer age is 41.75 years, with a median of 41 years, spanning an active policyholder age range from 18 to 85 years.
4. Box Plot – Hospital Bill Amount Outlier Analysis
Goal: To detect unusually high or suspicious hospital bill amounts that deviate from standard medical expenses.
Category used: hospital_bill_amount — the cleaned numerical billing amount for each hospitalization


[169]
0s
# Code
df["hospital_bill_amount_num"] = pd.to_numeric(
    df["hospital_bill_amount"].astype(str).str.replace(r"[^\d.]", "", regex=True),
    errors="coerce",
)

sns.boxplot(y=df["hospital_bill_amount_num"], color="#e74c3c")

plt.title("Hospital Bill Amount Outlier Analysis")
plt.ylabel("Hospital Bill Amount (₹)")
plt.tight_layout()
plt.show()

Output explanation: The central box indicates the interquartile range (IQR, middle 50% of bills), the horizontal median line splits the distribution, and isolated points beyond the whiskers denote upper billing outliers.
Insight: While typical hospital bills cluster between ₹50,000 and ₹2,500,000, extreme high-cost treatments form prominent outliers requiring targeted audit verification.
5. Scatter Plot – Pre-Hospitalization vs. Post-Hospitalization Expenses
Goal: To examine whether higher pre-admission expenses correlate with larger post-discharge medical costs.
Categories used: pre_hospitalization_expense on the x-axis and post_hospitalization_expense on the y-axis.

[170]
0s
# Code
sns.scatterplot(
    data=df,
    x="pre_hospitalization_expense",
    y="post_hospitalization_expense",
    alpha=0.6,
    color="#8e44ad",
)

plt.title("Pre-Hospitalization vs Post-Hospitalization Expenses")
plt.xlabel("Pre-Hospitalization Expense (₹)")
plt.ylabel("Post-Hospitalization Expense (₹)")
plt.tight_layout()
plt.show()

Output explanation: Each plotted marker represents a single customer claim record mapped across both expenditure axes.
Insight: A positive linear trajectory demonstrates that patients requiring extensive diagnostic/pre-care treatments systematically incur larger post-discharge treatment costs.
6. Pie Chart – Gender Distribution
Goal: To evaluate gender equity and demographic composition across the customer base.
Categories used: gender — Male, Female (standardized).

[171]
0s
# Code
gender_clean = df["gender"].str.upper().map(
    {"M": "Male", "MALE": "Male", "F": "Female", "FEMALE": "Female"}
).fillna(df["gender"])

gender_clean.value_counts().plot(
    kind="pie",
    autopct="%1.2f%%",
    colors=["#3498db", "#e74c3c"],
    startangle=90,
)

plt.title("Gender Distribution")
plt.ylabel("")
plt.tight_layout()
plt.show()

Output explanation: Circular wedges convey relative percentage contributions of male and female policyholders to the full customer portfolio.
Insight: The customer base shows near-equal gender balance, with female policyholders accounting for ~50.2% and male policyholders accounting for ~49.8%.
7. Correlation Heatmap – Numerical Health & Financial Variables
Goal: To identify key dependencies among age, health indicators, stay duration, and financial expenses.
Categories used: age, bmi, alcohol_units_per_week, stress_level_score, sum_insured, icu_days, length_of_stay, pre_hospitalization_expense, post_hospitalization_expense, deductible_amount, and co_pay_amount.

[172]
0s
# Code
num_cols = [
    "age",
    "bmi",
    "alcohol_units_per_week",
    "stress_level_score",
    "sum_insured",
    "icu_days",
    "length_of_stay",
    "pre_hospitalization_expense",
    "post_hospitalization_expense",
    "deductible_amount",
    "co_pay_amount",
]

corr = df[num_cols].corr()

sns.heatmap(corr, annot=True, cmap="coolwarm", fmt=".2f", linewidths=0.5)

plt.title("Correlation Heatmap – Health & Financial Metrics")
plt.tight_layout()
plt.show()

Output explanation: Color-coded cells display Pearson correlation coefficients ranging from −1.0 (strong negative) to +1.0 (strong positive).
Insight: ICU days and length of stay share a strong positive correlation (+0.78), while post-hospitalization costs closely align with total hospital stay length.
8. Bar Chart – Hospital Tier-wise Customer Count
Goal: To assess customer utilization patterns across different hospital facility classifications.
Categories used: hospital_tier and the count of patient admissions per tier

[173]
3s


Output explanation: Vertical columns indicate total admissions in each hospital tier, labeled with exact counts for precise review.
Insight: Private corporate hospitals lead facility utilization with over 50.5% of claims, followed by private small hospitals (34.6%) and government institutions (14.9%)
9. Scatter Plot – BMI vs. Total Claim Amount
Goal: To explore whether higher BMI values correlate with larger medical claim settlements.
Categories used: bmi on the X-axis and total_claim_amount_num on the Y-axis.

[174]
2s
# Code
df["total_claim_amount_num"] = pd.to_numeric(
    df["total_claim_amount"].astype(str).str.replace(r"[^\d.]", "", regex=True),
    errors="coerce",
)

fig = px.scatter(
    df,
    x="bmi",
    y="total_claim_amount_num",
    title="BMI vs Total Claim Amount",
    labels={
        "bmi": "Body Mass Index (BMI)",
        "total_claim_amount_num": "Total Claim Amount (₹)",
    },
    opacity=0.6,
    trendline="ols",
)

fig.show()

Output explanation: Data points spread across the grid illustrate individual patient profiles, while the fitted trend line summarizes the overarching directional trend.
Insight: Higher BMI metrics (over 30.0) show a distinct upward drift in total claim amounts, driven by higher rates of chronic co-morbidities requiring extended care.
10. Violin Plot – Stress Level Score by Policy Type
Goal: To compare psychological stress levels among individual, family floater, and senior citizen plan holders.
Categories used: policy_type and stress_level_score.

[175]
0s
# Code
fig = px.violin(
    df,
    x="policy_type",
    y="stress_level_score",
    box=True,
    title="Stress Level Score by Policy Type",
    color="policy_type",
    color_discrete_sequence=["#2ecc71", "#e67e22", "#e74c3c"],
)

fig.show()

Output explanation: The width of each violin shape reflects data concentration at various stress score values, while internal box lines mark medians and interquartile ranges.
Insight: Senior citizen policyholders demonstrate a slightly higher median stress score (around 6.2/10) compared to individual plan holders (around 4.9/10), reflecting age-related health management concerns.
Colab paid products
-
Cancel contracts here
