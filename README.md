# Outlier_Detection
Use for outlier detection and removal using boxplot

# Calculate the 25th and 75th percentiles
percentile25 = df['Duration'].quantile(0.25) ##### Duration is name of a column it can be vary 
print("25th Percentile:", percentile25)

percentile75 = df['Duration'].quantile(0.75)
print("75th Percentile:", percentile75)

# Calculate the interquartile range (IQR)
iqr = percentile75 - percentile25

# Calculate the upper and lower limits for outliers
uplimit = percentile75 + 1.5 * iqr
lolimit = percentile25 - 1.5 * iqr
print("Upper Limit:", uplimit, "Lower Limit:", lolimit)

# Create a copy of the DataFrame
new_df = df.copy()

# Capping the outliers
new_df['Duration'] = np.where(
    new_df['Duration'] > uplimit, uplimit,
    np.where(new_df['Duration'] < lolimit, lolimit, new_df['Duration'])
)

# Display the first few rows of the new DataFrame to check the changes
print(new_df.head())
df = new_df.copy()
