# **NUMPY**
NUMPY Library is the basis of a large amount of mathematical and scientific packages of python.  It is specialised for data analysis and developed using the concepts introduced by NumPy.
> Built-in tools in standard python library are inadequate and inefficient for data analysis.

## **Numpy objct**

The library us based on one main object , called the `ndarray`

These arrays are:
- Homogeneous and have items of the same size
- Mutable but of fixed size. This means that the number of items cannot be changed once created but items can.

Size of the array is to be determined at the time of the creation.
`dtype` is an attribute of the array object which specifies the data type of the items in the array. Every array is associated with one `dtype`.


The main attributes of the `ndarray` object:

- __axes__:The directions in which data is laid out or the dimensions of the array object.
- __shape__: A tuple that indicates the size along each dimension 
- __size__: The total number of elements in the array
- __rank__or__ndim__: The total number of dimensions or axes.
- __itemsize__: size of the item in bytes
- __data__: Holds the buffer(raw memory) of the array

> NOTE: axis 0 means 1D , axis 1 corresponds to 2D and so on..
> The attributes *shape, size,ndime & dtype* can be accessed `arrayname.attribute`.


## **Array Creation**

In the python session, import the library

	`import numpy as np`

- Using the `array()` function
	
	`a = np.array([[1,2],[3,4]])`

- Arrays in this library are a completely different objects from standard lists and tuples. We can pass tuples, lists or even a mix of them in the `array()` function to create the array
	`a = np.array(([1,1],(2,2)))`
	
- Arrays in numpy have a lot of dtypes, even strings.
dtype can be passed as an argument to `array()` function to specify the datatype.
	
	`a = np.array([1,2],dtype=bool)`

> arrays can have Strings as datatype
### **Intrinsic Creation**

- `zeros()` and `ones()` take the *shape* attribute as argument and even *dtype*
- `arange()` takes start,end,step as parameter and even dtype. Also the function `reshape()` can be used to change the shape attribute by passing it as argument.	
	

## **Array Operations**

## **Accessing the elements**

## **Array Manipulation**

## **General Concepts**
