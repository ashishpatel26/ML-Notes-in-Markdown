# Python Programming

## Data Types

### Tuples

**Tuples** are immutable ordered objects that are created using **()**. For defining a new tuple, one could simply write `x = (1, 2, 3)`. This would create a new tuple with the values defined. In order to extract these values into separate variables, one could write `a, b, c = x` and then the values would be mapped to the corresponding variables. Individual elements can also be accessed, just like the elements of lists are accessed, i.e. `print(x[2])` would print **3**, as one would expect from a list.

### Dictionaries

#### Validity

These are data types that store data in form of key-value pairs. The only thing worth noting here is that **keys** need to be immutable variables, i.e. they cannot be lists of other dictionaries because they are mutable by their very definition.

#### Check for existence

In order to quickly check whether or not a key exists in a particular dictionary, use the syntax `"key" in dict`  which would return `True` if the key is present in the dictionary object `dict`.

#### Deletion

The obvious function for most deletions, `del` is used for **deleting** a **key-value pair** in any dictionary with the syntax being `del(dict["key"])`.

## Manipulations

### Iteration 

* **Iterable**: Any object that has an associated `iter()` method is called an iterable in Python terminology. 
* **Iterator**: Any object that has an associated `next()` method that presents the next value when called. An iterator object can be created using the `iter()` method as follows
	
	```python
	x = 'Test'
	it_obj = iter('Test')
	
	next(it_obj)
	# Prints 'T'
	
	next(it_obj)
	# Prints 'e'
	# ... so forth and so on
	```
	
	All objects of the iterator can be printed in a single call using **\*** operator as `print(*it_obj)`. This would print `T e s t` and calling `next()` again on this object would throw the end of iteration error.

#### Lists

We can iterate over lists using the `enumerate` function like `for i, val in enumerate(my_list)` would then return the index and values in `i` and `val` respectively on every iteration of the loop. We can change the first index of the enumeration by using `start` parameter of `enumerate` function like `for i, val in enumerate(my_list, start = 10)`, which would, in this case, start the indexing at 10 instead of 0.

#### Dictionaries 

##### Using for loop

In case of dictionaries, the method `items()` must be called in order to properly iterate over items. The syntax for this, is as follows:

```
for key, value in my_dict.items():
	do_something(key)
```

##### Enumeration

A common lookup for `for` loops is the iteration dictionaries using both keys and values. The simple syntax to do this is `for index, value in enumerate(my_list)` would then product both indices and values for lists. 

### Zipping

Zipping objects using the `zip()` function creates a zip object, which can be used as follows:

```python
name = ["Apple", "Xiomi", "LG"]
brand_id = [121, 289, 323]

z = zip(name, brand_id)
```
A **zip object** is an iterator of tuples, which can be turned into a list object, using the **list** function. This list object would be a list of tuples containing pairs in the format *(name, brand_id)*.

Objects of **zip** type can be unzipped into two separate variables using the **zip()** function with a combination of **\*** as shown in `name_new, brand_id_new = zip(*z)`.

## Functions

New functions can be defined in python on using the following structure:

```python
def my_function(parameters):
	""" Docstring for the function """
	code_to_execute
	return result
	
my_function(arguments)
```

Here the name of the function is `my_function` and it takes in the parameters and returns a value. This value can then be stored for later use whenever necessary. 

> The **Docstring** serves as a documentation and should be written enclosed in triple double-quotes helping future interpretation and modifications to our functions.

### Functions with variables arguments

1. **Variable number of parameters**
	
	```python
	def my_function(*parameters):
		""" Docstring for the function """
		code_to_execute
		return result
		
	my_function(argument1, argument2)
	```

	The function defined above would take as many inputs as provided, and then convert them into a tuple therefore allowing you to add as many arguments as necessary in one go.

2. **Variable type of parameters**
	
	```python
	def my_function(**parameters):
		""" Docstring for the function """
		for k,v in parameters.items():
			do_something(k, v)
		return result
		
	my_function(key1 = value1, key2 = value2)
	```
	
	The function above allows us to pass multiple arguments in the form of key-value pairs therefore allowing us to access the values with names that they came with depending on the use case. 
	
### Scope

The scope heirarchy is as follows:

1. Local Scope
2. Enclosing Scope(s) (in order)
3. Global Scope
4. Builtin Scope


If a variable in the global scope needs to be altered from within a function, it can be done using the keyword `global`. Therefore

```python
x = 5
def my_function(parameters):
	""" Docstring for the function """
	global x
	x = 10
	
	
my_function(arguments)
```

the function above would alter the global value of x because we have defined that currently we want to fiddle with the `global` value of **x** using the `global` keyword.

### Lambda Functions

Generation of functions when required can be done in quicker way using the keyword `lambda` as `x = lambda x, y: x*y` would create a function `x` that can then be called like a normal function to find products of `x` and `y`.

### Exception Handling

We can catch different types of exceptions that occur during runtime for a given function using the code below. 

```python
def add_two(parameter):
	""" Adds 2 to any number provided """
	try: 
		return parameter + 2
	except:
		print("parameter must be an integer or float")
```

### Custom Errors

We can manually raise different types of error for a given function using the code below. 

```python
def add_two_to_int(parameter):
	""" Adds 2 to any number provided """
	if round(parameter) != parameter:
		raise ValueError("argument provided must be a positive integer") 
	try: 
		return parameter + 2
	except:
		print("parameter must be an integer or float")
```