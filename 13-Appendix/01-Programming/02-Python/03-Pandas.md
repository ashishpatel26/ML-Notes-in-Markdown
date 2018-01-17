# Pandas 

The high level data manipulation tool used by data scientists. It can be imported with the syntax `import pandas as pd`.

## Creating a Pandas Dataframe

### From Dictionaries

There are multiple ways to create a Pandas dataframe, the commonly used one is to create it from a dictionary by setting a key for every column label and a the value to be a list of observations of that label for each column. Then simply calling `pd.DataFrame(dict)` would create the data frame. 

#### Assigning row labels

This can be done by using the syntax `df.index = ['label1', 'label2', ... 'labeln']` for **n** observations that exist in the dataframe.

### From Lists

If we are to create a DataFrame from two conforming lists that are defined as follows, we would need to use the `list` and `zip` functions.

```python
labels = ['n1', 'n2']
x = [1, 2, 3]
y = [4, 5, 6]
```

1. We would first need to create a list of lists like `list_columns = [x, y]`
2. Then we would need create a list after element-wise zipping of the columns with their labels, as shown in `z = list(zip(labels, list_columns))`
3. This will now need to be converted into a dictionary which would have column names (`labels`) and columns (`z`) using `data = dict(z)`
4. After this, we use the method defined above for dictionaries, i.e. `pd.DataFrame(data)` to create a DataFrame.

### Broadcasting

It is the concept of **recycling** from R, that is called **broadcasting** in Python. The idea is, that a particular value can be recycled and used to fill all the other observations, if unsuitable number of details have been provided.

```python
x = [1, 2, 3]
y = {'n': x, 'is_int': 'Yes'}
z = pd.DataFrame(y)
```
would return a DataFrame with two columns, the column containing `Yes` thrice. 

## Reading and Importing Data

### From CSVs

It is relatively straightforward to be reading data from CSVs. One can use `pd.read_csv('path_to_csv.csv')` in order to read from a file. 

1. **No column labels**: If the data does not have column labels, `pd.read_csv('path_to_csv.csv', header = None)` will allow it to read data without it.
2. **External column names**: External column names can be added to the data frame using the names argument, `pd.read_csv('path_to_csv.csv', header = None, names = list_of_names)`
3. **Null value declaration**: If our data uses any other convention than `NaN` for declaring null values in it, we can explicitly define it, by setting the `na_values` attritbute to that character `pd.read_csv('path_to_csv.csv', na_values =  '-1')`
	
	This can also be done if there are more than one kinds of `NaN` values present in the dataset using a list of values as shown in `pd.read_csv('path.csv', na_values =  ['-1', '999'])` or using a dictionary as shown `pd.read_csv('path.csv', na_values =  {col1: '-1', col2: '999'})` if there are separate `NaN` characters in separate columns.
4. **Assigning row labels**: In case the first column of the csv contains row labels for the data, then use `pd.read_csv('path_to_csv.csv', index_col=0)` for using the (row) labels for your dataframe.
5. **Date values**: If year, month and date are in separate columns and need to be converged into one column, it can be done using `parse_dates` argument of the `read_csv()` function, e.g. `pd.read_csv('path_to_csv.csv', parse_dates = [[1, 2, 3]])` where columns with indices would contain year, month and day data.
6. **Handling comments**: If the file contains comments within the data, they can be distinguished using the delimiter passed to the `comment` argument as shown in `pd.read_csv('path_to_csv.csv', comment='#')`

#### Chunckwise loading

In case of large datasets, data can be loaded and processed in chunks. It can be done with the help of `for` loop as in `for chunk in pd.read_csv('path_to_csv.csv', chunksize = 1000)`.

## Exporting Data

1. **csv**: The method `to_csv()` for every DataFrame object allows us to export it to any file that we desire. It works as `pd_df.to_csv('filename.csv')`.
2. **Excel**: The method `to_excel()` for every DataFrame object allows us to export it to an excel spreadsheet file that we desire. It works as `pd_df.to_csv('filename.xlsx')`.

## Data Overview

1. **Dimensions**: The `shape` attribute of any DataFrame can be used to check the dimensions.
2. **Column Names**: The `columns` attribute of a DataFrame returns the names of all the columns.
3. **Indices**: The atrributes `columns` and `index` can be used to retrieve the columns' and rows' index of a DataFrame.
4. **Column Details**: Much like the `str` function in R, `info()` method can be used over any pandas DataFrame object in order to retrieve meaningful insight on columns. 

## Selecting and Index Data 

### Column Selection 

A column in a dataframe `df` may easily be selected using the syntax `df["columnName"]`. 

> **NOTE:** The returned object from the code above is **NOT** a dataframe but an object of the type series. This may lead to unexpected results and therefore this method is not recommended.

There are two fixes for the problem mentioned above:

1. The fix for the problem mentioned above is to use double square brackets like `df[["columnName"]]` for selecting the column. This would return a dataframe instead of a **series** as was the case in the method above. 
2. Use the `values` attribute for any **Series** object in order to retrieve the numerical values involved in form of a **Numpy** array.

### Slicing for Row Selection

It is uncommon to use regular square brackets for row selection but it can be done using `df[1:5]` which would return the rows with indices 1 through 4 (because as always, the last index would not be included).

If alternative slicing methods are required then it can be achieved as `pd_df[::3,:]` would select every third row of the DataFrame.

### Loc and iLoc

These are the two most commonly used methods (of Pandas Data Frame objects) for selecting or subsetting data. The **loc** technique operates on **labels** and the **iloc** technique relies on **integer positions**.

1. **loc**: This method allows us to select certain rows based on labels as follows `df.loc[["row_label1", "row_label2"]]` would select the rows with these two labels. 
	> **Note:** The use of `[[ ]]` is still necessary for making sure that the returned object is indeed a Pandas DataFrame in order to avoid any inconsistencies.
	
	It can be further extended to include only specific columns using a comma, as in `df.loc[["row_label1", "row_label2"], ["column_label1", "column_label2"]]`. This query would only return the columns with labels **column_label1** and **column_label2**.

2. **iloc**: Everything remains the same except that indices are used instead of labels.

### Iterations

#### Columns

A basic `for` loop would result in iteration over column names. For instance, 

```
for i in pd_df:
	print(i)
```

would simply print the columns names that exist in the pandas dataframe `pd_df`.

#### Rows

The rows need to be iterated over using the method `iterrows` of the pandas dataframe object that we are trying to access.

```
for lab, row in pd_df.iterrows():
	print(lab)
	print(row)
```

would then print, first the label, and then the contents of each row as a **Series** object.

## Modifying a Dataframe

### Adding a new column 

#### Single Value: loc

The operator `loc` can be used to add a new column to an existing dataframe. 

```
pd_df.loc["new_column"] = 2
```
should create a new column names `new_column` in the `pd_df` dataframe with the value `2` on all rows.

#### Mutation: apply

`pd_df["new_column"] = pd_df["old_column"].apply(len)` would add a new column with the length of values present in currently existing `old_column`.