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
8. **Skipping rows**: Rows can be skipped while reading a csv file by using `skiprows` argument in combination with `header` argument.
9. **Skipping footer**: Rows at the end of the file can be skipped using the `skipfooter = n` argument. This would skip the last `n` rows of the file. 
	> **NOTE**: The `skipfooter` argument doesn't work with the default C Engine so we need to specify the `engine = python` when setting this parameter.

#### Chunkwise loading

In case of large datasets, data can be loaded and processed in chunks. It can be done with the help of `for` loop as in `for chunk in pd.read_csv('path_to_csv.csv', chunksize = 1000)`.

#### Globbing

The process of looking for file names with specific patterns, and loading them is called **globbing**. 

```python 
import glob

pattern = '*.csv'
csv_files = glob.glob(pattern)
```

The code above, would return a list of files names, called `csv_files`. Then we can loop over this list to load all data frames. *Concatenation* can be used for merging all the datasets into one single dataset if required. 

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

	One trick for range of slicing is to use `df.loc[["row_label2", "row_label1":-1]]` for reverse slicing. It would select rows from `row_label1` to `row_label2` but in reverse order.
	
	> **Note:** The use of `[[ ]]` is still necessary for making sure that the returned object is indeed a Pandas DataFrame in order to avoid any inconsistencies.
	
	> **WARNING**: Unlike conventional slicing (with numbers) slicing with `loc` using `'column_name_1':'column_name_2'` would include `column_name_2` in the resulting object. This is different from the index based slicing as that ignores the last index.
	
	It can be further extended to include only specific columns using a comma, as in `df.loc[["row_label1", "row_label2"], ["column_label1", "column_label2"]]`. This query would only return the columns with labels **column_label1** and **column_label2**.

2. **iloc**: Everything remains the same except that indices are used instead of labels.

### Filtering

1. **any and all**: `any()` or `all()` methods are helpful in filtering the columns that have certain properties. They're usually used in combination with `isnull()` or `notnull()` methods.
2. **Drop na**: The `dropna()` method can be used on data frames to filter out rows with any or all na values based on the argument `how='any'` or `how='all'`.

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

## Manipulating Dataframes

> NOT COMPLETE: would need to visit more websites and research materials to complete manipulatio

1. **Adding a new column**

	1. **Single Value(loc)**: The operator `loc` can be used to add a new column to an existing dataframe. 
		
		```python
		pd_df.loc["new_column"] = 2
		```
		should create a new column names `new_column` in the `pd_df` dataframe with the value `2` on all rows.
	2. **Mutation(apply)**: `pd_df["new_column"] = pd_df["old_column"].apply(len)` would add a new column with the length of values present in currently existing `old_column`.
 
2. **Tidying Data**

	1. **Melting Dataframes**: If columns contain values instead of variables, then we would need to use the `melt()` function. It can be used as 
	
		```python
		pd.melt(	frame = df, 
					id_vars = 'identifier_column', 
					value_vars = ['column1', 'column2'],
					var_name = 'new_key_column_name',
					value_name = 'new_value_column_name')
		```
		
		where `id_vars` is the column/set of columns that contain the ID, and `value_vars` are the columns that need to be merged.
		
	2. **Pivoting Data**: It's the opposite process of melting data. It can be used to change a column into multiple columns as follows:
	
		```python
		pd.pivot(	frame = df, 
					index = 'index_column', 
					columns = 'key_column',
					values = 'value_column')	
		```
		
		This would work just fine if we're dealing with perfect data, i.e. there are no duplicates. If there are duplicates though, then we would need to use the `pivot_table()` method in order to deal with them. It is done with one additional parameter, and with , as shown below
		
		```python
		df.pivot_table(	index = 'index_column', 
							columns = 'key_column',
							values = 'value_column',
							aggfunction = np.mean)	
		```
		
		where we are telling Pandas to mean the duplicate numeric values using the `aggfunction` attribute. 
		
		> `reset_index()` method is used on the data frames that have been pivoted in order to flatten them2
		
	3. **Concatenating Data**: A list of dataframes can be passed to the `pd.concat()` function for concatenating data.
	
		The `axis = 1` argument can be used for **column wise concatenation**.
		
		> **Note:** We need to reset the index labels by passing the `ignore_index=True` argument to the `pd.concat()` function so that there are no duplicate indices in order to avoid using `reset_index()` method later.
	
3. **Merging Data**

	We can use the Pandas equivalent of **join** to merge two dataframes as follows
	
	```python
	pd.merge(		left = left_df, right = right_df,
					on = None, 
					left_on = 'left_df_column_name', 
					right_on = 'right_df_column_name')
	```
	
	If the column name is same on both left and right dataframes, then only the `on` parameter can be specified in the function above and the other factors will be redundant. 
	
	There are multiple kinds of merges that can happen in Pandas:
	
	1. **One to One**: Both the keys take a value only 1 time on both sides
	2. **Many to One/ One to Many**: This merge happens when there are more than one duplicates on either of the tables. In this case, the value from the other key will be duplicated to fill in the missing repition.

4. **Data Type Cleaning**
	
	We can observe the datatypes of various columns by viewing the `dtypes` attribute of the dataframe that we want to check these details for.
	
	1. **Converting Data Types**: The data types can be converted using the `astype()` method of any column. 
	2. **Convert to categorical column**: We would often want to convert the column type to a categorical variable, we can pass the `'category'` argument to the `astype()` method of any column to convert it into a categorical column.
	3. **Convert to Numeric**: If there is a column that should be of numeric type but is not, because of mistreated data, or erroneous characters in the data, we can use the `pd.to_numeric(df['column_name'])` function and pass it the additional argument `errors = 'coerce'` in order to convert all that erroneous data to `NaN` with ease.
	4. **Drop NA**: If there are really few data points that have missing values in them, we can lose them with the `dropna()` method. 
	5. **Recode Missing Values**: We can customize the missing values using the `fillna('missing_value_placeholder')` method of every data frame object and the columns. 
	6. **String Cleaning**: The `re` library for regular expressions gives us a neat way to do string manipulations. We can formulate regular expression formalue like `x = re.compile('\d{3}-\d{3}-\d{4}')`. This would create a new regex object called `x` which has a method `match()`. We can pass any string to this `match()` method to match it with our regular expression and it returns a boolean `True` if the string matches. 
	7. **Duplicate Data**: There may be mulitple rows where redundant partial or complete row information is stored and these may be sorted out by using the `drop_duplicates()` methods of the data frame object.

5. **Vectorized Operations**: Whenever possible, it is recommended to use vectorized computations rather than going for custom solutions. 
	1. **Operating on Strings**: There are vectorized methods in the `str` attribute of every dataframe column that contains strings. These functions enable us to do quick vectorized transformations on the df. 
	2. **Map Method**: There are often times when the `str` or other vectorized attributes will not be present. In such cases the `map()` method can be used for mapping operation succinctly. 

6. **Assigning Index**: We can designate a column, or any other Numpy array of the same length to be the index by assigning it to the `df.index` attribute. 

	1. **Index Name**: Index by default, won't have name associated with it, but one can assign a name to the index by assigning it to the attribute `df.index.name`. The similar operation can be carried for assigning an index name to the column names using the `df.columns.name` attribute.
	2. **Using Tuples as Index**: Often we would need to set two or more columns as index (much like composite keys in SQL). This can be done using Tuples. They list of columns that we need to be set as the composite index of a dataframe can be passed to the `set_index(["composite_key_column_1", "composite_key_column_2"])` to achieve this. It is called the **MultiIndex**.
	3. **Sorting Index**: If we are using a **Multiindex** as shown above, we can also use the `sort_index()` method to sort the index and display it in a more organized manner. 
	
		> This allows for **fancy indexing**, i.e. calling `df.loc[(["index_1_low" : "index_1_high"], "index_2"), :]` would select all the columns for rows that belong in the range provided for `index_1` and all sub rows belonging to `index_2`. 
		
		> The `slice()` function must be used for slicing both indexes.
	4.  **Stacking and Unstacking Index**: We might want to remove some of the indexes from the multi level indexes to be columns. To do this, we use the method `unstack()` with the `level="index_name_to_remove"`. This will give us a hierarchical data frame and this effect can be reversed using the `stack()` method in the same format.
	5. **Swapping Index Levels**: The index levels can be swapped using the method `swaplevel(0, 1)` on any dataframe. This would essentially exchange the hierarchical arrangement of indices and running `sort_index()` right after it would do the rest.
  
7. **Aggregation/Reduction**: The `groupby()` method is the Python equivalent of R's `aggregate()` method. It allows us to create virtual groups within the dataframe. It is usually chained together with other aggregation functions like `sum()`, `count()`, `unique()` etc. to produce meaningful results. We can use a typical grouping operation as follows:

	```python
	titanic.groupby(['pclass', 'sex'])['survived'].count()
	```
	
	There is also the option of finding out multiple aggregation details on the grouped dataframe:
	1. **Multiple Aggregations**: We can use `titanic.groupby('pclass').agg(['mean', 'sum'])` to compute multiple aggregation values at once.
	2. **Custom Aggregations**: We can pass custom functions as arguments to `agg()` method that would take `Series`  objects as inputs and produce results from them. When used, they would receive as inputs multiple `Series` objects (one for each group) and would produce grouped results like other functions.
 	3. **Differnet Agg on Different Columns**: We can pass a `dictionary` object to `agg()` method, as an argument, which would contain column names as keys and corresponding aggregation functions to apply as values. This allows us to compute different statistics for the same grouping of objects, upon different columns.
 
8. **Transformation**: Transformation functions are used to transform one or more columns after they have been grouped and is usually chained after the `groupby()` method as `transform(transformation_function)`. This transformation method passes the Series to `transform_function()` which could be a user defined function or a builtin one, which then returns a transformed series of a conforming size. 
9. **Grouping and Filtering**: We can use the dictionary object created by `groupby()` method to loop over and therefore filter only the rows of interest.
10. **Sorting**: We can sort the values in any column by using the `sort_values(ascending = False)` method available for columns of all dataframe objects.
11. **Matrix Operations**: Direct matrix operations will not work on Dataframes but `pandas.core.frame.DataFrame` object comes with an `as_matrix()` method available to each object for converting it readily into a Numpy 2D Array. This will only work for DataFrames with only numerical values though. There is a crucial difference between **Numpy 2D Arrays** and **Pandas' DataFrames** and that is, `X[0]` for a Numpy 2D Array returns the ***0th row*** while accessing a DataFrame ***X[0]*** would return the ***0th column*** of the DataFrame.
12. **Mathematical Operations**: There are various mathematical operations available for our use.
	1. **pct_change()**: This method can used to detect percentage change over a particular column or aggregation values.
	2. **add()**: This method can be used to add two Series with corresponding row indices as `a.add(b)`. This would add the series `a` and `b`. However, if there are non matching indices, i.e. an index in `a` does not have any corresponding index in `b`, then this could return an `NaN` value. We can change this by changing the default non existent value by passing the argument `fill_value` into the `add()` method. This method is chainable so more than one Series can be added in a single line. 

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
12. **Data Type**: We can explore the data type for any column that we want to, by having a look at the values of the attribute `dtypes` for each column in data frame.
13. **Index of Max**: The `idxmax()` and `idxmin()` methods allow us to find the row or column labels where the maximum or minimum values are located with the help of `axis = 'columns'` for the column labels, and these methods default to `min()` so we won't have to specify anything there. 
14. **Indexes of Non NULL Values**: One can get the indices of non null values by using the `notnull()` method available for Series objects in Pandas.

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

```

"""
for key in keys['order']:
  key_weight = keys['weights'][key] # Weight of the key
  key_data = keys['data'][key]
  if key_data['type'] == "singular":
    print("Jacuzzi")
  else:
    for section in key_data['order']: 
      section_weight = key_data['weights'][section]
      section_data = key_data['data'][section]
      
      for unit in section_data:
        user_df[key+'_'+section+'_'+unit] = user_data_raw[section_data[unit]['user']].notnull().astype(int)
        
    
print(user_df.columns)
"""
```


	
	