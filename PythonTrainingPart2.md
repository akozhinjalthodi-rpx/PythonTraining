Date : 28 July 2022

------------------

## Python Data Types
Data types are the classification or categorization of data items. It represents the kind of value that tells what operations can be performed on a particular data. Since everything is an object in Python programming, data types are actually classes and variables are instance (object) of these classes.

Following are the standard or built-in data type of Python:

* Numeric
* Sequence Type
* Boolean
* Set
* Dictionary

### Numeric
In Python, numeric data type represent the data which has numeric value. Numeric value can be integer, floating number or even complex numbers. These values are defined as int, float and complex class in Python.

* *Integers* – This value is represented by int class. It contains positive or negative whole numbers (without fraction or decimal). In Python there is no limit to how long an integer value can be.
* *Float* – This value is represented by float class. It is a real number with floating point representation. It is specified by a decimal point. Optionally, the character e or E followed by a positive or negative integer may be appended to specify scientific notation.
* *Complex Numbers* – Complex number is represented by complex class. It is specified as (real part) + (imaginary part)j. For example – 2+3j

Example:
```python
# Python program to
# demonstrate numeric value

a = 5
print("Type of a: ", type(a))

b = 5.0
print("\nType of b: ", type(b))

c = 2 + 4j
print("\nType of c: ", type(c))
```
Output:

```
Type of a:  <class 'int'>

Type of b:  <class 'float'>

Type of c:  <class 'complex'>
```
### Sequence Type

In Python, sequence is the ordered collection of similar or different data types. Sequences allows to store multiple values in an organized and efficient fashion. There are several sequence types in Python.
* Strings
* Lists
* Tuple

#### Strings: 

In Python, Strings are arrays of bytes representing Unicode characters. A string is a collection of one or more characters put in a single quote, double-quote or triple quote. In python there is no character data type, a character is a string of length one. It is represented by str class.

Example 
```python
# Python Program for
# Creation of String
	
# Creating a String
# with single Quotes
String1 = 'Welcome to the Geeks World'
print("String with the use of Single Quotes: ")
print(String1)
	
# Creating a String
# with double Quotes
String1 = "I'm a Geek"
print("\nString with the use of Double Quotes: ")
print(String1)
print(type(String1))
	
# Creating a String
# with triple Quotes
String1 = '''I'm a Geek and I live in a world of "Geeks"'''
print("\nString with the use of Triple Quotes: ")
print(String1)
print(type(String1))

# Creating String with triple
# Quotes allows multiple lines
String1 = '''Geeks
			For
			Life'''
print("\nCreating a multiline String: ")
print(String1)

```

Output :
```
String with the use of Single Quotes: 
Welcome to the Geeks World

String with the use of Double Quotes: 
I'm a Geek
<class 'str'>

String with the use of Triple Quotes: 
I'm a Geek and I live in a world of "Geeks"
<class 'str'>

Creating a multiline String: 
Geeks 
            For 
            Life
```

#### Accessing elements of String
In Python, individual characters of a String can be accessed by using the method of Indexing. Indexing allows negative address references to access characters from the back of the String, e.g. -1 refers to the last character, -2 refers to the second last character and so on.

```python
# Python Program to Access
# characters of String
	
String1 = "GeeksForGeeks"
print("Initial String: ")
print(String1)
	
# Printing First character
print("\nFirst character of String is: ")
print(String1[0])
	
# Printing Last character
print("\nLast character of String is: ")
print(String1[-1])

```

Output:
```
Initial String: 
GeeksForGeeks

First character of String is: 
G

Last character of String is: 
s
```

#### Lists
Lists are just like the arrays, declared in other languages which is a ordered collection of data. It is very flexible as the items in a list do not need to be of the same type.

```python3
# Python program to demonstrate
# Creation of List
	
# Creating a List
List = []
print("Initial blank List: ")
print(List)
	
# Creating a List with
# the use of a String
List = ['GeeksForGeeks']
print("\nList with the use of String: ")
print(List)
	
# Creating a List with
# the use of multiple values
List = ["Geeks", "For", "Geeks"]
print("\nList containing multiple values: ")
print(List[0])
print(List[2])
	
# Creating a Multi-Dimensional List
# (By Nesting a list inside a List)
List = [['Geeks', 'For'], ['Geeks']]
print("\nMulti-Dimensional List: ")
print(List)

```

```
Initial blank List: 
[]

List with the use of String: 
['GeeksForGeeks']

List containing multiple values: 
Geeks
Geeks

Multi-Dimensional List: 
[['Geeks', 'For'], ['Geeks']]
```
#### Tuple
Just like list, tuple is also an ordered collection of Python objects. The only difference between tuple and list is that tuples are immutable i.e. tuples cannot be modified after it is created. It is represented by tuple class.

Note: Tuples can also be created with a single element, but it is a bit tricky. Having one element in the parentheses is not sufficient, there must be a trailing ‘comma’ to make it a tuple.

```python
# Python program to demonstrate
# creation of Set
	
# Creating an empty tuple
Tuple1 = ()
print("Initial empty Tuple: ")
print (Tuple1)
	
# Creating a Tuple with
# the use of Strings
Tuple1 = ('Geeks', 'For')
print("\nTuple with the use of String: ")
print(Tuple1)
	
# Creating a Tuple with
# the use of list
list1 = [1, 2, 4, 5, 6]
print("\nTuple using List: ")
print(tuple(list1))

# Creating a Tuple with the
# use of built-in function
Tuple1 = tuple('Geeks')
print("\nTuple with the use of function: ")
print(Tuple1)

# Creating a Tuple
# with nested tuples
Tuple1 = (0, 1, 2, 3)
Tuple2 = ('python', 'geek')
Tuple3 = (Tuple1, Tuple2)
print("\nTuple with nested tuples: ")
print(Tuple3)

```
Note – Creation of Python tuple without the use of parentheses is known as Tuple Packing.


### Boolean
Data type with one of the two built-in values, True or False. Boolean objects that are equal to True are truthy (true), and those equal to False are falsy (false). But non-Boolean objects can be evaluated in Boolean context as well and determined to be true or false. It is denoted by the class bool.

Note – True and False with capital ‘T’ and ‘F’ are valid booleans otherwise python will throw an error.

```python3
# Python program to
# demonstrate boolean type

print(type(True))
print(type(False))

print(type(true))

```
```
Traceback (most recent call last):
  File "/home/7e8862763fb66153d70824099d4f5fb7.py", line 8, in 
    print(type(true))
NameError: name 'true' is not defined
```
### Sets
In Python, Set is an unordered collection of data type that is iterable, mutable and has no duplicate elements. The order of elements in a set is undefined though it may consist of various elements.

Sets can be created by using the built-in set() function with an iterable object or a sequence by placing the sequence inside curly braces, separated by ‘comma’. Type of elements in a set need not be the same, various mixed-up data type values can also be passed to the set.

```python3
# Python program to demonstrate
# Creation of Set in Python
	
# Creating a Set
set1 = set()
print("Initial blank Set: ")
print(set1)
	
# Creating a Set with
# the use of a String
set1 = set("GeeksForGeeks")
print("\nSet with the use of String: ")
print(set1)

# Creating a Set with
# the use of a List
set1 = set(["Geeks", "For", "Geeks"])
print("\nSet with the use of List: ")
print(set1)

# Creating a Set with
# a mixed type of values
# (Having numbers and strings)
set1 = set([1, 2, 'Geeks', 4, 'For', 6, 'Geeks'])
print("\nSet with the use of Mixed Values")
print(set1)

```

Output:
```
Initial blank Set: 
set()

Set with the use of String: 
{'F', 'o', 'G', 's', 'r', 'k', 'e'}

Set with the use of List: 
{'Geeks', 'For'}

Set with the use of Mixed Values
{1, 2, 4, 6, 'Geeks', 'For'}
```
#### Accessing elements of Sets
Set items cannot be accessed by referring to an index, since sets are unordered the items has no index. But you can loop through the set items using a for loop, or ask if a specified value is present in a set, by using the in keyword.

```python
# Python program to demonstrate
# Accessing of elements in a set
	
# Creating a set
set1 = set(["Geeks", "For", "Geeks"])
print("\nInitial set")
print(set1)
	
# Accessing element using
# for loop
print("\nElements of set: ")
for i in set1:
	print(i, end =" ")
	
# Checking the element
# using in keyword
print("Geeks" in set1)

```
```
Initial set: 
{'Geeks', 'For'}

Elements of set: 
Geeks For 

True

```
#### Using add() method
Elements can be added to the Set by using the built-in add() function. Only one element at a time can be added to the set by using add() method, loops are used to add multiple elements at a time with the use of add() method.

Note: Lists cannot be added to a set as elements because Lists are not hashable whereas Tuples can be added because tuples are immutable and hence Hashable

```python3
# Python program to demonstrate
# Addition of elements in a Set

# Creating a Set
set1 = set()
print("Initial blank Set: ")
print(set1)

# Adding element and tuple to the Set
set1.add(8)
set1.add(9)
set1.add((6, 7))
print("\nSet after Addition of Three elements: ")
print(set1)

# Adding elements to the Set
# using Iterator
for i in range(1, 6):
	set1.add(i)
print("\nSet after Addition of elements from 1-5: ")
print(set1)

```
Output:
```
Initial blank Set: 
set()

Set after Addition of Three elements: 
{8, 9, (6, 7)}

Set after Addition of elements from 1-5: 
{1, 2, 3, (6, 7), 4, 5, 8, 9}
```
#### Using update() method
For the addition of two or more elements Update() method is used. The update() method accepts lists, strings, tuples as well as other sets as its arguments. In all of these cases, duplicate elements are avoided.

```python3
# Python program to demonstrate
# Addition of elements in a Set

# Addition of elements to the Set
# using Update function
set1 = set([4, 5, (6, 7)])
set1.update([10, 11])
print("\nSet after Addition of elements using Update: ")
print(set1)

```
#### Using remove() method or discard() method:
Elements can be removed from the Set by using the built-in remove() function but a KeyError arises if the element doesn’t exist in the set. To remove elements from a set without KeyError, use discard(), if the element doesn’t exist in the set, it remains unchanged.

```python3
# Python program to demonstrate
# Deletion of elements in a Set

# Creating a Set
set1 = set([1, 2, 3, 4, 5, 6,
			7, 8, 9, 10, 11, 12])
print("Initial Set: ")
print(set1)

# Removing elements from Set
# using Remove() method
set1.remove(5)
set1.remove(6)
print("\nSet after Removal of two elements: ")
print(set1)

# Removing elements from Set
# using Discard() method
set1.discard(8)
set1.discard(9)
print("\nSet after Discarding two elements: ")
print(set1)

# Removing elements from Set
# using iterator method
for i in range(1, 5):
	set1.remove(i)
print("\nSet after Removing a range of elements: ")
print(set1)

```
Output:
```
Initial Set: 
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}

Set after Removal of two elements: 
{1, 2, 3, 4, 7, 8, 9, 10, 11, 12}

Set after Discarding two elements: 
{1, 2, 3, 4, 7, 10, 11, 12}

Set after Removing a range of elements: 
{7, 10, 11, 12}
```

### Dictionary
Dictionary in Python is an unordered collection of data values, used to store data values like a map, which unlike other Data Types that hold only single value as an element, Dictionary holds key:value pair. Key-value is provided in the dictionary to make it more optimized. Each key-value pair in a Dictionary is separated by a colon :, whereas each key is separated by a ‘comma’.

#### Creating Dictionary
In Python, a Dictionary can be created by placing a sequence of elements within curly {} braces, separated by ‘comma’. Values in a dictionary can be of any datatype and can be duplicated, whereas keys can’t be repeated and must be immutable. Dictionary can also be created by the built-in function dict(). An empty dictionary can be created by just placing it to curly braces{}.

Note – Dictionary keys are case sensitive, same name but different cases of Key will be treated distinctly.

```python
# Creating an empty Dictionary
Dict = {}
print("Empty Dictionary: ")
print(Dict)
	
# Creating a Dictionary
# with Integer Keys
Dict = {1: 'Geeks', 2: 'For', 3: 'Geeks'}
print("\nDictionary with the use of Integer Keys: ")
print(Dict)
	
# Creating a Dictionary
# with Mixed keys
Dict = {'Name': 'Geeks', 1: [1, 2, 3, 4]}
print("\nDictionary with the use of Mixed Keys: ")
print(Dict)
	
# Creating a Dictionary
# with dict() method
Dict = dict({1: 'Geeks', 2: 'For', 3:'Geeks'})
print("\nDictionary with the use of dict(): ")
print(Dict)
	
# Creating a Dictionary
# with each item as a Pair
Dict = dict([(1, 'Geeks'), (2, 'For')])
print("\nDictionary with each item as a pair: ")
print(Dict)

```

```
Empty Dictionary: 
{}

Dictionary with the use of Integer Keys: 
{1: 'Geeks', 2: 'For', 3: 'Geeks'}

Dictionary with the use of Mixed Keys: 
{1: [1, 2, 3, 4], 'Name': 'Geeks'}

Dictionary with the use of dict(): 
{1: 'Geeks', 2: 'For', 3: 'Geeks'}

Dictionary with each item as a pair: 
{1: 'Geeks', 2: 'For'}
```

#### Accessing elements of Dictionary
In order to access the items of a dictionary refer to its key name. Key can be used inside square brackets. There is also a method called get() that will also help in accessing the element from a dictionary.

```python
# Python program to demonstrate
# accessing a element from a Dictionary
	
# Creating a Dictionary
Dict = {1: 'Geeks', 'name': 'For', 3: 'Geeks'}
	
# accessing a element using key
print("Accessing a element using key:")
print(Dict['name'])

# accessing a element using get()
# method
print("Accessing a element using get:")
print(Dict.get(3))

```

```
Accessing a element using key:
For
Accessing a element using get:
Geeks
```

Date : 29 July 2022

__________________

## Iterators
Iterator in python is an object that is used to iterate over iterable objects like lists, tuples, dicts, and sets. The iterator object is initialized using the iter() method. It uses the next() method for iteration.


```__iter(iterable)__ ```  method that is called for the initialization of an iterator. This returns an iterator object

``` next ( __next__ in Python 3)  ``` The next method returns the next value for the iterable. When we use a for loop to traverse any iterable object, internally it uses the iter() method to get an iterator object which further uses next() method to iterate over. This method raises a StopIteration to signal the end of the iteration.

How an iterator really works in python

```python
# Here is an example of a python inbuilt iterator
# value can be anything which can be iterate
iterable_value = 'Geeks'
iterable_obj = iter(iterable_value)

while True:
	try:

		# Iterate by calling next
		item = next(iterable_obj)
		print(item)
	except StopIteration:

		# exception will happen when iteration will over
		break
```
Output:
```
G                                                                                                                                                                            
e                                                                                                                                                                            
e                                                                                                                                                                            
k                                                                                                                                                                            
s



```
Below is a simple Python custom iterator that creates iterator type that iterates from 10 to a given limit. For example, if the limit is 15, then it prints 10 11 12 13 14 15. And if the limit is 5, then it prints nothing.

```python
# A simple Python program to demonstrate
# working of iterators using an example type
# that iterates from 10 to given value

# An iterable user defined type
class Test:

	# Constructor
	def __init__(self, limit):
		self.limit = limit

	# Creates iterator object
	# Called when iteration is initialized
	def __iter__(self):
		self.x = 10
		return self

	# To move to next element. In Python 3,
	# we should replace next with __next__
	def __next__(self):

		# Store current value ofx
		x = self.x

		# Stop iteration if limit is reached
		if x > self.limit:
			raise StopIteration

		# Else increment and return old value
		self.x = x + 1;
		return x

# Prints numbers from 10 to 15
for i in Test(15):
	print(i)

# Prints nothing
for i in Test(5):
	print(i)
```

Output:
```
10
11
12
13
14
15
```

## When to use yield instead of return in Python?
The yield statement suspends a function’s execution and sends a value back to the caller, but retains enough state to enable the function to resume where it left off. When the function resumes, it continues execution immediately after the last yield run. This allows its code to produce a series of values over time, rather than computing them at once and sending them back like a list.

Example:
```python
# A Simple Python program to demonstrate working
# of yield

# A generator function that yields 1 for the first time,
# 2 second time and 3 third time


def simpleGeneratorFun():
	yield 1
	yield 2
	yield 3


# Driver code to check above generator function
for value in simpleGeneratorFun():
	print(value)

```

Output:
```
1
2
3
```
"Return" sends a specified value back to its caller whereas Yield can produce a sequence of values. We should use yield when we want to iterate over a sequence, but don’t want to store the entire sequence in memory. Yield is used in Python generators. A generator function is defined just like a normal function, but whenever it needs to generate a value, it does so with the yield keyword rather than return. If the body of a def contains yield, the function automatically becomes a generator function. 

```python
# A Python program to generate squares from 1
# to 100 using yield and therefore generator

# An infinite generator function that prints
# next square number. It starts with 1


def nextSquare():
	i = 1

	# An Infinite loop to generate squares
	while True:
		yield i*i
		i += 1 # Next execution resumes
		# from this point


# Driver code to test above generator
# function
for num in nextSquare():
	if num & gt
	100:
		break
	print(num)
```

## Generators in Python
Generator-Function : A generator-function is defined like a normal function, but whenever it needs to generate a value, it does so with the yield keyword rather than return. If the body of a def contains yield, the function automatically becomes a generator function

Generator-Object : Generator functions return a generator object. Generator objects are used either by calling the next method on the generator object or using the generator object in a “for in” loop (as shown in the above program).

```python
# A Python program to demonstrate use of
# generator object with next()

# A generator function
def simpleGeneratorFun():
	yield 1
	yield 2
	yield 3

# x is a generator object
x = simpleGeneratorFun()

# Iterating over the generator object using next
print(x.next()) # In Python 3, __next__()
print(x.next())
print(x.next())

```
Output:
```
1
2
3
```
So a generator function returns an generator object that is iterable, i.e., can be used as an Iterators .

```python
# A simple generator for Fibonacci Numbers
def fib(limit):
	
	# Initialize first two Fibonacci Numbers
	a, b = 0, 1

	# One by one yield next Fibonacci Number
	while a < limit:
		yield a
		a, b = b, a + b

# Create a generator object
x = fib(5)

# Iterating over the generator object using next
print(x.next()) # In Python 3, __next__()
print(x.next())
print(x.next())
print(x.next())
print(x.next())

# Iterating over the generator object using for
# in loop.
print("\nUsing for in loop")
for i in fib(5):
	print(i)
```

Output:

```
0
1
1
2
3

Using for in loop
0
1
1
2
3
```
Applications : Suppose we to create a stream of Fibonacci numbers, adopting the generator approach makes it trivial; we just have to call next(x) to get the next Fibonacci number without bothering about where or when the stream of numbers ends.
A more practical type of stream processing is handling large data files such as log files. Generators provide a space efficient method for such data processing as only parts of the file are handled at one given point in time. We can also use Iterators for these purposes, but Generator provides a quick way (We don’t need to write __next__ and __iter__ methods here).

## Short Hand if-else statement
This can be used to write the if-else statements in a single line where there is only one statement to be executed in both if and else block. 

Syntax:
```
statement_when_True if condition else statement_when_False
```
Example: Python if else shorthand 

```python
# Python program to illustrate short hand if-else
i = 10
print(True) if i < 15 else print(False)

```

## Chaining comparison operators in Python
Checking more than two conditions is very common in Programming Languages. Let’s say we want to check the below condition:
```
a < b < c
```
The most common syntax to do it is as follows:
```
if a < b and b < c :
{....}
```
In Python, there is a better way to write this using Comparison operator Chaining. The chaining of operators can be written as follows:
```
if a < b < c :
    {.....}
```

According to associativity and precedence in Python, all comparison operations in Python have the same priority, which is lower than that of any arithmetic, shifting, or bitwise operation. Also unlike C, expressions like a < b < c have the interpretation that is conventional in mathematics

## Exception Handling in Python

Error in Python can be of two types i.e. Syntax errors and Exceptions. Errors are the problems in a program due to which the program will stop the execution. On the other hand, exceptions are raised when some internal events occur which changes the normal flow of the program. 

Exceptions: Exceptions are raised when the program is syntactically correct, but the code resulted in an error. This error does not stop the execution of the program, however, it changes the normal flow of the program.

Note: Exception is the base class for all the exceptions in Python.

Exception Hierarchy : https://docs.python.org/2/library/exceptions.html#exception-hierarchy

### Try and Except Statement – Catching Exceptions
Try and except statements are used to catch and handle exceptions in Python. Statements that can raise exceptions are kept inside the try clause and the statements that handle the exception are written inside except clause.

Example:
```python
# Python program to handle simple runtime error
#Python 3

a = [1, 2, 3]
try:
	print ("Second element = %d" %(a[1]))

	# Throws error since there are only 3 elements in array
	print ("Fourth element = %d" %(a[3]))

except:
	print ("An error occurred")

```

Output:
```
Second element = 2
An error occurred
```
In the above example, the statements that can cause the error are placed inside the try statement (second print statement in our case). The second print statement tries to access the fourth element of the list which is not there and this throws an exception. This exception is then caught by the except statement

### Catching Specific Exception
A try statement can have more than one except clause, to specify handlers for different exceptions. Please note that at most one handler will be executed. For example, we can add IndexError in the above code. The general syntax for adding specific exceptions are – 

```
try:
    # statement(s)
except IndexError:
    # statement(s)
except ValueError:
    # statement(s)
```
Example: Catching specific exception in Python

```python
# Program to handle multiple errors with one
# except statement
# Python 3

def fun(a):
	if a < 4:

		# throws ZeroDivisionError for a = 3
		b = a/(a-3)

	# throws NameError if a >= 4
	print("Value of b = ", b)
	
try:
	fun(3)
	fun(5)

# note that braces () are necessary here for
# multiple exceptions
except ZeroDivisionError:
	print("ZeroDivisionError Occurred and Handled")
except NameError:
	print("NameError Occurred and Handled")
```
Output:

```python
ZeroDivisionError Occurred and Handled
```
If you comment on the line fun(3), the output will be 

```
NameError Occurred and Handle
```

The output above is so because as soon as python tries to access the value of b, NameError occurs. 


### Try with Else Clause
In python, you can also use the else clause on the try-except block which must be present after all the except clauses. *The code enters the else block only if the try clause does not raise an exception*.

Example: Try with else clause

```python
# Program to depict else clause with try-except
# Python 3
# Function which returns a/b
def AbyB(a , b):
	try:
		c = ((a+b) / (a-b))
	except ZeroDivisionError:
		print ("a/b result in 0")
	else:
		print (c)

# Driver program to test above function
AbyB(2.0, 3.0)
AbyB(3.0, 3.0)
```

Output:
```
-5.0
a/b result in 0 
```

### Finally Keyword in Python
Python provides a keyword finally, which is always executed after the try and except blocks. The final block always executes after normal termination of try block or after try block terminates due to some exception.

Syntax:
```python
try:
    # Some Code.... 

except:
    # optional block
    # Handling of exception (if required)

else:
    # execute if no exception

finally:
    # Some code .....(always executed)
```

Example:

```python
# Python program to demonstrate finally

# No exception Exception raised in try block
try:
	k = 5//0 # raises divide by zero exception.
	print(k)

# handles zerodivision exception
except ZeroDivisionError:
	print("Can't divide by zero")

finally:
	# this block is always executed
	# regardless of exception generation.
	print('This is always executed')
```
Output:

```
Can't divide by zero
This is always executed
```

### Raising Exception
The raise statement allows the programmer to force a specific exception to occur. The sole argument in raise indicates the exception to be raised. This must be either an exception instance or an exception class (a class that derives from Exception).

```python
# Program to depict Raising Exception

try:
	raise NameError("Hi there") # Raise Error
except NameError:
	print ("An exception")
	raise # To determine whether the exception was raised or not

```

The output of the above code will simply line printed as “An exception” but a Runtime error will also occur in the last due to the raise statement in the last line. So, the output on your command line will look like 

```
Traceback (most recent call last):
  File "/home/d6ec14ca595b97bff8d8034bbf212a9f.py", line 5, in <module>
    raise NameError("Hi there")  # Raise Error
NameError: Hi there
```


## Function Decorator

Decorators are a very powerful and useful tool in Python since it allows programmers to modify the behaviour of a function or class. Decorators allow us to wrap another function in order to extend the behaviour of the wrapped function, without permanently modifying it. But before diving deep into decorators let us understand some concepts that will come in handy in learning the decorators.

### First Class Objects
In Python, functions are first class objects which means that functions in Python can be used or passed as arguments.
Properties of first class functions:

* A function is an instance of the Object type.
* You can store the function in a variable.
* You can pass the function as a parameter to another function.
* You can return the function from a function.
* You can store them in data structures such as hash tables, lists, …

### Example 2: Passing the function as an argument 

```python
# Python program to illustrate functions
# can be passed as arguments to other functions
def shout(text):
	return text.upper()

def whisper(text):
	return text.lower()

def greet(func):
	# storing the function in a variable
	greeting = func("""Hi, I am created by a function passed as an argument.""")
	print (greeting)

greet(shout)
greet(whisper)

```

Output:
```
HI, I AM CREATED BY A FUNCTION PASSED AS AN ARGUMENT.
hi, i am created by a function passed as an argument.
```
In the above example, the greet function takes another function as a parameter (shout and whisper in this case). The function passed as an argument is then called inside the function greet.

### Example 3: Returning functions from another function.

```python
# Python program to illustrate functions
# Functions can return another function

def create_adder(x):
	def adder(y):
		return x+y

	return adder

add_15 = create_adder(15)

print(add_15(10))

```
Output:
```
25
```
In the above example, we have created a function inside of another function and then have returned the function created inside.
The above three examples depict the important concepts that are needed to understand decorators. After going through them let us now dive deep into decorators.

### Decorators
As stated above the decorators are used to modify the behaviour of function or class. In Decorators, functions are taken as the argument into another function and then called inside the wrapper function.

Syntax for Decorator: 

```
@gfg_decorator
def hello_decorator():
    print("Gfg")

'''Above code is equivalent to -

def hello_decorator():
    print("Gfg")
    
hello_decorator = gfg_decorator(hello_decorator)'''
```

In the above code, gfg_decorator is a callable function, that will add some code on the top of some another callable function, hello_decorator function and return the wrapper function.


```python3
# Python program to illustrate functions
# can be treated as objects
def shout(text):
	return text.upper()

print(shout('Hello'))

yell = shout

print(yell('Hello'))

```

Output:
```
HELLO
HELLO
```
```python
# A Python program to demonstrate that a function
# can be defined inside another function and a
# function can be passed as parameter.

# Adds a welcome message to the string
def messageWithWelcome(str):

	# Nested function
	def addWelcome():
		return "Welcome to "

	# Return concatenation of addWelcome()
	# and str.
	return addWelcome() + str

# To get site name to which welcome is added
def site(site_name):
	return site_name

print messageWithWelcome(site("GeeksforGeeks"))

```
A decorator is a function that takes a function as its only parameter and returns a function. This is helpful to “wrap” functionality with the same code over and over again. For example, above code can be re-written as following.
We use @func_name to specify a decorator to be applied on another function.

```python
# Adds a welcome message to the string
# returned by fun(). Takes fun() as
# parameter and returns welcome().
def decorate_message(fun):

	# Nested function
	def addWelcome(site_name):
		return "Welcome to " + fun(site_name)

	# Decorator returns a function
	return addWelcome

@decorate_message
def site(site_name):
	return site_name;

# Driver code

# This call is equivalent to call to
# decorate_message() with function
# site("GeeksforGeeks") as parameter
print site("GeeksforGeeks")

```
Output:
```
Welcome to GeeksforGeeks

```

Decorators can also be useful to attach data (or add attribute) to functions.

```python
# A Python example to demonstrate that
# decorators can be useful attach data

# A decorator function to attach
# data to func
def attach_data(func):
	func.data = 3
	return func

@attach_data
def add (x, y):
	return x + y

# Driver code

# This call is equivalent to attach_data()
# with add() as parameter
print(add(2, 3))

print(add.data)
```

Output:
```
5
3
```
‘add()’ returns sum of x and y passed as arguments but it is wrapped by a decorator function, calling add(2, 3) would simply give sum of two numbers but when we call add.data then ‘add’ function is passed into then decorator function ‘attach_data’ as argument and this function returns ‘add’ function with an attribute ‘data’ that is set to 3 and hence prints it.

Python decorators are a powerful tool to remove redundancy.

