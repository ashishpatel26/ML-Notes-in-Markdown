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

#### Broadcasting

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
3. **Null value declaration**: If our data uses any other convention than `NaN` for declaring null values in it, we can explicitly define it, by setting the `na_values` attritbute to that character `pd.read_csv('path_to_csv.csv', na_values =  ['-1'])`
	
	This can also be done if there are more than one kinds of `NaN` values present in the dataset using a list of values as shown in `pd.read_csv('path.csv', na_values =  ['-1', '999'])` or using a dictionary as shown `pd.read_csv('path.csv', na_values =  {col1: '-1', col2: '999'})` if there are separate `NaN` characters in separate columns.
4. **Assigning row labels**: In case the first column of the csv contains row labels for the data, then use `pd.read_csv('path_to_csv.csv', index_col=0)` for using the (row) labels for your dataframe.
5. **Date values**: If year, month and date are in separate columns and need to be converged into one column, it can be done using `parse_dates` argument of the `read_csv()` function, e.g. `pd.read_csv('path_to_csv.csv', parse_dates = [[1, 2, 3]])` where columns with indices would contain year, month and day data. 
	
	Alternatively, we can parse the date-time values using `parse_dates = True` which would then convert all the dates that are ISO 8601 compatible (yyyy-mm-dd hh:mm:ss), into appropriate date structure. 
	
6. **Handling comments**: If the file contains comments within the data, they can be distinguished using the delimiter passed to the `comment` argument as shown in `pd.read_csv('path_to_csv.csv', comment='#')`
7. **Delimiter**: The delimiter in while reading a csv to a Pandas DataFrame object can be set using `sep` argument

#### Chunkwise loading

In case of large datasets, data can be loaded and processed in chunks. It can be done with the help of `for` loop as in `for chunk in pd.read_csv('path_to_csv.csv', chunksize = 1000)`.

### From URLs

Importing a csv from a web URL can be done with the **UrlLib** package as follows

```python
from urllib.request import urlretrieve

urlretrieve('http://onlinefilepath', 'local_file_path.csv')
```

And then proceed with `read_csv()` function as usual.

### From Excel

1. **Reading a file**: A simple read operation over an Excel Spreadsheet can be executed by using `x = pd.ExcelFile('filepath.xlsx')`. 
2. **Listing sheets**: There can be multiple sheets involved in any particular file and they can be listed by using the `sheet_names` attribute as `print(x.sheet_names)`
3. **Reading a particular sheet**: It is done by passing the sheet name to the `parse()` method as shown in `df_sheet = x.parse('sheet1')`
4. **Custom Headers**: One can define custom headers while parsing from an excel sheet by using the `names()` argument.

### From HDF5 (Hierarchical Data Format version5)

This is data format commonly used for storing large quantities of numerical data in Python. This is done using the following code segment

```python
import h5py
data = h5py.File("path_to_file.hdf5", "r")
```

You can explore the `data` object so obtained by using code similar to that required to explore a dictionary. 

### From Pickles

```python
with open('file_path.pkl', 'rb') as file:
    data = pickle.load(file)
```

### From SQL

1. **Creating a Database engine**

	```python
	from sqlalchemy import create_engine
	engine = create_engine("path to sql db connector") 
	```
2. **List Tables**: This can be done using `engine.table_names()` method of **engine** object.
3. **Connecting to the engine**: This is done using the `connect()` method available with every sqlalchemy `engine` object.
4. **Querying**: There are two ways to query an SQL database and they are as follows: 
	1. The first one takes all of the above methods and works as follows:
	
		```python
		con = engine.connect()
		results = con.execute("SELECT * FROM table_name")
		df = pd.DataFrame(results.fetchall())
		df.columns = results.keys()
		con.close()
		```
		
		This syntax is very similar to the **PHP** syntax for this operation. We create a connection, then execute the query and get returned a results binary object. We then use `fetchall()` method to convert it to a flat structure and store it in a pandas dataframe. Finally, we add the column names to the dataframe that we created and close the connection. 
	
	2. The second method is much more concise and works just fine. It harnesses the power of Pandas library and works as follows:
		
		```python
		df = pd.read_sql_query("SELECT * FROM table_name", engine)
		```
		
		This single line of code then executes the command and returns the results in form of a DataFrame.

5. **Fetch fewer rows**: Sometimes the SQL query that we execute might return humongous results, then we can use the `fetchmany()` function with the `size` argument over the `results` object in order to fetch a certain number of rows instead of all.
	


## Exporting Data

1. **csv**: The method `to_csv()` for every DataFrame object allows us to export it to any file that we desire. It works as `pd_df.to_csv('filename.csv')`.
2. **Excel**: The method `to_excel()` for every DataFrame object allows us to export it to an excel spreadsheet file that we desire. It works as `pd_df.to_csv('filename.xlsx')`.
3. **Numpy array**: Any Pandas DataFrame can be converted into a Numpy array object using `values` attribute of every pandas dataframe object. 



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

## Exploring Data

1. **Dimensions**: The `shape` attribute of any DataFrame can be used to check the dimensions.
2. **Column Names**: The `columns` attribute of a DataFrame returns the names of all the columns.
3. **Indices**: The atrributes `columns` and `index` can be used to retrieve the columns' and rows' index of a DataFrame.
4. **Column Details**: Much like the `str` function in R, `info()` method can be used over any pandas DataFrame object in order to retrieve meaningful insight on columns. It returns the name of the column and the number of Non Null values preent in the data column.
5. **Statistical Summary**: Statistical summaries for pandas DataFrames can be quickly generated using the `describe()` method on any pandas DataFrame.
6. **Interquantile range (IQR)**: Quantile ranges are useful when exploring a dataset and it can easily be determined by using `quantile()` method of Pandas dataframes. For instance, `pd_df.quantile([0.25, 0.75])` would return two values for each column in the dataset and half the data for those columns would lie between those two values. 
7. **Range**: The range can be calculated using the `min()` and `max()` methods on any DataFrame.
8. **Median**: The `median()` method can be used for finding out the median of any given dataset. 
9. **Standard deviation**: The method `std()` can be used for finding out the standard deviation for any given column.
10. **Unique objects**: Unique categories in any categorical column can be found using the `unique()` method.
11. **Frequency Count**: The frequency  of factors in a column containing factors by using the `value_counts()` method on that column. Optionally, we could specify the `dropna` argument to this method with a Boolean Value specifying whether or not to involve null values. 

## Time Series with Pandas

1. **Slicing on the basis of time**: Interesting selections can be done on date time indices, using selection operators like `pd_df.loc['2017-01-22':'2018-01-02']` to select the values for that 1 month.

2. **Reindexing**: Any time series can be reindexed using the index of another time series by using the syntax `time_s2.reindex(time_s1.index)`
3. **Forward Filling of Null Values**: Null values in a time series can be forward filled using `time_series.reindex(new_index, method = "ffill")`
4. **Resampling**: There are two kinds of sampling that can be done with time series in Pandas dataframes:
	1. **Downlsampling**: Reduce datetimes to lower frequency, i.e. from daily to weekly etc. 
	2. **Upsampling**: Increasing the times to higher frequency, i.e. from daily to hourly etc.
	
	There are multiple parameters that we can pass to `resample()` method for allowing us to derive quick statistics from a time series. For instance, `pd_ts.resample('D').mean()` would allow us to have daily averages of all numeric columns of the time series dataframe.
	
	| Code | Meaning |
	| ---- | ------- |
	| `min`, `T` | Minute |
	| `H`  | Hour |
	| `D` | Day |
	| `B` | Business Day |
	| `W` | Week |
	| `M` | Month |
	| `Q` | Quarter |
	| `Y` | Year |

	Numeric values can be used as prefixes to the parameters above in order to increase or decrease the sampling size. For instance, `2W` can be used for downsampling for 2 weeks in `pd_ts.resample('2W').mean()`
	
	> The `ffill()` and `bfill()` methods can be used for filling in, rolling values as in `pd_ts.resample('2H').ffill()`.
	
	**Interpolation**: It can be carried out as follows:

	```python 
	pd_ts.resample('A').first().interpolate('linear')
	
	```
	
	This would resample and fill in the gaps between any two data points with **NaN** values. Then the `interpolate()` method would interpolate the values. 
	
5. **Datetime Methods**: These methods allow us to slice and select specific date time attributes from the data. 
	1. **Select hours**: For instance `pd_ts['date'].dt.hour` would extract and return the *hour* where **0** is 12AM and **23** is 12PM.
	2. **Timezone**: We can **define** the timezone for a particular column by using `pd_ts['date'].dt.tz_localize('US/Central')`. On the other hand, easy **conversions** can be made, using the method `tz_convert()` that is specifically used for converting dates and times in one timezone to another.
	3. 
	
### Moving Averages

We can calculate moving averages, that allows us to focus on long term trends instead of being stuck in short term fluctuations. We do so by using the `rolling()` method as shown in `time_series.rolling(window=24).mean()` which would compute **new values for each point** but it will still be hourly data. This would instead set the value of that point as an average of trailing 24 datapoints, hence making it smoother. 


	
	