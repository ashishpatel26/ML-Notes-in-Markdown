# Performance Evaluation

## R-Squared 

There are a few terms that need to be understood before we can calculate the R-squared value for any regression model and are as follows:

1. **Sum of squared residuals** ![ssres](http://mathurl.com/ycattv9v.png) : It is exactly what the name suggests. A residual is the difference between actual values and the predicted values. If we add the squares of all residuals, that would give us the value of ![ssres](http://mathurl.com/ycattv9v.png), shown as follows in mathematical terms:
    ![](http://mathurl.com/yawhk57s.png)

2. **Total sum of squares** ![sstot](http://mathurl.com/y7hyn3w4.png):  Instead of calculating the residuals, we calculate the difference between the average **y** values and the actual **y** values present in the dataset. We then add the squares of these values, represented mathematically as :
    ![](http://mathurl.com/yazstja5.png)

R-sqaure is given by the following formula ![rsq](http://mathurl.com/ybf2xwp2.png) 

The idea is to minimize ![ssres](http://mathurl.com/ycattv9v.png) so as to keep the value of ![rsq](http://mathurl.com/3kwwdyh.png) as close as possible to 1. The calculation essentially gives us a numeric value as to how good is our regression line, as compared to the average value.

## Adjusted R-Squared

The value of ![rsq](http://mathurl.com/3kwwdyh.png) is considered to be better as it gets closer to 1, but there's a catch to this statement. The ![rsq](http://mathurl.com/3kwwdyh.png) value can be artifically inflated by simply adding more variables. This is a problem because the complexity of the model would increase due to this and would result in overfitting. The formulae for Adjusted R-squared is mathematically given as:

![](http://mathurl.com/yclkhq5z.png) 

where **p** is the number of regressors and **n** is the sample size. Adjusted R-squared has a penalizing factor that reduces it's value when a non-significant variable is added to the model.

> **p-value** based backward elimination can be useful in removing non-significant variables that we might have added in our model initially. (full process explained in **Linear Regression** section of the book.

