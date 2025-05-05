# COVID-19-Global-Data-Tracker

A data analysis project on COVID-19 global trends — covering cases, deaths, and vaccinations across countries using real-world data.


##  1. Data Collection

Dataset Source: [Our World in Data](https://ourworldindata.org/covid-deaths)

# Install libraries if needed
# !pip install pandas matplotlib seaborn plotly

import pandas as pd

# Load the dataset
df = pd.read_csv('owid-covid-data.csv')
df.shape

##  2. Data Exploration
Explore structure, missing values, and basic features.

# Preview data
df.head()
df.columns

# Check for missing values
df.isnull().sum().sort_values(ascending=False)

##  3. Data Cleaning
Focus on a few countries and clean missing/incorrect values.

# Convert date column to datetime
df['date'] = pd.to_datetime(df['date'])

# Select countries of interest
countries = ['Kenya', 'United States', 'India']
df_subset = df[df['location'].isin(countries)]

# Drop rows with missing total_cases or total_deaths
df_subset = df_subset.dropna(subset=['total_cases', 'total_deaths'])

# Optional: Fill other missing values
df_subset = df_subset.fillna(method='ffill')


## 4. Exploratory Data Analysis (EDA)
Analyze time trends for cases and deaths.

import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(12,6))
for country in countries:
    country_data = df_subset[df_subset['location'] == country]
    plt.plot(country_data['date'], country_data['total_cases'], label=country)

plt.title('Total COVID-19 Cases Over Time')
plt.xlabel('Date')
plt.ylabel('Total Cases')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()

##  5. Vaccination Analysis
Visualize vaccination progress over time.

plt.figure(figsize=(12,6))
for country in countries:
    country_data = df_subset[df_subset['location'] == country]
    plt.plot(country_data['date'], country_data['total_vaccinations'], label=country)

plt.title('Total COVID-19 Vaccinations Over Time')
plt.xlabel('Date')
plt.ylabel('Total Vaccinations')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()

---

## 6. Insights & Conclusions

- **Insight 1:** India showed a rapid increase in vaccination from mid-2021.
- **Insight 2:** The USA had a high death count in early 2021 but managed to flatten the curve post-vaccination.
- **Insight 3:** Kenya’s data shows slower vaccination uptake but better death recovery rates than expected.

## ✅ Summary

This notebook explored COVID-19 data trends across countries using real-world datasets. Key steps included:
- Data loading and cleaning
- Time-series analysis of cases and deaths
- Vaccination comparisons
- Visual storytelling using Python libraries








