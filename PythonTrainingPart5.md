Date : 4 Aug 2022

-----------------
## Reading and Writing to text files in Python
Python provides inbuilt functions for creating, writing, and reading files. There are two types of files that can be handled in python, normal text files and binary files (written in binary language, 0s, and 1s).
* Text files: In this type of file, Each line of text is terminated with a special character called EOL (End of Line), which is the new line character (‘\n’) in python by default.
* Binary files: In this type of file, there is no terminator for a line, and the data is stored after converting it into machine-understandable binary language.

In this article, we will be focusing on opening, closing, reading, and writing data in a text file.

### File Access Modes
Access modes govern the type of operations possible in the opened file. It refers to how the file will be used once it's opened. These modes also define the location of the **file pointer** (sometimes called a file handle or cursor), which indicates the current position in the file for reading or writing.

Python provides several access modes:

| Mode | Description                                                                                                                               | File Pointer Position | If File Exists?      | If File Doesn't Exist? |
|------|-------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|----------------------|------------------------|
| `r`  | **Read Only (Default):** Opens the file for reading.                                                                                      | Beginning of file     | Read from start      | `FileNotFoundError`    |
| `r+` | **Read and Write:** Opens for both reading and writing.                                                                                   | Beginning of file     | Read/Write from start| `FileNotFoundError`    |
| `w`  | **Write Only:** Opens for writing. **Caution: Truncates (empties) the file if it exists.**                                                | Beginning of file     | **Truncated**        | Creates new file       |
| `w+` | **Write and Read:** Opens for writing and reading. **Caution: Truncates (empties) the file if it exists.**                               | Beginning of file     | **Truncated**        | Creates new file       |
| `a`  | **Append Only:** Opens for writing. Data is appended to the end of the file.                                                              | End of file           | Appends to end       | Creates new file       |
| `a+` | **Append and Read:** Opens for reading and writing. Data is appended to the end when writing. The pointer is at the end for writing. For reading, the pointer's initial position might depend on the OS or previous operations (often at the end, requiring `seek(0)` to read from the beginning). | End of file (for writing) | Appends to end       | Creates new file       |

**Note on Binary Mode:** You can append `'b'` to any of these modes (e.g., `'rb'`, `'wb'`, `'ab+'`) to open the file in binary mode, which is used for handling non-text files like images or executables.

#### Understanding File Operations and Memory
When you work with files in Python (or any programming language), you're interacting with data stored on **secondary storage** (like your hard drive or SSD). This storage is persistent, meaning data remains even when the computer is powered off.

To use a file (read from it or write to it), Python needs to bring parts of it (or information about it) into the computer's **primary memory** (RAM). RAM is volatile; its contents are lost when the power is off.

Python interacts with files through **file objects** (also sometimes referred to by the concept of "file handlers" or "file descriptors" at the operating system level). When you `open()` a file, the operating system gives your Python program a reference to this file object. This object keeps track of things like the current position in the file (the file pointer) and the mode in which the file was opened. Operations like `read()` and `write()` then occur via this file object, moving data between your program's memory and the file on secondary storage.

#### Opening a File
The built-in `open()` function is used to create a file object and associate it with a file on your system.

**Basic Syntax:**
```python
file_object = open("file_name.txt", "access_mode")
```
*   `file_name.txt`: The name of the file (or its full path if it's not in the current working directory).
*   `access_mode`: A string specifying how you want to open the file (e.g., `'r'`, `'w'`, `'a'`).

**File Path Formatting:**
*   If the file is in the same directory as your Python script, you can just use its name: `open("myfile.txt", "r")`.
*   If the file is in a different directory, you need to provide the path.
    *   **Windows:** Paths use backslashes (`\`). Since `\` is an escape character in Python strings, you should either:
        *   Use raw strings: `open(r"C:\Users\YourName\Documents\myfile.txt", "r")` (recommended)
        *   Escape the backslashes: `open("C:\\Users\\YourName\\Documents\\myfile.txt", "r")`
    *   **macOS/Linux:** Paths use forward slashes (`/`), which don't require special handling in Python strings: `open("/home/yourname/documents/myfile.txt", "r")`
    *   **Cross-platform paths:** For better portability, use `pathlib.Path`:
        ```python
        from pathlib import Path
        file_path = Path("D:") / "Text" / "MyFile2.txt" 
        # file2 = open(file_path, "w+") 
        ```

**Example (Traditional, less recommended way):**
```python
# Open "MyFile.txt" (in the same directory) in append mode
# file1 = open("MyFile.txt", "a") 

# Open "MyFile2.txt" (in D:\Text) in write and read mode, creating it if it doesn't exist
# file2 = open(r"D:\Text\MyFile2.txt", "w+") 
```
(Note: As mentioned, `with open(...)` is preferred for opening files.)

#### Closing a file
The `close()` method flushes any unwritten information and closes the file object, after which no more writing can be done. Python automatically closes a file when the reference object of a file is reassigned to another file. However, it is good practice to use the `close()` method to close a file.

```python
# Opening and Closing a file "MyFile.txt"
# for object name file1.
# file1 = open("MyFile.txt","a") # This is the old way, prefer 'with open()'
# ... some operations ...
# file1.close() # Explicitly closing the file
```
**Caution:** Forgetting to close files or improper handling of exceptions during file operations can lead to resource leaks or data corruption. The `with open(...)` statement is the recommended way to handle files as it ensures files are closed automatically.

### Using the `with open(...)` statement (Recommended)

The `with open(...)` statement is the modern and recommended way to work with files in Python. It simplifies file handling by ensuring that the file is automatically closed when the block of code is exited, even if errors occur. This is achieved through context management.

**Syntax:**
```python
with open("filename.txt", "mode") as file_object:
    # Perform operations on file_object
    # e.g., content = file_object.read()
    # file_object.write("some text")
# File is automatically closed here, outside the 'with' block
```

**Benefits:**
*   **Automatic Resource Management:** The file is guaranteed to be closed when exiting the `with` block, regardless of how the block is exited (normally or due to an exception). This prevents resource leaks.
*   **Cleaner Code:** It eliminates the need for explicit `try...finally` blocks just for closing files, making the code more readable and less verbose.
*   **Error Handling:** While `with` handles closing, you still might need `try...except` blocks inside or outside the `with` statement to handle other file-related errors like `FileNotFoundError` or `PermissionError`.

**Before `with open()` (Manual `try...finally`):**
```python
# Manual file handling (less recommended)
f = None # Initialize f outside try in case open() fails
try:
    f = open("manual_example.txt", "w")
    f.write("This is a manually managed file.\n")
    # Imagine an error occurring here:
    # result = 10 / 0 
except IOError as e:
    print(f"An IOError occurred: {e}")
# except ZeroDivisionError as zde: # Example of another error
    # print(f"A calculation error occurred: {zde}")
finally:
    if f: # Check if f was successfully assigned (file opened)
        print("Closing file manually in 'finally' block.")
        f.close()
    else:
        print("File was not opened or an error occurred before assignment.")
```

**After `with open()` (Recommended):**
```python
# File handling with 'with' statement (recommended)
try:
    with open("with_example.txt", "w") as f:
        f.write("This file is managed by a 'with' statement.\n")
        # Imagine an error occurring here:
        # result = 10 / 0 
        print("File 'with_example.txt' written (will be auto-closed).")
    # File 'f' is automatically closed here.
# except ZeroDivisionError as zde: # Example of another error
    # print(f"A calculation error occurred: {zde}")
except IOError as e: # Catching file-specific errors
    print(f"An IOError occurred: {e}")

print("Exited 'with' block for 'with_example.txt'.")
```
Subsequent examples in this document will primarily use the `with open(...)` statement for file operations.

#### Writing to a file
There are two ways to write in a file.
1. *write() :* Inserts the string str1 in a single line in the text file.
```
File_object.write(str1)
```
2. *writelines() :* For a list of string elements, each string is inserted in the text file.Used to insert multiple strings at a single time.
```python
File_object.writelines(L) for L = [str1, str2, str3] 
```
#### Reading from a file
There are three ways to read data from a text file.

1. `read([n])`: Returns the read bytes in the form of a string. Reads **at most** `n` bytes if `n` is specified; if `n` is not specified or is negative, it reads and returns the entire file content. If the end of the file has been reached, `file_object.read()` will return an empty string (`''`).
```python
File_object.read([n])
```
2. readline() : Reads a line of the file and returns in form of a string.For specified n, reads at most n bytes. However, does not reads more than one line, even if n exceeds the length of the line.
```
File_object.readline([n])
```

3. readlines() : Reads all the lines and return them as each line a string element in a list

```
File_object.readlines()
```

Note: ‘\n’ is treated as a special character of two bytes (on some systems, depending on encoding and OS, it's typically one byte in UTF-8). More accurately, it's a single character representing a newline.

**Example: Demonstrating `read()`, `readline()`, `readlines()`, and `seek()`**

This program demonstrates various ways to read and write data in a file, now updated to use the `with open(...)` statement for better resource management.

```python
# Define the content to be written
lines_to_write = ["This is Delhi \n", "This is Paris \n", "This is London \n"]
initial_content = "Hello \n"
file_name = "myfile_demo.txt" # Using a different name for clarity

# Writing to the file using 'with open()'
try:
    with open(file_name, "w") as file: # Opens in write mode, creates if not exists, truncates if exists
        print(f"Writing initial content and lines to '{file_name}'...")
        file.write(initial_content)
        file.writelines(lines_to_write)
        print("Content written successfully.")
    # File is automatically closed here
except IOError as e:
    print(f"Error writing to file: {e}")

print("-" * 30)

# Reading from the file using 'with open()' in read and write mode ('r+')
try:
    with open(file_name, "r+") as file: # Opens for reading and writing
        print("\n--- Demonstrating file reading methods ---")

        # read(): Reads the entire file content
        print("\nOutput of Read function (entire file):")
        # The file pointer is at the beginning by default in 'r' or 'r+' mode.
        print(file.read())
        print("--- End of read() ---")

        # seek(offset, whence=0): Moves the file pointer.
        # seek(0) moves the pointer to the absolute beginning of the file.
        # This is necessary if you want to read the file again from the start
        # without closing and reopening it.
        print("\nMoving file pointer to the beginning using seek(0)...")
        file.seek(0) 

        # readline(): Reads a single line from the current pointer position
        print("\nOutput of Readline function (first line):")
        print(file.readline(), end='') # end='' to avoid double newline as readline() keeps '\n'
        print("--- End of readline() ---")

        file.seek(0) # Reset pointer to the beginning

        # read(n): Reads at most n characters (or bytes in binary mode)
        print("\nOutput of Read(9) function (first 9 characters):")
        print(file.read(9))
        print("--- End of read(9) ---")

        file.seek(0) # Reset pointer

        # readline(n): Reads at most n characters from the current line
        print("\nOutput of Readline(9) function (first 9 chars of the first line):")
        print(file.readline(9)) # Reads up to 9 chars from the current line
        print("--- End of readline(9) ---")
        
        file.seek(0) # Reset pointer

        # readlines(): Reads all lines from the current pointer position and returns them as a list of strings
        print("\nOutput of Readlines function (all lines as a list):")
        print(file.readlines())
        print("--- End of readlines() ---")

except FileNotFoundError:
    print(f"Error: The file '{file_name}' was not found.")
except IOError as e:
    print(f"Error reading from file: {e}")

```

**Expected Output (for the reading part, assuming writing was successful):**
```
Writing initial content and lines to 'myfile_demo.txt'...
Content written successfully.
------------------------------

--- Demonstrating file reading methods ---

Output of Read function (entire file):
Hello 
This is Delhi 
This is Paris 
This is London 

--- End of read() ---

Moving file pointer to the beginning using seek(0)...

Output of Readline function (first line):
Hello 
--- End of readline() ---

Moving file pointer to the beginning using seek(0)...

Output of Read(9) function (first 9 characters):
Hello 
Th
--- End of read(9) ---

Moving file pointer to the beginning using seek(0)...

Output of Readline(9) function (first 9 chars of the first line):
Hello 
--- End of readline(9) ---

Moving file pointer to the beginning using seek(0)...

Output of Readlines function (all lines as a list):
['Hello \n', 'This is Delhi \n', 'This is Paris \n', 'This is London \n']
--- End of readlines() ---
```
**Explanation of `seek()`:**
The `file.seek(offset, whence)` method changes the current file pointer position.
*   `offset`: The number of bytes to move.
*   `whence` (optional): Defines the starting point for the offset.
    *   `0` (default): Absolute file positioning (from the beginning of the file).
    *   `1`: Seek relative to the current position.
    *   `2`: Seek relative to the file's end.
In the example, `file.seek(0)` is used to move the file pointer back to the start of the file so that subsequent read operations can read the file content from the beginning again. Without `seek(0)`, after the first `file.read()`, the pointer would be at the end of the file, and subsequent `read()`, `readline()`, or `readlines()` calls would return empty strings or lists because there's no more data to read from that point.

### Appending to a file
```python
# Python program to illustrate
# Append vs write mode
file1 = open("myfile.txt","w")
L = ["This is Delhi \n","This is Paris \n","This is London \n"]
file1.writelines(L)
file1.close()

# Append-adds at last
file1 = open("myfile.txt","a")#append mode
file1.write("Today \n")
file1.close()

file1 = open("myfile.txt","r")
print("Output of Readlines after appending")
print(file1.readlines())
print()
file1.close()

# Write-Overwrites
file1 = open("myfile.txt","w")#write mode
file1.write("Tomorrow \n")
file1.close()

file1 = open("myfile.txt","r")
print("Output of Readlines after writing")
print(file1.readlines())
print()
file1.close()
```
Output:
```
Output of Readlines after appending
['This is Delhi \n', 'This is Paris \n', 'This is London \n', 'Today \n']

Output of Readlines after writing
['Tomorrow \n']
```

### Working with Different File Encodings

Text is stored as bytes, and encoding defines how characters are represented as those bytes. Common encodings include:
*   **UTF-8:** A variable-width encoding that can represent every character in the Unicode standard. It's the dominant encoding for the web and recommended for most text files today due to its broad compatibility.
*   **ASCII:** An older, 7-bit encoding that can only represent 128 characters (basic English letters, digits, punctuation). It cannot represent accented characters, symbols from other languages, or emojis.
*   **ISO-8859-1 (Latin-1):** An 8-bit encoding that extends ASCII to include characters for Western European languages.

When opening a file for reading or writing text, you can (and often should) specify its encoding using the `encoding` parameter of the `open()` function. If no encoding is specified, Python uses a system-dependent default encoding (which can be checked with `locale.getpreferredencoding()`), which might not always be what you want.

**Syntax:**
```python
with open("filename.txt", mode="r", encoding="utf-8") as f:
    # ... operations ...
```

**Example: Reading and Writing with a Specific Encoding (UTF-8)**
```python
# File encoding example
file_name_encoded = "encoded_file.txt"
text_to_write = "Hello, world! Привет, мир! 你好，世界！ 😊" # Includes non-ASCII characters

try:
    # Writing with UTF-8 encoding
    with open(file_name_encoded, "w", encoding="utf-8") as f:
        f.write(text_to_write)
    print(f"Successfully wrote to '{file_name_encoded}' with UTF-8 encoding.")

    # Reading with UTF-8 encoding
    with open(file_name_encoded, "r", encoding="utf-8") as f:
        content = f.read()
        print(f"Read content from '{file_name_encoded}' (UTF-8):")
        print(content)
    
    # Attempting to read with an incompatible encoding (ASCII) to show potential error
    print("\nAttempting to read the UTF-8 encoded file as ASCII...")
    with open(file_name_encoded, "r", encoding="ascii") as f: # This will likely cause an error
        try:
            content_ascii_error = f.read()
            print(f"Content if read as ASCII (might be garbled or error): {content_ascii_error}")
        except UnicodeDecodeError as e:
            print(f"UnicodeDecodeError caught: {e}")
            print("This error occurs because ASCII cannot represent all characters in the UTF-8 encoded file.")

except IOError as e:
    print(f"An I/O error occurred: {e}")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
```
**Expected Output:**
```
Successfully wrote to 'encoded_file.txt' with UTF-8 encoding.
Read content from 'encoded_file.txt' (UTF-8):
Hello, world! Привет, мир! 你好，世界！ 😊

Attempting to read the UTF-8 encoded file as ASCII...
UnicodeDecodeError caught: 'ascii' codec can't decode byte 0xd0 in position 14: ordinal not in range(128)
This error occurs because ASCII cannot represent all characters in the UTF-8 encoded file.
```
**Key Points for Encodings:**
*   Always be mindful of the encoding of files you are working with.
*   UTF-8 is a good default for new text files.
*   If you encounter `UnicodeDecodeError` when reading a file, it often means you're trying to read it with the wrong encoding.
*   If you see garbled text (mojibake), it might also be an encoding mismatch.
*   The `errors` argument in `open()` can specify how to handle encoding errors (e.g., `errors='ignore'` or `errors='replace'`), but it's usually better to identify and use the correct encoding.

### Working with JSON Files

JSON (JavaScript Object Notation) is a lightweight data-interchange format that is easy for humans to read and write and easy for machines to parse and generate. Python's built-in `json` module provides methods to work with JSON data.

**Common Operations:**
*   **`json.dump(data, file_object, indent=None)`:** Serializes a Python object (`data`, typically a dictionary or list) as a JSON formatted stream to a file-like object (`file_object`). `indent` can be used for pretty-printing.
*   **`json.dumps(data, indent=None)`:** Serializes a Python object to a JSON formatted string.
*   **`json.load(file_object)`:** Deserializes a JSON formatted stream from a file-like object into a Python object.
*   **`json.loads(json_string)`:** Deserializes a JSON formatted string into a Python object.

**Example: Writing to and Reading from a JSON file**
```python
import json

data_to_store = {
    "name": "John Doe",
    "age": 30,
    "isStudent": False,
    "courses": [
        {"title": "History", "credits": 3},
        {"title": "Math", "credits": 4}
    ],
    "address": None
}
json_file_name = "data.json"

try:
    # Writing Python dictionary to a JSON file
    with open(json_file_name, "w", encoding="utf-8") as f:
        json.dump(data_to_store, f, indent=4) # indent=4 for pretty printing
    print(f"Data successfully written to {json_file_name}")

    # Reading data from the JSON file
    with open(json_file_name, "r", encoding="utf-8") as f:
        loaded_data = json.load(f)
    print(f"\nData loaded from {json_file_name}:")
    print(type(loaded_data)) # Will be <class 'dict'>
    print(loaded_data)
    print(f"Name: {loaded_data.get('name')}")

except FileNotFoundError:
    print(f"Error: The file {json_file_name} was not found for reading.")
except json.JSONDecodeError as e:
    print(f"Error decoding JSON from {json_file_name}: {e}")
except IOError as e:
    print(f"An I/O error occurred: {e}")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
```
**Expected Output:**
```
Data successfully written to data.json

Data loaded from data.json:
<class 'dict'>
{'name': 'John Doe', 'age': 30, 'isStudent': False, 'courses': [{'title': 'History', 'credits': 3}, {'title': 'Math', 'credits': 4}], 'address': None}
Name: John Doe
```

### Working with CSV Files

CSV (Comma Separated Values) is a common plain text format for storing tabular data. Each line in a CSV file represents a row, and columns within that row are typically separated by commas. Python's built-in `csv` module provides tools to easily read and write CSV files.

**Key `csv` module objects:**
*   **`csv.reader(file_object, delimiter=',', quotechar='"', ...)`:** Returns a reader object which will iterate over lines in the given `file_object`.
*   **`csv.writer(file_object, delimiter=',', quotechar='"', quoting=csv.QUOTE_MINIMAL, ...)`:** Returns a writer object responsible for converting the user’s data into delimited strings on the given file-like object.
*   **`csv.DictReader(file_object, fieldnames=None, ...)`:** Creates an object that operates like a regular reader but maps the information in each row to a `dict` whose keys are given by the optional `fieldnames` parameter or inferred from the first row of the CSV file.
*   **`csv.DictWriter(file_object, fieldnames, ...)`:** Creates an object which operates like a regular writer but maps dictionaries onto output rows. The `fieldnames` parameter is a sequence of keys that identify the order in which values in the dictionary passed to the `writerow()` method are written to the file.

**Example: Writing to and Reading from a CSV file using `DictReader` and `DictWriter`**
```python
import csv

csv_file_name = "students.csv"
field_names = ['name', 'age', 'grade', 'major']
student_data = [
    {'name': 'Alice', 'age': 20, 'grade': 'A', 'major': 'Computer Science'},
    {'name': 'Bob', 'age': 22, 'grade': 'B', 'major': 'Physics'},
    {'name': 'Charlie', 'age': 21, 'grade': 'A-', 'major': 'Mathematics'}
]

try:
    # Writing to a CSV file using DictWriter
    # It's important to open CSV files with newline='' to prevent blank rows on some platforms.
    with open(csv_file_name, mode="w", newline='', encoding="utf-8") as f_write:
        writer = csv.DictWriter(f_write, fieldnames=field_names)
        writer.writeheader()  # Writes the header row
        writer.writerows(student_data) # Writes all rows from the list of dicts
    print(f"Data successfully written to {csv_file_name}")

    # Reading from a CSV file using DictReader
    print(f"\nData read from {csv_file_name}:")
    with open(csv_file_name, mode="r", newline='', encoding="utf-8") as f_read:
        reader = csv.DictReader(f_read)
        for row in reader:
            # Each 'row' is an OrderedDict (or dict in newer Python versions)
            print(f"  Name: {row['name']}, Age: {row['age']}, Grade: {row['grade']}, Major: {row['major']}")

except FileNotFoundError:
    print(f"Error: The file {csv_file_name} was not found for reading.")
except IOError as e:
    print(f"An I/O error occurred: {e}")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
```
**Expected Output:**
```
Data successfully written to students.csv

Data read from students.csv:
  Name: Alice, Age: 20, Grade: A, Major: Computer Science
  Name: Bob, Age: 22, Grade: B, Major: Physics
  Name: Charlie, Age: 21, Grade: A-, Major: Mathematics
```
Using `DictReader` and `DictWriter` is often preferred when working with CSVs that have headers, as it allows you to access columns by name rather than index. Remember `newline=''` to correctly handle line endings across different platforms.

## Input and Output in Python

Python provides several built-in functions for handling input from the user and displaying output.

### How to Take Input from User in Python

The `input()` function is used to get input from the user. It reads a line from the input (usually the keyboard), converts it to a string, and returns it.

**Syntax:**
```python
variable = input('prompt_message')
```
*   `prompt_message` (optional): A string that is displayed to the user before they enter input.

**Example 1: Basic string input**
```python
# Taking input from the user
name = input("Enter your name: ")

# Output
print("Hello, " + name + "!") # Using string concatenation
print(f"Welcome, {name}!")   # Using an f-string (more modern)
print(f"The type of 'name' is: {type(name)}")
```
Output:
```
Enter your name: GFG
Hello, GFG!
Welcome, GFG!
The type of 'name' is: <class 'str'>
```
**Note:** The `input()` function **always** returns a string. If you need a different data type (like an integer or float), you must explicitly convert it.

**Example 2: Integer input and type conversion**
```python
# Taking input from the user and converting to an integer
try:
    num_str = input("Enter a number: ")
    num = int(num_str) # Explicitly convert the input string to an integer

    add = num + 1
    # Output
    print(f"You entered {num}. Adding 1 gives: {add}")
    print(f"The type of 'num' is: {type(num)}")
except ValueError:
    print(f"Error: '{num_str}' is not a valid integer. Please enter a whole number.")
```
Output (if user enters "25"):
```
Enter a number: 25
You entered 25. Adding 1 gives: 26
The type of 'num' is: <class 'int'>
```
Output (if user enters "hello"):
```
Enter a number: hello
Error: 'hello' is not a valid integer. Please enter a whole number.
```

### How to take Multiple Inputs in Python

You can take multiple inputs from the user in a single line by splitting the input string and then mapping the parts to the desired data type.

*   **`split(separator=None, maxsplit=-1)` method:** Splits a string into a list of substrings.
    *   If `separator` is not provided or is `None`, any whitespace string is a separator and empty strings are removed from the result.
    *   If `separator` is specified (e.g., `','`, `' '`), it acts as the delimiter.
*   **`map(function, iterable)` function:** Applies `function` to every item of `iterable` and returns a map object (which is an iterator).

**Example: Taking multiple integer inputs separated by spaces**
```python
# Taking multiple integer inputs separated by spaces
try:
    print("Enter three numbers separated by spaces (e.g., 10 20 30):")
    a, b, c = map(int, input().split()) 
    # 1. input() reads the line: "10 20 30"
    # 2. .split() splits it by space into a list: ['10', '20', '30']
    # 3. map(int, ...) applies int() to each item: [10, 20, 30]
    # 4. The three integers are unpacked into variables a, b, c

    print("The numbers are:", a, b, c)
    print(f"Their sum is: {a + b + c}")
except ValueError:
    print("Error: Please enter numbers separated by spaces, e.g., '10 20 30'.")

# Example: Taking multiple string inputs separated by commas
print("\nEnter three fruits separated by commas (e.g., apple,banana,cherry):")
fruit1, fruit2, fruit3 = map(str, input().split(',')) # Using ',' as a custom delimiter
# map(str, ...) is often redundant here as split() already gives strings, but shown for consistency
print("The fruits are:", fruit1.strip(), fruit2.strip(), fruit3.strip()) # .strip() removes leading/trailing whitespace
```
Output:
```
Enter three numbers separated by spaces (e.g., 10 20 30):
10 20 30
The numbers are: 10 20 30
Their sum is: 60

Enter three fruits separated by commas (e.g., apple,banana,cherry):
apple, banana, cherry
The fruits are: apple banana cherry
```

### How to take inputs for Sequence Data Types (List, Set, Tuple)

#### Taking List/Set elements
You can populate lists or sets in a couple of ways:

1.  **Element by element (using a loop):**
    ```python
    my_list = []
    n = int(input("Enter the number of elements for the list: "))
    print("Enter the elements:")
    for _ in range(n):
        item = input("Enter element: ") # Or int(input()), float(input()), etc.
        my_list.append(item)
    print(f"Your list: {my_list}")
    ```

2.  **Using `map()` and `split()` (for a single line of input):**
    This is very common for competitive programming or when input items are space-separated.
    ```python
    # Input for a list of integers
    integer_list = list(map(int, input("Enter space-separated integers for a list: ").split()))
    print(f"Integer List: {integer_list}")

    # Input for a set of strings
    string_set = set(input("Enter space-separated strings for a set: ").split())
    print(f"String Set: {string_set}")
    ```
    Output Example:
    ```
    Enter space-separated integers for a list: 1 2 3 4 5
    Integer List: [1, 2, 3, 4, 5]
    Enter space-separated strings for a set: apple banana apple orange
    String Set: {'orange', 'apple', 'banana'}
    ```

#### Taking Input for Tuples
Tuples are immutable, meaning you cannot directly append elements to an existing tuple after it's created. To "add" an element, you typically:
1.  Convert the tuple to a list.
2.  Append the new element(s) to the list.
3.  Convert the list back to a tuple.

Or, more commonly, you create a tuple directly from an input sequence:
```python
# Creating a tuple from a space-separated string of numbers
input_string = input("Enter space-separated numbers for a tuple: ")
try:
    number_tuple = tuple(map(int, input_string.split()))
    print(f"Created tuple: {number_tuple}")
except ValueError:
    print("Invalid input. Please enter numbers separated by spaces.")

# Example of "adding" to an existing tuple (by creating a new one)
original_tuple = (2, 3, 4, 5, 6)
print(f"\nOriginal Tuple: {original_tuple}")
try:
    new_element_str = input("Enter a new integer element to add: ")
    new_element = int(new_element_str)
    
    # Create a new tuple by concatenating
    updated_tuple = original_tuple + (new_element,) # Note the comma to make (new_element,) a tuple
    print(f"Tuple after adding the new element: {updated_tuple}")
except ValueError:
    print(f"Invalid input: '{new_element_str}' is not an integer.")
```
Output Example:
```
Enter space-separated numbers for a tuple: 7 8 9
Created tuple: (7, 8, 9)

Original Tuple: (2, 3, 4, 5, 6)
Enter a new integer element to add: 35
Tuple after adding the new element: (2, 3, 4, 5, 6, 35)
```

### How to Display Output in Python

The `print()` function is used to display output to the console.

**Syntax:**
```python
print(value(s), sep=' ', end='\n', file=sys.stdout, flush=False)
```
**Parameters:**
*   `value(s)`: One or more objects to be printed. They will be converted to strings before being displayed.
*   `sep='separator'` (optional): Specifies how to separate multiple objects. Default is a single space (`' '`).
*   `end='end'` (optional): Specifies what to print at the end of all values. Default is a newline character (`'\n'`).
*   `file` (optional): An object with a `write(string)` method. Default is `sys.stdout` (the standard output stream, usually your console).
*   `flush` (optional): A boolean. If `True`, the stream is forcibly flushed. Default is `False`.

**Example: Basic `print()` usage**
```python
print("GFG") # Prints GFG followed by a newline
print('G', 'F', 'G') # Prints G F G followed by a newline (default sep is space)
```
Output:
```
GFG
G F G
```

**Example: `print()` with custom `sep` and `end` parameters**
```python
print("GFG", end="@") # Prints GFG, then @, then stays on the same line
print('G', 'F', 'G', sep="#") # Prints G#F#G, then a newline
```
Output:
```
GFG@G#F#G
```

### Formatting Output
Python offers several ways to format output strings, making them more readable and structured.

#### 1. Using Formatted String Literals (f-strings)
Introduced in Python 3.6, f-strings are the most modern and often preferred way to format strings. They are prefixed with `f` or `F` and allow you to embed expressions inside string literals by placing them inside curly braces `{}`.

**Example: f-string formatting**
```python
name = "Alice"
age = 30
print(f"Hello, {name}! You are {age} years old.")
print(f"In 5 years, {name} will be {age + 5} years old.")
# You can also include formatting specifications:
pi_approx = 3.14159265
print(f"Pi to 3 decimal places: {pi_approx:.3f}")
```
Output:
```
Hello, Alice! You are 30 years old.
In 5 years, Alice will be 35 years old.
Pi to 3 decimal places: 3.142
```

#### 2. Using the `str.format()` method
This method is available on string objects and uses curly braces `{}` as placeholders, which are then filled by the arguments to `format()`.

**Example: `str.format()`**
```python
item = "book"
price = 19.99
quantity = 2

# Positional arguments
print("Item: {}, Price: ${}, Quantity: {}".format(item, price, quantity))
# Indexed arguments
print("Item: {0}, Price: ${1:.2f}, Quantity: {2}".format(item, price, quantity))
# Keyword arguments
print("Item: {itm}, Price: ${prc:.2f}, Quantity: {qty}".format(itm=item, prc=price, qty=quantity))
```
Output:
```
Item: book, Price: $19.99, Quantity: 2
Item: book, Price: $19.99, Quantity: 2
Item: book, Price: $19.99, Quantity: 2
```

#### 3. Using the `%` Operator (Old Style)
This is an older style of string formatting, similar to `printf` in C. It uses `%` followed by a format specifier (e.g., `%s` for string, `%d` for integer, `%f` for float).

*   `%d` – integer
*   `%f` – float (e.g., `%.2f` for 2 decimal places)
*   `%s` – string
*   `%x` – hexadecimal
*   `%o` – octal

**Note:** While still functional, f-strings and `str.format()` are generally preferred in modern Python code for their improved readability and flexibility.

**Example: `%` operator formatting**
```python
name = "Bob"
score = 95.7
print("Name: %s, Score: %.1f%%" % (name, score)) # Note: %% to print a literal %
```
Output:
```
Name: Bob, Score: 95.7%
```

## Python Type Casting
Type Casting (or type conversion) is the process of changing a variable's data type from one type to another. Python supports both implicit and explicit type casting.

### Implicit Type Conversion
Implicit type conversion is performed automatically by the Python interpreter when an operation involves different data types that are compatible. Python promotes the "smaller" data type to the "larger" data type to avoid data loss. For example, adding an integer and a float results in a float.

```python
# Python program to demonstrate implicit type casting

# Integer type
a = 7
print(f"Variable 'a' is {a} of type: {type(a)}")

# Float type
b = 3.0
print(f"Variable 'b' is {b} of type: {type(b)}")

# Python automatically converts 'a' to float for the addition
c = a + b 
print(f"Sum 'c' ({a} + {b}) is {c} of type: {type(c)}")

# Python automatically converts 'a' to float for the multiplication
d = a * b
print(f"Product 'd' ({a} * {b}) is {d} of type: {type(d)}")

# Example: Integer and boolean
e = 10
f_bool = True # True is 1, False is 0 in numeric contexts
sum_bool_int = e + f_bool
print(f"Sum of {e} and {f_bool} is {sum_bool_int} of type: {type(sum_bool_int)}") # Becomes int
```
Output:
```
Variable 'a' is 7 of type: <class 'int'>
Variable 'b' is 3.0 of type: <class 'float'>
Sum 'c' (7 + 3.0) is 10.0 of type: <class 'float'>
Product 'd' (7 * 3.0) is 21.0 of type: <class 'float'>
Sum of 10 and True is 11 of type: <class 'int'>
```

### Explicit Type Casting
Explicit type casting (or explicit type conversion) requires the programmer to manually convert a variable from one data type to another using built-in functions like `int()`, `float()`, `str()`, `list()`, `tuple()`, `set()`, `bool()`, etc.

**Common Type Casting Functions:**
*   `int(value, base=10)`: Converts `value` to an integer. `base` is optional (default is 10). Can convert floats (by truncating) and strings representing numbers.
*   `float(value)`: Converts `value` to a floating-point number. Can convert integers and strings representing numbers.
*   `str(object)`: Converts `object` to its string representation.
*   `list(iterable)`: Converts an `iterable` (e.g., tuple, string, set, dictionary keys) to a list.
*   `tuple(iterable)`: Converts an `iterable` to a tuple.
*   `set(iterable)`: Converts an `iterable` to a set (removes duplicates).
*   `bool(value)`: Converts `value` to a boolean (`True` or `False`). Most values are `True` except for `False`, `None`, numeric zero of all types, and empty sequences/mappings.

#### Examples of Explicit Type Casting:

**1. Numeric Conversions (int, float, str):**
```python
# Integer to float
int_val = 5
float_val = float(int_val)
print(f"Integer {int_val} to float: {float_val} (type: {type(float_val)})") # 5.0

# Float to integer (truncates decimal part)
float_val_2 = 5.987
int_val_2 = int(float_val_2)
print(f"Float {float_val_2} to integer: {int_val_2} (type: {type(int_val_2)})") # 5

# String to integer
str_num = "123"
try:
    int_from_str = int(str_num)
    print(f"String '{str_num}' to integer: {int_from_str} (type: {type(int_from_str)})") # 123
except ValueError:
    print(f"Error: Could not convert string '{str_num}' to integer.")

str_invalid_num = "45.67" # This is a float string, not an int string
try:
    int_from_invalid_str = int(str_invalid_str)
    print(f"String '{str_invalid_num}' to integer: {int_from_invalid_str}")
except ValueError as e:
    print(f"Error converting string '{str_invalid_num}' to int: {e}") # ValueError

# String to float
str_float = "78.99"
try:
    float_from_str = float(str_float)
    print(f"String '{str_float}' to float: {float_from_str} (type: {type(float_from_str)})") # 78.99
except ValueError:
    print(f"Error: Could not convert string '{str_float}' to float.")

# Integer/Float to String
num_to_str = str(100)
float_to_str = str(23.45)
print(f"Integer 100 to string: '{num_to_str}' (type: {type(num_to_str)})")
print(f"Float 23.45 to string: '{float_to_str}' (type: {type(float_to_str)})")
```
Output:
```
Integer 5 to float: 5.0 (type: <class 'float'>)
Float 5.987 to integer: 5 (type: <class 'int'>)
String '123' to integer: 123 (type: <class 'int'>)
Error converting string '45.67' to int: invalid literal for int() with base 10: '45.67'
String '78.99' to float: 78.99 (type: <class 'float'>)
Integer 100 to string: '100' (type: <class 'str'>)
Float 23.45 to string: '23.45' (type: <class 'str'>)
```

**2. Casting to Boolean (`bool()`):**
Python has a concept of "truthy" and "falsy" values.
*   **Falsy values:** `False`, `None`, numeric zero (e.g., `0`, `0.0`, `0j`), empty sequences (e.g., `''`, `[]`, `()`, `{}`), empty mappings (e.g., `{}`).
*   **Truthy values:** Most other values are considered `True`.

```python
print(f"\n--- Boolean Casting ---")
print(f"bool(0): {bool(0)}")         # False
print(f"bool(1): {bool(1)}")         # True
print(f"bool(-10): {bool(-10)}")     # True
print(f"bool(0.0): {bool(0.0)}")     # False
print(f"bool(''): {bool('')}")       # False
print(f"bool('Hello'): {bool('Hello')}") # True
print(f"bool([]): {bool([])}")       # False (empty list)
print(f"bool([1,2]): {bool([1,2])}") # True (non-empty list)
print(f"bool(None): {bool(None)}")   # False
```
Output:
```
--- Boolean Casting ---
bool(0): False
bool(1): True
bool(-10): True
bool(0.0): False
bool(''): False
bool('Hello'): True
bool([]): False
bool([1,2]): True
bool(None): False
```

**3. Casting Between Sequence Types (`list()`, `tuple()`, `set()`):**
```python
print(f"\n--- Sequence Type Casting ---")
my_string = "hello"
my_list = [1, 2, 2, 3, 4]
my_tuple = (10, 20, 30, 20)

# String to list/tuple/set
print(f"String '{my_string}' to list: {list(my_string)}")   # ['h', 'e', 'l', 'l', 'o']
print(f"String '{my_string}' to tuple: {tuple(my_string)}") # ('h', 'e', 'l', 'l', 'o')
print(f"String '{my_string}' to set: {set(my_string)}")     # {'o', 'h', 'l', 'e'} (order may vary, duplicates removed)

# List to tuple/set
print(f"List {my_list} to tuple: {tuple(my_list)}") # (1, 2, 2, 3, 4)
print(f"List {my_list} to set: {set(my_list)}")     # {1, 2, 3, 4} (duplicates removed)

# Tuple to list/set
print(f"Tuple {my_tuple} to list: {list(my_tuple)}") # [10, 20, 30, 20]
print(f"Tuple {my_tuple} to set: {set(my_tuple)}")   # {10, 20, 30} (duplicates removed)
```
Output:
```
--- Sequence Type Casting ---
String 'hello' to list: ['h', 'e', 'l', 'l', 'o']
String 'hello' to tuple: ('h', 'e', 'l', 'l', 'o')
String 'hello' to set: {'l', 'o', 'e', 'h'}
List [1, 2, 2, 3, 4] to tuple: (1, 2, 2, 3, 4)
List [1, 2, 2, 3, 4] to set: {1, 2, 3, 4}
Tuple (10, 20, 30, 20) to list: [10, 20, 30, 20]
Tuple (10, 20, 30, 20) to set: {10, 20, 30}
```
Explicit type casting is essential when you need to ensure data is in the correct format for operations, function arguments, or storage. Always be mindful of potential `ValueError` exceptions when converting strings to numeric types.