# EX.NO:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

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
# import libarary
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt


# Step 2: Read the Dataset

# Replace with your actual CSV file
df1 = pd.read_csv('Data_set.csv')
df1.head()

# Step 3: Dataset Information
df1.info()
df1.describe()

# Step 4: Handling Missing Values
# Check Null Values
df1.isnull()
df1.isnull().sum()

# Fill Missing Values with 0
df1_fill_0 = df1.fillna(0)
df1_fill_0

# Forward Fill
df1_ffill = df1.ffill()
df1_ffill

# Backward Fill
df1_bfill = df1.bfill()
df1_bfill

# Fill with Mean (Numerical Column Example)

df1['rating'] = df1['rating'].fillna(df1['rating'].mean())
df1

# Drop Missing Values
df1_dropna = df1.dropna()
df1_dropna

#Step 5: Save Cleaned Data
df1_dropna.to_csv('Data_set_new.csv', index=False)

# OUTLIER DETECTION
# Step 6: IQR Method (Using  Datasetnew)
ra = pd.read_csv('Data_set_new.csv')
ra.head()
ra.info()  
ra.describe() 

# Boxplot for Outlier Detection
sns.boxplot(x=ra['rating'])
plt.show()

# Calculate IQR
Q1 = ra['rating'].quantile(0.25)
Q3 = ra['rating'].quantile(0.75)
IQR = Q3 - Q1
print("IQR:", IQR)

# Detect Outliers
outliers_iqr = ra[
    (ra['rating'] < (Q1 - 1.5 * IQR)) |
    (ra['rating'] > (Q3 + 1.5 * IQR))
]
outliers_iqr

# Remove Outliers
ra_cleaned = ra[
    ~((ra['rating'] < (Q1 - 1.5 * IQR)) |
      (ra['rating'] > (Q3 + 1.5 * IQR)))
]
ra_cleaned

# Step 7: Z-Score Method

data = [1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,
        54,57,60,63,66,69,72,75,78,81,84,87,90,93]

df_z = pd.DataFrame(data, columns=['values'])
df_z

# Calculate Z-Scores
z_scores = np.abs(stats.zscore(df_z))
z_scores

# Detect Outliers
threshold = 1.5
outliers_z = df_z[z_scores > threshold]
print("Outliers:")
outliers_z

# Remove Outliers
df_z_cleaned = df_z[z_scores <= threshold]
df_z_cleaned

<img width="1189" height="813" alt="Screenshot 2026-02-09 111159" src="https://github.com/user-attachments/assets/6a323445-e576-4fb4-9abd-84e7d2fdd071" />

<img width="1079" height="280" alt="Screenshot 2026-02-09 111222" src="https://github.com/user-attachments/assets/7a440a5d-f7a4-485d-b24a-4892f3415cb4" />

<img width="1039" height="714" alt="Screenshot 2026-02-09 111241" src="https://github.com/user-attachments/assets/c65430ac-4b50-421f-afe6-e6527379377d" />


[DS exp-1(udhaya.s).pdf](https://github.com/user-attachments/files/25174930/DS.exp-1.udhaya.s.pdf)

# Result
   Thus,the  the given data is cleaned and saved successfully.
