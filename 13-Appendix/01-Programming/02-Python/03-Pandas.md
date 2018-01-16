# Pandas 

The high level data manipulation tool used by data scientists. It can be imported with the syntax `import pandas as pd`.

## Creating a Pandas Dataframe

### From Dictionaries

There are multiple ways to create a Pandas dataframe, the commonly used one is to create it from a dictionary by setting a key for every column label and a the value to be a list of observations of that label for each column. Then simply calling `pd.DataFrame(dict)` would create the data frame. 

#### Assigning row labels

This can be done by using the syntax `df.index = ['label1', 'label2', ... 'labeln']` for **n** observations that exist in the dataframe.

## Reading and Importing Data

### From CSVs

It is relatively straightforward to be reading data from CSVs. One can use `pd.read_csv('path_to_csv.csv')` in order to read from a file. 

#### Assigning row labels

In case the first column of the csv contains row labels for the data, then use `pd.read_csv('path_to_csv.csv', index_col=0)` for using the labels for your dataframe.

#### Chunckwise loading

In case of large datasets, data can be loaded and processed in chunks. It can be done with the help of `for` loop as in `for chunk in pd.read_csv('path_to_csv.csv', chunksize = 1000)`.

## Selecting and Index Data 

### Column Selection 

A column in a dataframe `df` may easily be selected using the syntax `df["columnName"]`. 

> **NOTE:** The returned object from the code above is **NOT** a dataframe but an object of the type series. This may lead to unexpected results and therefore this method is not recommended.

The fix for the problem mentioned above is to use double square brackets like `df[["columnName"]]` for selecting the column. This would return a dataframe instead of a **series** as was the case in the method above. 

### Slicing for Row Selection

It is uncommon to use regular square brackets for row selection but it can be done using `df[1:5]` which would return the rows with indices 1 through 4 (because as always, the last index would not be included).

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