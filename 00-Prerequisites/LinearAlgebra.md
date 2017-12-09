# Linear Algebra

## Linear Equations

### Structure

One of the most basic motivations towards making computers was solving a system linear equations given by 
![lineq](http://mathurl.com/yacqpchy.png)

where ![x1](http://mathurl.com/2ga69bb.png), ![x2](http://mathurl.com/2cbdldp.png), ... ![xn](http://mathurl.com/3ac5npr.png) are unknowns and ![aij](http://mathurl.com/nb755rs.png) 's and ![bi](http://mathurl.com/y94hxh5j.png) 's  denote the constants, either complex or real. 

### Definitions
A system ![solset](http://mathurl.com/yc9hspko.png) is called a **solution** of the above system of linear equations if ![solset2](http://mathurl.com/yckmsc45.png) satisfies each of the eqations in our system of linear equations simultaneously and when ![b1=](http://mathurl.com/yd44a5r8.png) ![b2=](http://mathurl.com/y7l9ygqn.png) ![b3=](http://mathurl.com/y9ld77ug.png) ![ellipsis](http://mathurl.com/3dfnuhs.png) ![bn=](http://mathurl.com/y7fzg8ng.png) ![zero](http://mathurl.com/2vzzs3z.png), then the system of equations is called to be **homogeneous**. Such system of equations have one certain solution ![x1](http://mathurl.com/2ga69bb.png) = ![zero](http://mathurl.com/2vzzs3z.png), ![x2](http://mathurl.com/2cbdldp.png) = ![zero](http://mathurl.com/2vzzs3z.png), ... ![xn](http://mathurl.com/3ac5npr.png) = ![zero](http://mathurl.com/2vzzs3z.png) called the **trivial solution**. A system of Linear equations is said to be **consistent** if it has at least one solution and **inconsistent** if it has no solutions.



## Vectors

A vector is a numeric measurement with directions. In two dimensions, a vector ![v](http://mathurl.com/36zvquj.png) is of the form ![vector1](http://mathurl.com/y93w4hhl.png) and the magnitude of this vector is given by 

![magV](http://mathurl.com/y8nt6wqb.png) 

### Dot Products 

The dot products can be defined for two vectors or matrices in the following ways:

1. ![dotProd1](http://mathurl.com/y9qc43b6.png)

	This is the summation of element wise multiplication of the two vectors. The notation ![atransb](http://mathurl.com/y7wgs22g.png) denotes that the vectors are column vectors and the result of the equation above would be a 1x1 vector which is a scalar quantity. 
	
	This definition can be emulated in Python (using Numpy) in various ways:
	
	1. Without using Numpy functions)
	
		```
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

		```
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
		
## Matrices

Matrices are two dimensional set of numbers. These are very efficient data types for quick computations.

### Initializing a matrix

This can