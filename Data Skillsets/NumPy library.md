## NumPy
> NumPy is the fundamental package for scientific computing, use to calculate things and process numbers, with Python. NumPy is also famous as a multi-dimentional array library.
- Other important libraries such as *pandas* and *mathplotlib* is build on top of NumPy.

- **NumPy vs pure Python:**
	- In pure Python, processing numbers is very slow when processing a large amounts of data (as everything, so do `int` and `float`, in Python is object, it needs a lot of memory and computing power to process numbers) => NumPy solve that problem as uses primitive numeric (fixed) types but not object! (NumPy even give the choice to choose the number of bytes we want to store our variables)
	![[Pasted image 20220114152110.png|600]]
	- NumPy array also utilizes Contiguous Memory, which data is densely packed together, contrast to the Scattered Memory use by Python lists -> Boost CPU vector processing and Effective cache utilization.
	![[Pasted image 20220118110057.png|600]]
	- NumPy array is more powerful and can do way more tasks than Python list when it comes to matrix computation.


 > **Suggestion:** Thinking about how to optimize memory and reduce computing time when deal with a large amount of data!!
### Import NumPy:
- Normally we use syntax: `import numpy as np` to import NumPy library. np is an abbreviation -> less typing!
### NumPy array:
- A NumPy array works more or less the same a Python list.
- NumPy usually use for numeric processing -> not a common thing to have an NumPy array of `str` or `dict`.
#### Create an array:
- [**Create a basic 1D array:**](https://numpy.org/devdocs/user/absolute_beginners.html#how-to-create-a-basic-array)
	- [`numpy.array()`](https://numpy.org/doc/stable/reference/generated/numpy.array.html): create an basic array
	- `numpy.zeros()` : create an array filled with 0
	- `numpy.ones()` : create an array filled with 1
	- `numpy.empty()` : create an array whose initial content is random
	- [`numpy.arange()`](https://numpy.org/doc/stable/reference/generated/numpy.arange.html?highlight=arange#numpy-arange) : create an array whose content is similar to `range()` in Python
	- [`numpy.linspace()`](https://numpy.org/devdocs/reference/generated/numpy.linspace.html#numpy.linspace): create an array with a specified number of elements and spaced equally between the specified beginning and end values.
	- `dtype` is an attribute used to specific array type.
- [**Create a 2D array:**](https://numpy.org/devdocs/user/basics.creation.html#id1):
	- `numpy.eye(n,m)`: create 2D (nxm) matrix where the array\[i,i] = 1 and other = 0
	- `numpy.diag()`:
		1. create a square 2D array with values in the diagonal are equal to 1D array input arguments
		2. take a 2D array as argument and return only the diagonal elements of that array.
	- [`numpy.vander()`](https://numpy.org/devdocs/reference/generated/numpy.vander.html#numpy.vander): create a Vandermonde matrix
- [**Create a multi-D array:**](https://numpy.org/devdocs/user/basics.creation.html#general-ndarray-creation-functions)
	- `numpy.zeros()`: with specified shape
		- `numpy.zeros_like(a, dtype=None)`: return an array of zeros with the same shape and types as given array `a`, but we can override the data type by assigning `dtype`
	- `numpy.ones()`: with specified shape
	- [`numpy.indices()`](https://numpy.org/devdocs/reference/generated/numpy.indices.html#numpy.indices):
#### Index and Slicing:
##### Basic indexing:
[**ref**](https://numpy.org/devdocs/user/basics.indexing.html#basic-indexing)
> For single element indexing and slicing, we manipulate NumPy arrays in the same ways as Python lists

> Basic indexing and slicing returns **a view** not a copy.
- Negative indexing i (i<0) is interpreted as n+i
- Dimensional indexing tools: 
	- Syntax: `numpy.array[dim1,dim2,dim3...]` in each `dim` we can indexing and slicing it as a 1D array -> the slicing will expand for the whole array. 
	- Using `numpy.newaxis` or `None` to expand a new dimension by one unit-length dimension (example in section link)
##### Advanced indexing:
[**ref**](https://numpy.org/devdocs/user/basics.indexing.html#advanced-indexing)
> Advanced indexing is triggered when the selection object, obj, is a non-tuple sequence object, an `ndarray` (of data type integer or bool), or \[a tuple with at least one sequence object (plus other things) or `ndarray` (of data type integer or bool)].

> Advanced indexing and slicing returns **a copy** not a view.
- [**Integer array indexing:**](https://numpy.org/devdocs/user/basics.indexing.html#integer-array-indexing):
	- Syntax: `numpy.array[dim1,dim2,dim3...]` in each `dim` we input as non-tuple sequence, `ndarray`, or a tuple with at least one sequence object or `ndarray`
		- The result of a multidimentional slicing using integer array indexing is the elements which the position is a pair (or trio or collection of) same index element of the arrays used as input dimensions.
			- e.g. ![[Pasted image 20220115121606.png|400]]
	- The integer in one dimension of advanced indexing can be repeated multiple times:
		- e.g. ![[Pasted image 20220115102003.png|300]]
- [**Boolean array indexing (indexing using condition):**](https://numpy.org/devdocs/user/basics.indexing.html#boolean-array-indexing)
	- Boolean array indexing can use a tuple sequence of `True` and `False` values to filter the values it gets from the array:
		- e.g. ![[Pasted image 20220115115111.png|300]]
	- This advanced indexing occurs when *obj* is an array object of Boolean type, such as may be returned from comparison operators (using broadcasting boolean array).
		- e.g. ![[Pasted image 20220114165205.png|500]]
	- `np.nonzero()`: to get indices of the non-zero elements from an array
		- e.g. ![[Pasted image 20220114165804.png|500]]
	- `np.nan`: stand for "not a number", and it is used to represent a missing numerical value in an array (not `np.nan` is `~np.isnan()`)
		- e.g. ![[Pasted image 20220115103958.png|450]]
- Other way of indexing:
	- [`np.triu_indices_from(arr, k=0)`](https://numpy.org/doc/stable/reference/generated/numpy.triu_indices_from.html#numpy-triu-indices-from): return the indices for the upper-triangle of the `arr`, `k` is diagonal offset (1 is not include diagonal)
	- `np.tril_indices_from()`:
	- `np.diag_indices_from()`: 
#### Array manipulation:
[**ref**](https://numpy.org/doc/stable/reference/routines.array-manipulation.html)
Common uses functions:
- `numpy.shape(<ndarray>)`: return the shape of an array
- `numpy.copyto(dst, src[, casting, where])`: copy values from `src` array to `dst` array, broadcasting as necessary
- `numpy.reshape()`: give new shape to an array w.o. changing its data
- `numpy.resize()`: return a new array with the specified shape
- `ndarray.T`: the transposed array
- `numpy.concatenate()`: join a sequence of arrays along an existing axis
- `numpy.vstack()`: stack arrays in sequence vertically (number of columns is constant)
- `numpy.hstack()`: stack arrays in sequence horizontally (number of rows is constant)
- `numpy.unique()`: find unique elements of an array.
- `numpy.delete()`
- `numpy.insert()`
- `numpy.append()`
#### Summary Statistics with NumPy:
[**ref**](https://numpy.org/doc/stable/reference/routines.statistics.html)
Some common ones:
- `numpy.sum()`
- `numpy.mean()`
- `numpy.median()`
- `numpy.std()`
- `numpy.var()`
#### Broadcasting Operations: 
[**ref**](https://numpy.org/devdocs/user/basics.broadcasting.html)
> **Broadcasting** describes how NumPy treats arrays with different shapes during arithmetic operations. **Subject to certain constraints**, the smaller array is "broadcast" across the larger array so that they have compatible shapes -> to make the operations.
- Simple example:
	- Normally, two arrays need to have exactly the same shape to make to operation:
		- e.g. ![[Pasted image 20220115105412.png|250]]
	- NumPy can relaxes this constraint in this cases (as elements of the second array are the same) -> make operation with scalar instead of array:
		- e.g. ![[Pasted image 20220115105638.png|250]]
	- In this example, the scalar *b* is stretched to become an array of same shape as *a*, therefore compatible to multiplication.
		- ![[Pasted image 20220115105857.png|400]]
	- The code in **the scalar example is more efficient** than array example because broadcasting moves less memory around during the multiplication.
- General Broadcasting Rules:
	> When operating on two arrays, NumPy compares their shapes element-wise. It starts with the trailing (i.e. **rightmost**) dimensions and **works its way left**. Two dimensions are compatible when: 1/ they are equal, or 2/ one of them is 1.
	> If there is more than one incompatible dimension pairs in the operation => `ValueError: operands could not be broadcast together`
	- No-error examples: 
		- ![[Pasted image 20220115113929.png]]
		- ![[Pasted image 20220115113942.png]]
	- Error examples:
		- ![[Pasted image 20220115114119.png|500]]
	- Using `np.newaxis` to perform operations for two 1-d arrays:
		- e.g. ![[Pasted image 20220115114337.png|330]]
#### NumPy Linear Algebra:
[**ref**](https://numpy.org/doc/stable/reference/routines.linalg.html) 
### Other stuffs:
#### Logic functions
- **Logical operations:**
	- `&`: `numpy.logical_and()`
	- `|`: `numpy.logical_or()`
	- `~`: `numpy.logical_not()`
	- `numpy.logical_xor()`: both args are the same -> 0; both args are different -> 1.
#### Finding missing data:
- `np.isnan()`: return a boolean values `DataFrame` or `Series` having the same shape as the input argument, `True` for `NaN` value and `False` for not `NaN` value.
- `np.isinf()`: return a boolean values `DataFrame` or `Series` having the same shape as the input argument, `True` for infinite value and `False` for not infinite value.
- `np.isfinite()`: return a boolean values `DataFrame` or `Series` having the same shape as the input argument, `True` for finite value (not `NaN` or infinite) and `False` for not finite value.