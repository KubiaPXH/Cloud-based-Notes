```ad-info
`str` or string: is an immutable sequence of Unicode characters
```
- In Python 3 (different Python 2), all strings are Unicode.
## Index `str`
- `str` is a sequence of characters -> we can index (start with 0) within string -> can use string directly after `in` in `for` loop.
- e.g. ![[Pasted image 20211228142107.png|200]]
- e.g. using string directly in `for` loop: ![[Pasted image 20211228143010.png|200]]
- for index: normal direction starts with 0 -> (n-1) but reverse direction starts with (-1) -> (-n)
	- e.g. ![[Pasted image 20211228144714.png|400]]
- `str` is immutable, meaning cannot using index operator to change `char` element in a string. 
	- e.g. ![[Pasted image 20211228170413.png|300]]
## Slicing `str`
- [ref](https://www.geeksforgeeks.org/string-slicing-in-python/):
- Method 1: using `slice()` constructor that creates a slice object representing the set of indices specified.
	- Step 1: define `slice()` 
		- Syntax: ![[Pasted image 20211228144315.png|200]]
			- *start*: starting index where the slicing of object starts
			- *stop*: ending index where the slicing object stops **but ending index is not included**.
			- *step*: the increment btw each index for slicing
	- Step 2: input `slice()` in string index syntax.
		- e.g. ![[Pasted image 20211228144902.png|200]]
- Method 2: using directly string index syntax.
	- Syntax: ![[Pasted image 20211228145120.png|200]]
	- e.g. ![[Pasted image 20211228145208.png|200]]
## `str` methods
- [ref](https://www.w3schools.com/python/python_ref_string.asp) and [more details](https://docs.python.org/3/library/stdtypes.html#textseq)
- There are functions (methods), in the *string* library, are already built into every string (object), but these functions do not modify the original string but return a new string that has been altered. 
	- e.g. ![[Pasted image 20211228151758.png|300]]
- To see built in methods in string using `dir(str_variable)`
	- some common methods: ![[Pasted image 20211228151921.png]]
	- `str.split('<delimiter>')` : split the strings a part using delimiter (multiple spaces are default delimiter) and create a list of strings (or words).
		- e.g. ![[Pasted image 20211228173151.png|250]]
## Misc.
- `len()` function gives us the length of a *string*.
- for `str`, `+` means "concatenate"
- `in` can be use as a logical operator.
	- e.g. ![[Pasted image 20211228150417.png|200]]
- (not so common use) but we can compare *strings* together using comparison operators.
- `\n` is a *newline* character in string (`\n` is still one character not two, better remember when counting).
	- e.g. ![[Pasted image 20211228160036.png|250]]