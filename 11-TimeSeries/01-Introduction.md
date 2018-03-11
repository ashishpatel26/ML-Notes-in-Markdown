# Introduction

How is time series different than any other data? It is because it contains a variable *Time*. It is an continuous ordered variable though. Therefore, we would need to anchor ourselves at some point, and we could call this anchor 0 (denoting the present), then we can represent the future as T+1, T+2... and the past as T-1, T-2 ... In order to build a model and have accurate predictions, we would usually want to have 50 or more degrees of freedom. 
> Note: Degrees of freedom are usually pieces of independent information. Calculating a mean or any other non-parameter and including it in the model would cause us to lose a degree of freedom.

# Key Terms

There are a few key terms that are commonly encountered when working with Time Series, these are inclusive of but not exclusively described in the following list:

**Trend**: A time series is supposed to have an upward or downward trend if the plot shows a constant slope when plotted. It is noteworthy that for a pattern to be a trend, it needs to be consistent through the series. If we start getting upwards and downwards trend in the same plot, then it could be an indication of cyclical behavior. 
![TS with an upward trend](https://www.dtreg.com/uploaded/pageimg/TsTrend_1.jpg)

**Sesonality**: If a TS has a regular repeating pattern based on the calendar or clock, then we call it to have seasonality. Soemtimes there can be different amount of seasonal variation across years, and in such cases it is ideal to take the **log** of values in order to get a better idea about seasonality. It is noteworthy that Annual Data would rarely have a seasonal component.
![TS with a seasonal component](http://a-little-book-of-r-for-time-series.readthedocs.io/en/latest/_images/image5.png)

**Cyclical TS**: Cyclical patterns are irregular based on calendar or clock. In these cases there are trends in the Time Series that are of irregular lengths, like business data, there can be revenue gain or loss due to a bad product but how long the upward or downward trend would last, is unknown beforehand. Often, when a plot shows cyclical behavior, it would be a combination of big and small cycles. Also, these are very difficult to model because there is no specific pattern and we do not know what would happen next.  
![TS with cyclical patterns](http://slideplayer.com/8134442/25/images/8/Components+of+Time+Series+Data.jpg)

**Autocorrelation/Serial Correlation**: The dependence on the past in case of a univariate time series is called autocorrelation.

# Types of Time Series

The two major types of time series are as follows:

> Most of the theory that has been developed was developed for stationary time series.

1. **Stationary**: Such time series have constant mean and reasonably constant variance through time. eg. annual rainfall
2. **Non-Stationary**: If we have a non-stationary time series then there are additional patterns in our series, like Trends, Seasonality or Cycles. These do not necessarily have a constant mean variance through time. 

    a. **Univariate Time Series**: We usually use regression technique to model non-stationary time series and we also have to consider the time series aspects (like autocorrelation i.e. dependence on the past and differencing, i.e. the technique used in TS to try and get rid of autocorrelation). **If we have a Time Series with trend, seasonality and non-constant variance, then it is best to log the data which would then allow us to stabilize the variance, hence the name 'Variance Stablizing Transformation' This allows us to fit our data in additive models, making it a very useful technique.** 
    
    b. **Multivariate Time Series**: Many variables measured through time, typically measured on the same time points. In some other cases, they may be measured on different time points but within an year. Such data would need to be analyzed using multiple regression models. We might also want to fit the time variable in the model (after transformations maybe) but this could allow us to determince whether there was any **trend** in the response and capture it. If you do not find any trend in the data, then the time variable can be chucked out but **modelling the data without checking for the time variable would be a horrible idea**.

> More observations is often a good thing because it allows greater degrees of freedom. (Clarification needed, will read a few paper to better this concept)

3. **Panel Data/Logitudinal Data**: Panel data is a combination of cross-sectional data and time series. There can be two kinds of time logging for panel data, **implicit** and **explicit**. In econometrics and finance studies, the time is **implicitly** marked which in areas like medical studies **explicit** marking of time is done on Panel data. The idea is to take a cross-sectional measurements at some point in time and then repeat the measurements again and again to form a time series. 

4. **Continuous Time Models**: In this kind of data, we have a Point(Time component) process and a Stochastic (Random) process. For instance, the number of people arriving at a particular restaurant is an example of this where the groups of people ae arriving at certain points in time(point process) and the size of the group is random (stochastic process). 

> NOTE: No matter what a time series data is about, on the axis (while modeling) we always use a sequence of numbers starting from 1, up to the total number of observations. This allows us to focus on the sequence of measurements because we already know the frequency the time interval between any two observations.

# Features of Time Series

A few key features to remember when modelling time series are as follows: 

1. Past will affect the future but the future cannot affect the past
2. There will rarely be any independence between observations, temperature, economics and all other major fields have dependence on the past in case of Time Series data  
3. The pattern is often exploited to predict and build better models
4. Stationary techniques can be used to model non-stationary time series, and also to remove trends, seasonality, and sometimes even cycles.
5. We can also try to decompose time series into various components, model each one of them separately and then forecast each of the components and then combine again.  
6. we also use Moving Averages (also known as filtering or smoothing) because it tries to remove the seasonal component of time series.
7. We would often also need to transform the data before it can be used. The most common time we need to do transformations in Time Series is when we have an **increasing seasonal variation** because that represents a multiplicative model, which can be hard to explain. 

