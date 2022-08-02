Date : 2 Aug 2022

-----------------

## Python Modules
A Python module is a file containing Python definitions and statements. A module can define functions, classes, and variables. A module can also include runnable code. Grouping related code into a module makes the code easier to understand and use. It also makes the code logically organized.

Example : create a simple module
```python
# A simple module, calc.py

def add(x, y):
	return (x+y)

def subtract(x, y):
	return (x-y)
```

### Import Module in Python –  Import statement
We can import the functions, classes defined in a module to another module using the import statement in some other Python source file. 

Syntax:
```python
import module
```
When the interpreter encounters an import statement, it imports the module if the module is present in the search path. A search path is a list of directories that the interpreter searches for importing a module. For example, to import the module calc.py, we need to put the following command at the top of the script.

Example: Importing modules in Python
```python
# importing module calc.py
import calc

print(calc.add(10, 2))
```
Output:
```
12
```
### The from import Statement 
Python’s from statement lets you import specific attributes from a module without importing the module as a whole.

Example: Importing specific attributes from the module

```python
# importing sqrt() and factorial from the
# module math
from math import sqrt, factorial

# if we simply do "import math", then
# math.sqrt(16) and math.factorial()
# are required.
print(sqrt(16))
print(factorial(6))
```
Output:
```
4.0
720
```

### Import all Names – From import *  Statement
The * symbol used with the from import statement is used to import all the names from a module to a current namespace.

Syntax:
```
from module_name import *
```
The use of * has its advantages and disadvantages. If you know exactly what you will be needing from the module, it is not recommended to use *, else do so.

Example: Importing all names

```python
Example: Importing all names
```

### Locating Modules
Whenever a module is imported in Python the interpreter looks for several locations. First, it will check for the built-in module, if not found then it looks for a list of directories defined in the sys.path. Python interpreter searches for the module in the following manner –

* First, it searches for the module in the current directory.
* If the module isn’t found in the current directory, Python then searches each directory in the shell variable PYTHONPATH. The PYTHONPATH is an environment variable, consisting of a list of directories.
* If that also fails python checks the installation-dependent list of directories configured at the time Python is installed.

```python
# importing sys module
import sys

# importing sys.path
print(sys.path)
```
Output:
```
[‘/home/aneesh/Desktop/gfg’, ‘/usr/lib/python38.zip’, ‘/usr/lib/python3.8’, ‘/usr/lib/python3.8/lib-dynload’, ”, ‘/home/aneesh/.local/lib/python3.8/site-packages’, ‘/usr/local/lib/python3.8/dist-packages’, ‘/usr/lib/python3/dist-packages’, ‘/usr/local/lib/python3.8/dist-packages/IPython/extensions’, ‘/home/aneesh/.ipython’]
```
### Importing and renaming module
We can rename the module while importing it using the as keyword. 
Example: Renaming the module
```python
# importing sqrt() and factorial from the
# module math
import math as gfg

# if we simply do "import math", then
# math.sqrt(16) and math.factorial()
# are required.
print(gfg.sqrt(16))
print(gfg.factorial(6))
```
Output:
```
4.0
720
```
### The dir() function
The dir() built-in function returns a sorted list of strings containing the names defined by a module. The list contains the names of all the modules, variables, and functions that are defined in a module.

```python
# Import built-in module random
import random
print(dir(random))
```
Output:
```
[‘BPF’, ‘LOG4’, ‘NV_MAGICCONST’, ‘RECIP_BPF’, ‘Random’, ‘SG_MAGICCONST’, ‘SystemRandom’, ‘TWOPI’, ‘_BuiltinMethodType’, ‘_MethodType’, ‘_Sequence’, ‘_Set’, ‘__all__’, ‘__builtins__’, ‘__cached__’, ‘__doc__’, ‘__file__’, ‘__loader__’, ‘__name__’, ‘__package__’, ‘__spec__’, ‘_acos’, ‘_bisect’, ‘_ceil’, ‘_cos’, ‘_e’, ‘_exp’, ‘_inst’, ‘_itertools’, ‘_log’, ‘_pi’, ‘_random’, ‘_sha512’, ‘_sin’, ‘_sqrt’, ‘_test’, ‘_test_generator’, ‘_urandom’, ‘_warn’, ‘betavariate’, ‘choice’, ‘choices’, ‘expovariate’, ‘gammavariate’, ‘gauss’, ‘getrandbits’, ‘getstate’, ‘lognormvariate’, ‘normalvariate’, ‘paretovariate’, ‘randint’, ‘random’, ‘randrange’, ‘sample’, ‘seed’, ‘setstate’, ‘shuffle’, ‘triangular’, ‘uniform’, ‘vonmisesvariate’, ‘weibullvariate’]
```

### Code Snippet illustrating python built-in modules: 

```python
# importing built-in module math
import math

# using square root(sqrt) function contained
# in math module
print(math.sqrt(25))

# using pi function contained in math module
print(math.pi)

# 2 radians = 114.59 degrees
print(math.degrees(2))

# 60 degrees = 1.04 radians
print(math.radians(60))

# Sine of 2 radians
print(math.sin(2))

# Cosine of 0.5 radians
print(math.cos(0.5))

# Tangent of 0.23 radians
print(math.tan(0.23))

# 1 * 2 * 3 * 4 = 24
print(math.factorial(4))

# importing built in module random
import random

# printing random integer between 0 and 5
print(random.randint(0, 5))

# print random floating point number between 0 and 1
print(random.random())

# random number between 0 and 100
print(random.random() * 100)

List = [1, 4, True, 800, "python", 27, "hello"]

# using choice function in random module for choosing
# a random element from a set such as a list
print(random.choice(List))


# importing built in module datetime
import datetime
from datetime import date
import time

# Returns the number of seconds since the
# Unix Epoch, January 1st 1970
print(time.time())

# Converts a number of seconds to a date object
print(date.fromtimestamp(454554))
```

Output:
```
5.0

3.14159265359

114.591559026

1.0471975512

0.909297426826

0.87758256189

0.234143362351

24

3

0.401533172951

88.4917616788

True

1461425771.87
```

## Python Requests Tutorial
Requests library is one of the integral part of Python for making HTTP requests to a specified URL. Whether it be REST APIs or Web Scrapping, requests is must to be learned for proceeding further with these technologies. When one makes a request to a URI, it returns a response. Python requests provides inbuilt functionalities for managing both the request and response.

### Why learn Python requests module?
* Requests is an Apache2 Licensed HTTP library, that allows to send HTTP/1.1 requests using Python.
* To play with web, Python Requests is must. Whether it be hitting APIs, downloading entire facebook pages, and much more cool stuff, one will have to make a request to the URL.
* Requests play a major role is dealing with REST APIs, and Web Scrapping.

Ref Example : https://www.geeksforgeeks.org/implementing-web-scraping-python-beautiful-soup/ 

### Installing Requests

```python
pip install requests
```

The basic method for installation of requests on any operating system is to grab the base files and install requests manually and Requests is actively developed on GitHub, where the code is always available. For code – https://github.com/psf/requests

## Making a Request



