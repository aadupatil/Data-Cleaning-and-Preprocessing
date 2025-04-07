# Data-Cleaning-and-Preprocessing
this is my first github repository
<br>
Author=Aditya Patil
import pandas as pd

try:
    df = pd.read_csv('your_dataset.csv')
    print("Dataset loaded successfully.")
except FileNotFoundError:
    print("Error: Dataset file not found. Please check the file path.")
    data = {
        'age': [25, 30, None, 22, 28],
        'gender': ['male', 'female', 'female', 'male', None],
        'country': ['USA', 'CAN', 'MEX', None, 'CAN'],
        'date_column': ['01-01-2020', '15-02-2020', '12-03-2020', '30-04-2020', '05-05-2020']
    }
    df = pd.DataFrame(data)
    print("Simulated dataset used.")

print("Missing Values Count:")
print(df.isnull().sum())

df_cleaned = df.dropna()

df['age'] = df['age'].fillna(df['age'].median())
df['gender'] = df['gender'].fillna(df['gender'].mode()[0])
df['country'] = df['country'].fillna(df['country'].mode()[0])

df_cleaned = df_cleaned.drop_duplicates()

df_cleaned['gender'] = df_cleaned['gender'].str.lower().str.strip()
df_cleaned['country'] = df_cleaned['country'].str.title()

df_cleaned['date_column'] = pd.to_datetime(df_cleaned['date_column'], format='%d-%m-%Y')

df_cleaned.columns = df_cleaned.columns.str.lower().str.replace(' ', '_')

df_cleaned['age'] = df_cleaned['age'].astype(int)
df_cleaned['date_column'] = pd.to_datetime(df_cleaned['date_column'])

try:
    df_cleaned.to_csv('cleaned_dataset.csv', index=False)
    print("Data cleaning complete! The cleaned dataset has been saved as 'cleaned_dataset.csv'.")
except Exception as e:
    print(f"Error saving the file: {e}")

print("Cleaned Data:")
print(df_cleaned.head())

