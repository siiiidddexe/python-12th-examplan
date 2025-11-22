# Chapter 4: Libraries and Modules

## 1. Built-in Modules
Python comes with a rich standard library of built-in modules that provide ready-to-use functionality for various tasks.

### What is a Module?
A module is a file containing Python code (functions, classes, variables) that can be imported and used in other programs.

### Importing Modules
```python
import module_name
```

### Using Functions from a Module
```python
import math
print(math.sqrt(16))  # Output: 4.0
print(math.pi)        # Output: 3.141592653589793
```

### Importing Specific Items
```python
from math import sqrt, pi
print(sqrt(25))  # Output: 5.0
print(pi)        # Output: 3.141592653589793
```

### Importing with Aliases
```python
import math as m
print(m.sqrt(9))  # Output: 3.0
```

### Importing All Items (Not Recommended)
```python
from math import *
print(sqrt(4))  # Output: 2.0
```

### Common Built-in Modules

#### `math` Module
Provides mathematical functions.
*   `math.sqrt(x)` - Square root
*   `math.pow(x, y)` - x to the power y
*   `math.ceil(x)` - Smallest integer >= x
*   `math.floor(x)` - Largest integer <= x
*   `math.factorial(x)` - Factorial of x
*   `math.pi`, `math.e` - Constants

#### `random` Module
Generates random numbers.
*   `random.random()` - Random float between 0 and 1
*   `random.randint(a, b)` - Random integer between a and b (inclusive)
*   `random.choice(list)` - Random element from a list
*   `random.shuffle(list)` - Shuffles a list in place

```python
import random
print(random.randint(1, 10))
print(random.choice(['apple', 'banana', 'cherry']))
```

#### `datetime` Module
Works with dates and times.
*   `datetime.date.today()` - Current date
*   `datetime.datetime.now()` - Current date and time

```python
import datetime
today = datetime.date.today()
print(today)  # Output: 2025-11-22
```

#### `os` Module
Interacts with the operating system.
*   `os.getcwd()` - Current working directory
*   `os.listdir(path)` - List files in a directory
*   `os.mkdir(name)` - Create a directory
*   `os.remove(file)` - Delete a file

```python
import os
print(os.getcwd())
```

#### `sys` Module
Provides system-specific parameters.
*   `sys.version` - Python version
*   `sys.exit()` - Exit the program

### The `dir()` Function
Lists all functions and variables in a module.
```python
import math
print(dir(math))
```

## 2. User-Defined Modules
You can create your own modules by writing Python code in a `.py` file and importing it into other programs.

### Creating a Module
Create a file named `mymodule.py`:
```python
# mymodule.py
def greet(name):
    return f"Hello, {name}!"

def add(a, b):
    return a + b

pi = 3.14159
```

### Importing and Using the Module
Create another file in the same directory:
```python
# main.py
import mymodule

print(mymodule.greet("Alice"))  # Output: Hello, Alice!
print(mymodule.add(5, 3))        # Output: 8
print(mymodule.pi)               # Output: 3.14159
```

### Importing Specific Functions
```python
from mymodule import greet, add
print(greet("Bob"))
print(add(10, 20))
```

### Module Search Path
Python searches for modules in:
1.  Current directory
2.  PYTHONPATH environment variable directories
3.  Standard library directories

### The `__name__` Variable
Every module has a built-in attribute `__name__`. When a module is run directly, `__name__` is set to `"__main__"`. When imported, `__name__` is the module's name.

```python
# mymodule.py
def greet(name):
    return f"Hello, {name}!"

if __name__ == "__main__":
    # This code runs only when the module is executed directly
    print(greet("Test User"))
```

### Organizing Code into Packages
A package is a directory containing multiple modules and a special `__init__.py` file.

```
mypackage/
    __init__.py
    module1.py
    module2.py
```

Usage:
```python
from mypackage import module1
```

### Benefits of Modules
*   **Code Reusability**: Write once, use multiple times.
*   **Organization**: Break large programs into smaller, manageable files.
*   **Namespace Management**: Avoid naming conflicts.
*   **Maintainability**: Easier to debug and update code.
