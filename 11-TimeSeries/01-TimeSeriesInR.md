# Time Series in R

Time Series in R is handled in the form of **XTS**(extensible time series) data.  Almost all data types can be converted into their XTS objects by using the `as.xts()` constructor. The data format the comes out as an XTS object is usually a matrix with the rownames as dates, forming a time series. 

This becomes particularly useful when we are looking for long term patterns and things that reoccur over a certain period of time. 

### Intuition

The idea is to make timeseries self-sustained objects that we can think of, and operate upon, as events in time. 

### Subsetting 

The format for subsetting any XTS object is as follows:

```r
xts_object['YYYYMMDDTHHMMSS'] 

xts_object["Thh:mm/Thh:mm"]
```

There are few rules that need to be followed for our code to be compliant with the subsetting standards of **XTS**:

1. The components should be from left to right.
2. The data and time should be separated with with **T**
3. There may or may not be individual hyphens between years and months etc.
4. Colons may or may not be used between the values in 'time' section
5. The ranges are to be represented by `/` and in case the full ranges are not specified, the last part of date/time before the `/` will be ranged over. 

Key points to remember while subsetting XTS objects are:

* Just like all other matrix objects in R subsetting still works for all integer indexing as well, including the negative indices.
* It also works with logical vectors, i.e. `xts\_object(index(xts_object) > "YYYYMMDD")` words as well.
* When subsetting the **XTS** objects, there is also the option of using the parameter `which.i` within the square brackets that returns the indixes of elements that match the logical query.
* Order is always preserved while subsetting, even when the numeric indices are provided in arbitrary order, which makes sense for time series.
* Selecting even one column of the dataset would return a matrix and not a vector.
* In most cases, subsetting XTS objects **will be faster than base R**

```r
# Example subsetting for a date range starting at YYYYMMDD
xts_object["YYYY-MM-DD/"]
```

We often would need to do subsetting over periods of time and for such problems, it would be handy to have the ability to select certain periods of time at the beginnning or end of the series. Luckily enough, we have `first` and `last` functions in the XTS package that allows us to do this with ease.

```r
# The query below would extract as many rows necessary for the last one week of observations from a dataset
last(xts_object, "1 week")
```

> Notice the use of text format for retrieving the data relevant to our search from the time series. 

#### Mathematical Operations

The basic math operators are supposed to work as normal as **XTS** object is an extended matrix object as per se. This allows a lot of flexibility as most functions would be dispatched to default matrix functions or similar ones, whenever possible.

Although most matrix operations would work as normal, it is important to remember that all matrix operations will be carried out primarily upon the time dimension and by default **ONLY THE INTERSECTION OF TIMES WOULD BE PROVIDED IN THE RESULTS**.

#### Merging two or more XTS objects

There are three major types of merge operations that we can leverage when dealing with Time Series using XTS objects:

1. **Outer Join**: The default join method for any merge operation on XTS objects is the outer join. This can be called as `merge(x, y)` and would result in the union of two time series with missing values replaced as `NA`'s.
2. **Inner Join**: A call to `merge(x, y, join = "inner")` would result in an intersection of the two objects `x` and `y` keeping only the times that appear in both objects.
3. **Right & Left Joins**: We can also choose to keep elements from one of the two time series being joined by setting the `join` parameter to be `"left"` or `"right"` in the `merge` function.

In addition to merging two time series objects, we can operate with other data types as well. For instance, passing a vector to the merge function as a `y` argument, would append a new column to the XTS object (with all normal recycling rules still applicable).

##### NA Handling

We can use `fill` argument with any of these join functions to fill in any replacement for missing values. The most popular one being, `na.locf` which replaces missing arguments by last observed value in time for the particular attribute.

There is a dedicated `na.locf` function for handling missing observations where `locf` stands for **last observation carried forward** and allows us to take the values from the previous observation in time series and save it to the next one. 

There are four other functions that are commonly used for handling NA values in time series:

1. `na.fill` would simply fill a replacement based on our arguments with a constant 
2. `na.omit` and `na.trim` would skip the observations with NA's in them
3. `na.approx` does a linear interpolation for the missing values

##### Lagging and Leading

Two common operations in time series manipulations are lagging and leading, in order to find seasonality or stationarity properties of any time series dataset. We can easily calculate these in R using `lag` function. 



### Exporting and Importing 

It's pretty straight forward as **XTS** objects are built over **zoo** objects, we can do things like

```r
write.zoo(xts_object, sep = ",", file = "file_name")

# as.yearmon serves as the formatting function here
read.zoo(file_name, sep = ",", FUN = as.yearmon)
```

### Key Terms

* **Seasonality**: The idea that the series exhibits a particular behavior repeatedly in certain intervals is called seasonality.
* **Stationarity**: The idea that the series remains within certain bounds instead of being continuously increasing or decreasing is called stationarity.

>The `lag` and `diff` functions are to be used for searching seasonality and stationarity relations between elements.  
