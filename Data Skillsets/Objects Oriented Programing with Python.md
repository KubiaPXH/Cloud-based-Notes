## Main ideas:
- Object Oriented approach: A program is, "not really" perceive as a linear process anymore, made up many cooperative objects, objects make use of each other's capabilities.
	- Main idea: Object approach break the problem to smaller understandable parts (So what is the differences with functions?). 
## OO components:
> **Class** is a template (e.g. Dog)
> **Method** (or message) is a defined capability (functionality) of a class (e.g. `bark()`, `sit(),`, `eat()`... ). Methods are functions which live in a class. 
> **Field** (or attribute) is a bit of data in a class (e.g. age, fur colors, length...)
> **State** is a set of values of attributes. Class state = set of values of class attributes, object state= set of values of object attributes.
> **Object** (or instance) is a particular instance of a class -> that inherit every fields and methods of the class. (e.g. Miumiu)
> **Inheritance** the ability to extend (and inherit) a existing class to make a new class. The new class (child or subclass) inherits all the attributes and capabilities of the class from which it inherits (parent), then add some more things. 
- A Class defines is an extensible program-code-template for creating objects, including the initial nature of the object's characteristics (its attributes or fields or properties) and the initial nature of the object's behaviors (the things it can do or methods, operations or features).
- An Object is a bit of *self*-contained program, with Code and Data, which is an instance of a class. Objects have boundaries -> ignore un-needed details.
	- Set of values of the attributes of a particular objects, which is can be changed, is called *state*.
	- The object consists of its *state* and its *behaviors* (defined in the object's class)
- A very simple example of defining a class and create an object:
	- ![[Pasted image 20220101101110.png|500]]
- Subclass (enabled by Inheritance) is a more specialized versions of a class, which inherits attributes and behaviors from their parent classes and also can introduce their own.
	- e.g. ![[Pasted image 20220101155325.png|600]]
### Attributes:
#### Class/Instance/Special Attributes:
- **Class attributes**: are attributes which are owned by the class itself -> shared (have the same value) by all the objects of the class.
	- Assign class attributes: we assign class attributes outside all the methods, usually just below the class header. 
- **Instance attributes**: are not shared by objects -> each object has it own version of the instance attributes.
	- Assign instance attributes: we assign instance attributes inside methods with the syntax: `self.<attribute_name> = <attribute_value>`. It is possible to assign instance attributes inside any method other than `__init__()` but the best practices is to initialize them in `__init__()` as the method with be automatically called when a new object is created.
- We can also assign new instance attributes (or overwrite a class attribute)  to an object outside the scope of a class. This action only affects the corresponding object but not other objects.
	- e.g. ![[Pasted image 20220106164310.png|400]]
	- In above example, only `item2` has `has_numpad` attribute but `item1` doesn't have it.
- A same attribute name can take both different values: first as class level attribute, when we call `<class>.<attribute_name>`, and second as object level attribute, when call `<object>.<attribute_name>`
	- e.g. ![[Pasted image 20220107101501.png|400]]
- **Special Attributes**:
	- `__dict__`: a dictionary which stored attributes and functions of class or objects.
		- `<class>.__dict__`: stored class variables and (over)written functions as class level.
		- `<object>.__dict__`: stored instance variables as object level.
	- `__class__`: is property allow to find the class of the calling object
		- `__class__.__name__`: show the name of the class of the calling object
- **Best practice**:
	- Should create a class attribute, inside the class, which acts as a collection (`list` or `dict`) of all the created objects of the class.
#### [`property()` and `@property` to manage attributes](https://realpython.com/python-property/#the-getter-and-setter-approach-in-python)
- `@property` decorator (to set "getter") and `@<attribute>.setter` decorator (to set "setter") can be use to control how we assign (using `=` operator) and print (using `print()` function) that attribute  ([more documentation](https://docs.python.org/3/library/functions.html#property))
	- After set "getter", the `print(<attribute>)` function will execute all the code `<statement>` inside the "getter" -> give more freedom to control `print(<attribute>)` function: 
		- The "getter": ![[Pasted image 20220107180401.png|200]] 
	- `@<attribute>.setter` can only be declared after declare `@property` decorator. 
	- After set "setter", the assign `<attribute> = value` function will execute all the code `<statement>` inside the "setter" -> give more freedom to control `<attribute> = value` function: 
		- The "setter": ![[Pasted image 20220107180610.png|200]]
- `@property` decorator (to set "getter") and `@<attribute>.setter` decorator, therefore, are used to set read-only, read-write and write-only attributes:
	- [Read-only attributes](https://realpython.com/python-property/#providing-read-only-attributes): we declare a read-only attribute when we only use `@property` decorator, which turn <attribute_name>() into a "getter", for a attribute but not `@<attribute>.setter` decorator, which set "setter", or set a "setter" just to raise error but not to assign value.
		- Syntax class attribute: with mandatory `return` statement to return value ![[Pasted image 20220107170730.png|250]]
		- Syntax object attribute: ![[Pasted image 20220107170653.png|250]]
		- For adding object read only attributes, it is better to use a private variable (with two underscore - e.g. `self.__name`) rather than a protected variable (with one underscore - e.g. `self_name`) because the attribute is still be changed when we assign value protected attributes outside the class which is not the case with private attribute. 
			- e.g. ![[Pasted image 20220107165956.png|500]]
	- [Read-write attributes](https://realpython.com/python-property/#creating-read-write-attributes): we declare a read-write attribute when we use both `@property` to set "getter" and `@<attribute>.setter` to set "setter" (not to raise error).
		- Syntax for setter decorator: with mandatory second parameter (e.g. value) to receive assigned value ![[Pasted image 20220107172954.png|250]]
	- [Write-only attributes](https://realpython.com/python-property/#providing-write-only-attributes): we use both `@property` to raise error and then `@<attribute>.setter` to set "setter".
		- Syntax: ![[Pasted image 20220107175934.png|300]]
### Methods:
- **Class method**: a method can be access in the class level only -> doesn't need class object to call.
	- Syntax: 
		- marked with `@classmethod` decorator before the method's header `def...`
		- have `(cls)` as compulsory parameter
	- A class method, called by an class, needs to **always** take that calling class itself as its first argument as it is surely the class that executes the method (or action) here:
		- This first parameter of an method is (cls): e.g. `def method1(cls):`
		- No argument is passed to (cls) parameter as we already declare the object before calling the method: e.g. `class1.method1()`>)
	- Class method only has access to class arguments via `cls.` -> can't modify object instance state.
- **Instance method**: a method need (is belong to) a class object (or instance) and can access the object via `self.`
	- Syntax: need to have `(self)` as compulsory parameter.
	- A instance method, called by an object, needs to **always** take that calling object itself as its first argument as it is surely the object that executes the method (or action) here:
		- This first parameter of an method is (self): e.g. `def method1(self):`
		- No argument is passed to (self) parameter as we already declare the object before calling the method: e.g. `object1.method1()`
	- [Magic methods](https://www.realpythonproject.com/python-magic-oop-dunder/) or dunder methods are default, built-in but editable methods of a built-in class in Python. Normally, magic methods are not meant to be invoked directly by us but it can be the case if we overwrite it.
		- Syntax: a dunder method's name is preceded and succeeded by double underscores (e.g. `__int__()`)
		- Common dunder methods:
			- `__int__()`: constructor method which automatically runs when initiating an new object.
			- `__repr__()`: return a official **unambiguous** representation of the object (have all info about object).
				- Implement `__repr__()` for any class you implement -> should be second nature.
				- [Best practice](https://docs.python.org/3/reference/datamodel.html#object.%5C_%5C_repr_): `__repr__` should look like a valid Python expression that could be used to recreate an object with the same value.
				- if `__repr__()` is defined and `__str__()` is not -> the object will behave as though `__str__` equal to `__repr__`
			- `__str__()`: return a informal **nicely-readable** description of an object (useful for printing the object).
				- `print(<object>)` will priority `__str__` over `__repr__` of both are defined and different.
- **Static method**: a method takes neither `cls` nor `self` parameter (but free to accept other parameters) and it can neither modify class state or object state.
	- Syntax: marked with `@statismethod` decorator before the method's header `def...`
	- Static methods are rarely used but [it can be useful when](https://www.programiz.com/python-programming/methods/built-in/staticmethod):
		1. we need a utility method that doesn't access any properties of a class but makes sense that it belongs to the class (e.g. conversion methods)
		2. we don't want subclasses of a class change/override a specific implementation of a method (e.g. in the link above)
### [Public/Protected/Private Members](https://medium.com/@manjuladube/encapsulation-abstraction-35999b0a3911) (Attributes or Methods):
- **Public members**: Public members are accessible (read and write) from both inside and even outside the class (outside of `class <class>:`). If we define Python members (attributes or methods) in the common way, they are public members by default.
- **Protected members**: Protected members (in C++ or Java) of a class are **only** accessible from within the class and are also available to its sub-classes. No other environment is allowed to access them. But in Python, as everything is public, "protected members" in Python is just a convention (*but not true restriction*).
	- Define "protected members" by prefix its name with a single underscore `_<member>`, we intend to tell others "don't touch this, unless your are class or subclass"
	- As protected members in Python is just a convention but not a rule, there `_<member>` can still be access outside of the class (we can couple `_<member>` with `@property` "getter" to make a read-only `<member>` but `_<member>` is still modifiable outside of class)
- **Private members**: In Python, "private members" give stronger suggestion than "protected members" that the members shouldn't be touched outside of the class.
	- Define "private members" by prefix its name with double underscores `__<member>`.
	- Any attempt to call the "private member" using `<object>.__<member>` outside the class will result in an AttributeError.
		-  e.g. ![[Pasted image 20220108155858.png|600]]
	-  However, again as there is no real "private" members in Python, we can still access the "private members" outside the class using [*name mangling*](https://www.netjstech.com/2019/04/name-mangling-in-python.html).
-  [Interesting discussion](https://stackoverflow.com/questions/7456807/python-name-mangling) about why and when to use public/protected/private members in Python.
	-  Python culture applies for naming is that "When in doubt, leave it "public"". While in C++/Java culture, "when in doubt, better go with private".
### Inheritance:
- **A child class** (subclass) is a class which inherits all the attributes and behaviors of its parent class (superclass) and can add some more attributes and behaviors which are particular for that child class.
	- Syntax: `class <child_class>(<parent_class>):`
- To enable the inherited attributes and methods we need to use the [`super()` method](https://realpython.com/python-super/):
	- Simple case: we add `super().__init__(<parent_para1>,<parent_para2>,...)` inside the `__init__()` method of the child class to inherit all attributes and methods from parent class. 
- **[Overriding in Inheritance](https://www.geeksforgeeks.org/method-overriding-in-python/):** when we want the child class provides a specific implementation of an inherited method (or specific value of an inherited attribute) from parent class, we **override** the method in the parent class by defining child class method with the same name, parameters or signature and return type as the inherited method. 
	- `<parent_object>.<method>`: call the parent class' method (or overriden method)
	- `<child_object>.<method>`: call the child class' method (or overriding method)
## OOP Principles:
- There are four principles of OOP are [**encapsulation**, **abstraction**, **inheritance**, **polymorphism**](https://www.freecodecamp.org/news/object-oriented-programming-concepts-21bb035f7260/) (good example from the link!)
- More: [SOLID principles in plain english](https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/)
### Encapsulation:
> **Encapsulation:** wrapping up data in a single unit -> to hide or restrict direct access to them by clients (clients can only see what they should see, but not more)
- Encapsulation is based on the idea that the state of object can not (or should not) be directly and freely access from outside of the entities (e.g. other objects) -> each object should keep its state **private**. 
- Outside entities, which want to access or modify the object's state, can only do that through explicitly allowed public methods of the object -> access to object's state need to be control by public methods defined in the object's class.
### Abstraction:
> **Abstraction:** hiding the internal implementation details (how it **really** works) in a function or a object, therefore clients, or other objects, only need to know and expose to the high level of mechanism (how they should work with it) which is enough to allow them to preform their tasks.
- Abstraction helps avoid the unnecessary complexity for clients as the high level mechanism normally easy to use and rarely change overtime -> perform tasks more effectively.
### Inheritance:
> **Inheritance:** the ability to extend (and inherit) a existing thing (class) to make a new thing (or class). The new class (child or subclass) inherits all the attributes and capabilities of the class from which it inherits (parent), then add some more things. 
- Inheritance is super useful for code reuse and drawing inheritance tree for mapping related concepts.
### Polymorphism (many shapes):
> Polymorphism: is when we use a single interface (object or method) to exhibit different behavior or represent different types in different situation. 
## Object Life Cycle:
- Objects are created, used and discarded.
- Create an object by using constructor (a special blocks of code) and destroy an object by calling destructor. Normally, constructor and destructor are optional and called automatically by Python.
	- constructor: is typically used to set up variables.
		- constructor name: `__int__(self)` 
			- e.g. ![[Pasted image 20220101104039.png|250]]
	- destructor: is rarely used.
		- destructor name: `__del__(self)`
			- e.g. ![[Pasted image 20220101104920.png|250]]
	- e.g.1. ![[Pasted image 20220101105140.png|600]]
	- e.g.2. Using constructor to assign variable ![[Pasted image 20220101105533.png|400]]