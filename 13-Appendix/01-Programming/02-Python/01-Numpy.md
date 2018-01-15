# Numpy

Numpy is a library used specifically for advanced and faster data manipulation in Python. It allows us to effectively manage and manipulate our datasets with minimal programming. In this document, we will have a look at what are the most commonly used features of Numpy and how can we exploit them to optimize our Python programming. 


## Arrays

### 2-D Arrays

We can create 2-D Numpy arrays as `a = np.array([[1,2,3], [4,5,6]])` and this would lead to a 2 dimensional array. 

On this object, the attribute `shape` represents the dimensions. It can be used as `a.shape` to return `(2,3)` meaning **2 rows** and **3 columns** exist in this 2D array. 


## Operator overloading in 'np'

A simple operation like 

``` 
a = [1, 2, 3]
print(a+a) 
```
would return `[1,2,3,1,2,3]` but if you perform the operation with numpy as follows:

```
a = np.array([1,2,3])
print(a+a)
```
would return the element wise sum of the array, i.e. `[2,4,6]`


## Mathematics



### Dot Products 

The dot products can be defined for two vectors or matrices in the following ways:

1. ![dotProd1](http://mathurl.com/y9qc43b6.png)

	This is the summation of element wise multiplication of the two vectors. The notation ![atransb](http://mathurl.com/y7wgs22g.png) denotes that the vectors are column vectors and the result of the equation above would be a 1x1 vector which is a scalar quantity. 
	
	This definition can be emulated in Python (using Numpy) in various ways:
	
	1. Without using Numpy functions)
	
		```python
		# Create the necessary variables
		dotProd = 0
		a = np.array([1,2,3])
		b = np.array([2,3,4])
		
		# Use a for-loop to calculate the dot product
		for e,f in zip(a,b):
	 		dotProd += e*f
	 		
	 	
	 	# The value of dot now becomes 20 as one would expect
	 	```
	 
	2. Using `np.sum` function

		```python
		dotProd = np.sum(a*b)
		
		# The value of dotProd will be the same as the generic 
		# code we wrote above because the a*b notation creates 
		# a vector of products of individual elements and then
		# we just sum them to emulate the equation above
		```
		
	3. Using the `sum` function over the `np.array` object instances

		```
		dotProd = (a*b).sum()
		
		# Notice the use of object's sum function instead of
		# using the sum function of the class as in Method 2
		```
	
	4. Using the `np.dot` function

		```
		dotProd = np.dot(a,b)
		```	
		
	5. Using the `dot` function over the `np.array` object instances

		```
		dotProd = a.dot(b)
		
		# Notice the use of object's dot function instead of
		# using the dot function of the class as in Method 4
		```
		
	> `for` loops should be avoided whenever possible. The intrinsic functions of Numpy are magnitudes faster in operation.

2. ![cosDotProd1](http://mathurl.com/ycpoyuxb.png)
	
	This notation is not very convenient for vector multiplication unless a the angle on the right hand side is known to us. Although, it is a much more common practice to use this equation for finding out the angle between two vectors using 
	
	![cosDotProd2](http://mathurl.com/yd35x774.png)
	
	Let's use this equation to find the angle between the vectors above step by step:
	
	1. Find the magnitudes of the vectors.

		```
		# We can do this in two ways:
		
		# Option 1: Without using the built-in Numpy function 
		# for this task
		magA = np.sqrt(a.dot(a))
		
		# Option 2: Using the Linear Algebra module of the 
		# Numpy package to do this task
		magA = np.linalg.norm(a)
		
		# Using the equation in the starting of this chapter
		```
		
	2. Calculate the cosine of the angle between the two vectors. We know from the equation shown above that the angle between the two vectors can easily be calculated if we have the magnitudes of the two vectors and their cross product. 

		```
		costheta = a.dot(b) / ( np.linalg.norm(a) * np.linalg.norm(b) )
		```
		
	3. Once we have done this, the actual angle can easily be calculated by using the `np.arccos` function of the Numpy Library

		```
		theta = np.arccos(costheta)
		```
		
		The value that we obtain for `theta` from the operation above is in radians.

