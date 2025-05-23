## Virtual Environments

In Python development, managing project dependencies and ensuring that different projects don't interfere with each other is crucial. This is where virtual environments come into play.

### What are Virtual Environments and Why Use Them?

A **virtual environment** is an isolated Python environment that allows you to manage dependencies for a specific project separately from your global Python installation and other projects. Think of it as a self-contained directory tree that includes a specific version of Python and various additional packages.

**Key Benefits:**

*   **Avoiding Package Conflicts:** Different projects might require different versions of the same package. Without virtual environments, installing a new version for one project could break another. Virtual environments keep these dependencies separate.
*   **Clean Global Python Installation:** Your system's global Python installation remains clean and uncluttered by project-specific packages. This reduces the risk of versioning issues at the system level.
*   **Project-Specific Python Versions (with tools like `pyenv`):** While `venv` primarily manages package versions, tools like `pyenv` can be used in conjunction to manage different Python interpreter versions for different projects.
*   **Reproducibility:** Virtual environments make it easy to replicate a project's setup on another machine or at a later time. By listing a project's dependencies (typically in a `requirements.txt` file), you can quickly recreate the exact environment needed.
*   **Dependency Management:** Clearly defines and isolates what packages a particular project needs, making it easier to track and manage dependencies.

### Using `venv` (Python's Built-in Module)

Python comes with a built-in module called `venv` for creating virtual environments. It's the recommended way for most projects.

#### 1. Creating a Virtual Environment

To create a virtual environment, navigate to your project's root directory in your terminal and run:

```bash
python -m venv <environment_name>
```

A common convention is to name the environment `venv` or `.venv`.

**Example:**

```bash
# Navigate to your project folder
# cd my_python_project

# Create a virtual environment named 'venv'
python -m venv venv 
```
This command creates a new directory (e.g., `venv`) in your project folder. This directory contains:
*   A copy or symlink of the Python interpreter used to create the environment.
*   A `pyvenv.cfg` configuration file.
*   Subdirectories like `Scripts` (on Windows) or `bin` (on macOS/Linux) containing activation scripts and executables for pip and Python within this environment.
*   A `Lib` (Windows) or `lib` (macOS/Linux) directory where packages installed in this environment will reside.

#### 2. Activating the Virtual Environment

Once created, you need to "activate" the environment. Activation modifies your shell's PATH to point to the scripts and executables within the virtual environment.

*   **On Windows (Command Prompt or PowerShell):**
    ```batch
    venv\Scripts\activate
    ```
    (If using PowerShell, you might need to set execution policy: `Set-ExecutionPolicy Unrestricted -Scope Process` first, then run `venv\Scripts\Activate.ps1`)

*   **On macOS and Linux (bash/zsh):**
    ```bash
    source venv/bin/activate
    ```

**After activation, your shell prompt will typically change** to indicate that the virtual environment is active. For example, it might look like `(venv) C:\path\to\project> ` or `(venv) user@hostname:~/my_python_project$ `.

#### 3. Working in an Active Environment

With the virtual environment active:

*   **`pip install <package_name>`:** Any packages you install using `pip` will be installed *only* within this active virtual environment, not globally.
    ```bash
    (venv) $ pip install requests
    (venv) $ pip install numpy==1.20.3 
    ```
*   **`python` command:** Running `python` will use the interpreter isolated within the virtual environment. Any scripts you run will use this interpreter and its installed packages.
    ```bash
    (venv) $ python --version 
    # Will show the Python version of the venv
    (venv) $ python my_script.py 
    # my_script.py will use packages installed in 'venv'
    ```
*   **`pip list`:** Will show packages installed specifically in the active environment.

#### 4. Deactivating the Virtual Environment

When you're done working on the project, you can deactivate the environment to revert to your global Python context.

Simply type:
```bash
deactivate
```
Your shell prompt will return to normal.

### Best Practices for Virtual Environments

*   **One Environment Per Project:** Create a separate virtual environment for each Python project you work on. This ensures complete isolation of dependencies.
*   **Store Within Project Directory:** It's common practice to create the virtual environment directory directly inside your project's root folder (e.g., name it `venv` or `.venv`).
*   **Add to `.gitignore`:** The virtual environment directory (e.g., `venv/` or `.venv/`) should **always** be added to your project's `.gitignore` file. This directory can be large and contains files specific to your OS and Python build; it doesn't need to be (and shouldn't be) tracked by version control. Other collaborators will create their own environments based on the `requirements.txt` file.

    Example `.gitignore` entry:
    ```
    # Virtual Environment
    venv/
    .venv/
    ```

Virtual environments are a cornerstone of modern Python development, promoting cleaner, more manageable, and reproducible projects.

## Python PIP (Pip Installs Packages)

**PIP** (Pip Installs Packages) is the standard package manager for Python. It allows you to install and manage additional libraries and dependencies that are not part of the Python standard library. These packages are typically sourced from the Python Package Index (PyPI).

The basic syntax for `pip` commands in your terminal or command prompt is:

```bash
pip <command> [options] [arguments]
```
For example, `pip install numpy` or `pip list --outdated`.

### How to install pip?
**PIP** comes pre-installed with Python versions **3.4 and newer**. For older versions, manual installation might be required.

To check if `pip` is installed and to see its version, open your terminal or command prompt and type:

```bash
pip --version
```
If it's installed, you'll see output like `pip 23.0.1 from /path/to/pip (python 3.9)`.

### How to install Package with Pip

We can install additional packages by using the Python pip install command. Let’s suppose we want to install the Numpy using pip. We can do it using the below command.

Syntax:
```
pip install numpy
```

### Specifying Package Version

Syntax:
```
pip install package_name==version
```

### Display package information using pip

Syntax: 

```
pip show numpy
```
Note: 

* Requires column shows the dependencies required by the NumPy package
* Required by shows the packages that require NumPy

### Get a list of locally installed Python modules

Syntax:
```
pip list
```
### Uninstall packages with pip

Syntax:
```sh
pip uninstall numpy
```

Note: The pip uninstall command does not uninstall the package dependencies. If you want to remove the dependencies as well then you can see the dependencies using the pip show command and remove each package manually.


### Search packages with pip

Syntax:
```
pip search numpy
```
**Note on `pip search`:** As of late 2020/early 2021, the `pip search` command has been deprecated due to its reliance on an outdated XML-RPC API that PyPI (the Python Package Index) has discontinued for performance and security reasons. While it might still appear to work in some older `pip` versions, it's unreliable. **The recommended way to search for packages is directly on the PyPI website: [https://pypi.org/](https://pypi.org/)**.

### Managing Project Dependencies with `requirements.txt`

A `requirements.txt` file is a standard way to list the Python packages required for a specific project, along with their versions. This allows for easy and consistent replication of the project's environment.

#### 1. Generating `requirements.txt` with `pip freeze`

The `pip freeze` command is used to output a list of all currently installed packages in the active environment, in a format suitable for a `requirements.txt` file.

*   **Command:**
    ```bash
    pip freeze > requirements.txt
    ```
*   **Important:** Always run this command when your project's **virtual environment is active**. This ensures that only the packages relevant to your current project are listed, not globally installed packages.

**What `pip freeze` does:**
It lists all installed packages (including their exact versions) that were installed via `pip` in the current environment. Packages that are part of the Python standard library are not included.

#### 2. Purpose and Importance of `requirements.txt`

*   **Reproducibility:** Allows other developers (or your future self) to quickly set up an identical environment with all necessary dependencies.
*   **Collaboration:** Essential when working in teams, ensuring everyone uses the same package versions.
*   **Deployment:** Used by deployment tools and platforms to install the correct dependencies when deploying your application.
*   **Version Control:** The `requirements.txt` file should always be committed to your version control system (e.g., Git).

#### 3. Installing Packages from `requirements.txt`

To install all packages listed in a `requirements.txt` file, use:

```bash
pip install -r requirements.txt
```
This command reads the file and installs each specified package and version.

#### 4. Detailed Workflow Example

Here's a step-by-step example of a typical workflow using virtual environments and `requirements.txt`:

1.  **Navigate to your project directory:**
    ```bash
    cd path/to/your/my_python_project
    ```

2.  **Create a virtual environment (e.g., named `venv`):**
    ```bash
    python -m venv venv
    ```

3.  **Activate the virtual environment:**
    *   On macOS/Linux:
        ```bash
        source venv/bin/activate
        ```
        *(Your prompt should change, e.g., `(venv) $`)*
    *   On Windows:
        ```batch
        venv\Scripts\activate
        ```
        *(Your prompt should change, e.g., `(venv) C:\path\to\project>`)*

4.  **Install your project's dependencies:**
    Let's say your project needs `requests` and a specific version of `numpy`.
    ```bash
    (venv) $ pip install requests
    (venv) $ pip install numpy==1.23.5 
    (venv) $ pip install pandas # Another example package
    ```

5.  **Generate (or update) `requirements.txt`:**
    After installing or changing dependencies, update your requirements file.
    ```bash
    (venv) $ pip freeze > requirements.txt
    ```
    The `requirements.txt` file will now contain something like:
    ```
    # requirements.txt (example content)
    certifi==2023.7.22
    charset-normalizer==3.3.0
    idna==3.4
    numpy==1.23.5
    pandas==2.0.3 # Assuming pandas was installed
    python-dateutil==2.8.2
    pytz==2023.3.post1
    requests==2.31.0
    six==1.16.0
    urllib3==1.26.16 
    # Note: Actual versions and other indirect dependencies might vary.
    ```

6.  **Add `venv` directory to `.gitignore`:**
    Create or edit your `.gitignore` file in the project root and add the virtual environment directory:
    ```
    venv/
    *.pyc
    __pycache__/
    ```
    Commit `requirements.txt` and `.gitignore` to your version control.

7.  **Setting up the project elsewhere (for another user or future you):**
    *   Clone the repository (if applicable).
    *   Navigate to the project directory.
    *   Create and activate a new virtual environment (steps 2 & 3).
    *   Install dependencies using the `requirements.txt` file:
        ```bash
        (venv) $ pip install -r requirements.txt
        ```
        This ensures the same package versions are installed.

8.  **Deactivate the virtual environment when done:**
    ```bash
    (venv) $ deactivate
    ```

This workflow ensures that your project's dependencies are managed, isolated, and easily reproducible.

Python `pip list --outdated` command is used to list all the packages that are outdated. This command cross-checks the installed package information with the Python Package Index (PyPI).

Syntax:
```
pip list --outdated
```

### Upgrading packages with pip

Syntax:
```
pip install --user --upgrade package_name
```

We can also upgrade any package to a specific version using the below command.

```python
pip install --user --upgrade package_name==version
```
### Downgrading packages with pip

The Python pip install –user command is used to downgrade a package to the specific version.

Syntax:
```
pip install --user package_name==version
```

## Python Packages
We usually organize our files in different folders and subfolders based on some criteria, so that they can be managed easily and efficiently. For example, we keep all our games in a Games folder and we can even subcategorize according to the genre of the game or something like this. The same analogy is followed by the Python package. 

A Python module may contain several classes, functions, variables, etc. whereas a Python package can contains several module. In simpler terms a package is folder that contains various modules as files.

### Creating Package

Let’s create a package named mypckg that will contain two modules mod1 and mod2. To create this module follow the below steps – 

* Create a folder named mypckg.
* Inside this folder create an empty Python file i.e. \_\_init\_\_.py
* Then create two modules mod1 and mod2 in this folder.
Mod1.py

Mod1.py
```
def gfg():
	print("Welcome to GFG")
```
Mod2.py
```
def sum(a, b):
	return a+b
```

### The hierarchy of the our package looks like this – 

```
mypckg
|
|
---__init__.py
|
|
---mod1.py
|
|
---mod2.py

```

### Understanding `__init__.py`

The `__init__.py` file serves two main purposes:

1.  **Marking a Directory as a Package:** The primary role of `__init__.py` is to tell the Python interpreter that the directory containing it should be treated as a package. If a directory contains an `__init__.py` file (even if it's empty), Python will recognize it as a package, allowing you to import modules from it.
2.  **Package Initialization (Optional):** While an empty `__init__.py` file is sufficient to define a package, you can also use it to execute package initialization code. This code runs when the package or one of its modules is imported for the first time. Common uses include:
    *   **Making submodules or specific functions more accessible:** You can import selected functions or submodules from your package's modules directly into the package's namespace. This allows users to import them with a shorter path.
    *   **Defining package-level variables or constants.**
    *   **Running setup code required by the package.**

**Important Clarification:** An **empty** `__init__.py` file simply marks the directory as a package. It **does not** automatically import all functions or submodules from the package's modules into the package's top-level namespace. You still need to explicitly import them.

**Example: Controlling Imports with `__init__.py`**

Consider the `mypckg` example:

```
mypckg/
├── __init__.py
├── mod1.py
└── mod2.py
```

**Scenario 1: Empty `__init__.py`**

If `mypckg/__init__.py` is empty, to use `gfg` from `mod1` and `sum_func` from `mod2` (let's rename `sum` to avoid conflict with built-in `sum`), you would import them like this:

```python
# Assuming mypckg/__init__.py is empty
from mypckg import mod1
from mypckg import mod2 # or from mypckg.mod2 import sum_func

mod1.gfg()
result = mod2.sum_func(1, 2) 
print(result)
```

**Scenario 2: Using `__init__.py` to expose specific functions**

Let's modify `mypckg/__init__.py` to make `gfg` and `sum_func` directly available when importing `mypckg`.

`mypckg/__init__.py`:
```python
# This code runs when 'mypckg' is imported
print("Initializing mypckg...")
from .mod1 import gfg        # Import gfg from mod1.py into mypckg's namespace
from .mod2 import sum_func   # Import sum_func from mod2.py into mypckg's namespace

# You can also define package-level variables
VERSION = "1.0" 
```

`mypckg/mod1.py`:
```python
def gfg():
    print("Welcome to GFG (from mod1)")
```

`mypckg/mod2.py`:
```python
def sum_func(a, b): # Renamed to avoid conflict with built-in sum
    return a + b
```

Now, you can import and use these functions more directly:
```python
import mypckg # This will execute __init__.py

# gfg and sum_func are now part of mypckg's namespace
mypckg.gfg() 
result = mypckg.sum_func(1, 2)
print(f"Sum result: {result}")
print(f"Package version: {mypckg.VERSION}")

# Alternatively, you could import them directly if __init__.py sets them up:
# from mypckg import gfg, sum_func, VERSION 
# gfg()
# result = sum_func(1,2)
# print(VERSION)
```
Output of the main script (after `import mypckg`):
```
Initializing mypckg...
Welcome to GFG (from mod1)
Sum result: 3
Package version: 1.0
```
By using `__init__.py` in this way, you can create a cleaner and more user-friendly API for your package.

### Import Modules from a Package
Syntax:
```
import package_name.module_name
```
Example: Import Module from package

```python
from mypckg import mod1
from mypckg import mod2

mod1.gfg()
res = mod2.sum(1, 2)
print(res)
```

Output:
```
Welcome to GFG
3
```
Example: Import Specific function from the module

```python
from mypckg.mod1 import gfg
from mypckg.mod2 import sum

gfg()
res = sum(1, 2)
print(res)
```
Output:
```
Welcome to GFG
3
```