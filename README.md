# Data-Cleaning-and-Preprocessing
this is my first github repository
<br>
Author=Aditya Patil
<br>
import pandas as pd
import os

data = {
    'age': [25, 30, None, 22, 28],
    'gender': ['male', 'female', 'female', 'male', None],
    'income': [30000, 40000, 50000, 35000, None],
    'education': ['High School', 'Bachelor', 'Master', 'PhD', None],
    'marital_status': ['Single', 'Married', 'Single', 'Divorced', 'Married'],
    'complain': [1, 0, 0, 1, 0]
}

df = pd.DataFrame(data)

df.columns = df.columns.str.strip()
df.columns = df.columns.str.lower().str.replace(' ', '_')

print("Column Names After Standardizing:")
print(df.columns)

df['age'] = df['age'].fillna(df['age'].median())
df['income'] = df['income'].fillna(df['income'].median())
df['education'] = df['education'].fillna(df['education'].mode()[0])
df['marital_status'] = df['marital_status'].fillna(df['marital_status'].mode()[0])
df['complain'] = df['complain'].fillna(df['complain'].mode()[0])

df_cleaned = df.drop_duplicates()

df_cleaned['gender'] = df_cleaned['gender'].str.lower().str.strip()
df_cleaned['education'] = df_cleaned['education'].str.title().str.strip()
df_cleaned['marital_status'] = df_cleaned['marital_status'].str.title().str.strip()

df_cleaned['age'] = df_cleaned['age'].astype(int)
df_cleaned['income'] = pd.to_numeric(df_cleaned['income'], errors='coerce')

output_path = '/path/to/your/folder/cleaned_customer_personality_analysis.csv'
try:
    df_cleaned.to_csv(output_path, index=False)
    print(f"Data cleaning complete! The cleaned dataset has been saved as '{output_path}'.")
except PermissionError as e:
    print(f"Permission error: {e}")
    print("Please ensure the file is not open and try saving to a different location.")
except Exception as e:
    print(f"An error occurred: {e}")



