# Netflix Data Cleaning and Transformation Project

## Project Overview

**Project Title**: Netflix Data Cleaning and Transformation
**Level**: Beginner to Intermediate
**Libraries Used**: `pandas`, `seaborn`, `numpy`, `matplotlib.pylab`
**Dataset**: `netflix1.csv` (Netflix Content Data)

This project focuses on demonstrating fundamental data cleaning and transformation techniques using the Python Pandas library. The goal is to take a raw Netflix content dataset and prepare it for further analytical tasks by performing various data manipulation steps. It serves as a practical example for anyone looking to understand and apply data preparation methods.

## Objectives

1.  **Data Understanding**: Gain initial insights into the dataset's structure, types, and summary statistics.
2.  **Data Cleaning**: Identify and handle redundant columns, duplicate entries, and missing values.
3.  **Data Transformation**: Modify existing columns for better usability, including renaming, changing data types, and reformatting values.
4.  **Export Cleaned Data**: Save the processed dataset into a new CSV file for future use.

## Project Structure

---

### 1. Data Import and Initial Setup

This initial step involves setting up the Python environment by importing the necessary data manipulation and visualization libraries, and then loading the raw Netflix dataset from a CSV file into a Pandas DataFrame.

```python
import pandas as pd
import seaborn as sns
import numpy as np
import matplotlib.pylab as plt

# Read the CSV file into a DataFrame
data = pd.read_csv("netflix1.csv")
```

### 2. Data Understanding and Exploration

Before making any changes, it's crucial to understand the dataset's characteristics. This phase includes checking the shape of the DataFrame, inspecting the first and last few rows, listing column names, verifying data types, and generating descriptive statistics.

```python
# Dataframe shape
data.shape

# Head
data.head(10)

# Tail
data.tail(10)

# Columns
data.columns

# Data Types
data.dtypes

# Describe
data.describe()

# Info
data.info()
```

### 3. Data Preparation and Transformation

This is the core phase of the project where the raw data undergoes cleaning and transformation processes. This involves dropping irrelevant columns, standardizing column names, checking for and handling duplicates, managing missing values, and performing specific column-level transformations to ensure data quality and usability.

```python
data.columns

# Deleting redundant columns
data.drop(columns='rating', inplace=True)

# Renaming column
new_columns_name = []
for i in data.columns:
    new_columns_name.append(i.capitalize())
data.columns = new_columns_name

# Checking columns after rename
data.head(5)

# Checking data duplicated
data.duplicated().sum()

# If any duplicated data, we can check with:
# --> data.drop_duplicates(inplace=True)

# Checking missing value in data (NaN)
data.isna().sum()

# If we had NaN values, we can check with:
# -->data.dropna(inplace=True)

# Transform/change (split) "Show_id" into integer with deleting 's' (string)
data['Show_id'] = data['Show_id'].apply(lambda x : x.split("s")[1])

# Checking after transform
data.head(10)

# Checking type data of Show_id column
type(data['Show_id'][0])

# Transform into int data type
data['Show_id'] = data['Show_id'].astype(int)

# Checking data type of Show_id column
type(data['Show_id'][0])

# Transform format of Date_added (before with delimiter '/' into '-')
data['Date_added'] = data['Date_added'].apply(lambda x : x.replace('/','-'))

# Checking after transform Date_added column
data.head(5)

# If we want to search any country at Country column
df = data['Country'].value_counts().reset_index()
df[df['Country']=='Turkey']

# Convert into csv file
data.to_csv('Cleaned_Data_CSV.csv', index=False)
```


### Conclusion

This project successfully demonstrates essential data cleaning and transformation techniques using the Pandas library in Python. By meticulously following these steps, the raw Netflix dataset has been refined into a clean and structured format, making it suitable for subsequent analytical tasks such as data visualization, statistical modeling, or machine learning. The process specifically included:

1. Removal of irrelevant columns (`rating`).
2. Standardization of column names (capitalizing the first letter).
3. Checking for and addressing duplicate entries.
4. Identification of missing values.
5. Specific column transformations, such as converting `Show_id` to an integer and reformatting `Date_added`.
   
The final cleaned dataset is exported to `Cleaned_Data_CSV.csv`, providing a reliable foundation for any future data analysis endeavors.
