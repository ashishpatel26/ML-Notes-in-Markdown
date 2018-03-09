# Time Series

Any data recorded at fixed interval of time over a certain period of time, is called time series. It is a stochastic process, i.e. the values are dependent on, and change with time. There are special techniques that are used for tackling such models.

## Key Terms

There are a few key terms that are commonly encountered when working with Time Series, these are inclusive of but not exclusively described in the following list:

**Trend**: A time series is supposed to have an upward or downward trend if the plot shows a constant slope when plotted. It is noteworthy that for a pattern to be a trend, it needs to be consistent through the series. If we start getting upwards and downwards trend in the same plot, then it could be an indication of cyclical behavior. 
![TS with an upward trend](https://www.dtreg.com/uploaded/pageimg/TsTrend_1.jpg)

**Sesonality**: If a TS has a regular repeating pattern based on the calendar or clock, then we call it to have seasonality. Soemtimes there can be different amount of seasonal variation across years, and in such cases it is ideal to take the **log** of values in order to get a better idea about seasonality. It is noteworthy that Annual Data would rarely have a seasonal component.
![TS with a seasonal component](http://a-little-book-of-r-for-time-series.readthedocs.io/en/latest/_images/image5.png)

**Cyclical TS**: Cyclical patterns are irregular based on calendar or clock. In these cases there are trends in the Time Series that are of irregular lengths, like business data, there can be revenue gain or loss due to a bad product but how long the upward or downward trend would last, is unknown beforehand. Often, when a plot shows cyclical behavior, it would be a combination of big and small cycles. Also, these are very difficult to model because there is no specific pattern and we do not know what would happen next.  
![TS with cyclical patterns](http://slideplayer.com/8134442/25/images/8/Components+of+Time+Series+Data.jpg)


The implementation is handled as follows: 

1. [R](./01-TimeSeriesInR.md)
2. Python
