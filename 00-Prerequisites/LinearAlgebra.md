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

### Vector Multiplications
#### Dot Product 

There are two ways to go about this:

1. ![dotProd1](http://mathurl.com/y9qc43b6.png)

	This is the summation of element wise multiplication of the two vectors. The notation ![atransb](http://mathurl.com/y7wgs22g.png) denotes that the vectors are column vectors and the result of the equation above would be a 1x1 vector which is a scalar quantity. 
	
2. ![cosDotProd1](http://mathurl.com/ycpoyuxb.png)
	
This notation is not very convenient for vector multiplication unless a the angle on the right hand side is known to us. Although, it is a much more common practice to use this equation for finding out the angle between two vectors using 
	
![cosDotProd2](http://mathurl.com/yd35x774.png)
		
#### Outer Product
The outer product of two vectors results in a matrix and is given by the equation:

If there are two column vectors `u1` and `v1` that are given by ![u1](http://mathurl.com/ybqz6wvv.png) and ![u1](http://mathurl.com/y7y5yr4e.png) respectively. Then their outer product is written as ![representation](http://mathurl.com/ycex27tr.png)

which then results to be ![outProductResult](http://mathurl.com/y7kgwn2n.png).

## Matrices

Matrices are two dimensional set of numbers. These are very efficient data types for quick computations.

### Matrix Multiplications


#### Dot Product
The product of two matrices A and B in given by the formulae 

![matrixMultiplication](http://mathurl.com/ycnfztus.png)


