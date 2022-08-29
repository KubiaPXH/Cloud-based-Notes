## Functions in Python
### Why using Functions:
1. **Abstract then Reuse** a set of code using procedure or function -> [Don't Repeat Yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle! Even make a library if needed :).
2. **Reliability and easier/faster to debug** -> if prob, only need to correct one time the function source code then every place we call that function will be fine!
3. **Modularity**: break down complex processes into smaller and manageable steps.
### Procedure & function:
#### Procedure (or void function): 
- **Definition:** A procedure is a pre-defined data structure (e.g. set of code) that can be called upon at any point in a program, it can take arguments or parameters (values that is passed/inputed into a function) but **does not** return a value. But in Python, the procedure concept is not explicitly defined and used.
#### Function (or fruitful function):
```ad-info
[**ref**](https://realpython.com/defining-your-own-python-function/) 
```
- **Definition:** A function is a pre-defined data structure that can be called upon at any point in a program, it can take arguments but **does** return a value.
	- e.g. ![[Pasted image 20211227153541.png|500]]
- We can use **[built-in functions](https://docs.python.org/3/library/functions.html)**:
	- `print()` 
		- [f-string](https://realpython.com/python-f-strings/#f-strings-a-new-and-improved-way-to-format-strings-in-python) (or *formatted string literals*) is new and improved way to format string in Python. f-string is prefixed with `f` or `F` (e.g. `print(f"abc")`)
	- [`ord()`](https://docs.python.org/3/library/functions.html#ord): read a character and return an integer representing that character -> the return integer is the underlying order that Python use for its `sort()` function.
	- [`dir()`](https://docs.python.org/3/library/functions.html#dir): Without arguments, return the list of names in the current local scope. With an argument, attempt to return a list of valid attributes for that object.
		- [Underscore meaning in `dir()` results](https://dbader.org/blog/meaning-of-underscores-in-python) #dig-deeper 
	- [`main()`](https://realpython.com/python-main-function/): #dig-deeper
		- Using the `if __name__ == "__main__":` to determine the execution context.
		- Create `main()` to contain the code you want to run when call the file in the command line:
		```python
		def main():
			<statements>
		if __name__ == "__main__":
			main()		
   ```
			- 
			- e.g. 
- Or we can **[define and call a function](https://realpython.com/defining-your-own-python-function/)** ourselves:
	- To define a function we use `def` statement:
		- Syntax: ![[Pasted image 20211227151533.png|300]]
		- *parameters*: variable(s) (or placeholders) we use in the function definition which later can handle different inputs (arguments in function call) in the function, when it is called in different times.
		- A function need to have return value(s) using `return` statement (when procedure have no return), a `return`statement will:
			1. It immediately terminates the function -> passes running line back to caller's line.
			2. It send back the value after `return` as output of the caller.
		- Using [`yield`](https://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do) instead of `return `
			- When you call a function contains a `yield` statement, you get an generator object.
			- Then, each time you extract an object from the generator, Python executes code in the function until a `yield` statement, then **pauses** and delivers object in `yield` statement.
			- Then, when you extract another object, Python resumes after the pause of previous `yield` object and execute code until another `yield`
			- This continues until the generator exhausted.
		- To specify the type of parameters and the type of the return ([more details](https://stackoverflow.com/questions/2489669/how-do-python-functions-handle-the-types-of-parameters-that-you-pass-in))
			- e.g. ![[Pasted image 20220104165055.png|300]]
	- To call(or invoke) a procedure/function we just need to use:
		- Syntax: ![[Pasted image 20211227152918.png|300]]
		- *arguments* are the values passed into the function, corresponding to *parameters* in the defining part.
	- [Default argument values](https://docs.python.org/3.9/tutorial/controlflow.html#default-argument-values): use to specify a default value for one or more arguments -> default arguments are also optional arguments -> allow to call a function with fewer arguments than it is defined to allow.
		- e.g. ![[Pasted image 20220111151635.png|650]]
	- [Keyword arguments](https://docs.python.org/3.9/tutorial/controlflow.html#keyword-arguments): functions can also be called using keyword arguments of the form `<kwarg>=<value>`.
		- function def: ![[Pasted image 20220111152212.png|500]]
		- function call can be: ![[Pasted image 20220111152323.png|600]]
	- [Special parameters](https://docs.python.org/3.9/tutorial/controlflow.html#special-parameters): By default, arguments may be passed to a function either by position or explicitly by keyword. Specific syntax is necessary for readability and performance.
		- Function def syntax: ![[Pasted image 20220111152815.png|400]]
	- Passing an unspecified number of arguments to a function: [`*args` and `**kwargs`](https://book.pythontips.com/en/latest/args_and_kwargs.html)
		> the 'args' and 'kwargs' in `*args` and `**kwargs` are just writing convention, only the `*` is necessary (we can change them to `*vars` or `**vars` if we want)
		- `*args` and `**kwargs` are mostly used in function definitions -> to allow to pass an unspecified number of arguments to a function.
			- `*args` is used to send unspecified number of **non-keyworded** arguments to the function.
				- e.g. ![[Pasted image 20220111141306.png|400]]
			- `**kwargs` is used to pass unspecified number of **keyword** arguments to the function -> handle **named arguments**.
				- e.g. ![[Pasted image 20220111141609.png|400]]
#### Lambda function (or Lambda expression)
```ad-info
[**ref**](https://realpython.com/python-lambda/)
```
- Lambda function is a one-line anonymous functions, lambda function is also saw by Python as an expression.
	- Syntax: `lambda *args: <function_body>` 
		- `*args` are bound variables which is arguments of lambda function
		- `<function_body>` also includes the implicit return value
		- e.g. ![[Pasted image 20220129110634.png|200]]
	- Input arguments to lambda function using parenthesis:
		- e.g. ![[Pasted image 20220129110804.png|250]]
	- Lambda function (as an expression) can be named:
		- e.g. ![[Pasted image 20220129111205.png|300]]
	- Lambda function is frequently used with higher-order functions, which take one or more functions as arguments or return one or more functions as results.
		- e.g. ![[Pasted image 20220129111631.png|450]]

