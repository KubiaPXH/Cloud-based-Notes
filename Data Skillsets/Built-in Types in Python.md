## Text Type 
### [[String in Python]]
## Numeric Types: `int`, `float`, `complex`
### `float` type
- [Formatting float number](https://appdividend.com/2021/03/31/how-to-format-float-values-in-python/) #dig-deeper 
## Sequence Types: `list`, `tuple`, `range`
### `list` type
```ad-info
a `list` is a kind of collection, which allows us to put many values in a single "variable"
```
- a `list` element can be any Python object - even another list.
	- e.g. ![[Pasted image 20211228165833.png|250]]
- a `list` can be empty too.
- `list` is mutable, meaning that we can change an element of a list using index operator.
- Syntax: a `list` are surrounded by square brackets (\[]) and its elements are separated by commas.		
#### Index `list`
- Indexing list is (more or less) the same with `str`
- index of `list`, same as `str`, also start with 0.
#### Slicing `list`
- same with `str`
#### `list` methods
- [ref](https://www.w3schools.com/python/python_ref_list.asp): [more details](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)
#### `list` comprehension
- [ref](https://realpython.com/list-comprehension-python/):
	- Syntax: ![[Pasted image 20211229180007.png]]
#### Misc.
- `list()` function is used to make an empty `list`
- `len()` function is used to count the number of element in a `list` -> `range(len(list_name))` can be used with `for` function to indexing a `list` and get the exact position of each element in the `list`.
- `+` operator use for `lists` is equal to concatenating `lists`
	- e.g. ![[Pasted image 20211228171851.png|150]]
### `tuple` type
- Definition: `tuple` is another kind of sequence that functions much like a `list`, but `tuple` is immutable -> a `tuple` is a constant a `list`.
- Why use `tuple` instead of `list`? because they are more efficient (in term of memory use and performance) than `list` in some cases -> when we make temporary and immutable variable, we prefer `tuple` over `list`
- Syntax: a `tuple` are surrounded by parenthesis () and its elements are separated by commas.
- [`tuple` methods](https://www.w3schools.com/python/python_ref_tuple.asp): same as `list` methods but exclude all the methods that can modify its content.
- `tuple` can be put on the left-hand side of an assignment statement (e.g.1.) -> can be used as iteration variable in two iteration variables `for` loop (e.g.2.).
	- e.g.1. ![[Pasted image 20211229172012.png|200]]
	- e.g.2. ![[Pasted image 20211229172537.png|220]]
- `tuples` can be compared using comparison operators -> the direction of the differences = the direction of the non-equal pair of the two `tuples`
	- e.g. ![[Pasted image 20211229173035.png|350]]

## Mapping Type: 
### `dict` type
```ad-info
A `dict` (or dictionary) is a non-order collection in which each value has its own key to label them -> *key-value pair*.
```
- Syntax: a `dict` are surrounded by curly brackets ({}) and its key-value pairs are separated by commas.
	- e.g. ![[Pasted image 20211229162309.png|500]]
- Index `dict`: as `dict` has no order -> we index the values we put in dictionary with a "lookup tag"
	- e.g. ![[Pasted image 20211229161512.png|350]]
#### Differences btw `list` and `dict`
- `list`: a linear collection of values that stay in order (which we can index by position from 0->(n-1))
- `dict`: a collection with no real sense of order, instead each values has its own label (or key) to access them. However, we can still use `for` and `in` which `dict` variable.
#### `dict` methods
- [ref]](https://www.w3schools.com/python/python_ref_dictionary.asp): 
- `dict.get()`: return the value of the item with the specified key.
- `dict.keys()`
- `dict.values()`
- `dict.items()`: return the whole `dict` variable as a list and each key-value pair as a `tuple`
	- e.g. ![[Pasted image 20211229170044.png|350]]
#### "Sorting" with `dict`
- "Sorting" by key: `dict` don't have order -> can't be sorted, but we can convert a `dict` to a `list` of `tuples` using `dict.items()` then use `sorted()` function to sorted that `list`. 
	- e.g. ![[Pasted image 20211229173615.png|350]]
- "Sorting" by value: 
	- classic version: ![[Pasted image 20211229174315.png|300]]
	- even shorter version using list comprehension:
		- e.g. ![[Pasted image 20211229175557.png|400]] 
#### Misc.
- `dict()` function is used to make an empty dictionary.
	- if we want to create non-empty dictionary with `dict()`, we can use:
		- this syntax: ![[Pasted image 20211229163818.png|400]]
		- or this syntax: ![[Pasted image 20211229163847.png|300]]
- histogram with `dict.get()` pattern:
	- e.g. ![[Pasted image 20211229164456.png|400]]
## Set Types: `set`, `frozenset`
### `set` type
- [ref](https://realpython.com/python-sets/):
	- `set` type has the following characteristics:
		- `set` are unordered (like `dict`)
		- `set` elements are unique (duplicates are not allowed)
		- a `set` itself can be modified, but its elements are immutable
## Boolean Type: `bool`
## Binary Types: `bytes`, `bytearray`, `memoryview`
## None Type: `None`