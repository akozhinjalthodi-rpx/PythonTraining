Date : 2 Aug 2022

-----------------

## Python Modules
A Python module is a file containing Python definitions and statements (like functions, classes, and variables). Modules allow you to organize your Python code logically, making it easier to understand, use, and maintain. Grouping related code into a module promotes reusability.

**Example: Creating a simple module**
Let's create a file named `calc.py`:
```python
# A simple module, calc.py

def add(x, y):
    """This function adds two numbers."""
    return (x+y)

def subtract(x, y):
    """This function subtracts two numbers."""
    return (x-y)
```
This `calc.py` file is a module named `calc`.

### Import Module in Python – The `import` statement
You can bring the functionality of a module into your current script using the `import` statement. When Python encounters an `import` statement, it searches for the module in a list of directories and then executes the module's code (if found) to make its definitions available.

**Syntax:**
```python
import module_name
# To access items from the module, you use dot notation:
# module_name.function_name()
# module_name.variable_name
```

**Module Search Path:**
When you import a module (e.g., `import my_module`), the Python interpreter searches for `my_module.py` (or a package named `my_module`) in the following locations, in order:
1.  **Current Directory:** The directory where the script currently being run is located.
2.  **PYTHONPATH Directories:** A list of directories specified by the `PYTHONPATH` environment variable, if set. This variable allows you to add custom locations for your modules.
3.  **Installation-Dependent Default Path:** Standard library directories and paths for site-packages (where third-party libraries installed via `pip` usually reside). This is configured when Python is installed.

You can inspect Python's search path using the `sys` module:
```python
import sys
print(sys.path)
# Output will be a list of strings, e.g.:
# ['/path/to/current_script_dir', '/usr/lib/python3.9', ..., '/usr/local/lib/python3.9/dist-packages']
```

**Example: Importing the `calc` module**
Assuming `calc.py` (defined earlier) is in the same directory or in Python's search path:
```python
# main_script.py
import calc # Imports the entire calc module

# Access functions using module_name.function_name()
result_add = calc.add(10, 2)
result_subtract = calc.subtract(10, 2)

print(f"calc.add(10, 2) = {result_add}")       # Output: 12
print(f"calc.subtract(10, 2) = {result_subtract}") # Output: 8
```

### The `from ... import ...` Statement 
This statement allows you to import specific attributes (functions, classes, variables) directly from a module into your current script's namespace. This means you can use the imported items directly without prefixing them with the module name.

**Syntax:**
```python
from module_name import name1, name2, ...
# Now you can use name1, name2 directly:
# name1()
# print(name2)
```

**Example: Importing specific attributes from the `math` module**
```python
# Import only the sqrt (square root) and factorial functions from the math module
from math import sqrt, factorial

# Now sqrt and factorial can be called directly
print(f"Square root of 16 is: {sqrt(16)}")     # Output: 4.0
print(f"Factorial of 6 is: {factorial(6)}") # Output: 720

# If we had used "import math", we would need to call them as:
# math.sqrt(16)
# math.factorial(6)
```
Using `from ... import ...` can make your code more concise, but be mindful of potential name collisions if the imported names are the same as names already defined in your script.

### The `from ... import *` Statement
This statement imports all public names (those not starting with an underscore `_`) from a module directly into the current script's namespace.

**Syntax:**
```python
from module_name import *
```
**Usage and Discouragement:**
While this might seem convenient, **it is generally discouraged for most use cases** due to several reasons:
*   **Namespace Pollution:** It can flood your current namespace with many names, making it unclear where a particular function or variable originated.
*   **Readability:** It makes code harder to read and understand, as you can't immediately tell which module a name belongs to without looking at the import statements.
*   **Name Collisions:** It significantly increases the risk of unintentionally overwriting existing names (functions, variables) in your script if the imported module has names that are identical.
*   **Static Analysis:** Tools for static code analysis might have difficulty detecting undefined names or other issues.

**When it might be seen (though still often avoidable):**
*   Sometimes used in interactive sessions for convenience.
*   Occasionally used within a package's `__init__.py` to make parts of submodules available at the package level (though explicit imports are often clearer).

**Example:**
Let's assume `calc.py` has `add` and `subtract`.
```python
# Assume calc.py exists with add() and subtract()

# Generally discouraged:
from calc import * 

result1 = add(20, 5)       # Works, but 'add' is now in the global namespace
result2 = subtract(20, 5)  # Works, but 'subtract' is also global

print(f"Result of add(20, 5): {result1}")
print(f"Result of subtract(20, 5): {result2}")

# If you define your own 'add' function now, it might lead to confusion or errors.
# def add(a, b):
#    print("This is a different add!")
# add(1,1) # Which add is called? Depends on order if not careful.
```
It's usually better to use `import module_name` or `from module_name import specific_name` for clarity.

### Locating Modules
Whenever a module is imported in Python, the interpreter searches for it in a specific order:

1.  **Built-in Modules:** Python first checks if the module is a built-in module (written in C and part of the Python interpreter itself, e.g., `sys`, `os`, `math`).
2.  **Current Directory:** The directory from which the input script was run (or the current directory if running interactively).
3.  **PYTHONPATH:** A list of directories specified by the `PYTHONPATH` environment variable. This variable allows you to add custom locations where Python should look for modules.
4.  **Installation-Dependent Default Path:** Standard library directories and paths for site-packages (where third-party libraries installed via `pip` usually reside). This is configured when Python is installed.

You can inspect Python's search path using the `sys.path` list:
```python
import sys

# Print the list of directories Python searches for modules
print("Python's Module Search Path (sys.path):")
for path_entry in sys.path:
    print(path_entry)
```
The output will be a list of strings, showing the actual paths Python will check. For example:
```
Python's Module Search Path (sys.path):
/path/to/current_script_dir
/usr/lib/python3.9
/usr/lib/python3.9/lib-dynload
/home/user/.local/lib/python3.9/site-packages
/usr/local/lib/python3.9/dist-packages
/usr/lib/python3/dist-packages
# ... (paths may vary based on your OS and Python installation)
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

### The `if __name__ == "__main__":` Idiom

In Python, the `if __name__ == "__main__":` block is a common and important idiom used to control the execution of code within a module. It allows a module to be both:
1.  **Importable:** Its functions, classes, and variables can be imported and used by other scripts.
2.  **Runnable:** It can also be executed as a standalone script, typically for testing, examples, or specific command-line functionality.

**Purpose and How it Works:**

*   **`__name__` Variable:** Python sets a special built-in variable called `__name__` for every module.
    *   When a Python script is run **directly**, the `__name__` variable for that script is set to the string `"__main__"`.
    *   When a module is **imported** into another script, the `__name__` variable for the imported module is set to its own **module name** (i.e., the filename without the `.py` extension).

*   **Conditional Execution:** The `if __name__ == "__main__":` statement checks the value of `__name__`.
    *   The code block indented under this `if` statement will **only execute** if the module is being run directly (not when it's imported).

**Example:**

Let's modify our `calc.py` module to include this idiom.

`calc.py`:
```python
# A simple module, calc.py

def add(x, y):
    """This function adds two numbers."""
    return (x+y)

def subtract(x, y):
    """This function subtracts two numbers."""
    return (x-y)

# This block will only execute if calc.py is run directly.
# It will NOT execute if calc.py is imported into another module.
if __name__ == "__main__":
    print("Running calc.py as a standalone script!")
    
    # Example usage or test code for the module's functions
    num1 = 15
    num2 = 7
    
    sum_result = add(num1, num2)
    difference_result = subtract(num1, num2)
    
    print(f"The sum of {num1} and {num2} is: {sum_result}")
    print(f"The difference between {num1} and {num2} is: {difference_result}")
    
    print("\nValue of __name__ in calc.py when run directly:", __name__) 
    # Will print: __main__
```

**Behavior:**

1.  **Running `calc.py` directly:**
    If you execute `python calc.py` from your terminal, the output will be:
    ```
    Running calc.py as a standalone script!
    The sum of 15 and 7 is: 22
    The difference between 15 and 7 is: 8
    
    Value of __name__ in calc.py when run directly: __main__
    ```

2.  **Importing `calc.py` into another script:**
    Create another Python file, say `main_program.py`, in the same directory:

    `main_program.py`:
    ```python
    import calc # Import the calc module

    print("Using functions from the imported calc module:")
    result = calc.add(100, 50)
    print(f"calc.add(100, 50) = {result}")

    print("\nValue of __name__ in main_program.py:", __name__) 
    # Will print: __main__
    # To see calc.py's __name__ when imported, you'd need to print it from calc.py
    # outside the if __name__ == "__main__": block, or have a function in calc.py return it.
    ```
    When you run `python main_program.py`, the output will be:
    ```
    Using functions from the imported calc module:
    calc.add(100, 50) = 150

    Value of __name__ in main_program.py: __main__
    ```
    Notice that "Running calc.py as a standalone script!" and the other print statements from within the `if __name__ == "__main__":` block in `calc.py` **do not appear**. This is because when `calc.py` is imported, its `__name__` is `"calc"`, not `"__main__"`.

**Benefits:**

*   **Modularity:** Keeps test code, example usage, or script-specific logic separate from the importable parts of your module.
*   **Reusability:** Allows your module's functions and classes to be cleanly imported and reused in other programs.
*   **Testability:** Provides a convenient place to put unit tests or simple test cases for the module's functionality.
*   **Clarity:** Makes it clear which part of the code is intended for direct execution versus which parts are for providing functionality when imported.

This idiom is a standard best practice in Python for writing modules that are both useful libraries and potentially runnable scripts.

### The `dir()` function
The `dir()` built-in function is a versatile tool used to get a list of names (attributes, methods, etc.) defined by an object.

*   **With an argument (e.g., `dir(module_name)` or `dir(object_instance)`):** It returns a sorted list of strings containing the names defined by that module or object. This includes functions, classes, variables, and built-in attributes.
*   **Without an argument (`dir()`):** When called without an argument, `dir()` lists the names in the current local scope (e.g., variables and functions defined in the current script or interactive session).

**Example: Using `dir()` with a module**
```python
import math # Import the built-in math module
import random # Import the built-in random module

print("--- Names defined in the 'math' module ---")
# print(dir(math)) 
# Output will be a long list of math functions like 'acos', 'sqrt', 'pi', etc.

print("\n--- Names defined in the 'random' module ---")
# print(dir(random))
# Output will be a long list of random module functions like 'randint', 'choice', 'shuffle', etc.

# Example of dir() on a list object
my_list = [1, 2, 3]
print("\n--- Attributes and methods of a list object ---")
# print(dir(my_list))
# Output will include methods like 'append', 'sort', 'pop', etc.
```
The actual output for `dir(random)` would be similar to:
```
['BPF', 'LOG4', 'NV_MAGICCONST', 'RECIP_BPF', 'Random', 'SG_MAGICCONST', 'SystemRandom', 'TWOPI', '_Sequence', '_Set', '__all__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', '_accumulate', '_acos', '_bisect', '_ceil', '_cos', '_e', '_exp', '_floor', '_inst', '_log', '_os', '_pi', '_random', '_repeat', '_sha512', '_sin', '_sqrt', '_test', '_test_generator', '_urandom', '_warn', 'betavariate', 'choice', 'choices', 'expovariate', 'gammavariate', 'gauss', 'getrandbits', 'getstate', 'lognormvariate', 'normalvariate', 'paretovariate', 'randbytes', 'randint', 'random', 'randrange', 'sample', 'seed', 'setstate', 'shuffle', 'triangular', 'uniform', 'vonmisesvariate', 'weibullvariate']
```
(Note: The exact list of names can vary slightly between Python versions.)

### Code Snippet Illustrating Python Built-in Modules: 

This snippet demonstrates the use of some common functions from Python's built-in `math`, `random`, and `datetime` modules.

```python
# Importing built-in module math
import math

print("--- Math Module Examples ---")
# Using square root(sqrt) function contained in math module
print(f"Square root of 25: {math.sqrt(25)}")      # Output: 5.0

# Using pi constant contained in math module
print(f"Value of pi: {math.pi}")                # Output: 3.141592653589793

# Converting 2 radians to degrees
print(f"2 radians in degrees: {math.degrees(2)}") # Output: 114.59155902616465

# Converting 60 degrees to radians
print(f"60 degrees in radians: {math.radians(60)}") # Output: 1.0471975511965976

# Sine of 2 radians
print(f"Sine of 2 radians: {math.sin(2)}")          # Output: 0.9092974268256817

# Cosine of 0.5 radians
print(f"Cosine of 0.5 radians: {math.cos(0.5)}")    # Output: 0.8775825618903728

# Tangent of 0.23 radians
print(f"Tangent of 0.23 radians: {math.tan(0.23)}")  # Output: 0.2341433623508909

# Factorial of 4 (4! = 4*3*2*1)
print(f"Factorial of 4: {math.factorial(4)}")      # Output: 24

# Importing built-in module random
import random

print("\n--- Random Module Examples ---")
# Printing random integer between 0 and 5 (inclusive)
print(f"Random integer between 0 and 5: {random.randint(0, 5)}")

# Print random floating point number between 0.0 (inclusive) and 1.0 (exclusive)
print(f"Random float (0.0 to 1.0): {random.random()}")

# Random number between 0 and 100 (exclusive of 100.0 for random())
# print(f"Random float (0.0 to 100.0): {random.random() * 100}")
# For a specific range, use random.uniform(a, b)
print(f"Random float between 10 and 20: {random.uniform(10, 20)}")


my_sample_list = [1, 4, True, 800, "python", 27, "hello"]
# Using choice function in random module for choosing a random element from a sequence
print(f"Random choice from list: {random.choice(my_sample_list)}")

# Importing built-in modules/classes for date and time
import datetime
from datetime import date # Import specific class 'date' from datetime module
import time

print("\n--- Date and Time Examples ---")
# Returns the number of seconds since the Unix Epoch (January 1st 1970, 00:00:00 UTC)
current_epoch_time = time.time()
print(f"Seconds since epoch: {current_epoch_time}")

# Converts a number of seconds (timestamp) since the epoch to a date object
example_timestamp = 1678886400 # Example: March 15, 2023
print(f"Date from timestamp {example_timestamp}: {date.fromtimestamp(example_timestamp)}")

# Get current date and time
now = datetime.datetime.now()
print(f"Current date and time: {now}")
print(f"Current year: {now.year}")
print(f"Current month: {now.month}")
print(f"Current day: {now.day}")
print(f"Formatted date: {now.strftime('%Y-%m-%d %H:%M:%S')}")
```

**Note on Output:**
The output for examples involving `random` functions will naturally vary with each execution. Similarly, `time.time()` and `datetime.datetime.now()` will produce results based on the exact moment they are run.

Example Output (will vary):
```
--- Math Module Examples ---
Square root of 25: 5.0
Value of pi: 3.141592653589793
2 radians in degrees: 114.59155902616465
60 degrees in radians: 1.0471975511965976
Sine of 2 radians: 0.9092974268256817
Cosine of 0.5 radians: 0.8775825618903728
Tangent of 0.23 radians: 0.2341433623508909
Factorial of 4: 24

--- Random Module Examples ---
Random integer between 0 and 5: 3  # Example value
Random float (0.0 to 1.0): 0.4015331729511382 # Example value
Random float between 10 and 20: 15.678... # Example value
Random choice from list: python # Example value

--- Date and Time Examples ---
Seconds since epoch: 1678886400.123456 # Example value, will be current time
Date from timestamp 1678886400: 2023-03-15 # Or your local equivalent date
Current date and time: 2023-10-27 10:00:00.000000 # Example value
Current year: 2023
Current month: 10
Current day: 27
Formatted date: 2023-10-27 10:00:00
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

Date : 3 Aug 20222

---------------------------

### Making HTTP Requests

The `requests` module simplifies making various types of HTTP requests. Each HTTP method (GET, POST, PUT, DELETE, etc.) has a corresponding function in the library.

#### Making a GET Request

The `GET` method is used to retrieve information from a server using a given URI. Data is typically passed in the URL's query string.

**Syntax:**
```python
response = requests.get(url, params=None, **kwargs)
```
*   `url`: The URL to which the request is sent.
*   `params` (optional): A dictionary, list of tuples, or bytes to be sent in the query string for the Request.
*   `**kwargs` (optional): Other arguments that `request` takes, such as `headers`, `auth`, `timeout`, etc.

**Example: Basic GET Request**
```python
import requests

# Target URL (GitHub API endpoint for a user)
url = 'https://api.github.com/users/naveenkrnl' 

try:
    # Making a GET request
    response = requests.get(url)
    
    # Check if the request was successful (status code 200-299)
    response.raise_for_status() # This will raise an HTTPError for bad responses (4xx or 5xx)

    # Print the status code (e.g., 200 for success)
    print(f"Status Code: {response.status_code}")

    # Print the content of the response (in bytes)
    # print(f"Raw Content (bytes): {response.content}")

    # For text-based responses (like JSON or HTML), use .text
    # print(f"Text Content: {response.text}")
    
    # If the response is JSON, you can parse it directly
    # It's good practice to check Content-Type or use a try-except for .json()
    if 'application/json' in response.headers.get('Content-Type', ''):
        user_data = response.json() # Parses JSON content into a Python dictionary
        print("\nUser Data (parsed JSON):")
        print(f"  Login: {user_data.get('login')}")
        print(f"  ID: {user_data.get('id')}")
        print(f"  Public Repos: {user_data.get('public_repos')}")
    else:
        print("\nResponse was not JSON, printing as text:")
        print(response.text)

except requests.exceptions.HTTPError as http_err:
    print(f"HTTP error occurred: {http_err} - Status Code: {response.status_code if 'response' in locals() else 'N/A'}")
except requests.exceptions.ConnectionError as conn_err:
    print(f"Connection error occurred: {conn_err}")
except requests.exceptions.Timeout as timeout_err:
    print(f"Timeout error occurred: {timeout_err}")
except requests.exceptions.RequestException as req_err:
    print(f"An unexpected error occurred with the request: {req_err}")
```
**Output (Example for a successful request):**
```
Status Code: 200

User Data (parsed JSON):
  Login: naveenkrnl
  ID: 14209499
  Public Repos: 33 
```
(Note: The exact number of public repos and other details might change.)

#### Passing URL Parameters (Query Strings) with `params`

Often, you need to pass data to a server via the URL's query string (e.g., `?key1=value1&key2=value2`). The `requests` library makes this very easy using the `params` argument in the `get()` method.

*   **Purpose:** To send data to the server as part of the URL, typically for filtering results, specifying search terms, or other GET request configurations.
*   **Method:** Provide a dictionary to the `params` argument of `requests.get()`. `requests` will automatically construct the correctly URL-encoded query string.

**Example using `https://httpbin.org/get` (a service for testing HTTP requests):**

```python
import requests

# Define the parameters you want to send
payload = {
    'name': 'John Doe',
    'age': 30,
    'occupation': 'Software Developer & Tester' # Note the space and '&'
}

# Make the GET request with the params
try:
    response_with_params = requests.get('https://httpbin.org/get', params=payload)
    response_with_params.raise_for_status() # Raise an exception for bad status codes (4xx or 5xx)

    # Print the URL that was actually constructed and sent
    print(f"Constructed URL: {response_with_params.url}")

    # httpbin.org/get returns a JSON response reflecting the request details
    response_data = response_with_params.json() 
    
    print("\nResponse JSON (args part shows received parameters):")
    # The 'args' key in the response from httpbin.org/get will show the parameters it received
    print(response_data.get('args')) 

except requests.exceptions.HTTPError as http_err:
    print(f"HTTP error occurred: {http_err}")
except requests.exceptions.RequestException as err:
    print(f"Other error occurred: {err}")
```

**Expected Output:**

```
Constructed URL: https://httpbin.org/get?name=John+Doe&age=30&occupation=Software+Developer+%26+Tester
Response JSON (args part shows received parameters):
{'age': '30', 'name': 'John Doe', 'occupation': 'Software Developer & Tester'}
```
**Explanation:**
*   The `payload` dictionary is passed to `params`.
*   `requests` automatically URL-encodes the values (e.g., "John Doe" becomes "John+Doe", "Software Developer & Tester" becomes "Software+Developer+%26+Tester").
*   The resulting URL clearly shows the appended query string.
*   The server (`httpbin.org/get`) receives these parameters and reflects them in its JSON response under the `args` key.

Using the `params` argument is the recommended way to construct query strings, as it handles special characters and encoding correctly, making your code cleaner and less error-prone than manually constructing the URL string.

#### Making a POST Request

The `POST` method is used to send data to a server to create or update a resource. The data is sent in the **body** of the HTTP request.

**Syntax:**
```python
response = requests.post(url, data=None, json=None, **kwargs)
```
*   `url`: The URL to which the request is sent.
*   `data` (optional): A dictionary, list of tuples, bytes, or a file-like object to send in the body of the Request. This is typically used for sending HTML form data (i.e., `application/x-www-form-urlencoded`).
*   `json` (optional): A JSON serializable Python object to send in the body of the Request. If you use this, `requests` will automatically encode it as JSON and set the `Content-Type` header to `application/json`.
*   `**kwargs`: Other arguments like `headers`, `auth`, `timeout`.

**1. Sending Form Data using `data` parameter:**

When you pass a dictionary to the `data` argument, `requests` sends it as form-encoded data (like an HTML form submission).

```python
import requests

url_post = 'https://httpbin.org/post' # This endpoint echoes the POST data
form_payload = {
    'username': 'johndoe_form',
    'email': 'john.form@example.com',
    'role': 'user'
}

try:
    response_form = requests.post(url_post, data=form_payload)
    response_form.raise_for_status()

    print("--- POST Request with Form Data ---")
    print(f"Status Code: {response_form.status_code}")
    
    # httpbin.org/post returns the received data in its response
    response_data_form = response_form.json()
    print(f"Sent Form Data (reflected by server): {response_data_form.get('form')}")
    print(f"Content-Type Header Sent: {response_data_form.get('headers', {}).get('Content-Type')}")

except requests.exceptions.RequestException as e:
    print(f"Error during form data POST request: {e}")
```
**Expected Output:**
```
--- POST Request with Form Data ---
Status Code: 200
Sent Form Data (reflected by server): {'email': 'john.form@example.com', 'role': 'user', 'username': 'johndoe_form'}
Content-Type Header Sent: application/x-www-form-urlencoded
```

**2. Sending JSON Data using `json` parameter:**

For APIs that expect JSON payloads, using the `json` parameter is more convenient. `requests` automatically serializes the dictionary to a JSON string and sets the `Content-Type` header to `application/json`.

```python
import requests # requests should be imported once at the top

url_post_json = 'https://httpbin.org/post'
json_payload = {
    'username': 'janedoe_json',
    'email': 'jane.json@example.com',
    'preferences': {'theme': 'dark', 'notifications': True}
}

try:
    response_json = requests.post(url_post_json, json=json_payload)
    response_json.raise_for_status()

    print("\n--- POST Request with JSON Data ---")
    print(f"Status Code: {response_json.status_code}")

    response_data_json = response_json.json()
    print(f"Sent JSON Data (reflected by server as 'json'): {response_data_json.get('json')}")
    print(f"Received 'data' field (raw body): {response_data_json.get('data')}")
    print(f"Content-Type Header Sent: {response_data_json.get('headers', {}).get('Content-Type')}")

except requests.exceptions.RequestException as e:
    print(f"Error during JSON POST request: {e}")
```
**Expected Output:**
```
--- POST Request with JSON Data ---
Status Code: 200
Sent JSON Data (reflected by server as 'json'): {'email': 'jane.json@example.com', 'preferences': {'notifications': True, 'theme': 'dark'}, 'username': 'janedoe_json'}
Received 'data' field (raw body): {"username": "janedoe_json", "email": "jane.json@example.com", "preferences": {"theme": "dark", "notifications": true}}
Content-Type Header Sent: application/json
```
Choosing between `data` and `json` depends on what the server API expects. Modern APIs typically prefer JSON.

#### Sending Custom Headers

HTTP headers allow the client and the server to pass additional information with an HTTP request or response. You can send custom headers with your requests using the `headers` parameter, which takes a dictionary of header names and values.

**Common Use Cases for Custom Headers:**

*   **Authentication:** Sending API keys or tokens (e.g., `Authorization: Bearer <your_token>`).
*   **Content Type Specification:** Explicitly telling the server the format of your request body (though `requests` often handles this automatically for `json` and `data` parameters, e.g. `Content-Type: application/json`).
*   **User-Agent:** Identifying your client application to the server. Some APIs might block default `requests` User-Agent or require a specific one.
*   **Accept Header:** Specifying the content types your client can understand in the response (e.g., `Accept: application/json`).

**Example: Sending a `User-Agent` and a custom header**

```python
import requests

url_get_headers = 'https://httpbin.org/headers' # This endpoint returns the request's headers

custom_headers = {
    'User-Agent': 'MyPythonApp/1.0 (LearningRequests)',
    'X-Custom-Header': 'MyCustomValue123',
    'Accept': 'application/json' 
}

try:
    response_custom_headers = requests.get(url_get_headers, headers=custom_headers)
    response_custom_headers.raise_for_status()

    print("--- GET Request with Custom Headers ---")
    print(f"Status Code: {response_custom_headers.status_code}")
    
    # httpbin.org/headers returns the headers it received
    received_headers = response_custom_headers.json().get('headers', {})
    print("\nHeaders received by server:")
    print(f"  User-Agent: {received_headers.get('User-Agent')}")
    print(f"  X-Custom-Header: {received_headers.get('X-Custom-Header')}")
    print(f"  Accept: {received_headers.get('Accept')}")
    # Note: httpbin might add/modify some headers like X-Amzn-Trace-Id or Host

except requests.exceptions.RequestException as e:
    print(f"Error during GET request with custom headers: {e}")

```

**Expected Output (order of headers in output might vary):**
```
--- GET Request with Custom Headers ---
Status Code: 200

Headers received by server:
  User-Agent: MyPythonApp/1.0 (LearningRequests)
  X-Custom-Header: MyCustomValue123
  Accept: application/json
```
The server (`httpbin.org/headers`) receives the custom headers sent by the `requests` client and includes them in its JSON response, confirming they were transmitted correctly.

### Http Request Methods –

|Method|Description|
|------|-----------|
|GET|GET method is used to retrieve information from the given server using a given URI.|
POST|	POST request method requests that a web server accepts the data enclosed in the body of the request message, most likely for storing it. It's used to send data to a server to create or update a resource. |
PUT	|The PUT method requests that the enclosed entity be stored under the supplied URI. If the URI refers to an already existing resource, it is modified (replaced). If the URI does not point to an existing resource, then the server can create the resource with that URI. Typically sends the entire resource. |
DELETE|	The DELETE method deletes the specified resource. |
HEAD|	The HEAD method asks for a response identical to that of a GET request, but without the response body. Useful for checking resource metadata (like `Content-Type` or `Content-Length`) without downloading the actual content. |
PATCH|	The PATCH method is used for making partial modifications to an existing resource. Unlike PUT, PATCH typically only needs to contain the changes to the resource, not the complete resource. |


### Inspecting the Response

When you make a request using `requests`, the library returns a `Response` object. This object contains the server's response to your HTTP request and has many useful attributes and methods.

```python
import requests
import json # For json.JSONDecodeError if using older requests/Python versions

# Example: Making a request to inspect its response
url = 'https://api.github.com/users/python-requests' 
# A more specific endpoint that's likely to return JSON
try:
    response = requests.get(url, timeout=10) # Added a timeout for robustness

    # 1. Check the Status Code
    print(f"--- Status Code ---")
    print(f"Status: {response.status_code}") # e.g., 200 for OK, 404 for Not Found
    print(f"Status Reason: {response.reason}") # e.g., "OK", "Not Found"

    # You can check if the request was successful (status code 200-299)
    if response.ok: # response.ok is True if status_code < 400
        print("Request was successful (status code < 400)")
    else:
        print("Request failed (status code >= 400)")

    # 2. Inspect Headers
    print(f"\n--- Headers ---")
    print(f"Response Headers (dict-like object): {response.headers}")
    # Headers are case-insensitive dictionary-like objects
    print(f"Content-Type: {response.headers.get('Content-Type')}") 
    print(f"Date: {response.headers.get('Date')}")

    # 3. Accessing the Response Body
    print(f"\n--- Response Body ---")
    # response.content: Raw response body in bytes (for images, files, etc.)
    # print(f"Raw content (first 100 bytes): {response.content[:100]}") 
    
    # response.text: Decoded response body as a string (for text-based responses like HTML, JSON)
    # Requests attempts to guess the encoding based on headers.
    # You can also set response.encoding = 'utf-8' (or other) before accessing .text if needed.
    print(f"Text content (first 200 chars): {response.text[:200]}...") 

    # 4. Parsing JSON Response with response.json()
    print(f"\n--- JSON Parsing ---")
    if 'application/json' in response.headers.get('Content-Type', '').lower():
        try:
            # This method deserializes the JSON content into a Python dictionary or list.
            json_data = response.json()
            print("Successfully parsed JSON response:")
            # print(json_data) # Can be very long, print specific parts instead
            print(f"  Login: {json_data.get('login')}")
            print(f"  ID: {json_data.get('id')}")
            print(f"  Public Repos: {json_data.get('public_repos')}")
        except requests.exceptions.JSONDecodeError as json_err: # More specific exception
             # In modern versions of requests, this might be json.JSONDecodeError
            print(f"Failed to decode JSON: {json_err}")
            print("Printing raw text instead (if any):")
            print(response.text[:500] + "..." if response.text else "No text content.")
    else:
        print("Response Content-Type is not application/json.")

    # 5. Other useful attributes/methods
    print(f"\n--- Other Info ---")
    print(f"URL of the request: {response.url}")
    print(f"Time elapsed for the request: {response.elapsed}") # A timedelta object
    # response.history would show a list of redirection response objects if any occurred.
    # response.cookies would show cookies sent by the server.

except requests.exceptions.RequestException as e:
    print(f"An error occurred: {e}")

```
**Expected Output (will vary based on current data from GitHub API):**
```
--- Status Code ---
Status: 200
Status Reason: OK
Request was successful (status code < 400)

--- Headers ---
Response Headers (dict-like object): {'Server': 'GitHub.com', ... 'Content-Type': 'application/json; charset=utf-8', ...}
Content-Type: application/json; charset=utf-8
Date: <Current Date and Time from Header>

--- Response Body ---
Text content (first 200 chars): {"login":"python-requests","id":3370945,"node_id":"MDEyOk9yZ2FuaXphdGlvbjMzNzA5NDU=","avatar_url":"https://avatars.githubusercontent.com/u/3370945?v=4","gravatar_id":"","url":"https://api.github.com/users/py...

--- JSON Parsing ---
Successfully parsed JSON response:
  Login: python-requests
  ID: 3370945
  Public Repos: <Number>

--- Other Info ---
URL of the request: https://api.github.com/users/python-requests
Time elapsed for the request: 0:00:00.XXXXXX 
```

### Error Handling in Requests

Network requests can fail for various reasons (network issues, server errors, timeouts, etc.). Robust applications should handle these potential errors gracefully.

#### Using `response.raise_for_status()`
The `Response` object has a convenient method `raise_for_status()` that will raise an `requests.exceptions.HTTPError` if the HTTP request returned an unsuccessful status code (4xx client error or 5xx server error). If the status code indicates success (2xx), `raise_for_status()` does nothing.

```python
import requests

try:
    response_error = requests.get('https://httpbin.org/status/404') # This URL returns a 404 error
    response_error.raise_for_status() # This will raise an HTTPError
    print("Request was successful (this won't print for 404).")
except requests.exceptions.HTTPError as e:
    print(f"HTTP error occurred: {e}") # e.g., 404 Client Error: NOT FOUND for url: https://httpbin.org/status/404
```

#### Catching Specific Exceptions
For more fine-grained error handling, you can use `try...except` blocks to catch specific exceptions provided by the `requests` library.

Common exceptions include:
*   `requests.exceptions.HTTPError`: For bad HTTP status codes (4xx or 5xx), raised by `raise_for_status()`.
*   `requests.exceptions.ConnectionError`: For network connectivity problems (e.g., DNS failure, refused connection).
*   `requests.exceptions.Timeout`: If the request times out.
*   `requests.exceptions.TooManyRedirects`: If the request exceeds the configured number of maximum redirections.
*   `requests.exceptions.RequestException`: The base class for all exceptions raised by `requests`. Catching this will handle any request-related error.

```python
import requests

url_test = 'https://example.com/nonexistentpage' # Likely a 404
# url_test = 'http://thissitedoesnotexistatallhopefully.com' # For ConnectionError
# url_test = 'https://httpbin.org/delay/5' # For Timeout (if timeout is set low)

try:
    response = requests.get(url_test, timeout=2.5) # Set a timeout of 2.5 seconds
    response.raise_for_status() # Check for HTTP errors
    
    # Process successful response here
    print("Response content:", response.text[:100] + "...")

except requests.exceptions.HTTPError as http_err:
    print(f"HTTP error: {http_err} (Status code: {http_err.response.status_code})")
except requests.exceptions.ConnectionError as conn_err:
    print(f"Connection error: {conn_err}")
except requests.exceptions.Timeout as timeout_err:
    print(f"Timeout error: {timeout_err}")
except requests.exceptions.RequestException as req_err: # Catch any other requests error
    print(f"An unexpected requests error occurred: {req_err}")
except Exception as e: # Catch any other non-requests error during processing
    print(f"A non-requests error occurred: {e}")
```

### Response Methods Summary
Here's a table summarizing some of the most commonly used attributes and methods of the `Response` object:

| Attribute/Method             | Description                                                                                                |
|------------------------------|------------------------------------------------------------------------------------------------------------|
| `response.status_code`       | Integer Code of responded HTTP Status, e.g. `200`, `404`.                                                  |
| `response.reason`            | Textual equivalent of the HTTP status code, e.g. "OK", "Not Found".                                        |
| `response.ok`                | Boolean: `True` if `status_code` is less than 400, `False` otherwise.                                      |
| `response.headers`           | Case-insensitive dictionary of response headers.                                                           |
| `response.text`              | Content of the response, in Unicode (decoded based on HTTP headers or guessed encoding).                     |
| `response.content`           | Content of the response, in bytes (raw binary content).                                                    |
| `response.json(**kwargs)`    | Parses the response text as JSON and returns a Python dictionary or list. Raises `requests.exceptions.JSONDecodeError` (or `json.JSONDecodeError`) if parsing fails. |
| `response.url`               | The final URL of the response (after any redirections).                                                    |
| `response.encoding`          | The encoding used to decode `response.text`. Can be set manually if guessed incorrectly.                 |
| `response.elapsed`           | A `timedelta` object representing the time elapsed between sending the request and the arrival of the response. |
| `response.raise_for_status()`| Raises an `requests.exceptions.HTTPError` if the HTTP request returned an unsuccessful status code (4xx or 5xx). |
| `response.cookies`           | A `CookieJar` object with cookies sent by the server.                                                      |
| `response.history`           | A list of `Response` objects from any prior redirections.                                                  |
| `response.close()`           | Closes the connection to the server. (Usually not needed as `requests` handles this with connection pooling). |
| `response.iter_content(...)` | Iterates over the response data in chunks. Useful for large downloads.                                     |
| `response.request`           | The `Request` object that this `Response` is a response to.                                                |

### Authentication with Python Requests

Authentication is the process of verifying your identity to gain access to a protected resource. Many web APIs require authentication. `requests` supports several authentication methods.

#### 1. Basic Authentication

Basic Authentication is a simple authentication scheme built into the HTTP protocol. The client sends HTTP requests with an `Authorization` header that contains the word `Basic` followed by a space and a base64-encoded string of `username:password`.

`requests` provides a shorthand for this using the `auth` parameter:

```python
import requests
from requests.auth import HTTPBasicAuth # For explicit Basic Auth

# Target URL that requires Basic Authentication.
# httpbin.org/basic-auth/user/passwd will challenge for username "user" and password "passwd".
# Replace 'myuser' and 'mypass' in the URL and in HTTPBasicAuth with actual credentials for a real endpoint.
basic_auth_url = 'https://httpbin.org/basic-auth/myuser/mypass' # Example URL

try:
    # Method 1: Using a tuple (username, password) with the auth parameter
    print("\n--- Attempting Basic Authentication (tuple method) ---")
    # Replace 'myuser' and 'mypass' with the actual credentials expected by basic_auth_url
    response_basic = requests.get(basic_auth_url, auth=('myuser', 'mypass'))
    response_basic.raise_for_status() # Check for HTTP errors (401 if auth fails, etc.)
    print(f"Basic Authentication Successful! Status Code: {response_basic.status_code}")
    # For httpbin.org/basic-auth, the response JSON indicates authenticated status
    # print(f"Response Content: {response_basic.json()}") 

    # Method 2: Using HTTPBasicAuth object (more explicit)
    # print("\n--- Attempting Basic Authentication (HTTPBasicAuth object method) ---")
    # response_explicit_basic = requests.get(basic_auth_url, auth=HTTPBasicAuth('myuser', 'mypass'))
    # response_explicit_basic.raise_for_status()
    # print(f"Basic Authentication Successful! Status Code: {response_explicit_basic.status_code}")
    # print(f"Response Content: {response_explicit_basic.json()}")

except requests.exceptions.HTTPError as http_err:
    if http_err.response.status_code == 401: # Specifically handle unauthorized error
        print(f"Authentication failed: {http_err}")
    else:
        print(f"An HTTP error occurred: {http_err}")
except requests.exceptions.RequestException as e:
    print(f"An error occurred: {e}")
```
**Expected Output (for successful authentication with correct credentials for the endpoint):**
```
--- Attempting Basic Authentication (tuple method) ---
Basic Authentication Successful! Status Code: 200
```
If authentication fails (e.g., wrong credentials for the actual `basic_auth_url`), `response.raise_for_status()` will raise an `HTTPError`, and you'll typically see a 401 Unauthorized status code. The example URL `https://httpbin.org/basic-auth/myuser/mypass` is set up to expect "myuser" and "mypass".

#### 2. Token-Based Authentication (Common for APIs)

Many modern APIs use token-based authentication. This usually involves sending an API key or a bearer token in an HTTP header, most commonly the `Authorization` header. This method is generally preferred over Basic Auth for APIs as tokens can be revoked, have specific scopes, and don't require sending username/password with every request.

**Example: Sending a Bearer Token**

```python
import requests

# Placeholder for a real API endpoint and token
# api_url_token = 'https://api.example.com/data' # Replace with a real API endpoint
auth_token = 'your_secret_api_token_here'      # Replace with your actual token

# We'll use httpbin.org/headers to demonstrate how the header is sent,
# as we don't have a live API that uses 'your_secret_api_token_here'.
httpbin_headers_url = 'https://httpbin.org/headers'

headers_with_token = {
    'Authorization': f'Bearer {auth_token}', # Common format for Bearer tokens
    'X-Custom-Client': 'MyPythonClient'      # Example of another custom header
}

print("\n--- Token-Based Authentication (Header Check with httpbin.org) ---")
try:
    response_token_auth = requests.get(httpbin_headers_url, headers=headers_with_token)
    response_token_auth.raise_for_status()

    print(f"Status Code: {response_token_auth.status_code}")
    
    # httpbin.org/headers will echo back the headers sent
    received_headers = response_token_auth.json().get('headers', {})
    print("Headers sent to server:")
    print(f"  Authorization: {received_headers.get('Authorization')}")
    print(f"  X-Custom-Client: {received_headers.get('X-Custom-Client')}")

except requests.exceptions.HTTPError as http_err:
    print(f"HTTP error with token auth: {http_err}")
except requests.exceptions.RequestException as e:
    print(f"Error with token auth request: {e}")
```
**Expected Output (when using httpbin.org/headers):**
```
--- Token-Based Authentication (Header Check with httpbin.org) ---
Status Code: 200
Headers sent to server:
  Authorization: Bearer your_secret_api_token_here
  X-Custom-Client: MyPythonClient
```
Different APIs might require different header names (e.g., `X-API-Key`, `apikey`) or token schemes (e.g., `Token <your_token>`). Always refer to the specific API's documentation for the correct authentication method and header format.

### SSL Certificate Verification
`requests` verifies SSL certificates for HTTPS requests by default, similar to how a web browser does. This ensures that your communication with the server is secure and that you're connecting to the server you intend to.

*   **Default Behavior:** SSL verification is **enabled**. If `requests` cannot verify the server's certificate (e.g., it's self-signed, expired, or issued by an unknown certificate authority), it will raise an `requests.exceptions.SSLError`.

**Example: Accessing a site with an invalid SSL certificate (for demonstration)**
```python
import requests

# expired.badssl.com is a site designed to have an expired SSL certificate
url_invalid_ssl = 'https://expired.badssl.com/'

print(f"\n--- SSL Verification Demo ---")
try:
    response_ssl_error = requests.get(url_invalid_ssl)
    print(f"Response from {url_invalid_ssl}: {response_ssl_error.status_code}") # This line won't be reached
except requests.exceptions.SSLError as ssl_err:
    print(f"SSLError for {url_invalid_ssl}: {ssl_err}")
except requests.exceptions.RequestException as e: # Catch other potential request errors
    print(f"Other request error for {url_invalid_ssl}: {e}")
```
**Expected Output:**
```
--- SSL Verification Demo ---
SSLError for https://expired.badssl.com/: HTTPSConnectionPool(host='expired.badssl.com', port=443): Max retries exceeded with url: / (Caused by SSLError(SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:XXXX)')))
```
(The exact error message and line number in `_ssl.c` might vary slightly based on your Python and OpenSSL versions.)

#### Custom SSL Certificates (`verify` parameter)

If you are dealing with internal systems that use custom (e.g., self-signed) SSL certificates, you can tell `requests` to use a specific CA bundle file or a directory containing CA certificates by passing the path to the `verify` parameter:

```python
import requests

# Example: Using a custom CA bundle file
# response = requests.get('https://myserver.internal/api', verify='/path/to/custom_ca_bundle.pem')

# Example: Using a directory containing CA certificates
# response = requests.get('https://myserver.internal/api', verify='/path/to/ca_certs_directory/')
```
If `verify` is set to a path to a CA bundle file or directory, `requests` will use those CAs for verification. If you have the server's certificate file itself (not the CA), you can also point `verify` to that file.

#### Disabling SSL Verification (with a Warning)

In some cases (e.g., development environments, trusted internal networks where you understand the risks), you might need to disable SSL verification. **This is generally discouraged for production systems interacting with external services as it introduces security vulnerabilities (e.g., man-in-the-middle attacks).**

To disable SSL verification, set `verify=False`:

```python
import requests
import warnings # To manage warnings

# Suppress only the InsecureRequestWarning, if desired for cleaner output in specific cases.
# This is often done in controlled development environments.
from requests.packages.urllib3.exceptions import InsecureRequestWarning
warnings.simplefilter('ignore', InsecureRequestWarning)


url_disable_ssl = 'https://self-signed.badssl.com/' # Site with a self-signed certificate

print(f"\n--- Disabling SSL Verification (Use with Extreme Caution!) ---")
try:
    # When verify=False, requests will accept any TLS certificate presented by the server
    # and will ignore hostname mismatches and/or expired certificates, which is insecure.
    # An InsecureRequestWarning will be issued unless suppressed.
    response_no_verify = requests.get(url_disable_ssl, verify=False) 
    print(f"Status code from {url_disable_ssl} (SSL verification disabled): {response_no_verify.status_code}")
    # Even if status is 200, the connection was not secure in the usual sense.
except requests.exceptions.RequestException as e:
    print(f"Request error for {url_disable_ssl} (SSL verification disabled): {e}")
```
**Expected Output (when verification is disabled for a site like self-signed.badssl.com):**
```
--- Disabling SSL Verification (Use with Extreme Caution!) ---
Status code from https://self-signed.badssl.com/ (SSL verification disabled): 200
```
When `verify=False` is used, `requests` will issue an `InsecureRequestWarning` if warnings are not suppressed. It's crucial to understand the security implications before disabling SSL verification.

### Session Objects
Session objects allow you to persist certain parameters across multiple requests. They are particularly useful for:
*   **Cookie Persistence:** Cookies set by the server are automatically sent back on subsequent requests made with the same `Session` object. This is essential for interacting with services that use cookies to maintain login sessions or track user state.
*   **Connection Pooling:** When making several requests to the same host, the underlying TCP connection will be reused (HTTP keep-alive), which can significantly improve performance by reducing the overhead of establishing new connections.
*   **Default Headers/Configuration:** You can set default headers, authentication credentials, or other configurations (like `timeout` or `proxies`) on a `Session` object, and they will apply to all requests made by that session instance.

A `Session` object has all the methods of the main `requests` API (e.g., `session.get()`, `session.post()`).

#### Using Session Objects for Cookie Persistence

Let's illustrate how a session object persists cookies:

```python
import requests

# Create a Session object
s = requests.Session()

# First, make a request to a URL that sets a cookie.
# httpbin.org/cookies/set will set a cookie with the name and value provided in the URL.
url_set_cookie = 'https://httpbin.org/cookies/set/mytestcookie/mytestvalue123'
print(f"\n--- Session Object: Setting a cookie ---")
try:
    response_set = s.get(url_set_cookie)
    response_set.raise_for_status()
    print(f"Response from setting cookie (server reflects cookies it just set): {response_set.json().get('cookies')}")

    # Now, make another request to a URL that displays cookies sent by the client.
    # The session 's' should automatically send back the 'mytestcookie' it received.
    url_get_cookies = 'https://httpbin.org/cookies'
    print(f"\n--- Session Object: Checking if cookie is sent back ---")
    response_get = s.get(url_get_cookies)
    response_get.raise_for_status()
    
    # The response from httpbin.org/cookies will show the cookies it received from our client
    cookies_received_by_server = response_get.json().get('cookies', {})
    print(f"Cookies received by server on subsequent request: {cookies_received_by_server}")

    if 'mytestcookie' in cookies_received_by_server and cookies_received_by_server['mytestcookie'] == 'mytestvalue123':
        print("Cookie 'mytestcookie' was successfully persisted and sent back by the session!")
    else:
        print("Cookie 'mytestcookie' was NOT found or had an unexpected value.")

except requests.exceptions.RequestException as e:
    print(f"An error occurred with the session requests: {e}")

# To show that a regular requests.get() (without a session) would not persist the cookie:
print(f"\n--- Regular requests.get() (no session, no cookie persistence) ---")
try:
    # First request sets the cookie, but it's not stored and reused by the default requests module
    # for subsequent independent calls.
    requests.get(url_set_cookie) 
    # Second request (new, independent) won't have the cookie from the previous request.
    r_no_session = requests.get(url_get_cookies) 
    r_no_session.raise_for_status()
    print(f"Cookies received by server (no session): {r_no_session.json().get('cookies')}")
except requests.exceptions.RequestException as e:
    print(f"An error occurred with non-session requests: {e}")
```
**Expected Output:**
```
--- Session Object: Setting a cookie ---
Response from setting cookie (server reflects cookies it just set): {'mytestcookie': 'mytestvalue123'}

--- Session Object: Checking if cookie is sent back ---
Cookies received by server on subsequent request: {'mytestcookie': 'mytestvalue123'}
Cookie 'mytestcookie' was successfully persisted and sent back by the session!

--- Regular requests.get() (no session, no cookie persistence) ---
Cookies received by server (no session): {}
```
This demonstrates that the `Session` object automatically handled the cookie, storing it after the first response and sending it with the subsequent request. In contrast, standalone `requests.get()` calls are stateless regarding cookies.