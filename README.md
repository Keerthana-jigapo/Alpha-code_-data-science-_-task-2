# Import necessary libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
df = pd.read_csv("path_to_dataset.csv")  # Replace with the actual path to your dataset

# Display the first few rows of the dataset
print("Dataset Preview:\n", df.head())

# Check for missing values
print("\nMissing Values:\n", df.isnull().sum())

# Basic statistics of the dataset
print("\nDataset Statistics:\n", df.describe())

# Visualize the unemployment rate over time (assuming a "Date" and "Unemployment Rate" column)
df['Date'] = pd.to_datetime(df['Date'])  # Convert the Date column to datetime format
plt.figure(figsize=(12, 6))
plt.plot(df['Date'], df['Unemployment Rate'], marker='o', color='b')
plt.title("Unemployment Rate Over Time", fontsize=16)
plt.xlabel("Date", fontsize=12)
plt.ylabel("Unemployment Rate (%)", fontsize=12)
plt.grid(True)
plt.show()

# Correlation heatmap (if there are numeric columns)
plt.figure(figsize=(10, 6))
sns.heatmap(df.corr(), annot=True, cmap="coolwarm", fmt=".2f")
plt.title("Correlation Heatmap")
plt.show()

# Unemployment distribution visualization
plt.figure(figsize=(10, 6))
sns.histplot(df['Unemployment Rate'], kde=True, bins=20, color='purple')
plt.title("Distribution of Unemployment Rate", fontsize=16)
plt.xlabel("Unemployment Rate (%)", fontsize=12)
plt.ylabel("Frequency", fontsize=12)
plt.show()

# Analyzing unemployment by category (if a category column exists, e.g., "Region" or "State")
if 'Region' in df.columns:  # Replace "Region" with the relevant column name
    plt.figure(figsize=(12, 6))
    sns.boxplot(x='Region', y='Unemployment Rate', data=df, palette="viridis")
    plt.title("Unemployment Rate by Region", fontsize=16)
    plt.xlabel("Region", fontsize=12)
    plt.ylabel("Unemployment Rate (%)", fontsize=12)
    plt.xticks(rotation=45)
    plt.show()

# Save cleaned dataset (optional)
df.to_csv("cleaned_unemployment_data.csv", index=False)
print("\nCleaned dataset saved as 'cleaned_unemployment_data.csv'")
