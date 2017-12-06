# Linear Regression

The idea is to fit a straight line in the n-dimensional space that holds all our observational points. This would constitute forming an equation of the form **y = mx + c**. Because we have multiple variables, we might need to extend this **mx** to be **m<sub>1</sub>x<sub>1</sub>**, **m<sub>2</sub>x<sub>2</sub>** and so on. This extensions results in the following mathematical representation between the independent and dependent variables:

![eq](http://mathurl.com/y8eahwj3.png)

where 

1. **y** = dependent variable/outcome
2. **x<sub>1</sub> to x<sub>n</sub>** are the dependent variables
3. **b<sub>0</sub> to b<sub>n</sub>** are the coefficients of the linear model

A linear regression models bases itself on the following assumptions:

1. Linearity
2. Homoscedasticity
3. Multivariate normality
4. Independence of errors
5. Lack of multicollinearity

If these assumptions do not hold, then linear regression probably isn't the model for your problem. 



### Variable Selection

The dataset will, more often than not, contain columns that do not have any effect on the dependent variable. This becomes problematic because we don't want to add too much noise to the dataset. The variables that do not effect the dependent variable (the outcome) will usually only decrease the performance of our model, and even if they do not, there's always an additional computing complexity that comes along with them. This could influence the costs of building the model, especially when we want to do it iteratively. 

There are five ways for doing feature selection while building a model:

1. **All-in**: If we are aware that all the variables in the dataset are useful and are required for building the model, then we simply use all the variables that are available to us.
2. **Backward Elimination**: The following steps need to be taken in order to conduct a backward elimination feature selection:
	1. 	We set a significance level for a feature to stay in the model
	2. Fit the model with all possible predictors
	3. Consider the predictor with the highest p-value. If P > SL go to **Step 4**, otherwise go to **Step 6**
	4.  Remove the variable
	5.  Fit the model again, and move to **Step 3**
	6.  Finish
3. **Forward Selection**: Although, it may seem like a straightforward procedure, it is quite intricate in practical implementation. The following steps need to be performed in order to make a linear regressor using forward selection:
	1. We set a significance level to enter the model
	2. Fit regression models with each one of those independent variables and then select the one with the lowest p-value
	3. Fit all possible regression models with the one that we selected in previous step and one additional variable.  
	4.  Consider the model with the lowest p-value. If p < SL go to **Step 3** otherwise go to **Step 5**
	5.  Finish and select the second last model 
4. **Bidirectional Elimination**: The algorithm works as follows:
	1. Select a Significance Level to enter and a Significance Level to stay in the model, viz. SLENTER and SLSTAY
	2. Perform the next step of Forward Selection, i.e. all the new variables that are to be added must have p < SLENTER in order to enter the model
	3. Perform all the steps of Backward Elimination, i.e. all the existing variables must have p < SLSTAY in order to stay in the model
	4. No new variables can be added, and no new variables can be removed
		
> The details on variable selection by **Score Comparison** is yet to be found.

The **lower the p-value** is, the **more important** a particular variable is for our model.

> The term **'Step wise regression'** is often used for 2, 3, and 4 but sometimes, it refers only to 4, depending on context. 

**Dummy variables:**
The variables that are created when categorical variables are encoded, are called dummy variables. 

We usually use one-hot encoding to do this, and it might seem like not including one last categorical dummy variable would cause a positive bias towards the rest of the equation but this is not the case. The coefficient for the last dummy variable is included in the b<sub>0</sub> term of the equation.

*Dummy Variable trap*: One can never have all the dummy variables and b<sub>0</sub> in a model at the same time. We need to remove at least one dummy variable for each of the corresponding categorical variables because all of that will be modeled into b<sub>0</sub>. 

**CODE REFERENCES**

The function used for backward elimination in such models is from the class `statsmodels.formula.api` and is titled OLS (used as sm.OLS). The important thing to remember about this function is the fact that it requires the users to add a column of 1s in the matrix of features (at the beginning of the matrix) explicitly, to be a partner for the **b<sub>0</sub>** coefficient. 

