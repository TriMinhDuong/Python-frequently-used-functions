# Frequently Used Functions for Data Science

## Data Processing

Read Excel file to pandas:
```python
df = pd.read_excel(“directory_with_file_name.xlsx”, sheetname = 0)
```
Merge 2 pandas dataframes:
```python
merge_df = pd.merge(df1, df2, on = “common_field_with_same_name”)
```
Create pivot table:
```python
pvt_df = df.pivot_table(index=[“field1”], columns=[“column1”], values=“field_for_summary”)
```

## Data Exploration

Return to the numbers of unique values in each feature in pandas data frame:
```python
df.nunique()
```
Return the proportion of data grouped by specific features
```python
df[“feature”].value_counts() / df.shape[0]
```
Extract the descriptive statistics on each numerical variables
```python	
df.describe()
```
Pull the values necessary for a 95% confidence interval from a sampling distribution
```python
np.percentile(array_name, 2.5), np.percentile(array_name, 97.5)
```
Count number of unique values within groups
```python
df.groupby(‘categorical_variable’).agg({“feature_to_be_counted”: pd.Series.nunique})
```
Count number of unique values in all features grouped by specific categorical variables
```python
df.groupby(‘categorical_variable’).nunique()
```
Convert format of a datetime variable
```python
df[‘variable_name’] = pd.to_datetime(df[‘variable_name’], format=’%Y-%m-%d %H:%M:%S.%f’)
```
Check if any features in a dataframe have missing values
```python
df.isnull().sum()
```
Fill NaN with 0’s
```python
df = df.fillna(0)
```
Reset index for dataframe:
```python
df = df.reset_index()
```
List all records with duplicate values on identified features.
Example: list all records which have duplicated user_id
```python
ids = df.user_id
df[df.user_id.isin(ids[ids.duplicated()])]
```

## Data Visualization

Show visualization
```python
%matplotlib inline
```
Show histogram of an array or data frame
```python
plt.hist(array_name)
```

## Data Preparation for Predictive Models
Split train/test, balancing, feature engineering, dummy variables
