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


## Python OOPs Concepts

In Python object oriented programming (OOOPs) is a programming paradigm that uses objects and classes in programming. It aims to implement real world entities like inheritaince, polymorphisms,encapsulations, etc. in the programming. The main concept if OOPs is to bind the data and the functions that work on that together as a single unit so that no other part of the code can access this data.

### Main Concepts of Object Oriented Programming (OOPs)
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

##### The self :
* Class methods must have an extra parameter in the method definition. We don't need to give value for this parameter when we call a method (Python prvides it).
* If we have a method that takes no argument, we still have to have one argument.

When we call a method of an object for eg: myobject.method(arg1,arg2) is automatically converted by python into myobject.method(myobject,arg1,arg2)

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
Inheritance is the property of one class to derive or inherit the properties from another class. The class that derives properties is called derived class or child class and the class from which the properties are being derived is called the base class or parent class.

##### Benifits
* It represents real-world relationships well 
* It provides reusability of code 
* It is transitive in nature, meaning if class B inherit from another class A, then all the subclasses of B would automatically inherit from class A
##### Example : Inheritance in Python
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
* Single _ is used to define a protected variable/member

Note : Although the protected variable can be accessed out of the class as well as in the derived class(modified too in derived class), it is customary(convention not a rule) to not access the protected out the class body.

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


