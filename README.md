# EDA with Pandas - Cumulative Lab

## Introduction

In this section, you've learned a lot about importing, cleaning up, analyzing (using descriptive statistics) and visualizing data. In this cumulative lab, you'll get a chance to practice all of these skills with the Ames Housing dataset, which contains information about home sales in Ames, Iowa between 2006 and 2010.

## Objectives

You will be able to:

* Practice loading data with pandas
* Practice calculating measures of centrality and dispersion with pandas
* Practice creating subsets of data with pandas
* Practice using data visualizations to explore data, and interpreting those visualizations
* Perform a full exploratory data analysis process to gain insight about a dataset 

## Your Task: Explore the Ames Housing Dataset with Pandas

![aerial photo of a neighborhood](images/neighborhood_aerial.jpg)

Photo by <a href="https://unsplash.com/@mattdonders?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Matt Donders</a> on <a href="/@mattdonders?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>



### Data Understanding

Each record (row) in this dataset represents a home that was sold in Ames, IA.

Each feature (column) in this dataset is some attribute of that home sale. You can view the file `data/data_description.txt` in this repository for a full explanation of all variables in this dataset — 80 columns in total.

We are going to focus on the following features:

**SalePrice**: `Sale price of the house in dollars`

**TotRmsAbvGrd**: `Total rooms above grade (does not include bathrooms)`

**OverallCond**: `Rates the overall condition of the house`
```
       10	Very Excellent
       9	 Excellent
       8	 Very Good
       7	 Good
       6	 Above Average	
       5	 Average
       4	 Below Average	
       3	 Fair
       2	 Poor
       1	 Very Poor
```

**YrSold**: `Year Sold (YYYY)`

**YearBuilt**: `Original construction date`

**LandSlope**: `Slope of property`
```
       Gtl	Gentle slope
       Mod	Moderate Slope	
       Sev	Severe Slope
```

### Requirements

In this lab you will use your data munging and visualization skills to conduct an exploratory analysis of the dataset.

#### 1. Load the Dataset with Pandas

Import pandas with the standard alias `pd` and load the data into a dataframe with the standard name `df`.

#### 2. Explore Data Distributions

Produce summary statistics, visualizations, and interpretive text describing the distributions of `SalePrice`, `TotRmsAbvGrd`, and `OverallCond`.

#### 3. Explore Differences between Subsets

Separate the data into subsets based on `OverallCond`, then demonstrate how this split impacts the distribution of `SalePrice`.

#### 4. Explore Correlations

Find the features that have the strongest positive and negative correlations with `SalePrice`, and produce plots representing these relationships.

#### 5. Engineer and Explore a New Feature

Create a new feature `Age`, which represents the difference between the year sold and the year built, and plot the relationship between the age and sale price.

## 1. Load the Dataset with Pandas

In the cell below, import:
* `pandas` with the standard alias `pd`
* `matplotlib.pyplot` with the standard alias `plt`

And set `%matplotlib inline` so the graphs will display immediately below the cell that creates them.


```python
import pandas as pd
import matplotlib.pyplot as plt

%matplotlib inline
```

Now, use pandas to open the file located at `data/ames.csv` ([documentation here](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)). Specify the argument `index_col=0` in order to avoid creating an extra `Id` column. Name the resulting dataframe `df`.


```python
df=pd.read_csv("data/ames.csv",index_col=0)

```

The following code checks that you loaded the data correctly:


```python
# Run this cell without changes

# Check that df is a dataframe
assert type(df) == pd.DataFrame

# Check that there are the correct number of rows
assert df.shape[0] == 1460

# Check that there are the correct number of columns
# (if this crashes, make sure you specified `index_col=0`)
assert df.shape[1] == 80
```

Inspect the contents of the dataframe:


```python
# Run this cell without changes
df
```


```python
# Run this cell without changes
df.info()
```

## 2. Explore Data Distributions

Write code to produce histograms showing the distributions of `SalePrice`, `TotRmsAbvGrd`, and `OverallCond`.

Each histogram should have appropriate title and axes labels, as well as a black vertical line indicating the mean of the dataset. See the documentation for [plotting histograms](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.hist.html), [customizing axes](https://matplotlib.org/stable/api/axes_api.html#axis-labels-title-and-legend), and [plotting vertical lines](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.axvline.html#matplotlib.axes.Axes.axvline) as needed.

### Sale Price

In the cell below, produce a histogram for `SalePrice`.


```python
plt.figure(figsize=(10, 4))
plt.hist(df['SalePrice'], bins=30, color='lightblue', edgecolor='black')
plt.axvline(df['SalePrice'].mean(), color='black', linestyle='dashed', linewidth=2, label='Mean')
plt.title('Distribution of Sale Price')
plt.xlabel('Sale Price')
plt.ylabel('Frequency')
plt.legend()
plt.grid(True)#easy reading of the graph 
plt.show()
```

Now, print out the mean, median, and standard deviation:


```python
mean_price = df['SalePrice'].mean()
median_price = df['SalePrice'].median()
std_price = df['SalePrice'].std()

print("SalePrice Statistics Analysis:")
print(f"Mean: {mean_price:.2f}")#two decimal places 
print(f"Median: {median_price:.2f}")
print(f"Standard Deviation: {std_price:.2f}")
```

In the cell below, interpret the above information.


```python
# Replace None with appropriate text
"""
SalePrice Statistics Analysis:
The average (mean) sale price is $180,921.20, while the median is lower at $163,000.00, indicating a right-skewed distribution.
This suggests that most houses are moderately priced, but a few high-priced homes are pulling the average up.
The high standard deviation of $79,442.50 shows there is significant variation in house prices.
"""
```

### Total Rooms Above Grade

In the cell below, produce a histogram for `TotRmsAbvGrd`.


```python
# Your code here
plt.figure(figsize=(10, 4))
plt.hist(df['TotRmsAbvGrd'], bins=15, color='lightgreen', edgecolor='black')
plt.axvline(df['TotRmsAbvGrd'].mean(), color='black', linestyle='dashed', linewidth=2, label='Mean')
plt.title('Distribution of Total Rooms Above Ground')
plt.xlabel('Total Rooms Above Ground')
plt.ylabel('Frequency')
plt.legend()
plt.grid(True)#easy reading of figures in the graph
plt.show()

```

Now, print out the mean, median, and standard deviation:


```python

# Your code here
mean_price = df['TotRmsAbvGrd'].mean()
median_price = df['TotRmsAbvGrd'].median()
std_price = df['TotRmsAbvGrd'].std()

print("Total Rooms Above Ground Statistics Analysis:")
print(f"Mean: {mean_price:.2f}")#two decimal places 
print(f"Median: {median_price:.2f}")
print(f"Standard Deviation: {std_price:.2f}")
```

In the cell below, interpret the above information.


```python
# Replace None with appropriate text
"""
Total Rooms Above Ground Statistics Analysis:
The average number of rooms above ground is 6.52, slightly higher than the median of 6.00, indicating a mildly right-skewed distribution.
This suggests most homes have around 6 rooms, with a few having more.
The standard deviation of 1.63 shows moderate variation in room counts among houses.
"""
```

### Overall Condition

In the cell below, produce a histogram for `OverallCond`.


```python
# Your code here
plt.figure(figsize=(10, 4))
plt.hist(df['OverallCond'], bins=10, color='orange', edgecolor='black')
plt.axvline(df['OverallCond'].mean(), color='black', linestyle='dashed', linewidth=2, label='Mean')
plt.title('Distribution of Overall Condition')
plt.xlabel('Overall Condition')
plt.ylabel('Frequency')
plt.legend()
plt.grid(True)#easy reading figures on the graph
plt.show()
```

Now, print out the mean, median, and standard deviation:


```python
# Your code here
mean_price = df['OverallCond'].mean()
median_price = df['OverallCond'].median()
std_price = df['OverallCond'].std()

print("OverallCond Statistics Analysis:")
print(f"Mean: {mean_price:.2f}")#two decimal places 
print(f"Median: {median_price:.2f}")
print(f"Standard Deviation: {std_price:.2f}")
```

In the cell below, interpret the above information.


```python
# Replace None with appropriate text
"""
Overall Condition Statistics Analysis:
The average overall condition rating is 5.58, slightly above the median of 5.00, suggesting a slight right-skew in the data.
Most homes are rated around average condition, with fewer homes in excellent or poor condition.
The standard deviation of 1.11 indicates relatively low variation in condition ratings across homes.
"""
```

## 3. Explore Differences between Subsets

As you might have noted in the previous step, the overall condition of the house seems like we should treat it as more of a categorical variable, rather than a numeric variable.

One useful way to explore a categorical variable is to create subsets of the full dataset based on that categorical variable, then plot their distributions based on some other variable. Since this dataset is traditionally used for predicting the sale price of a house, let's use `SalePrice` as that other variable.

In the cell below, create three variables, each of which represents a record-wise subset of `df` (meaning, it has the same columns as `df`, but only some of the rows).

* `below_average_condition`: home sales where the overall condition was less than 5
* `average_condition`: home sales where the overall condition was exactly 5
* `above_average_condition`: home sales where the overall condition was greater than 5


```python
# Replace None with appropriate code
below_average_condition = df[df["OverallCond"]<5]
average_condition = df[df["OverallCond"]==5]
above_average_condition = df[df["OverallCond"]>5]
#print(f"Below_average_condition {below_average_condition}")
#print(f"Average_condition {average_condition}")
#print(f"Above_average_condition {above_average_condition}")
```

The following code checks that you created the subsets correctly:


```python
# Run this cell without changes

# Check that all of them still have 80 columns
assert below_average_condition.shape[1] == 80
assert average_condition.shape[1] == 80
assert above_average_condition.shape[1] == 80

# Check the numbers of rows of each subset
assert below_average_condition.shape[0] == 88
assert average_condition.shape[0] == 821
assert above_average_condition.shape[0] == 551
```

The following code will produce a plot of the distributions of sale price for each of these subsets:


```python
# Run this cell without changes

# Set up plot
fig, ax = plt.subplots(figsize=(15,5))

# Create custom bins so all are on the same scale
bins = range(df["SalePrice"].min(), df["SalePrice"].max(), int(df["SalePrice"].median()) // 20)

# Plot three histograms, with reduced opacity (alpha) so we
# can see them overlapping
ax.hist(
    x=above_average_condition["SalePrice"],
    label="above average condition",
    bins=bins,
    color="cyan",
    alpha=0.5
)
ax.hist(
    x=average_condition["SalePrice"],
    label="average condition",
    bins=bins,
    color="gray",
    alpha=0.3
)
ax.hist(
    x=below_average_condition["SalePrice"],
    label="below average condition",
    bins=bins,
    color="yellow",
    alpha=0.5
)

# Customize labels
ax.set_title("Distributions of Sale Price Grouped by Condition")
ax.set_xlabel("Sale Price")
ax.set_ylabel("Number of Houses")
ax.legend();
```

Interpret the plot above. What does it tell us about these overall condition categories, and the relationship between overall condition and sale price? Is there anything surprising?


```python
# Replace None with appropriate text
"""
Homes in above average condition generally have higher sale prices, with the distribution shifted to the right.
Average condition homes are the most common, centered around a moderate price range.
Surprisingly, below average condition homes still span a wide price range, showing that condition isn’t the only factor affecting sale price.
"""
```

## 4. Explore Correlations

To understand more about what features of these homes lead to higher sale prices, let's look at some correlations. We'll return to using the full `df`, rather than the subsets.

In the cell below, print out both the name of the column and the Pearson correlation for the column that is ***most positively correlated*** with `SalePrice` (other than `SalePrice`, which is perfectly correlated with itself).

We'll only check the correlations with some kind of numeric data type.

You can import additional libraries, although it is possible to do this just using pandas.


```python
# Your code here
numeric_df = df.select_dtypes(include='number')
correlations = numeric_df.corr()['SalePrice'].drop('SalePrice')
most_pos_corr = correlations.idxmax()#column name 
pos_corr_value = correlations.max()# exact figure or value
print(f"Most positively correlated column: {most_pos_corr}")
print(f"Pearson correlation: {pos_corr_value:.2f}")
```

Now, find the ***most negatively correlated*** column:


```python
# Your code here
most_neg_corr = correlations.idxmin()
neg_corr_value = correlations.min()
print(f"Most negatively correlated column: {most_neg_corr}, Correlation: {neg_corr_value:.2f}")

```

Once you have your answer, edit the code below so that it produces a box plot of the relevant columns.


```python
# Replace None with appropriate code

import seaborn as sns

fig, (ax1, ax2) = plt.subplots(ncols=2, figsize=(15,5))

# Plot distribution of column with highest correlation
sns.boxplot(
    x=df[most_pos_corr],#gives the actual data not column name 
    y=df["SalePrice"],
    ax=ax1
)
# Plot distribution of column with most negative correlation
sns.boxplot(
    x=df[most_neg_corr],#give actual data not column name 
    y=df["SalePrice"],
    ax=ax2
)

# Customize labels
ax1.set_title(f"{most_pos_corr} vs SalePrice")
ax1.set_xlabel(most_pos_corr)
ax1.set_ylabel("Sale Price")

ax2.set_title(f"{most_neg_corr} vs SalePrice")
ax2.set_xlabel(most_neg_corr)
ax2.set_ylabel("Sale Price");
```

Interpret the results below. Consult `data/data_description.txt` as needed.


```python
# Replace None with appropriate text
"""
The boxplot for OverallQual shows that as overall quality increases,
sale prices also increase significantly, confirming the strong positive correlation (0.79).
This indicates that homes with higher quality ratings consistently fetch higher prices.
On the other hand, the boxplot for KitchenAbvGr shows minimal variation in 
SalePrice across its values, supporting the weak negative correlation (-0.14) and suggesting it has little effect on price.
""" 
```

## 5. Engineer and Explore a New Feature

Here the code is written for you, all you need to do is interpret it.

We note that the data spans across several years of sales:


```python
# Run this cell without changes
df["YrSold"].value_counts().sort_index()
```

Maybe we can learn something interesting from the age of the home when it was sold. This uses information from the `YrBuilt` and `YrSold` columns, but represents a truly distinct feature.


```python
# Run this cell without changes

# Make a new column, Age
df["Age"] = df["YrSold"] - df["YearBuilt"]

# Set up plot
fig, ax = plt.subplots(figsize=(15,5))

# Plot Age vs. SalePrice
ax.scatter(df["Age"], df["SalePrice"], alpha=0.3, color="green")
ax.set_title("Home Age vs. Sale Price")
ax.set_xlabel("Age of Home at Time of Sale")
ax.set_ylabel("Sale Price");
```

Interpret this plot below:


```python
# Replace None with appropriate text
"""
The scatter plot shows that as the age of the home increases, the sale price generally decreases.
This indicates a negative relationship between home age and sale price. Newer homes tend to sell for more,
while older homes tend to sell for less. However, there are some exceptions, as a few older homes still
sell at high prices. This suggests that home age is an important feature that can help predict sale price.
"""
```

## Summary

Congratulations, you've completed an exploratory data analysis of a popular dataset. You saw how to inspect the distributions of individual columns, subsets of columns, correlations, and new engineered features.
