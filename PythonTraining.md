*Date : 7th June 2022*
# About Python 
Python is an interpreted, Object Oriented, High Level programming language with dynamic semantics. 

## Features 
    * High-level built in Data Structures 
    * Dynamic Typing 
    * Easy to learn Syntax 
    * Easy Debugging 

## Installation (Windows)

### Download and install Latest Version from https://www.python.org/downloads/


## Python OOP Concepts

Object-Oriented Programming (OOP) in Python is a programming paradigm based on the concept of "objects", which can contain data in the form of fields (often known as attributes or properties) and code in the form of procedures (often known as methods). It aims to implement real-world entities like inheritance, polymorphism, encapsulation, etc., in programming. The core principle of OOP is to bind data and the functions that operate on that data together as a single unit, restricting access to this data from other parts of the code.

### Main Concepts of Object-Oriented Programming (OOP)
    * Class 
    * Objects
    * Polymorphism
    * Encapsulation
    * Inheritance

#### Class
A Class is a collection of objects. A Class contains the blue print or prototype from which the objects are being created.
It is a logical entity that contains some attributes and methods.

##### Class Definition Syntax:

```python
class className:
    # statement 1
    # .
    # .
    # .
    # statement N
```
##### Example Creating an Empty Class
```python
class Dog:
    pass
```

#### Objects
An Object is an entity that has a state and behaviour associated with it.
##### An object consist of :
* State
  * It is represented by the attributes of an object. It also reflects the properties of an object
* Behaviour
  * It is represented by the methods of an object.
  * It also reflects the response of an object to other objects.
* Identity
  * It gives unique name to an object and enables one object to interact with other objects.
##### Example Creating an Object :
```python
obj = Dog()
```

##### The `self` Parameter:
* In Python, instance methods (methods belonging to an object) must have `self` as their first parameter in the method definition.
* When you call an instance method like `my_object.method(arg1, arg2)`, Python automatically passes the object `my_object` as the first argument to `self`. So, the call effectively becomes `ClassName.method(my_object, arg1, arg2)`.
* You do not explicitly pass a value for `self` when calling the method.
* Even if a method takes no other arguments, it must still include `self` as its first parameter. For example: `def my_method(self):`.

This `self` parameter provides a reference to the instance of the class, allowing you to access its attributes and other methods from within the instance method.

##### The `__init__` method :

The `__init__` method is similar to constructors. It runs as soon as an object if a class iss instantiated. The method is useful to do any initialization we want.

###### Example : Creating a class and its object.
```python
class Dog:
  
    # class attribute
    attr1 = "mammal"
  
    # Instance attribute
    def __init__(self, name):
        self.name = name
  
# Driver code
# Object instantiation
Rodger = Dog("Rodger")
Tommy = Dog("Tommy")
  
# Accessing class attributes
print("Rodger is a {}".format(Rodger.__class__.attr1))
print("Tommy is also a {}".format(Tommy.__class__.attr1))
  
# Accessing instance attributes
print("My name is {}".format(Rodger.name))
print("My name is {}".format(Tommy.name))

```
###### Output
```
Rodger is a mammal
Tommy is also a mammal
My name is Rodger
My name is Tommy
```

###### Example 2: Creating Class and objects with methods
```python
class Dog:

	# class attribute
	attr1 = "mammal"

	# Instance attribute
	def __init__(self, name):
		self.name = name
		
	def speak(self):
		print("My name is {}".format(self.name))

# Driver code
# Object instantiation
Rodger = Dog("Rodger")
Tommy = Dog("Tommy")

# Accessing class methods
Rodger.speak()
Tommy.speak()
```
###### Output
```
My name is Rodger
My name is Tommy
```
#### Inheritance
Inheritance is a fundamental concept in OOP where a class (known as a child or derived class) acquires the properties and behaviors (methods) of another class (known as a parent or base class).

##### Benefits of Inheritance
*   **Code Reusability:** Inheritance allows child classes to reuse code from parent classes, reducing redundancy and making code easier to maintain.
*   **Real-world Modeling:** It effectively models real-world "is-a" relationships (e.g., a `Car` is a `Vehicle`).
*   **Extensibility:** New features can be added to a child class without modifying the parent class.
*   **Transitivity:** If class `B` inherits from class `A`, and class `C` inherits from class `B`, then class `C` also inherits from class `A`. This allows for creating a hierarchy of classes.

##### Example: Inheritance in Python
```python
# Python code to demonstrate how parent constructors
# are called.

# parent class
class Person(object):

	# __init__ is known as the constructor
	def __init__(self, name, idnumber):
		self.name = name
		self.idnumber = idnumber

	def display(self):
		print(self.name)
		print(self.idnumber)
		
	def details(self):
		print("My name is {}".format(self.name))
		print("IdNumber: {}".format(self.idnumber))
	
# child class
class Employee(Person):
	def __init__(self, name, idnumber, salary, post):
		self.salary = salary
		self.post = post

		# invoking the __init__ of the parent class
		Person.__init__(self, name, idnumber)
		
	def details(self):
		print("My name is {}".format(self.name))
		print("IdNumber: {}".format(self.idnumber))
		print("Post: {}".format(self.post))


# creation of an object variable or an instance
a = Employee('Rahul', 886012, 200000, "Intern")

# calling a function of the class Person using
# its instance
a.display()
a.details()

``` 
##### Output 

```
Rahul
886012
My name is Rahul
IdNumber: 886012
Post: Intern
```
##### Types of Inheritance
* Single Inheritance :- Derived class inherits charecteristics from single parent class.
* Multilevel Inheritance :- child inherits properties from a parent class and the parent itself inherits properties from its parent class
* Hierarichical Inheritance :- Multiple derived classes inherits properties from a parent class.
* Multiple Inheritance :- One derived class inherits properties from more than one base(parent) class.
  
#### Polymorphism.
Polymorphism simply means, behave according to the situation. For example we need to determine if the given species of bird, fly or not. We can do this using a single function.

```python
class Bird:

	def intro(self):
		print("There are many types of birds.")

	def flight(self):
		print("Most of the birds can fly but some cannot.")

class sparrow(Bird):

	def flight(self):
		print("Sparrows can fly.")

class ostrich(Bird):

	def flight(self):
		print("Ostriches cannot fly.")

obj_bird = Bird()
obj_spr = sparrow()
obj_ost = ostrich()

obj_bird.intro()
obj_bird.flight()

obj_spr.intro()
obj_spr.flight()

obj_ost.intro()
obj_ost.flight()
```
##### Output

```
There are many types of birds.
Most of the birds can fly but some cannot.
There are many types of birds.
Sparrows can fly.
There are many types of birds.
Ostriches cannot fly.
```
Date : 22 July 2022
-------------------
-------------------

#### Encapsulation
Wrapping data and methods that work on data within one unit.This puts restrictions on accessing variables and methods directly and can prevent the accidental modification of data.

##### Protected Members
* Members of class which cannot be accessed outside the class.
* It can be accessed by members of the class or its subclass
* Single underscore `_` prefix is used by convention to indicate that a member (attribute or method) is "protected".

**Note on Protected Members:**
Protected members are intended for internal use by the class and its subclasses. While Python does not strictly enforce access control for protected members (they can still be accessed from outside the class), the underscore prefix serves as a strong convention signaling that these members should not be accessed directly from outside the class or by unrelated classes. It's a way to indicate that the member is part of the internal implementation and might change without notice.

```python
# Python program to
# demonstrate protected members

# Creating a base class
class Base:
	def __init__(self):

		# Protected member
		self._a = 2

# Creating a derived class
class Derived(Base):
	def __init__(self):

		# Calling constructor of
		# Base class
		Base.__init__(self)
		print("Calling protected member of base class: ",
			self._a)

		# Modify the protected variable:
		self._a = 3
		print("Calling modified protected member outside class: ",
			self._a)


obj1 = Derived()

obj2 = Base()

# Calling protected member
# Can be accessed but should not be done due to convention
print("Accessing protected member of obj1: ", obj1._a)

# Accessing the protected variable outside
print("Accessing protected member of obj2: ", obj2._a)

```
Output
```
Calling protected member of base class:  2
Calling modified protected member outside class:  3
Accessing protected member of obj1:  3
Accessing protected member of obj2:  2
```
##### Private Members
* Cannot be accessed outside the class/ or from its base class
* __ is used to define a private variable/member
* Note: Python’s private and protected members can be accessed outside the class through python name mangling. 

```python
# Python program to
# demonstrate private members

# Creating a Base class


class Base:
	def __init__(self):
		self.a = "GeeksforGeeks"
		self.__c = "GeeksforGeeks"

# Creating a derived class
class Derived(Base):
	def __init__(self):

		# Calling constructor of
		# Base class
		Base.__init__(self)
		print("Calling private member of base class: ")
		print(self.__c)


# Driver code
obj1 = Base()
print(obj1.a)

# Uncommenting print(obj1.c) will
# raise an AttributeError

# Uncommenting obj2 = Derived() will
# also raise an AtrributeError as
# private member of base class
# is called inside derived class
```

Output
```
GeeksforGeeks
```

```
Traceback (most recent call last):
  File "/home/f4905b43bfcf29567e360c709d3c52bd.py", line 25, in <module>
    print(obj1.c)
AttributeError: 'Base' object has no attribute 'c'

Traceback (most recent call last):
  File "/home/4d97a4efe3ea68e55f48f1e7c7ed39cf.py", line 27, in <module>
    obj2 = Derived()
  File "/home/4d97a4efe3ea68e55f48f1e7c7ed39cf.py", line 20, in __init__
    print(self.__c)
AttributeError: 'Derived' object has no attribute '_Derived__c' 

```
#### Data Abstraction
* Hides unnecessary code details from the user.
* Data abstraction can be achieved by using a abstract class.
##### Data Hiding
* In Python, we use double underscore (Or __) before the attributes name and those attributes will not be directly visible outside. 
```python
class MyClass:

	# Hidden member of MyClass
	__hiddenVariable = 0
	
	# A member method that changes
	# __hiddenVariable
	def add(self, increment):
		self.__hiddenVariable += increment
		print (self.__hiddenVariable)

# Driver code
myObject = MyClass()	
myObject.add(2)
myObject.add(5)

# This line causes error
print (myObject.__hiddenVariable)
```
Output
```
2
7
Traceback (most recent call last):
  File "filename.py", line 13, in 
    print (myObject.__hiddenVariable)
AttributeError: MyClass instance has 
no attribute '__hiddenVariable'
```
In the above program, we tried to access a hidden variable outside the class using an object and it threw an exception.

We can access the value of a hidden attribute by a tricky syntax: 
```python
# A Python program to demonstrate that hidden
# members can be accessed outside a class
class MyClass:

	# Hidden member of MyClass
	__hiddenVariable = 10

# Driver code
myObject = MyClass()	
print(myObject._MyClass__hiddenVariable)
```

Output
```
10
```
##### Printing Objects
Printing objects give us information about objects we are working with.
In python __repr__ or __str__ method is used to display information about the object.
We can define these methods inside the class and add contents about the object.

```python
class Test:
	def __init__(self, a, b):
		self.a = a
		self.b = b

	def __repr__(self):
		return "Test a:%s b:%s" % (self.a, self.b)

	def __str__(self):
		return "From str method of Test: a is %s," \
			"b is %s" % (self.a, self.b)

# Driver Code		
t = Test(1234, 5678)
print(t) # This calls __str__()
print([t]) # This calls __repr__()
```
Output
```
From str method of Test: a is 1234,b is 5678
[Test a:1234 b:5678]
```
Note: If no __str__ method is defined, it will use __repr__ method. If no __repr__ method is defined, then default is used(print object)

```python
class Test:
	def __init__(self, a, b):
		self.a = a
		self.b = b

# Driver Code		
t = Test(1234, 5678)
print(t)

```
Output
```
<__main__.Test instance at 0x7fa079da6710> 

```

Date : 25th July 2022

------------------------
## REPL
* REPL stands for READ EVALUATE PRINT LOOP
* It is an interactive Micro Python Prompt
* Features
  * Input history: use arrow up and arrow down to scroll through the history
  * Tab completion: press tab to auto-complete variables or module names
  * Halt any executing code: with Ctrl-C
  * Copy/paste code or output: Ctrl-C and Ctrl-V

## PyCharm 
PyCharm is a dedicated Python Integrated Development Environment (IDE) providing a wide range of essential tools for Python developers, tightly integrated to create a convenient environment for productive Python, web, and data science development.

Download Link : https://www.jetbrains.com/pycharm/download/#section=windows

## Python Operators

### Overview :
Python divides the operators in the following groups:
* Arithmetic operators
* Assignment operators
* Comparison operators
* Logical operators
* Identity operators
* Membership operators
* Bitwise operators

### Arithmetic Operators

Arithmetic operators are used with numeric values to perform common mathematical operations:

`+` Addition, Eg : `x + y`

`-` Substraction, Eg: `x - y`

`*` Multiplication, Eg : `x * y`

`/` Division, Eg : `x / y` 

`%` Modulus, Eg : `x % y`

`**` Exponentiation, Eg : `x ** y`

`//` Floor Division, Eg : ` x // y`

### Assignment Operators 


Assignment Operators are used to assign values to variables

Operator|Example|Same As
--------|-------|-------
=	|x = 5	|x = 5	
+=	|x += 3	|x = x + 3	
-=	|x -= 3	|x = x - 3	
*=	|x *= 3	|x = x * 3	
/=	|x /= 3	|x = x / 3	
%=	|x %= 3	|x = x % 3	
//=	|x //= 3|x = x // 3	
**=	|x **= 3|x = x ** 3	
&=	|x &= 3	|x = x & 3	
|=	|x |= 3	|x = x | 3	
^=	|x ^= 3	|x = x ^ 3	
\>>=	|x >>= 3	|x = x >> 3	
<<=	|x <<= 3	|x = x << 3

### Comparison Operators
Comparison operators are used to compare two values:

Operator|Name|Example
--------|-------|-----
== | Equal |x==y
!= | Not Equal | x!=y
\> | Greater than | x > y
< | Less than | x < y
\>= | Greater than or equal to | x >=y
<= | Less than or equal to | x <= y

### Python Logical Operators

Logical operators are used to combine conditional statements:

| Operator | Description | Example|
|----------|-------------|--------|
| and | Returns true if both statements are true | `x < 5 and x < 10`|
| or | Returns true if any one of the satements are true| `x = 5 or x < 10`|  
| not | Reverse the result, Return false if the result is true | `not (x < 5 and x < 10)`|

### Identity Operators

Identity operators are used to compare the objects, not if they are equal, but if they are actually the same object, with the same memory location

| Operator | Description | Example|
|----------|-------------|---------|
| is | Returns true if both variables are same object | `x is y`|
| is not | Returns true if both variables are different object | ` x is not y`|

### Membership Operators
| Operator | Description | Example|
|----------|-------------|---------|
| in | returns true, if a sequence with a specific value present in the object| x in y|
| not in | returns true, if if a sequence with a specific value not present in the object|

### Bitwise Operators

Bitwise operators are used to compare Binary Numbers:

Operator|Name|Description
--------|-------|-----|
& | AND |	Sets each bit to 1 if both bits are 1
| \| | OR |Sets each bit to 1 if one of two bits is 1
| ^	| XOR |Sets each bit to 1 if only one of two bits is 1
| ~ 	|NOT| Inverts all the bits
| << | Zero fill left shift	| Shift left by pushing zeros in from the right and let the leftmost bits fall off
|\>> | Signed right shift | Shift right by pushing copies of the leftmost bit in from the left, and let the rightmost bits fall off

Date : 26 July 2022

--------------------

## Variables 

* Variables are containers for storing data values.
* A variable is created the moment you first assign a value to it.
* A Python Variables is only a name given to a memory location, all the operations done on the variable effects that memory location.

### Rules for creating a variable
* A variable name must start with a letter or underscore character 
* A variable name cannot start with number
* A variable name can only contain alpha-numeric characters and underscores
* Variable names are Case Sensitive(name, Name and NAME are three different variables)
* Reserved keywords cannot be used to name a variable 


Example 
```python
x = 5
y = "John"
print(x)
print(y)
```
Output
```
5
John
```

### Assigning single value to multiple variables 

Python allows assigning a single value to several variables, Simultaniously with "=" operator

```python
a = b = c = 10

print(a)
print(b)
print(c)

```
Output:
```
10
10
10
```
### Assigning Different values to multiple variables
Python allows adding different values in a single line with “,”operators.

```python
a, b, c = 1, 20.2, "GeeksforGeeks"

print(a)
print(b)
print(c)
```
Output:
```
1
20.2
GeeksforGeeks
```
### Casting
If you want to specify the data type of a variable, this can be done with casting.
```python
x = str(3)    # x will be '3'
y = int(3)    # y will be 3
z = float(3)  # z will be 3.0
```
### Get the type
You can get the data type of a variable with the type() function.
```python
x = 5
y = "John"
print(type(x))
print(type(y))
```
Output
```
<class 'int'>
<class 'str'>
```
### Single or Double Quote?
String Variable can be defined by using either single quote or double quote

```python
x = "John"
# is the same as
x = 'John
```

### Global and Local Python Variables

* Local Variables are the ones that are defined and declared inside the function, We cannot call this variable outside the function.

```python
# This function uses global variable s
def f():
	s = "Welcome geeks"
	print(s)
f()
```
* Global Variables are the ones that are defined and declared outside a function
  
```python
# This function has a variable with
# name same as s.
def f():
	print(s)


# Global scope
s = "I love Geeksforgeeks"
f()
```
Output
```
I love Geeksforgeeks
```

### Global Keyword in python

Global keyword is a keyword that allows a user to modify a variable outside of the current scope. It is used to create global variables from a non-global scope i.e inside a function. Global keyword is used inside a function only when we want to do assignments or when we want to change a variable. Global is not needed for printing and accessing.

#### Rules of Global Keyword
* If a variable is assigned a value anywhere within the function’s body, it’s assumed to be a local unless explicitly declared as global.
* Variables that are only referenced inside a function are implicitly global.
* We Use global keyword to use a global variable inside a function.
* There is no need to use global keyword outside a function.

```python
# Python program to modify a global
# value inside a function

x = 15
def change():

	# using a global keyword
	global x

	# increment value of a by 5
	x = x + 5
	print("Value of x inside a function :", x)


change()
print("Value of x outside a function :", x)

```
Output:
```
Value of x inside a function : 20
Value of x outside a function : 20
```

### Variable type in Python
Data types are the classification or categorization of data items. It represents the kind of value that tells what operations can be performed on a particular data. Since everything is an object in Python programming, data types are actually classes and variables are instance (object) of these classes.

Following are the standard or built-in data type of Python:

* Numeric
* Sequence Type
* Boolean
* Set
* Dictionary

```python
# numberic
var = 123
print("Numbric data : ", var)

# Sequence Type
String1 = 'Welcome to the Geeks World'
print("String with the use of Single Quotes: ")
print(String1)

# Boolean
print(type(True))
print(type(False))

# Creating a Set with
# the use of a String
set1 = set("GeeksForGeeks")
print("\nSet with the use of String: ")
print(set1)

# Creating a Dictionary
# with Integer Keys
Dict = {1: 'Geeks', 2: 'For', 3: 'Geeks'}
print("\nDictionary with the use of Integer Keys: ")
print(Dict)

```

Output
```
Numbric data :  123
String with the use of Single Quotes: 
Welcome to the Geeks World
<class 'bool'>
<class 'bool'>

Set with the use of String: 
{'r', 'G', 'e', 'k', 'o', 's', 'F'}

Dictionary with the use of Integer Keys: 
{1: 'Geeks', 2: 'For', 3: 'Geeks'}
```
### Object References

```
x = 5
x=y
```
When Python looks at the first statement, what it does is that, first, it creates an object to represent the value 5. Then, it creates the variable x if it doesn’t exist and made it a reference to this new object 5. The second line causes Python to create the variable y, and it is not assigned with x, rather it is made to reference that object that x does. The net effect is that the variables x and y wind up referencing the same object. This situation, with multiple names referencing the same object, is called a *_Shared Reference_* in Python.

### Creating objects (or variables of a class type)

```python
# Python program to show that the variables with a value
# assigned in class declaration, are class variables and
# variables inside methods and constructors are instance
# variables.

# Class for Computer Science Student
class CSStudent:

	# Class Variable
	stream = 'cse'		

	# The init method or constructor
	def __init__(self, roll):
	
		# Instance Variable
		self.roll = roll	

# Objects of CSStudent class
a = CSStudent(101)
b = CSStudent(102)

print(a.stream) # prints "cse"
print(b.stream) # prints "cse"
print(a.roll) # prints 101

# Class variables can be accessed using class
# name also
print(CSStudent.stream) # prints "cse"

```
Output:
```
cse
cse
101
cse
```

## Types of Inheritance in Python
Inheritance is defined as the mechanism of inheriting the properties of the base class to the child class. Python supports several types of inheritance:

*   **Single Inheritance:** A derived class inherits from a single parent class.
*   **Multiple Inheritance:** A derived class inherits from more than one parent class.
*   **Multilevel Inheritance:** A derived class inherits from a parent class, which in turn inherits from another parent class (e.g., `A -> B -> C`).
*   **Hierarchical Inheritance:** Multiple derived classes inherit from a single parent class (e.g., `B -> A`, `C -> A`).
*   **Hybrid Inheritance:** A combination of two or more types of inheritance.

#### Single Inheritance
Single inheritance enables a derived class to inherit properties and methods from a single parent class, promoting code reusability and allowing for the extension of existing code.

```python
# Python program to demonstrate single inheritance

# Base Class
class Parent:
    def func1(self):
        print("This function is in the Parent class.") # Added clarity to the print statement
	
# Derived Class 
class Child(Parent): # Child class inherits from Parent class
    def func2(self):
        print("This function is in the Child class.") # Added clarity to the print statement

# Driver's code
obj = Child() # Create an object of the Child class
obj.func1()   # Call func1 from the Parent class (inherited by Child)
obj.func2()   # Call func2 from the Child class
```

Output:

```
This function is in the Parent class.
This function is in the Child class.
```

#### Multiple Inheritance
When a class is derived from more than one base class, it's called multiple inheritance. The derived class inherits all the features (attributes and methods) of all its parent classes.

```python
# Python program to demonstrate multiple inheritance

# Base class 1
class Mother:
    mothername = "" # Class attribute for mother's name

    def mother_info(self): # Renamed for clarity
        print(f"Mother's name: {self.mothername}")

# Base class 2
class Father:
    fathername = "" # Class attribute for father's name

    def father_info(self): # Renamed for clarity
        print(f"Father's name: {self.fathername}")

# Derived class inheriting from Mother and Father
class Son(Mother, Father):
    def display_parents_info(self): # Renamed for clarity
        # Accessing attributes and methods from both parent classes
        print(f"Father: {self.fathername}")
        print(f"Mother: {self.mothername}")
        # You can also call parent methods directly if needed:
        # self.father_info()
        # self.mother_info()

# Driver's code
s1 = Son()
s1.fathername = "RAM"   # Set father's name
s1.mothername = "SITA"  # Set mother's name
s1.display_parents_info() # Call method of Son class
```

Output:
```
Father: RAM
Mother: SITA
```

#### Multilevel Inheritance
In multilevel inheritance, a derived class inherits from a base class, which in turn inherits from another base class. This creates a "chain" of inheritance.

```python
# Python program to demonstrate multilevel inheritance

# Base class (Grandparent)
class Grandfather:
    def __init__(self, grandfathername):
        self.grandfathername = grandfathername

# Intermediate class (Parent, inherits from Grandfather)
class Father(Grandfather):
    def __init__(self, fathername, grandfathername):
        self.fathername = fathername
        # Invoking constructor of Grandfather class
        Grandfather.__init__(self, grandfathername)

# Derived class (Child, inherits from Father)
class Son(Father):
    def __init__(self, sonname, fathername, grandfathername):
        self.sonname = sonname
        # Invoking constructor of Father class
        Father.__init__(self, fathername, grandfathername)

    def print_family_names(self): # Renamed for clarity
        print(f'Grandfather name: {self.grandfathername}')
        print(f"Father name: {self.fathername}")
        print(f"Son name: {self.sonname}")

# Driver code
s1 = Son('Prince', 'Rampal', 'Lal mani')
print(f"Accessing grandfather's name directly: {s1.grandfathername}") # Accessing attribute from Grandfather class
s1.print_family_names() # Calling method of Son class
```

Output:
```
Accessing grandfather's name directly: Lal mani
Grandfather name: Lal mani
Father name: Rampal
Son name: Prince
```

#### Hierarchical Inheritance
When more than one derived class inherits from a single base class, it's called hierarchical inheritance. This allows multiple specialized classes to share common functionality from a single parent.

```python
# Python program to demonstrate Hierarchical inheritance

# Base class
class Parent:
    def common_function(self): # Renamed for clarity
        print("This function is in the Parent class.")

# Derived class 1 (inherits from Parent)
class Child1(Parent):
    def child1_function(self): # Renamed for clarity
        print("This function is in Child 1.")

# Derived class 2 (inherits from Parent)
class Child2(Parent):
    def child2_function(self): # Renamed for clarity
        print("This function is in Child 2.")

# Driver's code
object1 = Child1()
object2 = Child2()

object1.common_function() # Calling method from Parent class via Child1 object
object1.child1_function() # Calling method from Child1 class

object2.common_function() # Calling method from Parent class via Child2 object
object2.child2_function() # Calling method from Child2 class
```

Output:

```
This function is in the Parent class.
This function is in Child 1.
This function is in the Parent class.
This function is in Child 2.
```

#### Hybrid Inheritance
Hybrid inheritance is a combination of two or more types of inheritance. For example, it might involve a mix of multilevel and multiple inheritance.

```python
# Python program to demonstrate hybrid inheritance

class SchoolFaculty: # A base class
    def faculty_info(self):
        print("This function is in SchoolFaculty.")

class Student(SchoolFaculty): # Derived from SchoolFaculty (Single Inheritance)
    def student_info(self):
        print("This function is in Student.")

class Teacher(SchoolFaculty): # Also derived from SchoolFaculty (Hierarchical with Student)
    def teacher_info(self):
        print("This function is in Teacher.")

# TeachingAssistant inherits from Student and Teacher (Multiple Inheritance)
# This creates a hybrid inheritance structure (specifically a "diamond" shape if Student and Teacher
# were to inherit from a common grandparent of SchoolFaculty, but here it's simpler).
class TeachingAssistant(Student, Teacher):
    def ta_info(self):
        print("This function is in TeachingAssistant.")

# Driver's code
ta_object = TeachingAssistant()
ta_object.faculty_info()    # From SchoolFaculty (via Student or Teacher due to MRO)
ta_object.student_info()    # From Student
ta_object.teacher_info()    # From Teacher
ta_object.ta_info()         # From TeachingAssistant

# Example of MRO (Method Resolution Order)
# print(TeachingAssistant.mro())
```

Output:
```
This function is in SchoolFaculty.
This function is in Student.
This function is in Teacher.
This function is in TeachingAssistant.
```

Date : 27 July 2022

-------------------

## Detailed Control Flow

Control flow statements are fundamental to programming, allowing you to dictate the order in which code is executed. Python offers several clear and powerful control flow mechanisms.

### `for` Loops

`for` loops are used for iterating over a sequence (that is either a list, a tuple, a dictionary, a set, or a string) or other iterable objects.

#### Iterating with `range()`
The `range()` function generates a sequence of numbers, which is often used for looping a specific number of times.

```python
# Example: Iterating a specific number of times
print("--- Iterating with range() ---")
for i in range(5):  # Generates numbers from 0 to 4
    print(f"Current number: {i}")

# Example: range() with start, stop, and step
print("\n--- range() with start, stop, step ---")
for i in range(2, 10, 2):  # Generates numbers from 2 up to (but not including) 10, with a step of 2
    print(f"Even number: {i}")
```
Output:
```
--- Iterating with range() ---
Current number: 0
Current number: 1
Current number: 2
Current number: 3
Current number: 4

--- range() with start, stop, step ---
Even number: 2
Even number: 4
Even number: 6
Even number: 8
```

#### Iterating over Lists
You can directly iterate over the elements of a list.

```python
# Example: Iterating over a list
print("\n--- Iterating over a list ---")
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(f"Current fruit: {fruit}")

# Example: Iterating over a list with index using enumerate()
print("\n--- Iterating over a list with index ---")
for index, fruit in enumerate(fruits):
    print(f"Fruit at index {index}: {fruit}")
```
Output:
```
--- Iterating over a list ---
Current fruit: apple
Current fruit: banana
Current fruit: cherry

--- Iterating over a list with index ---
Fruit at index 0: apple
Fruit at index 1: banana
Fruit at index 2: cherry
```

#### Iterating over Strings
Strings are sequences of characters, and you can iterate over them.

```python
# Example: Iterating over a string
print("\n--- Iterating over a string ---")
word = "Python"
for char in word:
    print(f"Character: {char}")
```
Output:
```
--- Iterating over a string ---
Character: P
Character: y
Character: t
Character: h
Character: o
Character: n
```

#### Iterating over Dictionaries
When iterating over dictionaries, you can loop through keys, values, or key-value pairs.

```python
# Example: Iterating over dictionary keys (default behavior)
print("\n--- Iterating over dictionary keys ---")
my_dict = {"name": "Alice", "age": 30, "city": "New York"}
for key in my_dict:
    print(f"Key: {key}, Value: {my_dict[key]}")

# Example: Iterating over dictionary values
print("\n--- Iterating over dictionary values ---")
for value in my_dict.values():
    print(f"Value: {value}")

# Example: Iterating over dictionary key-value pairs
print("\n--- Iterating over dictionary key-value pairs ---")
for key, value in my_dict.items():
    print(f"Key: {key}, Value: {value}")
```
Output:
```
--- Iterating over dictionary keys ---
Key: name, Value: Alice
Key: age, Value: 30
Key: city, Value: New York

--- Iterating over dictionary values ---
Value: Alice
Value: 30
Value: New York

--- Iterating over dictionary key-value pairs ---
Key: name, Value: Alice
Key: age, Value: 30
Key: city, Value: New York
```

### `while` Loops

`while` loops are used to execute a block of statements as long as a given condition is true.

#### Basic Structure
The loop continues until the condition evaluates to `False`.

```python
# Example: Basic while loop
print("\n--- Basic while loop ---")
count = 0
while count < 5:  # Condition: count is less than 5
    print(f"Count is: {count}")
    count += 1  # Increment count, crucial to avoid an infinite loop
print("Loop finished.")
```
Output:
```
--- Basic while loop ---
Count is: 0
Count is: 1
Count is: 2
Count is: 3
Count is: 4
Loop finished.
```

#### Counter-Controlled Loops
`while` loops are often used when the number of iterations isn't known beforehand, but they can also be used for counter-controlled iterations, similar to `for` loops with `range()`.

```python
# Example: Counter-controlled while loop
print("\n--- Counter-controlled while loop ---")
i = 0
limit = 3
while i < limit:
    print(f"Iteration number {i+1}")
    i += 1
print("Counter-controlled loop finished.")
```
Output:
```
--- Counter-controlled while loop ---
Iteration number 1
Iteration number 2
Iteration number 3
Counter-controlled loop finished.
```
**Important:** When using `while` loops, ensure that the condition will eventually become false; otherwise, you'll create an infinite loop.

### `break` and `continue` Statements

`break` and `continue` are statements that alter the flow of a loop.

*   **`break`:** Terminates the current loop prematurely and transfers control to the statement immediately following the loop.
*   **`continue`:** Skips the rest of the code inside the current iteration of the loop and proceeds to the next iteration.

#### Combined Practical Example

```python
# Example: Using break and continue
print("\n--- break and continue example ---")
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for num in numbers:
    if num % 2 != 0:
        # If the number is odd, skip to the next iteration
        print(f"Skipping odd number: {num}")
        continue

    if num > 6:
        # If the number is greater than 6, terminate the loop
        print(f"Number {num} is greater than 6. Breaking loop.")
        break

    # This will only be executed for even numbers <= 6
    print(f"Processing even number: {num}")

print("Loop finished after break/continue.")
```
Output:
```
--- break and continue example ---
Skipping odd number: 1
Processing even number: 2
Skipping odd number: 3
Processing even number: 4
Skipping odd number: 5
Processing even number: 6
Skipping odd number: 7
Number 8 is greater than 6. Breaking loop.
Loop finished after break/continue.
```

### `if-elif-else` Chains (The `elif` Statement)

While `if` and `else` provide basic conditional logic, `elif` (short for "else if") allows you to check multiple expressions for `True` and execute a block of code as soon as one of the conditions is met.

#### Structure and Usage

```python
# Example: if-elif-else chain
print("\n--- if-elif-else chain example ---")
score = 75

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print(f"The score is {score}, which corresponds to a grade of {grade}.")

# Another example
name = "Alice"
if name == "Bob":
    print("Hello Bob!")
elif name == "Alice":
    print("Hello Alice!") # This block will be executed
else:
    print("Hello stranger!")
```
Output:
```
--- if-elif-else chain example ---
The score is 75, which corresponds to a grade of C.
Hello Alice!
```
Only one block in the `if-elif-else` chain will be executed – the one corresponding to the first true condition, or the `else` block if no conditions are true.

## List Comprehensions

List comprehensions provide a concise and readable way to create lists. They are often more efficient and easier to understand than using explicit `for` loops to populate a list.

**Definition and Syntax:**

A list comprehension consists of brackets containing an expression followed by a `for` clause, then zero or more `for` or `if` clauses. The general syntax is:

```
[expression for item in iterable if condition]
```

*   `expression`: The expression to compute for each item.
*   `item`: The variable representing each element in the `iterable`.
*   `iterable`: The sequence or collection to iterate over (e.g., a list, range, string).
*   `condition` (optional): A filter that only includes items for which the condition is true.

**Benefits:**

*   **Conciseness:** They are often shorter than equivalent `for` loop constructs.
*   **Readability:** When used appropriately, they can make code easier to read by clearly stating the intent of the list creation.
*   **Efficiency:** In many cases, list comprehensions can be faster than appending to a list in a `for` loop due to internal optimizations in Python.

**Examples:**

#### 1. Generating a List of Squares

Let's create a list of the first 10 perfect squares.

```python
# Using a for loop
squares_loop = []
for x in range(1, 11):  # Numbers from 1 to 10
    squares_loop.append(x * x)
print(f"Squares (using for loop): {squares_loop}")

# Using a list comprehension
squares_comp = [x * x for x in range(1, 11)]
print(f"Squares (using list comprehension): {squares_comp}")
```
Output:
```
Squares (using for loop): [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
Squares (using list comprehension): [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
The list comprehension version is more compact and directly expresses the transformation of each `x` into `x*x`.

#### 2. Filtering for Even Numbers

Let's create a list of even numbers from a given list of numbers.

```python
# Using a for loop with an if condition
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_numbers_loop = []
for num in numbers:
    if num % 2 == 0:
        even_numbers_loop.append(num)
print(f"Even numbers (using for loop): {even_numbers_loop}")

# Using a list comprehension with an if condition
even_numbers_comp = [num for num in numbers if num % 2 == 0]
print(f"Even numbers (using list comprehension): {even_numbers_comp}")
```
Output:
```
Even numbers (using for loop): [2, 4, 6, 8, 10]
Even numbers (using list comprehension): [2, 4, 6, 8, 10]
```
Again, the list comprehension offers a more succinct way to express the filtering and creation of the new list.

#### 3. More Complex Example: String Manipulation

Let's convert a list of strings to uppercase, but only for strings longer than 3 characters.

```python
words = ["apple", "bat", "cherry", "dog", "elephant"]
uppercase_long_words = [word.upper() for word in words if len(word) > 3]
print(f"Uppercase long words: {uppercase_long_words}")
```
Output:
```
Uppercase long words: ['APPLE', 'CHERRY', 'ELEPHANT']
```

List comprehensions are a powerful feature in Python for creating lists dynamically. They are a cornerstone of idiomatic Python code.

## f-Strings for String Formatting

Introduced in Python 3.6, f-strings (formatted string literals) provide a highly readable and concise way to embed expressions inside string literals for formatting.

**Syntax:**

An f-string is prefixed with an `f` or `F` before the opening quotation mark. Inside the string, you can embed Python expressions by placing them inside curly braces `{}`.

```python
name = "Alice"
age = 30
greeting = f"Hello, my name is {name} and I am {age} years old."
print(greeting)
```
Output:
```
Hello, my name is Alice and I am 30 years old.
```

**Key Features and Benefits:**

*   **Readability:** They are generally more readable than older formatting methods like `%`-formatting or `str.format()`. The expressions are directly embedded in the string.
*   **Conciseness:** They often require less typing.
*   **Arbitrary Expressions:** You can embed any valid Python expression inside the curly braces. This includes variable names, function calls, arithmetic operations, etc.
*   **Speed:** F-strings are often faster than other string formatting methods.

**Examples:**

#### 1. Embedding Variables

This is the most common use case.

```python
# Example: Embedding variables
print("\n--- Embedding variables with f-strings ---")
item = "book"
price = 19.99
quantity = 2
message = f"Item: {item.capitalize()}, Price: ${price:.2f}, Quantity: {quantity}"
print(message)
# Notice the formatting options like .capitalize() and :.2f for price
```
Output:
```
--- Embedding variables with f-strings ---
Item: Book, Price: $19.99, Quantity: 2
```

#### 2. Embedding Expressions and Function Calls

You can perform calculations or call functions directly within f-strings.

```python
# Example: Embedding expressions and function calls
print("\n--- Embedding expressions and function calls ---")
x = 10
y = 5
calculation_result = f"The sum of {x} and {y} is {x + y}."
print(calculation_result)

def get_user_status(is_active):
    return "Active" if is_active else "Inactive"

user_active = True
status_message = f"User status: {get_user_status(user_active).upper()}" # Calling function and method
print(status_message)
```
Output:
```
--- Embedding expressions and function calls ---
The sum of 10 and 5 is 15.
User status: ACTIVE
```

#### 3. Multiline f-Strings

F-strings can span multiple lines, just like regular strings.

```python
# Example: Multiline f-string
print("\n--- Multiline f-string ---")
name = "Bob"
age = 25
city = "London"

multiline_info = (
    f"User Information:\n"
    f"  Name: {name}\n"
    f"  Age: {age}\n"
    f"  City: {city}"
)
print(multiline_info)
```
Output:
```
--- Multiline f-string ---
User Information:
  Name: Bob
  Age: 25
  City: London
```

#### 4. Debugging with f-Strings (Python 3.8+)

Python 3.8 introduced a convenient way to print both an expression and its value, which is great for debugging.

```python
# Example: Debugging with f-strings (Python 3.8+)
print("\n--- Debugging with f-strings (Python 3.8+) ---")
num_apples = 10
num_oranges = 5
# By adding '=' after the variable, both the variable name and its value are printed
print(f"{num_apples=}, {num_oranges=}")
total_fruit = num_apples + num_oranges
print(f"{total_fruit=}")
```
Output (if run with Python 3.8+):
```
--- Debugging with f-strings (Python 3.8+) ---
num_apples=10, num_oranges=5
total_fruit=15
```

F-strings have become the preferred method for string formatting in modern Python due to their clarity and performance.

## Python Functions
Python Functions is a block of statements which return the specific task.

The idea is to put some commonly or repeatedly done tasks together and make a function so that instead of writing the same code again and again for different inputs, we can do the function calls to reuse code contained in it over and over again. 

### Creating a Python Function
We can create a  Python function using the def keyword.
```python
# A simple Python function

def fun():
	print("Welcome to GFG")
```


### Calling a  Python Function
After creating a function we can call it by using the name of the function followed by parenthesis containing parameters of that particular function.

```python
# A simple Python function
def fun():
	print("Welcome to GFG")


# Driver code to call a function
fun()

```

Output
```
Welcome to GFG

```
### Defining and calling a function with parameters

#### Python Function with parameters Syntax:

Note : This is for python 3.5 and above

```python
def function_name(parameter: data_type) -> return_type:
    """Doctring"""
    # body of the function
    return expression
```
Example 1:
```python
def add(num1: int, num2: int) -> int:
	"""Add two numbers"""
	num3 = num1 + num2

	return num3

# Driver code
num1, num2 = 5, 15
ans = add(num1, num2)
print(f"The addition of {num1} and {num2} results {ans}.")
```
Output:
```
The addition of 5 and 15 results 20.

```
Example 2:
```python
# some more functions
def is_prime(n):
	if n in [2, 3]:
		return True
	if n % 2 == 0:
		return False
	r = 3
	while r * r <= n:
		if n % r == 0:
			return False
		r += 2
	return True
print(is_prime(78), is_prime(79))
```
Output:
```
False True
```
### Arguments of a Python Function
Arguments are the values passed inside the parenthesis of the function. A function can have any number of arguments separated by a comma.

Example :

```python
# A simple Python function to check
# whether x is even or odd


def evenOdd(x):
	if (x % 2 == 0):
		print("even")
	else:
		print("odd")


# Driver code to call the function
evenOdd(2)
evenOdd(3)
```
Output:
```
even
odd
```
#### Types of Arguments
* Default arguments
* Keyword arguments
* Variable-length arguments

##### Default Arguments 

A default argument is a parameter that assumes a default value if a value is not provided in the function call for that argument. The following example illustrates Default arguments.

```python
# Python program to demonstrate
# default arguments


def myFun(x, y=50):
	print("x: ", x)
	print("y: ", y)


# Driver code (We call myFun() with only
# argument)
myFun(10)

```
Output:
```
x:  10
y:  50
```
Any number of arguments in a function can have a default value. But once we have a default argument, all the arguments to its right must also have default values.
##### Keyword arguments

The idea is to allow the caller to specify the argument name with values so that caller does not need to remember the order of parameters.

```python
# Python program to demonstrate Keyword Arguments
def student(firstname, lastname):
	print(firstname, lastname)


# Keyword arguments
student(firstname='Geeks', lastname='Practice')
student(lastname='Practice', firstname='Geeks')
```

Output:
```
Geeks Practice
Geeks Practice
```

##### Variable-length arguments
In Python, we can pass a variable number of arguments to a function using special symbols. There are two special symbols:

* *args (Non-Keyword Arguments)
* **kwargs (Keyword Arguments)

Example 1: Variable length non-keywords argument

```python
# Python program to illustrate
# *args for variable number of arguments


def myFun(*argv):
	for arg in argv:
		print(arg)


myFun('Hello', 'Welcome', 'to', 'GeeksforGeeks')

```
Output:
```
Hello
Welcome
to
GeeksforGeeks
```
Example 2: Variable length keyword arguments


```python
# Python program to illustrate
# *kwargs for variable number of keyword arguments


def myFun(**kwargs):
	for key, value in kwargs.items():
		print("%s == %s" % (key, value))


# Driver code
myFun(first='Geeks', mid='for', last='Geeks')

```
Output:
```
first == Geeks
mid == for
last == Geeks
```

### Docstring
The first string after the function is called the Document string or Docstring in short. This is used to describe the functionality of the function. The use of docstring in functions is optional but it is considered a good practice.

The below syntax can be used to print out the docstring of a function:
```
Syntax: print(function_name.__doc__)
```

Example:
```python
# A simple Python function to check
# whether x is even or odd


def evenOdd(x):
	"""Function to check if the number is even or odd"""
	
	if (x % 2 == 0):
		print("even")
	else:
		print("odd")


# Driver code to call the function
print(evenOdd.__doc__)
```
Output:
```
Function to check if the number is even or odd

```

### Return statement in Python function
The function return statement is used to exit from a function and go back to the function caller and return the specified value or data item to the caller. 

Syntax:
```
return [expression_list]

```

The return statement can consist of a variable, an expression, or a constant which is returned to the end of the function execution. If none of the above is present with the return statement a None object is returned.


### Pass by Reference or pass by value
One important thing to note is, in Python every variable name is a reference. When we pass a variable to a function, a new reference to the object is created. Parameter passing in Python is the same as reference passing in Java.

Example : 

```python
# Here x is a new reference to same list lst
def myFun(x):
	x[0] = 20


# Driver Code (Note that lst is modified
# after function call.
lst = [10, 11, 12, 13, 14, 15]
myFun(lst)
print(lst)
```
Output
```
[20, 11, 12, 13, 14, 15]
```

When we pass a reference and change the received reference to something else, the connection between the passed and received parameter is broken. For example, consider the below program as follows:

```python3
def myFun(x):

	# After below line link of x with previous
	# object gets broken. A new object is assigned
	# to x.
	x = [20, 30, 40]


# Driver Code (Note that lst is not modified
# after function call.
lst = [10, 11, 12, 13, 14, 15]
myFun(lst)
print(lst)

```
Output:
```
[10, 11, 12, 13, 14, 15]

```

### Anonymus Function
In Python, an anonymous function means that a function is without a name. As we already know the def keyword is used to define the normal functions and the lambda keyword is used to create anonymous functions.

```python
# Python code to illustrate the cube of a number
# using lambda function


def cube(x): return x*x*x

cube_v2 = lambda x : x*x*x

print(cube(7))
print(cube_v2(7))

```
Output:
```
343
343
```
### Python Function within Functions
A function that is defined inside another function is known as the inner function or nested function. Nested functions are able to access variables of the enclosing scope. Inner functions are used so that they can be protected from everything happening outside the function.

Example:
```python
# Python program to
# demonstrate accessing of
# variables of nested functions

def f1():
	s = 'I love GeeksforGeeks'
	
	def f2():
		print(s)
		
	f2()

# Driver's code
f1()

```
Output:
```
I love GeeksforGeeks
```


