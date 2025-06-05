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

## Context Managers (`with` statement)

Context managers are a powerful Python feature used for managing resources effectively. They ensure that resources are properly acquired and, more importantly, released, even if errors occur. This is crucial for operations like file handling, network connections, or database interactions.

The primary way to use a context manager is with the `with` statement.

**Purpose:**

*   **Resource Management:** To ensure resources (like files, locks, connections) are set up and torn down correctly.
*   **Automatic Cleanup:** Guarantees that cleanup actions (e.g., closing a file) are performed automatically.
*   **Error Handling:** Provides a clean way to handle exceptions that might occur while using the resource.
*   **Readability:** Makes code cleaner and easier to understand by abstracting resource management logic.

**Syntax: `with open(...) as f:`**

The most common example is opening a file:

```python
# Example: Using 'with' to open a file
print("--- Using 'with' for file handling ---")
try:
    with open("example.txt", "w") as f:
        f.write("Hello, context managers!\n")
        f.write("This file will be automatically closed.\n")
        # f.read() # Uncommenting this would cause an error as the file is opened in write mode 'w'
    print("File 'example.txt' written and closed successfully.")

    with open("example.txt", "r") as f:
        content = f.read()
        print("\nFile content:")
        print(content)
    print("File 'example.txt' read and closed successfully.")

except IOError as e:
    print(f"An IOError occurred: {e}")
```
Output (will vary slightly if example.txt is not cleaned up between runs, but the content will be as written):
```
--- Using 'with' for file handling ---
File 'example.txt' written and closed successfully.

File content:
Hello, context managers!
This file will be automatically closed.

File 'example.txt' read and closed successfully.
```
In this example, `open("example.txt", "w")` returns a file object that is also a context manager. The `as f` part assigns this object to the variable `f`. When the `with` block is exited (either normally or due to an exception), Python automatically calls a special method on the file object that closes the file.

**Before and After: Manual `try/finally` vs. `with`**

Let's see how context managers simplify resource handling compared to manual `try...finally` blocks.

**1. Manual File Handling (Before `with`):**

```python
# Manual file handling with try/finally
print("\n--- Manual file handling (try/finally) ---")
f = None # Initialize f outside try in case open() fails
try:
    f = open("manual_example.txt", "w")
    f.write("This is a manually managed file.\n")
    # Imagine an error occurring here:
    # raise ValueError("Something went wrong!")
    print("File 'manual_example.txt' written (still open).")
except IOError as e:
    print(f"An IOError occurred: {e}")
except ValueError as ve:
    print(f"A ValueError occurred: {ve}")
finally:
    if f: # Check if f was successfully assigned (file opened)
        print("Closing file in 'finally' block.")
        f.close()
    else:
        print("File was not opened, nothing to close in 'finally'.")
```
Output:
```
--- Manual file handling (try/finally) ---
File 'manual_example.txt' written (still open).
Closing file in 'finally' block.
```
If you uncomment `raise ValueError(...)`, the output would show the ValueError being caught and the file still being closed.

**2. Using `with` Statement (After):**

```python
# File handling with 'with' statement
print("\n--- File handling with 'with' statement ---")
try:
    with open("with_example.txt", "w") as f:
        f.write("This file is managed by a 'with' statement.\n")
        # Imagine an error occurring here:
        # raise ValueError("Something went wrong with 'with'!")
        print("File 'with_example.txt' written (will be auto-closed).")
    # No need for an explicit f.close() or a finally block for closing.
except IOError as e:
    print(f"An IOError occurred: {e}")
except ValueError as ve:
    print(f"A ValueError occurred during 'with': {ve}")

print("Exited 'with' block for 'with_example.txt'.")
```
Output:
```
--- File handling with 'with' statement ---
File 'with_example.txt' written (will be auto-closed).
Exited 'with' block for 'with_example.txt'.
```
If you uncomment `raise ValueError(...)` inside the `with` block, the ValueError will be caught, and the file `with_example.txt` will *still* be closed automatically before the exception handling proceeds.

**Benefits of Using `with` (Context Managers):**

| Benefit             | Description                                                                                                |
|---------------------|------------------------------------------------------------------------------------------------------------|
| **Automatic Cleanup** | Resources are guaranteed to be released, preventing resource leaks (e.g., too many open files).        |
| **Readability**       | Code is cleaner and more concise as resource setup and teardown logic is abstracted.                     |
| **Error Handling**    | Simplifies exception handling around resource usage; cleanup occurs even if errors are raised.             |
| **Reusability**       | You can create your own context managers for custom resource types by implementing `__enter__` and `__exit__` methods. |

Context managers are a fundamental part of writing robust and idiomatic Python code, especially when dealing with external resources.

## Iterators and Generators

This section explores how Python handles iteration, a fundamental concept for processing sequences of data.

### Iterators

An **iterator** in Python is an object that enables traversal through all elements of an iterable object (like lists, tuples, dictionaries, and sets) one at a time. The iterator pattern consists of two main parts:

1.  **The Iterable:** An object that can be iterated over. It must implement the `__iter__()` method, which returns an iterator object.
2.  **The Iterator:** An object that actually performs the iteration. It must implement the `__next__()` method to return the next item and `__iter__()` method to return itself.

**Core Methods for Iteration:**

*   **`iter(iterable)`:**
    *   This built-in function is called on an iterable object (e.g., a list).
    *   It returns an **iterator object** for that iterable.
    *   Internally, this calls the iterable's `__iter__()` method.

*   **`next(iterator)`:**
    *   This built-in function is called on an iterator object.
    *   It retrieves the next item from the iterator.
    *   Internally, this calls the iterator's `__next__()` method.
    *   If there are no more items to return, it raises a `StopIteration` exception, signaling that the iteration is complete.

**How `for` loops use iterators:**

When you use a `for` loop (e.g., `for item in my_list:`), Python automatically does the following:
1.  Calls `iter(my_list)` to get an iterator object.
2.  Repeatedly calls `next()` on this iterator object to get each item.
3.  Assigns the item to the loop variable (e.g., `item`).
4.  Handles the `StopIteration` exception gracefully to terminate the loop.

**Example: Manual Iteration**

This shows what Python does behind the scenes during a `for` loop:

```python
```python
# Example: Manual iteration with iter() and next()
print("--- Manual Iteration Example ---")
my_string = "Hi"
my_iterator = iter(my_string) # Get an iterator object for the string

try:
    print(next(my_iterator)) # Output: H
    print(next(my_iterator)) # Output: i
    print(next(my_iterator)) # This will raise StopIteration
except StopIteration:
    print("Iteration is complete (StopIteration caught).")
```
Output:
```
--- Manual Iteration Example ---
H
i
Iteration is complete (StopIteration caught).
```

**Custom Iterators (Class-based):**

You can create your own iterators by defining a class that implements the `__iter__()` and `__next__()` methods.

```python
# Example: Custom iterator for a range-like sequence
print("\n--- Custom Iterator Example (MyRange) ---")
class MyRange:
    """A simple custom iterator that mimics range()."""
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __iter__(self):
        # This method makes an object iterable.
        # It should return an iterator object (often self).
        return self

    def __next__(self):
        # This method should return the next item in the sequence.
        # It must raise StopIteration when there are no more items.
        if self.current < self.end:
            value = self.current
            self.current += 1
            return value
        else:
            raise StopIteration

# Using the custom iterator
print("Iterating from 1 to 3 (exclusive):")
for num in MyRange(1, 3):
    print(num)

print("\nIterating from 10 to 12 (exclusive) with no items to print if start >= end:")
# This loop won't execute if MyRange(12,10) was used,
# because the first __next__ call would immediately raise StopIteration
for num in MyRange(12, 10): # Start is not less than end
     print(num) # This line won't be reached
print("Finished MyRange(12,10) loop.")
```
Output:
```
--- Custom Iterator Example (MyRange) ---
Iterating from 1 to 3 (exclusive):
1
2

Iterating from 10 to 12 (exclusive) with no items to print if start >= end:
Finished MyRange(12,10) loop.
```

### Generators

Generators provide a more convenient way to create iterators. A generator is a special type of function that returns an iterator object which can be iterated upon one value at a time.

**`yield` vs. `return`:**

*   **`return`:** When a `return` statement is encountered in a function, it terminates the function's execution entirely and sends a specified value (or `None`) back to its caller. The function's local state (variables) is discarded.
*   **`yield`:** When a `yield` statement is encountered, the function's execution is **paused**, and the yielded value is sent back to the caller. Crucially, the function's local state (variables, instruction pointer) is **preserved**. When the iterator's `next()` method is called again, the function resumes execution right after the `yield` statement, with its previous state intact.

This "pausing" and "resuming" behavior allows `yield` to produce a sequence of values over time, making it highly memory-efficient, especially for large sequences, as it doesn't need to compute and store all values in memory at once.

**Generator Functions:**

A function becomes a generator function if it contains one or more `yield` statements.

```python
# Example: A simple generator function
print("\n--- Simple Generator Function Example ---")
def simple_generator():
    print("Generator started...")
    yield 10
    print("Generator resumed after first yield...")
    yield 20
    print("Generator resumed after second yield...")
    yield 30
    print("Generator finished.")

# Using the generator function
my_gen_obj = simple_generator() # Calling the function returns a generator object
print(f"Generator object: {my_gen_obj}")

try:
    print(f"First value: {next(my_gen_obj)}")
    print(f"Second value: {next(my_gen_obj)}")
    print(f"Third value: {next(my_gen_obj)}")
    print(next(my_gen_obj)) # This will raise StopIteration
except StopIteration:
    print("StopIteration caught as expected.")

print("\nIterating with a for loop (re-creating the generator):")
# For loop handles StopIteration automatically
for value in simple_generator():
    print(f"Value from for loop: {value}")
```
Output:
```
--- Simple Generator Function Example ---
Generator object: <generator object simple_generator at 0x...>
Generator started...
First value: 10
Generator resumed after first yield...
Second value: 20
Generator resumed after second yield...
Third value: 30
Generator finished.
StopIteration caught as expected.

Iterating with a for loop (re-creating the generator):
Generator started...
Value from for loop: 10
Generator resumed after first yield...
Value from for loop: 20
Generator resumed after second yield...
Value from for loop: 30
Generator finished.
```

**Example: Generating Squares (Memory Efficient)**

```python
# Example: Generator for squares
print("\n--- Generator for Squares Example ---")
def squares_generator(n):
    print(f"Initializing squares_generator up to {n-1}")
    for i in range(n):
        yield i * i # Pauses here and yields the square
        # Resumes here on next call to next()

# Using the squares generator
limit = 5
sq_gen = squares_generator(limit)
print(f"Generator object for squares: {sq_gen}")

print(f"\nSquares up to {limit-1}:")
for sq in sq_gen:
    print(sq)

# Example: Using a generator for a potentially large sequence
print("\n--- Squares up to 100 (stopping early) ---")
for num_sq in squares_generator(1000): # Potentially a million squares
    if num_sq > 100: # Corrected: > instead of &gt;
        break
    print(num_sq)
```
Output:
```
--- Generator for Squares Example ---
Initializing squares_generator up to 4
Generator object for squares: <generator object squares_generator at 0x...>

Squares up to 4:
0
1
4
9
16

--- Squares up to 100 (stopping early) ---
Initializing squares_generator up to 999
0
1
4
9
16
25
36
49
64
81
100
```

**Generator Objects:**

*   When you call a generator function, it doesn't execute the function body immediately. Instead, it returns a **generator object** (which is a type of iterator).
*   The code in the generator function is executed only when `next()` is called on the generator object.
*   Generator objects can be used in `for` loops or with `next()` directly.

```python
# Example: Using next() with a generator object
print("\n--- Using next() with Generator Object ---")
def simple_gen_for_next():
    yield "first"
    yield "second"

gen_obj_next = simple_gen_for_next()
print(f"Value from next(): {next(gen_obj_next)}") # In Python 3, it's just next()
print(f"Value from next(): {next(gen_obj_next)}")
# print(next(gen_obj_next)) # Would raise StopIteration
```
Output:
```
--- Using next() with Generator Object ---
Value from next(): first
Value from next(): second
```
A generator function returns a generator object that is iterable, i.e., it can be used as an iterator.

**Example: Fibonacci Sequence Generator**

```python
# Example: Fibonacci sequence generator
print("\n--- Fibonacci Sequence Generator ---")
def fibonacci_generator(limit):
    a, b = 0, 1          # Initialize first two Fibonacci numbers
    while a < limit:     # Loop as long as 'a' is less than the limit
        yield a          # Yield the current Fibonacci number 'a'
        a, b = b, a + b  # Update 'a' and 'b' for the next iteration

# Create a generator object for Fibonacci numbers up to 5
fib_gen = fibonacci_generator(5)
print(f"Fibonacci generator object: {fib_gen}")

print("\nFibonacci sequence (first few numbers using next()):")
# Iterating over the generator object using next()
# Note: Python 3 uses __next__() internally, but you call it with next()
try:
    print(next(fib_gen))
    print(next(fib_gen))
    print(next(fib_gen))
    print(next(fib_gen))
    print(next(fib_gen)) # This will be the last one before limit (5) is reached for 'a'
    print(next(fib_gen)) # This call will raise StopIteration
except StopIteration:
    print("StopIteration: No more Fibonacci numbers to generate within the limit.")

# Iterating over a new generator object using a for loop
print("\nFibonacci sequence (using for loop):")
for num in fibonacci_generator(5): # Creates a new generator object
    print(num)
```
Output:
```
--- Fibonacci Sequence Generator ---
Fibonacci generator object: <generator object fibonacci_generator at 0x...>

Fibonacci sequence (first few numbers using next()):
0
1
1
2
3
StopIteration: No more Fibonacci numbers to generate within the limit.

Fibonacci sequence (using for loop):
0
1
1
2
3
```

**Applications of Generators:**

*   **Memory Efficiency:** Ideal for working with large datasets or streams of data (e.g., reading large files line by line) because they only load one item into memory at a time.
*   **Infinite Sequences:** Can be used to represent infinite sequences (e.g., a counter that never ends) since values are generated on demand.
*   **Pipeline Data Processing:** Generators can be chained together to create efficient data processing pipelines.
*   **Simpler than Custom Iterators:** For many use cases, writing a generator function is much simpler than creating a custom iterator class with `__iter__()` and `__next__()`.

## Generator Expressions

Generator expressions offer a concise and memory-efficient way to create iterators. They are syntactically similar to list comprehensions but use parentheses `()` instead of square brackets `[]`.

**Key Characteristics:**

*   **Memory Efficiency:** Unlike list comprehensions, which create the entire list in memory at once, generator expressions produce items one at a time and only when requested (lazy evaluation). This makes them ideal for working with large datasets or infinite sequences.
*   **Lazy Evaluation:** Values are generated on-the-fly as you iterate over the generator. They are not all computed and stored in memory upfront.
*   **Iterator Protocol:** Generator expressions return a generator object, which is a type of iterator.

**Syntax:**

The basic syntax is very similar to a list comprehension, but with parentheses:

```python
(expression for item in iterable if condition)
```

*   `expression`: The expression to compute for each item.
*   `item`: The variable representing each element in the `iterable`.
*   `iterable`: The sequence or collection to iterate over.
*   `condition` (optional): A filter that only includes items for which the condition is true.

**Examples:**

#### 1. Simple Generator Expression for Squares

Let's create a generator for the squares of numbers.

```python
# List comprehension (creates a list in memory)
list_comp_squares = [x*x for x in range(5)]
print(f"List comprehension: {list_comp_squares}")

# Generator expression (creates a generator object)
gen_exp_squares = (x*x for x in range(5))
print(f"Generator expression object: {gen_exp_squares}")

print("\nIterating through the generator expression:")
for square in gen_exp_squares:
    print(square)
```
Output:
```
List comprehension: [0, 1, 4, 9, 16]
Generator expression object: <generator object <genexpr> at 0x...> # Address will vary
Iterating through the generator expression:
0
1
4
9
16
```
Notice that printing the generator expression itself shows a generator object, not the values. The values are produced when you iterate over it.

#### 2. Using with `sum()`, `min()`, `max()`

Generator expressions can be particularly useful when you want to perform an aggregation (like sum, min, max) on a sequence without materializing the entire sequence in memory.

```python
# Example: Summing squares using a generator expression
print("\n--- Summing with a generator expression ---")
sum_of_squares = sum(x*x for x in range(1, 1000001)) # Sum squares from 1 to 1,000,000
print(f"Sum of squares (1 to 1,000,000): {sum_of_squares}")
# This is memory efficient as it doesn't create a list of a million squares.

numbers = [10, 5, 20, 8, 15]
max_val_gen = max(n * 2 for n in numbers if n % 2 == 0) # Max of doubled even numbers
print(f"Max of doubled even numbers: {max_val_gen}")
```
Output:
```
--- Summing with a generator expression ---
Sum of squares (1 to 1,000,000): 333333833333500000
Max of doubled even numbers: 40
```

#### 3. Iterating with `next()`

Since a generator expression returns an iterator, you can use the `next()` function to get its items one by one.

```python
# Example: Iterating with next()
print("\n--- Iterating with next() ---")
gen_exp = (val for val in "Python")

print(next(gen_exp)) # P
print(next(gen_exp)) # y
print(next(gen_exp)) # t
# ... and so on
# If you call next() after all items are exhausted, it raises StopIteration
```
Output:
```
--- Iterating with next() ---
P
y
t
```

#### 4. Chaining Generator Expressions

Generator expressions can be chained for multi-step data processing pipelines that remain memory-efficient.

```python
# Example: Chaining generator expressions
print("\n--- Chaining generator expressions ---")
data = [1, 2, 3, 4, 5, 6, 7, 8]

# First, filter even numbers
evens = (x for x in data if x % 2 == 0)
# Next, square the even numbers
squared_evens = (x*x for x in evens) # This 'evens' is itself a generator

print("Squared even numbers from chained generators:")
for val in squared_evens:
    print(val)
```
Output:
```
--- Chaining generator expressions ---
Squared even numbers from chained generators:
4
16
36
64
```
Each step in the chain processes items lazily.

**When to Use Generator Expressions:**

*   When working with very large datasets where creating a full list in memory would be inefficient or impossible.
*   When you need to produce a sequence of items but only need to iterate over them once (e.g., for summing or processing in a loop).
*   For creating data processing pipelines that are memory-efficient.

Generator expressions are a key tool for writing memory-efficient and Pythonic code.

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

#### Comprehensive Example of Exception Handling

Let's consider a scenario where we try to process a list of numbers, performing division and potential type conversion.

```python
# Comprehensive Exception Handling Example
def process_data(data_list, divisor_str):
    results = []
    print(f"\n--- Processing with divisor: '{divisor_str}' ---")
    try:
        # Attempt to convert divisor to a float
        divisor = float(divisor_str)
        if divisor == 0:
            # Custom raise for a logical error not caught by standard exceptions
            raise ValueError("Divisor cannot be zero for logical reasons.")

        for item in data_list:
            try:
                # Attempt to convert item to a float
                item_float = float(item)
                result = item_float / divisor
                results.append(result)
                print(f"Processed {item_float} / {divisor} = {result}")

            # Specific exception for type conversion errors
            except ValueError as ve_item:
                print(f"Error converting item '{item}' to float: {ve_item}. Skipping.")
            # Specific exception for division by zero (though we raised a custom one earlier for the divisor itself)
            # This would catch if item_float was 0 and divisor was something else, leading to 0/non-zero which is fine,
            # but if we had item_float / 0 and `divisor` was not 0, this would be caught.
            except ZeroDivisionError:
                print(f"Error: Division by zero when processing item '{item}'. Skipping.")
            # Generic catch for other unexpected errors during item processing
            except Exception as e_item:
                print(f"An unexpected error occurred with item '{item}': {e_item}. Skipping.")

    # Specific exception for type conversion of the divisor
    except ValueError as ve_divisor:
        print(f"Error: Invalid divisor '{divisor_str}'. Not a valid number. Details: {ve_divisor}")
    # Catching any other exceptions related to initial setup or general processing
    except Exception as e_general:
        print(f"A general error occurred: {e_general}")

    # This block executes if the main try block (for divisor setup) completes without raising an exception
    else:
        print("All items in the list processed (or skipped due to item-specific errors).")
        if not results:
            print("No results were successfully calculated.")

    # This block always executes, regardless of exceptions in try, except, or else blocks
    finally:
        print("Data processing attempt finished.")
        if results:
            print(f"Successfully calculated results: {results}")
        else:
            print("No results were successfully calculated to display.")

# Test cases
print("--- Starting Exception Handling Demo ---")

# Valid case
process_data([10, 20, "30", 40], "2")

# Invalid item in data_list
process_data([10, "apple", 20], "5")

# Invalid divisor (cannot be converted to float)
process_data([10, 20], "banana")

# Divisor is zero (custom logical error)
process_data([10, 20], "0")

# Divisor becomes zero due to float conversion, but our custom check catches it first
process_data([10, 20], "0.0")

# Empty data list
process_data([], "5")
```

Output:
```
--- Starting Exception Handling Demo ---

--- Processing with divisor: '2' ---
Processed 10.0 / 2.0 = 5.0
Processed 20.0 / 2.0 = 10.0
Processed 30.0 / 2.0 = 15.0
Processed 40.0 / 2.0 = 20.0
All items in the list processed (or skipped due to item-specific errors).
Data processing attempt finished.
Successfully calculated results: [5.0, 10.0, 15.0, 20.0]

--- Processing with divisor: '5' ---
Processed 10.0 / 5.0 = 2.0
Error converting item 'apple' to float: could not convert string to float: 'apple'. Skipping.
Processed 20.0 / 5.0 = 4.0
All items in the list processed (or skipped due to item-specific errors).
Data processing attempt finished.
Successfully calculated results: [2.0, 4.0]

--- Processing with divisor: 'banana' ---
Error: Invalid divisor 'banana'. Not a valid number. Details: could not convert string to float: 'banana'
Data processing attempt finished.
No results were successfully calculated to display.

--- Processing with divisor: '0' ---
Error: Invalid divisor '0'. Not a valid number. Details: Divisor cannot be zero for logical reasons.
Data processing attempt finished.
No results were successfully calculated to display.

--- Processing with divisor: '0.0' ---
Error: Invalid divisor '0.0'. Not a valid number. Details: Divisor cannot be zero for logical reasons.
Data processing attempt finished.
No results were successfully calculated to display.

--- Processing with divisor: '5' ---
All items in the list processed (or skipped due to item-specific errors).
No results were successfully calculated.
Data processing attempt finished.
No results were successfully calculated to display.
```
This example illustrates:
*   Nested `try-except` blocks.
*   Catching specific exceptions (`ValueError`, `ZeroDivisionError`).
*   Catching general exceptions (`Exception`).
*   Using `else` to run code when no exceptions occur in the main `try` block.
*   Using `finally` to run cleanup code regardless of what happened.
*   Using `raise` to trigger an exception programmatically.

## Function Decorators

Decorators are a very powerful and useful tool in Python that allow programmers to modify the behavior of a function or class without permanently changing its source code. They enable you to wrap another function (the "decorated" function) to extend its functionality, often by adding setup or teardown code.

To understand decorators, it's important to grasp that functions in Python are **first-class objects**.

### First-Class Objects (Functions in Python)

In Python, functions have the following properties, making them first-class objects:
*   **Instances of Object Type:** A function is an instance of the `Object` type.
*   **Storable in Variables:** You can assign a function to a variable.
*   **Passable as Arguments:** You can pass a function as an argument to another function.
*   **Returnable from Functions:** A function can return another function.
*   **Storable in Data Structures:** You can store functions in lists, dictionaries, etc.

**Example 1: Storing a function in a variable**
```python
# Python program to illustrate functions can be treated as objects
print("--- Function as an Object Example ---")
def shout(text):
    return text.upper()

print(f"Output of shout('Hello'): {shout('Hello')}")

# Assigning the function shout to a variable yell
yell = shout
# Now, yell can be used just like shout
print(f"Output of yell('Hello'): {yell('Hello')}")
```
Output:
```
--- Function as an Object Example ---
Output of shout('Hello'): HELLO
Output of yell('Hello'): HELLO
```

**Example 2: Passing a function as an argument**
```python
# Python program to illustrate functions can be passed as arguments
print("\n--- Passing Function as Argument Example ---")
def shout_text(text):
    return text.upper()

def whisper_text(text):
    return text.lower()

def greet_user(modifier_func): # modifier_func is expected to be a function
    # Call the passed function and store its result
    message = modifier_func("Hi, I am created by a function passed as an argument.")
    print(message)

greet_user(shout_text)   # Pass the shout_text function
greet_user(whisper_text) # Pass the whisper_text function
```
Output:
```
--- Passing Function as Argument Example ---
HI, I AM CREATED BY A FUNCTION PASSED AS AN ARGUMENT.
hi, i am created by a function passed as an argument.
```
Here, `greet_user` takes another function (`shout_text` or `whisper_text`) as an argument and calls it.

**Example 3: Returning a function from another function**
```python
# Python program to illustrate a function returning another function
print("\n--- Function Returning Another Function Example ---")
def create_adder_function(x):
    """This function creates and returns a new function (adder)."""
    def adder(y):
        """This inner function adds x (from outer scope) to y."""
        return x + y
    return adder # Return the inner function itself, not its result

# Create an "add_15" function:
# When create_adder_function(15) is called, it returns the 'adder' function,
# where 'x' is fixed at 15 due to closure.
add_15 = create_adder_function(15)

# Now, add_15 is a function that takes one argument (y) and adds 15 to it.
result = add_15(10) # This calls the inner 'adder' function with y=10 (and x=15)
print(f"Result of add_15(10): {result}") # Output: 25
```
Output:
```
--- Function Returning Another Function Example ---
Result of add_15(10): 25
```
The `create_adder_function` returns the `adder` function. This concept of functions remembering their lexical scope (like `x` in `adder`) is called a closure, which is closely related to decorators.

### Decorators Explained

Decorators are functions that take another function as input (the decorated function), add some functionality to it, and then return the modified function (or a new function that wraps the original). This is done without explicitly altering the source code of the decorated function.

**Syntax for Decorators:**

The `@` symbol is used as syntactic sugar for applying a decorator.

```python
@my_decorator
def say_hello():
    print("Hello!")
```

This is equivalent to:

```python
def say_hello():
    print("Hello!")

say_hello = my_decorator(say_hello)
```
In both cases, `my_decorator` is a function that takes `say_hello` as an argument and returns a new function (or a modified version of `say_hello`). This returned function is then assigned back to the name `say_hello`.

**A Simple Decorator Example:**

Let's create a decorator that adds a welcome message to any function that returns a string.

```python
# Decorator function
print("\n--- Basic Decorator Example ---")
def welcome_decorator(original_function):
    """
    This is the decorator function. It takes another function
    (original_function) as an argument.
    """
    def wrapper_function(*args, **kwargs):
        """
        This is the wrapper function. It gets executed when the
        decorated function is called.
        It can access arguments passed to the original_function.
        """
        print("Wrapper executed before calling", original_function.__name__)
        # Call the original function and get its result
        result = original_function(*args, **kwargs)
        # Add new behavior
        return f"Welcome to {result}!"

    # The decorator returns the wrapper function
    return wrapper_function

# Applying the decorator using @ syntax
@welcome_decorator
def get_website_name(name):
    """This function returns a website name."""
    print(f"  Inside get_website_name({name})")
    return name

# Calling the decorated function
# This actually calls the 'wrapper_function' returned by 'welcome_decorator'
output = get_website_name("GeeksforGeeks")
print(f"Output after decoration: {output}")

# Without @ syntax (manual decoration)
def get_another_site(name):
    print(f"  Inside get_another_site({name})")
    return name

print("\n--- Manual Decoration Example ---")
manually_decorated_site = welcome_decorator(get_another_site)
manual_output = manually_decorated_site("TutorialsPoint")
print(f"Output from manual decoration: {manual_output}")
```
Output:
```
--- Basic Decorator Example ---
Wrapper executed before calling get_website_name
  Inside get_website_name(GeeksforGeeks)
Output after decoration: Welcome to GeeksforGeeks!

--- Manual Decoration Example ---
Wrapper executed before calling get_another_site
  Inside get_another_site(TutorialsPoint)
Output from manual decoration: Welcome to TutorialsPoint!
```
**Explanation of the example:**
1.  `welcome_decorator` is our decorator. It takes `original_function` (which will be `get_website_name`) as an argument.
2.  Inside `welcome_decorator`, we define `wrapper_function`. This function will eventually replace `get_website_name`.
    *   `*args` and `**kwargs` in `wrapper_function` ensure it can accept any positional or keyword arguments that the `original_function` might take.
    *   The wrapper prints a message, calls the `original_function` with its arguments, modifies its result, and returns the modified result.
3.  `welcome_decorator` returns `wrapper_function`.
4.  When `@welcome_decorator` is placed above `def get_website_name`, Python effectively does: `get_website_name = welcome_decorator(get_website_name)`.
5.  So, when `get_website_name("GeeksforGeeks")` is called, it's actually `wrapper_function("GeeksforGeeks")` that executes.

**Decorators for Attaching Data (Attributes) to Functions:**

Decorators can also be used to add attributes to functions, although this is less common than behavior modification.

```python
# Example: Decorator to attach data to a function
print("\n--- Decorator for Attaching Data ---")
def attach_metadata(func_to_decorate):
    """Decorator to add a 'version' attribute to a function."""
    func_to_decorate.version = "1.0" # Add an attribute to the function object
    return func_to_decorate

@attach_metadata
def calculate_sum(x, y):
    """This function calculates the sum of two numbers."""
    return x + y

# Call the function
sum_result = calculate_sum(10, 5)
print(f"Result of calculate_sum(10, 5): {sum_result}")

# Access the attribute added by the decorator
print(f"Version of calculate_sum function: {calculate_sum.version}")
```
Output:
```
--- Decorator for Attaching Data ---
Result of calculate_sum(10, 5): 15
Version of calculate_sum function: 1.0
```
In this case, `attach_metadata` directly modifies the passed function object by adding an attribute and then returns the same function object.

Python decorators are a powerful feature for code reuse and separation of concerns, allowing you to add functionality like logging, access control, instrumentation, and more to functions and methods in a clean and readable way.

Date : 01 Aug 2022

__________________

## Regular Expressions in Python

A **Regular Expression** (often shortened to RegEx or RE) is a special sequence of characters that defines a search pattern. This pattern is used to find, match, or manage specific parts of a string or a set of strings. Regular expressions are incredibly versatile for tasks like data validation, searching, splitting, and replacing text.

Python provides the `re` module to work with regular expressions. The core idea is to define a pattern and then use functions from the `re` module to apply this pattern to a target string.

**Basic Example: Searching for a word**

```python
import re # Import the regular expressions module

# Sample string
s = 'GeeksforGeeks: A computer science portal for geeks'

# Search for the word 'portal' in the string 's'
# r'portal' is a raw string. Using 'r' prefix is highly recommended for regex patterns
# to avoid issues with backslashes being interpreted as escape sequences by Python.
match_object = re.search(r'portal', s)

if match_object: # If a match is found, search() returns a match object
    print(f"Found '{match_object.group()}'") # .group() returns the matched string
    print(f"Start Index: {match_object.start()}") # .start() returns the starting index of the match
    print(f"End Index: {match_object.end()}")     # .end() returns the ending index (exclusive) of the match
else:
    print("No match found.")
```
Output:
```
Found 'portal'
Start Index: 34
End Index: 40
```
In this example, `re.search(r'portal', s)` attempts to find the pattern `portal` within the string `s`. If found, it returns a "match object" containing information about the match; otherwise, it returns `None`.

**Raw Strings (`r''`):**
Notice the `r` before the pattern string (e.g., `r'portal'`). This denotes a **raw string literal**. In raw strings, backslashes (`\`) are treated as literal characters and not as escape characters. This is crucial because regular expressions themselves use backslashes for special meanings (e.g., `\d` for digit), and using raw strings prevents Python from misinterpreting these backslashes before they reach the regex engine.

### Metacharacters

Metacharacters are special characters that have a unique meaning within a regular expression pattern. They are the building blocks for creating powerful search patterns.

| Metacharacter | Description                                                                 | Example Pattern | Sample Matches                    |
|---------------|-----------------------------------------------------------------------------|-----------------|-----------------------------------|
| `\`           | **Escape Character:** Escapes the special meaning of a metacharacter, or signals a special sequence. | `\.`            | Matches a literal dot `.`         |
| `[]`          | **Character Set:** Matches any single character from the set.               | `[aeiou]`       | `a`, `e`, `o` (in "apple")        |
| `^`           | **Start of String (or Line):** Matches the beginning of the string (or line if `re.MULTILINE` is used). | `^Hello`        | "Hello world"                     |
| `$`           | **End of String (or Line):** Matches the end of the string (or line if `re.MULTILINE` is used).   | `world$`        | "Hello world"                     |
| `.`           | **Any Character (except newline):** Matches any single character except `\n`. | `a.b`           | `acb`, `a!b`, `a_b`               |
| `\|`          | **OR:** Matches either the expression before or after the pipe.             | `cat\|dog`      | "cat", "dog"                      |
| `?`           | **Zero or One Occurrence:** Matches the preceding element zero or one time.   | `colou?r`       | "color", "colour"                 |
| `*`           | **Zero or More Occurrences:** Matches the preceding element zero or more times. | `ab*c`          | `ac`, `abc`, `abbbc`              |
| `+`           | **One or More Occurrences:** Matches the preceding element one or more times.   | `ab+c`          | `abc`, `abbbc` (but not `ac`)     |
| `{m}`         | **Exactly `m` Occurrences:** Matches exactly `m` occurrences of the preceding element. | `a{3}`          | `aaa`                             |
| `{m,n}`       | **`m` to `n` Occurrences:** Matches `m` to `n` occurrences of the preceding element. | `a{2,4}`        | `aa`, `aaa`, `aaaa`               |
| `()`          | **Group:** Groups sub-patterns. Captures the matched text for later use.    | `(a\|b)c`       | `ac`, `bc`                        |

---
**Detailed Explanations of Metacharacters:**

#### `\` – Backslash (Escape Character)
*   **Purpose:** Used to "escape" the special meaning of a metacharacter, treating it as a literal character. It's also used to signal special sequences (like `\d` for digit).
*   **Example:** To match a literal dot `.` (which normally means "any character"), you use `\.`.
    ```python
    import re
    s = 'geeks.forgeeks'

    # '.' matches any character (here, 'g')
    match_any = re.search(r'.', s)
    print(f"Search for '.': {match_any}") # Output: <_sre.SRE_Match object; span=(0, 1), match='g'>

    # '\.' matches the literal dot character
    match_literal_dot = re.search(r'\.', s)
    print(f"Search for '\.': {match_literal_dot}") # Output: <_sre.SRE_Match object; span=(5, 6), match='.'>
    ```

#### `[]` – Character Set (Square Brackets)
*   **Purpose:** Defines a set of characters, any one of which can match at that position in the string.
*   **Examples:**
    *   `[aeiou]` matches any lowercase vowel.
    *   `[0123456789]` or `[0-9]` matches any digit.
    *   `[a-zA-Z]` matches any uppercase or lowercase letter.
    *   `[^0-9]` (with `^` inside `[]`) matches any character that is NOT a digit (negation).
    *   `[.-]` matches a literal dot or hyphen. Inside a character set, most metacharacters lose their special meaning (e.g., `.` means literal dot, `*` means literal asterisk). However, `^` (at the start for negation), `-` (for ranges), and `\` (for escaping) are still special.
    ```python
    import re
    text = "The quick brown fox jumps over 1 lazy dog."
    vowels = re.findall(r'[aeiou]', text) # Find all lowercase vowels
    print(f"Vowels: {vowels}") # Output: ['e', 'u', 'i', 'o', 'o', 'u', 'o', 'e', 'a', 'o']

    non_digits = re.findall(r'[^0-9]', text) # Find all non-digit characters
    # print(f"Non-digits: {''.join(non_digits)}")
    ```

#### `^` – Caret (Start of String/Line)
*   **Purpose:** Matches the beginning of the string. If the `re.MULTILINE` flag is used, it matches the beginning of each line.
*   **Examples:**
    *   `^Hello` matches "Hello world" but not "Say Hello".
    ```python
    import re
    print(f"Match '^Geeks': {re.search(r'^Geeks', 'GeeksforGeeks')}") # Matches
    print(f"Match '^Geeks': {re.search(r'^Geeks', 'A Geeks')}")      # No match
    ```

#### `$` – Dollar (End of String/Line)
*   **Purpose:** Matches the end of the string. If the `re.MULTILINE` flag is used, it matches the end of each line (before the newline).
*   **Examples:**
    *   `world$` matches "Hello world" but not "world say hello".
    ```python
    import re
    print(f"Match 'geeks$': {re.search(r'geeks$', 'computergeeks')}") # Matches
    print(f"Match 'geeks$': {re.search(r'geeks$', 'geeks portal')}")  # No match
    ```

#### `.` – Dot (Any Character Except Newline)
*   **Purpose:** Matches any single character except a newline (`\n`). If the `re.DOTALL` flag is used, it will also match a newline.
*   **Examples:**
    *   `a.b` matches `aab`, `axb`, `a!b`, etc.
    *   `..` matches any two characters (e.g., "hi", "00", "a ").
    ```python
    import re
    print(f"Match 'h.t': {re.search(r'h.t', 'hat')}")  # Matches 'hat'
    print(f"Match 'h.t': {re.search(r'h.t', 'hot')}")  # Matches 'hot'
    print(f"Match 'h.t': {re.search(r'h.t', 'ht')}")   # No match (needs a char in between)
    ```

#### `|` – OR (Alternation)
*   **Purpose:** Acts like a boolean OR. Matches the expression before OR the expression after the `|`.
*   **Examples:**
    *   `cat|dog` matches "cat" or "dog".
    *   `^(cat|dog)$` matches "cat" or "dog" as the entire string.
    ```python
    import re
    print(f"Match 'apple|orange': {re.search(r'apple|orange', 'I like apples')}") # Matches 'apple'
    print(f"Match 'apple|orange': {re.search(r'apple|orange', 'I like oranges')}")# Matches 'orange'
    ```

#### `?` – Question Mark (Zero or One Occurrence)
*   **Purpose:** Makes the preceding character or group optional (matches it zero or one time).
*   **Examples:**
    *   `colou?r` matches "color" (zero 'u's) and "colour" (one 'u').
    *   `ab?c` matches "ac" or "abc". It will not match "abbc".
    ```python
    import re
    print(f"Match 'honou?r': {re.search(r'honou?r', 'honor')}")  # Matches 'honor'
    print(f"Match 'honou?r': {re.search(r'honou?r', 'honour')}") # Matches 'honour'
    ```

#### `*` – Star (Zero or More Occurrences)
*   **Purpose:** Matches the preceding character or group zero or more times.
*   **Examples:**
    *   `ab*c` matches "ac" (zero 'b's), "abc" (one 'b'), "abbc" (multiple 'b's).
    *   `.*` matches any sequence of characters (except newlines, unless `re.DOTALL`).
    ```python
    import re
    print(f"Match 'ab*c': {re.search(r'ab*c', 'ac')}")    # Matches 'ac'
    print(f"Match 'ab*c': {re.search(r'ab*c', 'abc')}")   # Matches 'abc'
    print(f"Match 'ab*c': {re.search(r'ab*c', 'abbbc')}") # Matches 'abbbc'
    ```

#### `+` – Plus (One or More Occurrences)
*   **Purpose:** Matches the preceding character or group one or more times.
*   **Examples:**
    *   `ab+c` matches "abc", "abbc", but NOT "ac" (requires at least one 'b').
    ```python
    import re
    print(f"Match 'ab+c': {re.search(r'ab+c', 'abc')}")   # Matches 'abc'
    print(f"Match 'ab+c': {re.search(r'ab+c', 'abbbc')}") # Matches 'abbbc'
    print(f"Match 'ab+c': {re.search(r'ab+c', 'ac')}")    # No match
    ```

#### `{m,n}` – Braces (Specific Number of Occurrences)
*   **Purpose:** Specifies the number of occurrences for the preceding character or group.
    *   `{m}`: Exactly `m` occurrences. (e.g., `\d{5}` matches exactly 5 digits).
    *   `{m,}`: At least `m` occurrences. (e.g., `a{2,}` matches "aa", "aaa", etc.).
    *   `{m,n}`: Between `m` and `n` occurrences, inclusive. (e.g., `a{2,4}` matches "aa", "aaa", "aaaa").
    ```python
    import re
    print(f"Match 'a{{2,3}}': {re.search(r'a{2,3}', 'aa')}")     # Matches 'aa'
    print(f"Match 'a{{2,3}}': {re.search(r'a{2,3}', 'aaa')}")    # Matches 'aaa'
    print(f"Match 'a{{2,3}}': {re.search(r'a{2,3}', 'aaaa')}")   # Matches 'aaa' from 'aaaa'
    print(f"Match 'a{{2,3}}': {re.search(r'a{2,3}', 'a')}")      # No match
    ```

#### `()` – Group (Parentheses)
*   **Purpose:**
    1.  **Groups sub-patterns:** Allows you to apply quantifiers (like `*`, `+`, `?`, `{}`) to a whole group. E.g., `(ab)+` matches "ab", "abab", "ababab".
    2.  **Captures matches:** Text matched by a group can be captured for later use (e.g., with `match.group(index)` or backreferences like `\1`).
*   **Example:**
    *   `(a|b)c` matches "ac" or "bc". The group `(a|b)` matches "a" or "b".
    *   `(\d{3})-(\d{3})-(\d{4})` can capture parts of a phone number.
    ```python
    import re
    match = re.search(r'(\w+)-(\d+)', 'item-123')
    if match:
        print(f"Full match: {match.group(0)}") # Output: item-123
        print(f"Group 1: {match.group(1)}")    # Output: item
        print(f"Group 2: {match.group(2)}")    # Output: 123
    ```

---
### Special Sequences

Special sequences start with a backslash `\` followed by a character. They act as shortcuts for commonly used character sets or represent special positions.

| Sequence | Description                                        | Equivalent to    | Example Usage                     |
|----------|----------------------------------------------------|------------------|-----------------------------------|
| `\A`     | Matches only at the **start** of the string.       | (Similar to `^` but not affected by `re.MULTILINE`) | `\AHello` matches "Hello world"   |
| `\b`     | **Word Boundary:** Matches the empty string, but only at the beginning or end of a word. A word is a sequence of word characters. |                  | `\bcat\b` matches "cat" in "the cat sat" but not in "catalog". |
| `\B`     | **Non-Word Boundary:** Matches the empty string, but only when it is NOT at the beginning or end of a word. |                  | `\Bcat\B` matches "cat" in "catalog" but not in "the cat sat". |
| `\d`     | **Digit:** Matches any decimal digit.              | `[0-9]`          | `\d\d` matches "12"               |
| `\D`     | **Non-Digit:** Matches any non-digit character.    | `[^0-9]`         | `\D\D` matches "ab"               |
| `\s`     | **Whitespace:** Matches any whitespace character.  | `[ \t\n\r\f\v]`  | `\s+` matches one or more spaces |
| `\S`     | **Non-Whitespace:** Matches any non-whitespace character. | `[^ \t\n\r\f\v]` | `\S+` matches words             |
| `\w`     | **Word Character:** Matches any alphanumeric character (letters, numbers) plus underscore. | `[a-zA-Z0-9_]`   | `\w+` matches "word_123"        |
| `\W`     | **Non-Word Character:** Matches any character that is not a word character. | `[^a-zA-Z0-9_]`  | `\W` matches "!", "@", " "      |
| `\Z`     | Matches only at the **end** of the string.         | (Similar to `$` but not affected by `re.MULTILINE` for `\n` at end) | `world\Z` matches "Hello world" |

**Example of `\b` (Word Boundary):**
```python
import re
text = "This is a catalog of cats."
print(f"Matches for r'cat': {re.findall(r'cat', text)}")             # Output: ['cat', 'cat']
print(f"Matches for r'\bcat\b': {re.findall(r'\bcat\b', text)}") # Output: ['cat'] (only the whole word)
```

---
### `re` Module Functions

Python's `re` module provides several functions to work with regular expressions.

#### `re.findall(pattern, string, flags=0)`
*   **Purpose:** Finds all non-overlapping occurrences of the `pattern` in the `string` and returns them as a list of strings.
*   **Behavior:**
    *   The string is scanned from left to right.
    *   Matches are returned in the order they are found.
    *   If the pattern includes capturing groups, the list will contain tuples of the captured groups. If there's only one group, the list contains strings of that group's matches. If no groups, the list contains the full pattern matches.
*   **Syntax:**
    ```python
    re.findall(pattern, string, flags=0)
    ```
    *   `pattern`: The regular expression to match.
    *   `string`: The string to search within.
    *   `flags` (optional): Modifiers like `re.IGNORECASE`, `re.MULTILINE`, `re.DOTALL`.

**Example: Finding all digits or words**
```python
import re

text = "Hello my Number is 12345 and my friend's number is 98765."

# Find all sequences of digits
digits = re.findall(r'\d+', text)
print(f"Digits found: {digits}") # Output: ['12345', '98765']

# Find all sequences of word characters (words)
words = re.findall(r'\w+', text)
print(f"Words found: {words}")
# Output: ['Hello', 'my', 'Number', 'is', '12345', 'and', 'my', 'friend', 's', 'number', 'is', '98765']

# Example with capturing groups:
# If the pattern has groups, findall returns a list of tuples (the groups)
emails = "user1@example.com, user2@test.org"
# Pattern with two groups: (username)@(domain_part)
email_parts = re.findall(r'([\w.-]+)@([\w.-]+)', emails)
print(f"Email parts: {email_parts}")
# Output: [('user1', 'example.com'), ('user2', 'test.org')]
# If you only want the full email, use a non-capturing group (?:...) or no group for the whole match.
full_emails = re.findall(r'[\w.-]+@[\w.-]+', emails) # No capturing groups
print(f"Full emails: {full_emails}")
# Output: ['user1@example.com', 'user2@test.org']
```

#### `re.compile(pattern, flags=0)`
*   **Purpose:** Compiles a regular expression pattern into a **pattern object**. This allows the pattern to be reused efficiently without recompiling it each time it's needed.
*   **Benefit:** If you intend to use the same regex multiple times in your code, compiling it once upfront can improve performance. The resulting pattern object has methods for matching (e.g., `match()`, `search()`, `findall()`) that are equivalent to the `re` module functions.
*   **Syntax:**
    ```python
    re.compile(pattern, flags=0)
    ```
    *   `pattern`: The regular expression string.
    *   `flags` (optional): Same flags as in other `re` functions.

**Example: Using `re.compile()`**
```python
import re

# Compile a pattern to find words starting with 'c' (case-insensitive)
# Case-insensitive matching due to re.IGNORECASE
pattern_obj = re.compile(r'\bc\w*', re.IGNORECASE)

text1 = "Cats, dogs, and chickens are common."
text2 = "A Cute cat."

# Use the compiled pattern object's findall() method
print(f"Matches in text1: {pattern_obj.findall(text1)}") # Output: ['Cats', 'chickens', 'common']
print(f"Matches in text2: {pattern_obj.findall(text2)}") # Output: ['Cute', 'cat']

# Example: Compiling a pattern for digits
digit_pattern = re.compile(r'\d+')
print(f"Digits in 'Year 2024, Month 07': {digit_pattern.findall('Year 2024, Month 07')}") # Output: ['2024', '07']
```
**Understanding the Output of `p.findall("Aye, said Mr. Gibenson Stark")` with `p = re.compile('[a-e]')`:**
*   The pattern `[a-e]` matches any single lowercase character from 'a' through 'e'.
*   `findall` returns a list of all non-overlapping matches.
*   "A**ye**, **sa**i**d** Mr. Gi**be**n**s**on St**a**r**k**"
    *   'e' in "Aye" (Note: 'A' is not matched because the pattern is case-sensitive by default).
    *   'a' in "said".
    *   'd' in "said".
    *   'b' in "Gibenson".
    *   'e' in "Gibenson".
    *   'a' in "Stark".
    Result: `['e', 'a', 'd', 'b', 'e', 'a']`

**Example: `\w` vs `\w+` vs `\W` with `compile()`**
```python
import re

# \w matches a single word character (alphanumeric or underscore)
p_single_w = re.compile(r'\w')
print(f"Single word chars in 'He said *': {p_single_w.findall('He said * in some_lang.')}")
# Output: ['H', 'e', 's', 'a', 'i', 'd', 'i', 'n', 's', 'o', 'm', 'e', '_', 'l', 'a', 'n', 'g']

# \w+ matches one or more consecutive word characters (i.e., words)
p_multi_w = re.compile(r'\w+')
print(f"Words in 'I went to him...': {p_multi_w.findall('I went to him at 11 A.M., he said *** in some_language.')}")
# Output: ['I', 'went', 'to', 'him', 'at', '11', 'A', 'M', 'he', 'said', 'in', 'some_language']

# \W matches a single non-word character
p_non_w = re.compile(r'\W')
print(f"Non-word chars in 'he said ***': {p_non_w.findall('he said *** in some_language.')}")
# Output: [' ', ' ', '*', '*', '*', ' ', ' ', '.']
```

**Example: `ab*` with `compile()`**
The pattern `ab*` means: an 'a', followed by zero or more 'b's.
```python
import re
p_ab_star = re.compile(r'ab*')
test_string = "ababbaabbb"
# Matches:
# 1. 'ab' at index 0
# 2. 'abb' at index 2
# 3. 'a' at index 5 (here 'b*' matches zero 'b's)
# 4. 'abbb' at index 6
print(f"Matches for 'ab*' in '{test_string}': {p_ab_star.findall(test_string)}")
# Output: ['ab', 'abb', 'a', 'abbb']
```

---
#### `re.split(pattern, string, maxsplit=0, flags=0)`
*   **Purpose:** Splits the `string` by the occurrences of the `pattern`.
*   **Behavior:** Returns a list of strings. If capturing parentheses `()` are used in `pattern`, then the text of all groups in the pattern are also returned as part of the resulting list.
*   **Syntax:**
    ```python
    re.split(pattern, string, maxsplit=0, flags=0)
    ```
    *   `maxsplit`: If non-zero, at most `maxsplit` splits are performed, and the remainder of the string is returned as the final element of the list. `maxsplit=0` (default) means no limit on splits.
    *   `flags`: Optional flags like `re.IGNORECASE`.

**Examples:**
```python
import re # Use import re once at the top of your script normally

# Splitting by non-alphanumeric characters
# \W+ matches one or more non-alphanumeric characters (e.g., ',', ' ').
# The parts of the string *between* these delimiters are returned.
print(f"Split 'Words, words , Words' by '\\W+': {re.split(r'\W+', 'Words, words , Words')}")
# Output: ['Words', 'words', 'Words']

# Note on "Word's words Words":
# ' (apostrophe) is a non-alphanumeric character.
# So, \W+ matches the apostrophe in "Word's", splitting "Word's" into "Word" and "s".
# It also matches the space.
print(f"Split 'Word's words Words' by '\\W+': {re.split(r'\W+', "Word's words Words")}")
# Output: ['Word', 's', 'words', 'Words']

# Splitting a more complex string by non-alphanumeric characters
print(f"Split 'On 12th Jan 2016, at 11:02 AM' by '\\W+': {re.split(r'\W+', 'On 12th Jan 2016, at 11:02 AM')}")
# Output: ['On', '12th', 'Jan', '2016', 'at', '11', '02', 'AM']

# Splitting by digits (\d+ matches one or more digits)
# The parts of the string *between* the digit sequences are returned.
print(f"Split 'On 12th Jan 2016, at 11:02 AM' by '\\d+': {re.split(r'\d+', 'On 12th Jan 2016, at 11:02 AM')}")
# Output: ['On ', 'th Jan ', ', at ', ':', ' AM']

# Using maxsplit
# Splits only at the first occurrence of one or more digits ('12').
print(f"Split with maxsplit=1: {re.split(r'\d+', 'On 12th Jan 2016, at 11:02 AM', 1)}")
# Output: ['On ', 'th Jan 2016, at 11:02 AM']

# Using flags (re.IGNORECASE)
# The pattern [a-f]+ will match both 'a'-'f' and 'A'-'F'.
text_mixed_case = "Aey, Boy oh Boy, come Here"
print(f"Split '{text_mixed_case}' by '[a-f]+' (IGNORECASE): {re.split(r'[a-f]+', text_mixed_case, flags=re.IGNORECASE)}")
# Output: ['', 'y, ', 'oy oh ', 'oy, ', 'om', ' H', 'r', '']
# Explanation of empty strings in output:
# - 'A' in 'Aey' is matched by '[a-f]+' (ignorecase). The part *before* 'A' is an empty string.
# - 'e' in 'Aey' is matched.
# - 'B' and 'o' in 'Boy' are not matched by '[a-f]+'.
# - 'o' in 'oh' is not matched.
# - 'B' and 'o' in 'Boy' are not matched.
# - 'c', 'o', 'm', 'e' in 'come' are matched.
# - 'H' in 'Here' is not matched.
# - 'e', 'r', 'e' in 'Here' are matched. The part *after* the last 'e' (before end of string) is an empty string.

print(f"Split '{text_mixed_case}' by '[a-f]+' (case-sensitive): {re.split(r'[a-f]+', text_mixed_case)}")
# Output: ['A', 'y, Boy oh ', 'oy, ', 'om', ' H', 'r', '']
# Here 'A', 'B', 'H' are not splitters because they are uppercase.
```

---
#### `re.sub(pattern, repl, string, count=0, flags=0)`
*   **Purpose:** Replaces the leftmost non-overlapping occurrences of `pattern` in `string` with the replacement `repl`.
*   **Behavior:** If the pattern isn't found, the string is returned unchanged. `repl` can be a string or a function. If `repl` is a string, any backslash escapes in it are processed (e.g., `\n` becomes a newline, `\1` refers to group 1 from the match).
*   **Syntax:**
    ```python
    re.sub(pattern, repl, string, count=0, flags=0)
    ```
    *   `pattern`: The regular expression to find.
    *   `repl`: The string or function to replace the matched pattern with.
    *   `string`: The string to perform the replacement on.
    *   `count`: Maximum number of pattern occurrences to replace. `0` (default) means replace all occurrences.
    *   `flags`: Optional flags like `re.IGNORECASE`.

**Examples:**
```python
import re

# Case-insensitive substitution
# Replaces 'ub' or 'Ub' with '~*'
print(f"Sub 'ub' with '~*' (IGNORECASE): {re.sub('ub', '~*', 'Subject has Uber booked already', flags=re.IGNORECASE)}")
# Output: S~*ject has ~*er booked already

# Case-sensitive substitution
# Only replaces 'ub', not 'Ub'
print(f"Sub 'ub' with '~*' (case-sensitive): {re.sub('ub', '~*', 'Subject has Uber booked already')}")
# Output: S~*ject has Uber booked already

# Using count to limit replacements
# Replaces only the first occurrence of 'ub' or 'Ub'
print(f"Sub 'ub' with '~*' (IGNORECASE, count=1): {re.sub('ub', '~*', 'Subject has Uber booked already', count=1, flags=re.IGNORECASE)}")
# Output: S~*ject has Uber booked already

# Replacing ' AND ' (with spaces around it) with ' & ', case-insensitive
# The r'\sAND\s' pattern ensures that 'AND' as a whole word is matched (surrounded by spaces).
print(f"Sub r'\sAND\s' with ' & ': {re.sub(r'\sAND\s', ' & ', 'Baked Beans And Spam', flags=re.IGNORECASE)}")
# Output: Baked Beans & Spam
```

---
#### `re.subn(pattern, repl, string, count=0, flags=0)`
*   **Purpose:** Performs the same function as `re.sub()`, but returns a tuple `(new_string, number_of_subs_made)`.
*   **Syntax:**
    ```python
    re.subn(pattern, repl, string, count=0, flags=0)
    ```

**Example:**
```python
import re

# Perform substitution and get the count of replacements
result_tuple = re.subn('ub', '~*', 'Subject has Uber booked already')
print(f"subn result (case-sensitive): {result_tuple}")
# Output: ('S~*ject has Uber booked already', 1)
# (The new string, number of substitutions)

result_tuple_ignorecase = re.subn('ub', '~*', 'Subject has Uber booked already', flags=re.IGNORECASE)
print(f"subn result (IGNORECASE): {result_tuple_ignorecase}")
# Output: ('S~*ject has ~*er booked already', 2)

# Accessing parts of the tuple
print(f"The new string: {result_tuple_ignorecase[0]}")
# Output: S~*ject has ~*er booked already
print(f"Number of substitutions: {result_tuple_ignorecase[1]}")
# Output: 2
```

---
#### `re.escape(pattern)`
*   **Purpose:** Escapes any special characters in the `pattern` string (treats them as literals rather than regex metacharacters). This is useful if you need to dynamically build a regex from a string that might itself contain characters special to regex, and you want to match them literally.
*   **Syntax:**
    ```python
    re.escape(string_to_escape)
    ```

**Example:**
```python
import re

# String with characters that are special in regex (e.g., '.', '[', ']', '*', '+', '?')
literal_string = "example.com [v1.0*] + (main branch)?"
escaped_string = re.escape(literal_string)

print(f"Original: {literal_string}")
# Original: example.com [v1.0*] + (main branch)?

print(f"Escaped: {escaped_string}")
# Escaped: example\.com\ \[v1\.0\*\]\ \+\ \(main\ branch\)\?
# Note how '.', '[', ']', '*', '+', '(', ')', '?' are now backslashed.

# Now, escaped_string can be safely used as part of a larger regex pattern
# if you want to match the literal_string exactly.
text_to_search = "Please visit example.com [v1.0*] + (main branch)? for details."
match = re.search(escaped_string, text_to_search)
print(f"Search result using escaped string: {match}")
# Output: <re.Match object; span=(13, 49), match='example.com [v1.0*] + (main branch)?'>
```

---
#### `re.search(pattern, string, flags=0)`
*   **Purpose:** Scans through `string` looking for the **first location** where the `pattern` produces a match.
*   **Behavior:** Returns a **match object** if a match is found anywhere in the string, otherwise returns `None`. It stops after the first match, making it suitable for checking if a pattern exists or for finding its first occurrence.
*   **Syntax:**
    ```python
    re.search(pattern, string, flags=0)
    ```

**Example:**
```python
import re

text = "I was born on June 24, 1990. My friend was born on July 10."
# Pattern to match a month name followed by a day number.
# Parentheses create capturing groups for the month and day.
pattern = r"([a-zA-Z]+) (\d+)"

match_obj = re.search(pattern, text) # Search for the pattern in the text

if match_obj:
    print(f"First match found: '{match_obj.group(0)}'") # group(0) is the entire match
    print(f"  Month (Group 1): '{match_obj.group(1)}'") # Month captured by the first parentheses
    print(f"  Day (Group 2): '{match_obj.group(2)}'")   # Day captured by the second parentheses
    print(f"  Start index of match: {match_obj.start()}, End index: {match_obj.end()}")
else:
    print("No match found.")
```
Output:
```
First match found: 'June 24'
  Month (Group 1): 'June'
  Day (Group 2): '24'
  Start index of match: 14, End index: 21
```
Even though "July 10" also matches the pattern, `re.search()` stops after finding "June 24".

---
### Match Object
A Match object contains all the information about the search and the result. If no match is found, functions like `re.search()` and `re.match()` return `None`.

Key methods and attributes of a Match Object:

#### `match.group([group1, ...])`
*   **Purpose:** Returns the part of the string where the match occurred.
*   **Arguments:**
    *   `group(0)` or `group()`: Returns the entire matched substring. This is the default if no argument is given.
    *   `group(N)`: Returns the substring matched by the Nth capturing group `()` in the pattern (1-indexed).
    *   `group('name')`: Returns the substring matched by a named capturing group `(?P<name>...)`.
    *   `group(group1, group2, ...)`: Returns a tuple containing the strings for the specified groups.

```python
import re
text = "User: john_doe, ID: 12345, Role: admin"
# Using named groups: ?P<username> and ?P<userid>
match = re.search(r"User: (?P<username>\w+), ID: (?P<userid>\d+)", text)
if match:
    print(f"Full match (group 0): {match.group(0)}")
    # Output: User: john_doe, ID: 12345
    print(f"Username (group 'username'): {match.group('username')}") # Access by name
    # Output: john_doe
    print(f"ID (group 2): {match.group(2)}") # Access by index (userid is the 2nd group)
    # Output: 12345
    print(f"Tuple of all captured groups: {match.groups()}")
    # Output: ('john_doe', '12345')
```

#### `match.start([group])`
*   **Purpose:** Returns the starting index (inclusive) of the substring matched by `group`.
*   `group` defaults to 0 (the entire match).

#### `match.end([group])`
*   **Purpose:** Returns the ending index (exclusive) of the substring matched by `group`.
*   `group` defaults to 0 (the entire match).

#### `match.span([group])`
*   **Purpose:** Returns a tuple `(start_index, end_index)` of the substring matched by `group`.
*   `group` defaults to 0 (the entire match).

```python
import re
s = "Welcome to GeeksForGeeks"
# Search for a word starting with 'G' followed by 'ee', and capture the whole word.
match_obj = re.search(r"(\bGee\w*)", s) # \b ensures word boundary, parentheses for group 1

if match_obj:
    print(f"Matched substring (group 0): '{match_obj.group(0)}'") # 'GeeksForGeeks'
    print(f"Start index (group 0): {match_obj.start(0)}")         # 11
    print(f"End index (group 0): {match_obj.end(0)}")           # 24
    print(f"Span (group 0): {match_obj.span(0)}")              # (11, 24)

    # Since we have a capturing group (the whole word)
    print(f"\nMatched substring (group 1): '{match_obj.group(1)}'") # 'GeeksForGeeks'
    print(f"Start index (group 1): {match_obj.start(1)}")         # 11
    print(f"End index (group 1): {match_obj.end(1)}")           # 24
    print(f"Span (group 1): {match_obj.span(1)}")              # (11, 24)
```

#### `match.re`
*   **Purpose:** The regular expression object (the compiled pattern) whose `match()` or `search()` method produced this instance.

#### `match.string`
*   **Purpose:** The string passed to `match()` or `search()`.

```python
import re
pattern_str = r"\b\w{4}\b" # Pattern for exactly four-letter words
text_str = "This is a test sentence."
compiled_pattern = re.compile(pattern_str)
match_instance = compiled_pattern.search(text_str) # Search for 'This'

if match_instance:
    print(f"\n--- Match Object Attributes ---")
    print(f"Matched string: '{match_instance.group()}'")
    # Output: 'This'
    print(f"Regex object used: {match_instance.re}")
    # Output: re.compile('\\b\\w{4}\\b')
    print(f"Original string searched: '{match_instance.string}'")
    # Output: 'This is a test sentence.'
```

---
#### `re.match(pattern, string, flags=0)`
*   **Purpose:** Tries to match the `pattern` at the **beginning** of the `string` only.
*   **Behavior:** If zero or more characters at the beginning of `string` match the `pattern`, returns a corresponding match object. Returns `None` if the string does not start with the pattern. This is different from `re.search()`, which scans the entire string.
*   **Syntax:**
    ```python
    re.match(pattern, string, flags=0)
    ```

**Example: `re.match()` vs `re.search()`**
```python
import re
text = "Chapter 2: The Beginning"

# Using re.match() - only matches if the pattern is at the START of the string
match_at_start = re.match(r"Chapter \d+", text)
if match_at_start:
    print(f"re.match() for 'Chapter \\d+' found: '{match_at_start.group()}'")
    # Output: 'Chapter 2'
else:
    print("re.match() for 'Chapter \\d+' found nothing.")

# This pattern is not at the start of 'text', so re.match() will fail.
match_middle_pattern = re.match(r"The Beginning", text)
if match_middle_pattern:
    print(f"re.match() for 'The Beginning' found: '{match_middle_pattern.group()}'")
else:
    print("re.match() for 'The Beginning' found nothing.")
    # Output: re.match() for 'The Beginning' found nothing.

# Using re.search() - scans the whole string for the first match
search_for_middle = re.search(r"The Beginning", text)
if search_for_middle:
    print(f"re.search() for 'The Beginning' found: '{search_for_middle.group()}'")
    # Output: 'The Beginning'
else:
    print("re.search() for 'The Beginning' found nothing.")
```

---
*The section "Regular Expressions in Python – Set 2 (Search, Match and Find All)" is largely redundant as its content has been integrated into the detailed explanations of `re.search()`, `re.match()`, and `re.findall()` above for better organization and clarity.*

Final example: Extracting email addresses:
```python
# Example: Extracting email addresses
print("\n--- Email Extraction Example ---")
text_with_emails = "Contact us at info@example.com or support@another.org for help. Test User <test.user@internal.example.co.uk>"
# A common (though not exhaustive for all valid RFC 5322 emails) regex for emails:
email_regex = r"[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}"

extracted_emails = re.findall(email_regex, text_with_emails)
print(f"Extracted emails: {extracted_emails}")
# Output: ['info@example.com', 'support@another.org', 'test.user@internal.example.co.uk']

# To make findall case-insensitive (though the pattern itself is mostly case-insensitive already for emails):
extracted_emails_ignorecase = re.findall(email_regex, text_with_emails, re.IGNORECASE)
print(f"Extracted emails (ignorecase): {extracted_emails_ignorecase}")
# Output: ['info@example.com', 'support@another.org', 'test.user@internal.example.co.uk']
```
