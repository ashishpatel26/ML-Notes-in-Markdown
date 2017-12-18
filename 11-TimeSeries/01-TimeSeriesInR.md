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

There are few rules that need to be followed in order for our code to be compliant with the subsetting standards of **XTS**:

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

### Exporting and Importing 

It's pretty straight forward as **XTS** objects are built over **zoo** objects, we can do things like

```r
write.zoo(xts_object, sep = ",", file = "file_name")

# as.yearmon serves as the formatting function here
read.zoo(file_name, sep = ",", FUN = as.yearmon)
```

