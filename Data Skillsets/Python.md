## What is Programming?
- Program is a tool installed in a computers to do (repetitive or not) things for us, things can be simple or hardly complicated.
	- Computer is dumb but thanks to its super computation power and emotionless property it can do a lot of thing better and faster than human. The thing that it needs is a good instructions = a good program.
	- A program is a sequence of steps to be done **in order**.
- **Programming = building a tool that tell computer what you want to do to solve our problems**. However, prob is computers have their own language (super hard for computers understand human language) -> We need to speak to computers in a language that it can understand = programming language.
	- If you program for other people, thinking about the things they want to do and their user's experiences.
- Code = a sequence of stored instructions (of how to solved a problem or do something).
	- Code need to be perfectly exact, because computer is extremely literacy.
- Algorithms: a set of rules or steps used to solve a problem.
- Data Structures: a particular way of organizing data in a computer. 
## Basic Hardware Architecture
- Basic Diagram:
	-	![[Pasted image 20211225152957.png|500]]
	-	Micro Processing Unit (or Central Processing Unit): ask for "What next?" (instruction) to process it (this called operation) and then move on to ask new instruction and again process it. The CPU is very dumb but very fast (can do billions operations in a second)
	-	Main memory (RAM): *fast small temporary storage* which stores the instructions fed to the CPU. But when turn off -> things in main memory vanish!
	-	Secondary memory (Hard drive): *slower large permanent storage* which is slower than Main memory but it stores thing more "permanently" (when turn off -> things still remain in Secondary memory) 
		- All OS and softwares are stored in Secondary memory and loaded in Main memory when to computer is running.
	- Input devices: Keyboard, Mouse, Touch Screen...
	- Output devices: Screen, Speakers, Printer...
	- Mother broad: is just a broad with wires to connect every components together.
- **What happen to your code when it is executed?**
	- Your code is written and stored in the Secondary memory.
	- Then, your code (in Python) is loaded (by a translation process) to the Main memory as Machine language.
	> **Remember:** Computer only can process binary data as 0 or 1 (a bit)
	- And, CPU ask "What Next?" -> Main memory fed your instruction in Machine Language, based on your code, to CPU -> CPU executes the operation according to your instruction -> CPU ask "What Next?" again... This 3 steps of the loop happen billions times per second.
## Talking to Python
Best resources: [Python 3.10.1 documentation](https://docs.python.org/3.10/)
> Remember: **syntax error** (grammar faults) is an attempt of Python to tell you that it doesn't understand you and ask you to help.
### Example of Python code and its Basic Components: 
- e.g. ![[Pasted image 20211225162600.png|400]]
- **Constant**: fixed (not-change) values of diff data type such as numbers, letters and strings. 
- **Reserved words**: already-defined words in Python -> can not use reserved words as variable names or identifiers.
- **Variable**: *a reserved and named place in the memory* where we can store data and later retrieve using the variable "name" (that we choose). we can change (overwrite) the value (data) of a variable.
	- Variable name: 
		- must start with letter or underscore _; 
		- must consist letters, numbers and underscores; 
		- lowercase and UPPERCASE is different (e.g. spam and Spam are different)
	- Best practice to give name: a variable's name should help us remember what we intend to store in them.
		- ![[Pasted image 20211225164810.png|500]]
		- Use Snake Case, word is separated by an underscore character, for naming variable (e.g. my_variable_name). For [more details](https://cs.stanford.edu/people/nick/py/python-style-readable.html).
### Operators:
#### Arithmetic Operators
- [ref](https://www.w3schools.com/python/gloss_python_arithmetic_operators.asp)
- Operator Precedence Rules: Parenthesis -> Power -> Multiplication -> Addition -> Left to Right.
- But when writing code using a lot of operators -> use parenthesis.
- If the operations is too complex -> break them up to small species to make them more clear.
#### Comparison Operators
- [ref](https://www.w3schools.com/python/gloss_python_comparison_operators.asp):
- `is` is a logical operator = "is the same as". `is` is similar to `==` but stricter, demand equality in both value and type of variable (e.g. 0 `==` 0.0 -> TRUE but 0 `is` 0.0 -> FALSE). `is not` is also a logical operator, strict as `is`.
### Data Type: 
#### [[Built-in Types in Python]]
#### Get Type & Type Conversion:
- `type()` function: get the type of the variable. 
- We can converse variables from one type to another using: `int(str)`, `float(str)`, `bool(val)`, `str(val)` (e.g. val can be int or float or other eligible types)
#### Files in Python
[**ref**](https://realpython.com/working-with-files-in-python/):
##### Open a file:
- Call `open()` function: `open()` returns a "file handler" - a variable used to perform operations on the file.
	- Syntax: ![[Pasted image 20211228154423.png|250]]
	- *filename* is a string and *mode* is (optional) intention to work with the file ('r' = read the file and 'w' = write to the file), 'r' is the default mode.
	- *handler* is a intermediate gateway, which is not the file itself, that allows Python to open, read, write and close a file.
	- We can input *filename* as variable (so we can use the same code to read other files later) and deal with the bad file name using try/expect structure.
		- e.g. ![[Pasted image 20211228163952.png|350]]
- `<handler>.close()`: It is a standard practice to close an opened file after used to free up resources and reduce the risk of being unwarrantedly modified or read 
- A text file can be thought as a sequence of lines -> a text file has `\n` (newline character) at the end of each line.
	- **A *file handle* open for read can be treated as a sequence of strings** where each line in the file is a string -> can use `for` statement to read through the file (as sequence).
		- e.g. ![[Pasted image 20211228161419.png|250]]
		- Notice: each of the string end with a `\n` (if want to delete that `\n` when reading line -> use `.rstrip()` method)
- [File methods](https://www.w3schools.com/python/python_ref_file.asp):
		- `.read()` returns the whole file content into a single string
##### Open a file using `with` statement: 
- with `with` statement the opened file is automatically close when it's not needed anymore, therefore we don't need to remember to close the file handler.
- Syntax, here <file_object> is <file_handler>: ![[Pasted image 20220117163751.png|300]]
- Remember to indent to work with <file_handler> in a `with open()` statement!
### Intergrate SQL Database with Python 
```ad-resources
[PyMySQL documentation](https://pymysql.readthedocs.io/en/latest/)
```
#### Simple example of SQL query in Python
- Step 1: Choose to import *PyMySql* library
	- `import pymysql`
- Step 2: Set connection
	- Syntax for *PyMySQL*: `conn = pymysql.connect()`
		- `host`: host where the database server is located
		- `user`
		- `password` or `passwd`
		- `database` or `db`: database to use (e.g. `db='mysql'`)
- Step 3: Set cursor having method `execute('<SQL_query>')` where argument is the SQL query to run against the database.
	- Syntax set cursor: `cur = conn.cursor()`
	- Syntax run `execute()` method: `cur.execute('<SQL_query>')`
- Step 4: Use `fetchall()` method of the cursor to get the query results -> work with results
	- Syntax: `results = cur.fetchall()`
- Step 5: Close the cursor and the connection:
	- Syntax: `cur.close()` and `conn.close()`
#### Components of PyMySQL
```ad-resources
- [PyMySQL API reference](https://pymysql.readthedocs.io/en/latest/modules/index.html)
- [PEP 249 -- Python Database API Specification v2.0](https://www.python.org/dev/peps/pep-0249/) for more details
```
- [**Connection Object:**](https://pymysql.readthedocs.io/en/latest/modules/connections.html)
	```ad-definition
	**Connection object** is responsible for connecting to the database, sending database info, handlings rollbacks (undo actions that have not been saved), and creating new cursor objects (connection can have many cursors).
	```
	- `Connection.commit()`: commit changes to stable storage
	- `Connection.close()`: send quick message and close the socket (connection)
- [**Cursor Object:**](https://pymysql.readthedocs.io/en/latest/modules/cursors.html)
	```ad-definition
	**Cursor object** keeps track of certain state information, such as which database (or schema?) it is using (we can use multiple cursors to write in multiple databases as the same time) and contains the results of the latest query it has executed.
	```
	- `Cursor.execute(query)`: execute an MySQL query
	- `Cursor.executemany(query,arg)`: run several data against one query
	- `Cursor.fetchall()`: fetch all rows
	- `Cursor.fetchmany()`: fetch several rows
	- `Cursor.fetchone()`: fetch the next row
	- `Cursor.callproc(procname, args=())`: execute stored procedure \<procname> with args
	- `Cursor.close()`: close a cursor just exhausts all remaining data
### [[Objects Oriented Programing with Python|Objects]]
### Basic Commands in Python
- Assignment Statements (=): Python calculates **the expression in the right hand side first** then assign it to the variable in the left hand side later. 
	- ![[Pasted image 20211225165312.png|300]]
#### Input and Output:
- [input()](https://www.w3schools.com/python/ref_func_input.asp) function: instruct Python to pause and read data from the user (e.g. typing sth + enter), `input()` function return `str`.
- [print()](https://realpython.com/python-print/) function: print the specified message to the screen (or other standard out device). Objects, whose type != `str` will be converted into a `str` before print. 
	- Small notice: the `print()` function normally ends with an `\n`.
#### Conditional Executions: 
- [`if` statement](https://realpython.com/python-conditional-statements/):
	- A full conditional execution includes: `if` statement, boolean expressions (using [[#Comparison Operators https www w3schools com python gloss_python_comparison_operators asp|comparison operators]]), `elif` clause(s) and `else` clause.
		- Syntax:  ![[Pasted image 20211227105557.png|180]]
		- `if`, `elif` and `else` are in the same level of indentation. 
		- The if statement end when we de-indent (a.k.a. reduce back to the same level of indentation with `if` statement).
	- [`pass` statement](https://realpython.com/python-pass/): normally using within block code (`if`, `for`, `def`... statement) as an equivalent of empty block in other language.
- [`try/expect` structure](https://pythonbasics.org/try-except/): can handle exceptions (a.k.a. blowups). Exceptions are errors that happen during execution of the program (exceptions can be [built-in or user-defined](https://pythonbasics.org/try-except/#Built-in-exceptions))
	- Syntax: ![[Pasted image 20211227115207.png|250]]
		- *try*: the code with the exception(s) to catch. If having exception(s) -> jump to except block.
		- *except*: this code is only executed if an exception occured in the try block. 
	- Can also combine try/except statement with [finally](https://pythonbasics.org/try-except/#try-finally) and [else](https://pythonbasics.org/try-except/#try-else) clause.
		- *else*: else block code is only executed if no exception(s) were caught in try block. 
		- *finally*: the code in finally block is always executed, regardless of if an exception was caught or not.
- `assert` statement: is use to continue the execute if the given condition to True.
	- Syntax: ![[Pasted image 20220106171359.png|300]]
	- e.g. ![[Pasted image 20220106171508.png|400]]
#### Loops and iterations
- **Iteration** means executing the same block of code over and over (many times) and a programming structure that implements iteration is called a **loop**.
	- Two types of iteration:
		1.  *indefinite iteration*: the number of times the loop is executed isn't specified explicitly in advance (e.g. `while` loop).
		2.  *definite iteration*: the number of times the loop will be executed is specified explicitly at the time the loop starts (e.g. `for` loop).
-  [`while` loop](https://realpython.com/python-while-loop/) (indefinite loop): `while` loop keeps continue to execute while the condition in the expression is true.
	- Syntax: ![[Pasted image 20211228075322.png|200]]
	- `break` control statement: immediately terminates a loop **entirely** -> execution moves to the first statement following the loop body.
	- `continue` control  statement: immediately terminates the current loop iteration -> execution moves back to the top of the loop, `while` line.
- [`for` loop](https://realpython.com/python-for-loop/) (definite loop): 
	- Syntax: ![[Pasted image 20211228081513.png]]
	- Python treat a `for` loop in exactly the same way as *iterables* and *iterators*:
		- [*iterable*](https://realpython.com/python-for-loop/#iterables): an object can be used in iteration. Normally, data types that are collection or container types are iterable but, in fact, almost any object in Python can be iterable.
		- *iterator*: An *iterable* can be passed to the built-in Python function `iter()`, which return an *iterator*. Thus, *iterator* is essentially a value producer that yields successive values from its associated *iterable* object.
	- [List-typed iterating](https://realpython.com/python-for-loop/#iterating-through-a-dictionary): `for` loop can deal with list-typed data such as `list`, `tuple`, `dict`.
	- `for` loop in Python can also deal with [*Numeric range loop*](https://realpython.com/python-for-loop/#numeric-range-loop) using `range()` function, [more details](https://realpython.com/python-for-loop/#the-range-function).
	- `break` and `continue` statements in `for` loop have the same function as `while` loop.
	- The `else` clause will be executed if the loop terminates through exhaustion of the *iterable*.
	- Bonus: Two iteration variables
		- We can loop through the key-value pair in a `dict` using two iteration variables in a `for` loop:
			- e.g. ![[Pasted image 20211229170332.png|350]]
#### [[Functions in Python]]
#### Generator expressions in Python
```ad-definition
Generator expression is an expression that returns a generator object (or iterator which becomes exhausted when you complete iterating over it)
```
- A [generator expression](https://www.python.org/dev/peps/pep-0289/) using brackets `()` instead of square brackets `[]` (like list comprehension), it supports complex syntaxes:
	- loops
	- `if` statements
	- multiple nested loops
	- nested comprehensions
- Example: 
	- Simple one: 
		- ![[Pasted image 20220308161152.png|250]]
	- Nested loops:
		- ![[Pasted image 20220308161233.png|500]]
	- `if` statement:
		- ![[Pasted image 20220308161346.png|400]]
#### Indentation
- `if` and `for` block using indentation:
	- **Increase indent** indent after an `if` statement or `for` statement (after `:`) -> create an `if` block or a `for` block
	- **Maintain indent** -> indicate the scope of the block (which lines are affected by the `if`/`for`)
	- **Reduce indent** back to the level of `if` or `for` statement -> indicate the end of the block
- Normally we indent 4 spaces: How? **Remember to Turn off Tabs** -> then can use tab key! **Attention**: not mixing btw tabs and spaces, if not you get "indentation errors".
	- Shortcut in **Jupyter Notebook**: 
		- To Indent: `ctrl + ]` or `tab`
		- To de-indent: `ctrl + [` or `shift + tab`
#### [[Regular Expressions]]
#### Comments
[**ref**](https://realpython.com/python-comments-guide/):
- One line comment: Comment start with the `#`: anything after a `#` is ignored by Python
- Multi line comment: Begin with `"""` and end with `"""`
- Set up region to collapse code blocks: using the couple `#region` and `#endregion`
- **Reason to use comments**:
	- Describe what below paragraph of code does
	- Document additional information to make clear a line of code
	- Turn off (temporarily) a line off code -> for testing purpose
### Libraries
#### `os` module
```ad-definition
`os` module provides a portable way to use operating system dependent functionality
```
```ad-resources
[Offical documentation for `os` module](https://docs.python.org/3/library/os.html)
```
- `os.path.dirname(os.path.realpath(__file__))`: get full path to the directory the current Python file contained in
	- `__file__`: the pathname of the current file 
	- `os.path.realpath(path)`: returns the canoncial path of the specified filename (path) by eliminating any symbolic links encountered in the path
	- `os.path.dirname(path)`: returns "the directory name of pathname `path`"
- `os.getcwd()`: returns the current working directory path that Python is on (not necessary the file folder)
- `os.chdir(path)`: change current working directory to `path`
#### `random` library
[ref](https://realpython.com/python-random/)
- **Disclaimer**: Most random data generated in Python is not fully random, in scientific sense - non-deterministic and lack of predictability, **pseudorandom** - a seemingly random but still reproducible data. 
- `random` module in Python is pseudorandom number generator (PRNG)
	```ad-caution
	The pseudo-random generators of this module should not be used for security purposes. ([link](https://docs.python.org/3/library/random.html)) -> It's imperative to use Cryptographically Secure Pseudorandom Number Generator (CSPRNG) for that purpose.
	```
- `random.seed()`: initialize the process of generating seemingly "random" results reproducible -> same input argument = same "random" sequence of data.
	- e.g. ![[Pasted image 20220111171724.png|250]]
- `random.random()`: return the next random floating point number in the range \[0.0,1.0)
- `random.randrange(start,stop[,step])`: generate integer number range \[start,stop)
- `random.uniform(start,stop)`: generate float number range \[start,stop)
- `random.choice()`: pick random with replacement element from a non-empty sequence (`list` or `tuple`)
	- e.g. ![[Pasted image 20220111172420.png|400]]
- `random.sample()`: pick random without replacement element from a non-empty sequence (`list` or `tuple`)
- `random.shuffle()`: take a non-empty list as input and randomly shuffle (change the order of) sequence's elements.
- If we generate a sequence of random numbers -> better use [`numpy.random`](https://realpython.com/python-random/#prngs-for-arrays-numpyrandom) package (below is the summarize most common functions of `random` module and `numpy.random` counterparts)
	- ![[Pasted image 20220111175104.png|550]]
#### `copy` library
[ref](https://realpython.com/copying-python-objects/):

#### [[NumPy library]]
#### [[Pandas library]]
### Datetime in Python
- [`date.strftime()`](https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior): return a string presenting the date, controlled by an explicit format string. With [`strftime()` cheatsheet](https://strftime.org/).
## Talking to the network using Python
### Using Sockets and Ports to (another endpoint in) the Network 
- TCP (Transmission Control Protocol) Connections/ Sockets: In computer networking, an Internet **socket** or network **socket** is an endpoint of a two-way (bidirectional) *inter-process* communication between two programs flow across an Internet Protocol-based computer network (e.g. the Internet). Normally, a socket is the combination of IP address plus port.
- TCP port: a **port** is an application-specific or process-specific software communications in the endpoint. Ports are identified by **port number**.
- An easy-to-understand explanation of [Sockets and TCP/IP Ports](http://www.steves-internet-guide.com/tcpip-ports-sockets/)
### Sockets in Python
- `socket` library: is a built-in library that supports for TCP sockets (for [more detail guides](https://realpython.com/python-sockets) and [more documentations](https://docs.python.org/3/library/socket.html))
- [Import and connect using socket](https://www.geeksforgeeks.org/socket-programming-python/):
	- import `socket` library -> make a socket instance:
		- Syntax: ![[Pasted image 20211230114901.png|400]]
		- *AF_NET* refers to the address-family ipv4.
		- *SOCK_STREAM* means connection-oriented TCP protocol.
	- connect a port in a host across the Internet.
		-  Syntax: ![[Pasted image 20211230115825.png|200]]
### HTTP in Python
- Definition: the **H**yper**T**ext **T**ransfer **P**rotocol is the set of rules to allow browsers to retrieve web documents from servers over the Internet.
	- Protocol is a set of rules that all parties follow so we can predict and understand each other's behavior and action.
	- example of an url (Uniform Resource Locators): ![[Pasted image 20211230120814.png|300]]
- Normally, when we click at a link, the browser (process or app) send a `GET <url>` (e.g. GET http://www.abc.com/page2.htm) to the Web server (remote process) through the port 80 (the port assigned to "listen to" function of the server) -> the Web server process the request and send back a response in HTML (the format of the document) -> then the browser render it and make a web page from the HTML.
- An HTTP request (simple web browser) in Python:
	- e.g. ![[Pasted image 20211230150158.png|550]]
	- `.encode()`: as we send bytes to talk to external resources, `encode()` function is to use to encode Python 3 string to a given character encoding (normally UTF-8 bytes). 
		- Why do we `encode()`? One reason is Unicode is heavy to send through the network so we `encode()` Unicode strings -> UTF-8 bytes so the message can be sent faster and taken less bandwidth of the network.
	- `.decode()`: when we receive data from an external resources, we must `decode()` it based on the character set (normally  UTF-8 bytes) so it is properly represented in Python 3 as string.
	- ![[Pasted image 20211230153950.png|500]]
- A shorter HTTP request: Using `urllib` library (URL handling modules) in Python ([more documentation](https://docs.python.org/3/library/urllib.html))
	- `urllib` is a library that does all the socket work for us and treats web pages (url) as a file
	- Import `urllib`: with 3 sub-library
		- e.g. ![[Pasted image 20211230155100.png|400]]
	- Using a handler with a request-and-receive the data from url function `urllib.request.urlopen(<url>)` -> deal with the new handler like other file handler (but don't forget to `decode()` it)
		- e.g. ![[Pasted image 20211230155553.png|500]]
		- Notice that when we use this method the header (or metadata) is hidden in the URL (and we can show them if we want)
- Web Scraping (or Parsing HTML) #dig-deeper:
	- Definition: when a program or script (pretends to be a browser) retrieves web pages, looks at those, extracts info and then looks at more web pages. Slang: when search engines scrape web pages, we call "web crawling" (or "spidering the web")
	- Using `BeautifulSoup` library, which can import to Python.
### Web Services
- Problem: Different applications written by different programming languages using different formats for their data so when we put on the network their applications can not easily communicate to each other -> Solution: Better to have a common format (the "Wire format") so every (or most) applications written by every (or most) languages.
- Example of diff applications using "Wire Format" (commonly is XML or JSON)
	- ![[Pasted image 20211230163340.png|500]]
- Service oriented approach is a way to approach solving complex application problem where all the data is spread out over the network, but not present in a centralized computer system.
#### XML
- Definition: XML stands for (eXtensible Markup Language). A markup language is a set of rules for encoding documents in a format that is both human-readable and machine-readable.
- XML Basics:
	- XML's basic tags, self closing tags, attributes, text context:
		- e.g. ![[Pasted image 20211230164409.png|350]]
	- XML's basic elements (or node): 
		- simple node: node which has no children node, node can have many attributes but only has 1 text node.
		- complex node: node which consists other node(s).
		- e.g. ![[Pasted image 20211230164741.png|350]]
		- We can see XML as tree: ![[Pasted image 20211230165454.png|500]]
		- Or we can see XML as paths: ![[Pasted image 20211230165619.png|300]]
- XML Schema:
	- Definition: XML Schema, which is a special kind of XML, describes **the legal format** of an XML document -> used to specify a "contract" (standard format) between systems. There are several XML Schemas.
	- A XML meets the specification of the Schema -> it is said to "validate"
	- The validation process: 
		- ![[Pasted image 20211231094436.png|600]]
	- Here, we focus on XML Schema from W3C (called XSD):
		- XSD structure: ![[Pasted image 20211231094730.png|500]]
		- We can have constraints and data types in XSD.
- [`xml.etree.ElementTree` library](https://docs.python.org/3/library/xml.etree.elementtree.html#module-xml.etree.ElementTree): Parsing XML in Python 
	- Import `xml.etree.ElementTree` library (as ET for the alias)
		- Syntax: ![[Pasted image 20211231095645.png|300]]
	- Parsing XML:
		- e.g. ![[Pasted image 20211231100317.png|300]]
#### JSON
- Definition: JSON stands for (JavaScript Object Notation). JSON can be considered as set of nested of objects, with different variable types, normally is dictionary.
- [`json` library](https://docs.python.org/3/library/json.html): Parsing JSON in Python
	- Import `json` library:
		- Syntax: ![[Pasted image 20211231102002.png|100]]
		- Parsing JSON:
			- e.g. ![[Pasted image 20211231102156.png|300]]
#### API #dig-deeper 
- Definition: API stands for Application Program Interface. API is a connection btw computers or btw computer programs (different from User Interface which connects btw a computer and a person). API is a type of software interface, offering a service to other pieces of software, and the controls of behavior of objects in that interface.
- Simple example of using API to retrieve info:
	- e.g. ![[Pasted image 20211231105438.png|500]]
	- JSON format file: ![[Pasted image 20211231105523.png|400]]
- API Security and Rate Limiting (e.g. retrieve times per day) -> Read the relevant documentation!! 
## Visualizing Data with Python
- A simple Multi-Step Data Analysis:
	- ![[Pasted image 20220101203058.png|600]]
- [ ] [Practical example from Dr. Chuck](https://www.freecodecamp.org/learn/scientific-computing-with-python/python-for-everybody/data-visualization-mailing-lists).
## Python Compiler
- Useful link: https://www.softwaretestinghelp.com/python-compiler/
- Translate Python code to other programming language: https://hackr.io/blog/best-python-compilers
### [[VS Code]]:
### VIM
- [ ] [VIM in 100 seconds (and VIM + VS Code)](https://www.youtube.com/watch?v=-txKSRn0qeA)
- [ ] [VIM kinda-complete tutorial](https://www.youtube.com/watch?v=IiwGbcd8S7I)
- [VIM channel](https://www.youtube.com/channel/UCUR1pFG_3XoZn3JNKjulqZg)