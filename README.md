
# Energy Consumption Data Analysis
# Author: Vijaya Kumari Meena

# Import libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset (example: Global Energy data from Kaggle or World Bank)
# Replace 'energy_data.csv' with your dataset file
df = pd.read_csv("energy_data.csv")

# Quick overview
print(df.head())
print(df.info())

# Handle missing values (basic cleaning)
df = df.dropna()

# Select relevant columns (example: Country, Year, Renewable, FossilFuel)
data = df[["Country", "Year", "Renewable_Energy", "Fossil_Fuel_Energy"]]

# Group by year (global trend)
yearly = data.groupby("Year")[["Renewable_Energy", "Fossil_Fuel_Energy"]].sum()

# Plot global renewable vs fossil fuel trends
plt.figure(figsize=(10,6))
plt.plot(yearly.index, yearly["Renewable_Energy"], label="Renewable Energy", color="green")
plt.plot(yearly.index, yearly["Fossil_Fuel_Energy"], label="Fossil Fuels", color="red")
plt.title("Global Energy Consumption Trends")
plt.xlabel("Year")
plt.ylabel("Energy Consumption (TWh)")
plt.legend()
plt.show()

# Compare top 5 countries by renewable adoption
top_countries = data.groupby("Country")["Renewable_Energy"].sum().sort_values(ascending=False).head(5)

plt.figure(figsize=(8,5))
sns.barplot(x=top_countries.values, y=top_countries.index, palette="Greens_r")
plt.title("Top 5 Countries by Renewable Energy Adoption")
plt.xlabel("Total Renewable Energy (TWh)")
plt.ylabel("Country")
plt.show()
