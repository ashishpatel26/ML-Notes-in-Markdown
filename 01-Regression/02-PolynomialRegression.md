# Polynomial Linear Regression

This regression allows us to regress over dependent variable(s) that has a polynomial relationship with the independent variables generally represented as 

![polyRegEq](http://mathurl.com/yd39otyo.png)

There are powers to the same variable that now jointly represent the relationship between dependent and independent variables.

> One question that may be pertinent here is that why is it still called 'Linear' when it clearly displays a Polynomial relationship. The reason for that is, the word Linear corresponds to the relationship of the various coefficients and not the 'x' term itself. 

## CODE REFERENCES

### Python
We would often not bother ourselves with feature scaling because most libraries have in-built support for the same. For instance `python from sklearn.linear_model import LinearRegression` does feature scaling on its own.

An example of creating a polynomial model in Python is


```python
from sklearn.preprocessing import PolynomialFeatures
poly_reg = PolynomialFeatures(degree = 2)

# The fit_transform method used here first fits the poly_ref object to X
# and then transforms it to X_poly
X_poly = poly_reg.fit_transform(X)
# This transformation leads to addition of column of 1 for b0 element and
# the the polynomial terms (depending on our choice of 'degree' parameter
# for the original variables of X. 

poly_reg1 =  LinearRegression()
poly_reg1.fit(X_poly, y)
```

