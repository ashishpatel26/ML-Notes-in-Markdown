# Pandas 

The high level data manipulation tool used by data scientists. It can be imported with the syntax `import pandas as pd`.

## Creating a Pandas Dataframe

### From Dictionaries

There are multiple ways to create a Pandas dataframe, the commonly used one is to create it from a dictionary by setting a key for every column label and a the value to be a list of observations of that label for each column. Then simply calling `pd.DataFrame(dict)` would create the data frame. 

#### Assigning row labels

This can be done by using the syntax `df.index = ['label1', 'label2', ... 'labeln']` for **n** observations that exist in the dataframe.

### From CSVs

It is relatively straightforward to be reading data from CSVs. One can use `pd.read_csv('path_to_csv.csv')` in order to read from a file. 

#### Assigning row labels

In case the first column of the csv contains row labels for the data, then use `pd.read_csv('path_to_csv.csv', index_col=0)` for using the labels for your dataframe.

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