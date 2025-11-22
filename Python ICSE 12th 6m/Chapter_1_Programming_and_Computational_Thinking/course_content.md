# Chapter 1: Programming and Computational Thinking

## 1. Introduction to Programming
Python is a high-level, interpreted programming language known for its readability and versatility.

### What is Programming?
Programming is the process of creating a set of instructions that tell a computer how to perform a task. It involves:
*   **Problem Analysis**: Understanding what needs to be solved
*   **Algorithm Design**: Planning the step-by-step solution
*   **Coding**: Writing the solution in a programming language
*   **Testing & Debugging**: Ensuring the program works correctly

### Why Python?
*   Easy to learn and read
*   Versatile (web, data science, AI, automation)
*   Large community and extensive libraries
*   Cross-platform (Windows, Mac, Linux)

### Basic Python Syntax
*   **Case Sensitivity**: Python is case-sensitive (`Var` and `var` are different).
*   **Indentation**: Python uses indentation (whitespace) to define blocks of code instead of curly braces `{}`.
    ```python
    if True:
        print("Correct indentation")  # 4 spaces or 1 tab
    ```
*   **Comments**:
    *   Single-line: `# This is a comment`
    *   Multi-line: `''' This is a multi-line comment '''` or `""" ... """`
    *   Purpose: Documentation, explaining code, temporarily disabling code

### Variables
Variables are containers for storing data values.

#### Variable Naming Rules
*   Must start with a letter (a-z, A-Z) or underscore (_)
*   Can contain letters, digits (0-9), and underscores
*   Cannot start with a digit
*   Cannot use Python keywords (if, for, while, etc.)
*   Case-sensitive (`age` and `Age` are different)

**Valid names**: `my_var`, `_private`, `name2`, `studentName`
**Invalid names**: `2name`, `my-var`, `for`, `class`

#### Variable Assignment
```python
x = 5           # Integer
name = "Alice"  # String
pi = 3.14159    # Float
is_student = True  # Boolean
```

#### Multiple Assignment
```python
a = b = c = 10
x, y, z = 1, 2, 3
```

#### Variable Memory Concept
*   Variables are references to objects in memory
*   Use `id()` to check memory address
*   Use `type()` to check data type

```python
x = 100
print(id(x))    # Memory address
print(type(x))  # <class 'int'>
```

### Data Types (Detailed)

#### 1. Numeric Types
*   **int (Integer)**: Whole numbers, positive or negative
    ```python
    age = 17
    temperature = -5
    big_num = 1000000
    ```
*   **float (Floating Point)**: Decimal numbers
    ```python
    pi = 3.14159
    price = 99.99
    scientific = 2.5e3  # 2500.0
    ```
*   **complex**: Complex numbers with real and imaginary parts
    ```python
    z = 3 + 4j
    print(z.real)  # 3.0
    print(z.imag)  # 4.0
    ```

#### 2. String (str)
Sequence of characters enclosed in quotes.
```python
name = "Alice"
message = 'Hello World'
multi_line = """This is
a multi-line
string"""
```

**String Operations**:
*   Concatenation: `"Hello" + " " + "World"`
*   Repetition: `"Ha" * 3`  → `"HaHaHa"`
*   Indexing: `name[0]`  → `'A'`
*   Slicing: `name[0:3]`  → `'Ali'`
*   Length: `len(name)`  → `5`

**String Methods**:
```python
text = "Hello World"
print(text.upper())      # HELLO WORLD
print(text.lower())      # hello world
print(text.replace("World", "Python"))  # Hello Python
print(text.split())      # ['Hello', 'World']
print(text.find("World")) # 6
print(text.count("l"))   # 3
print(text.strip())      # Removes whitespace
print(text.startswith("Hello"))  # True
print(text.endswith("ld"))      # True
```

**String Formatting**:
```python
name = "Alice"
age = 17
# Method 1: f-strings (Python 3.6+)
print(f"My name is {name} and I'm {age} years old")

# Method 2: format()
print("My name is {} and I'm {} years old".format(name, age))

# Method 3: % operator
print("My name is %s and I'm %d years old" % (name, age))
```

#### 3. Boolean (bool)
Represents True or False values.
```python
is_valid = True
has_passed = False
print(10 > 5)  # True
print(3 == 5)  # False
```

#### 4. Type Conversion (Casting)
Converting from one data type to another.
```python
# String to Integer
age_str = "17"
age_int = int(age_str)

# Integer to String
num = 100
num_str = str(num)

# String to Float
price = float("99.99")

# Integer to Float
x = float(5)  # 5.0

# Float to Integer (truncates decimal)
y = int(3.99)  # 3

# To Boolean
print(bool(0))    # False
print(bool(1))    # True
print(bool(""))   # False
print(bool("Hi")) # True
```

### Input and Output (Detailed)

#### Output with print()
```python
print("Hello, World!")
print("Name:", "Alice", "Age:", 17)
print("Value:", 100, sep=" | ")  # Custom separator
print("Hello", end=" ")  # Change end character
print("World")  # Output: Hello World
```

#### Input from User
```python
name = input("Enter your name: ")
age = int(input("Enter your age: "))  # Convert to integer
marks = float(input("Enter marks: "))  # Convert to float
```

**Important**: `input()` always returns a string, so type conversion is needed for numbers.

## 2. Operators (Detailed)
Operators are symbols that perform operations on variables and values.

### 2.1 Arithmetic Operators
*   `+` Addition: `5 + 3 = 8`
*   `-` Subtraction: `10 - 4 = 6`
*   `*` Multiplication: `3 * 7 = 21`
*   `/` Division (float result): `10 / 3 = 3.3333...`
*   `//` Floor Division (integer result): `10 // 3 = 3`
*   `%` Modulus (remainder): `10 % 3 = 1`
*   `**` Exponentiation (power): `2 ** 3 = 8`

```python
a = 10
b = 3
print(a + b)   # 13
print(a - b)   # 7
print(a * b)   # 30
print(a / b)   # 3.333...
print(a // b)  # 3
print(a % b)   # 1
print(a ** b)  # 1000
```

### 2.2 Relational (Comparison) Operators
Return Boolean values (True/False).
*   `==` Equal to: `5 == 5` → True
*   `!=` Not equal to: `5 != 3` → True
*   `>` Greater than: `10 > 5` → True
*   `<` Less than: `3 < 7` → True
*   `>=` Greater than or equal to: `5 >= 5` → True
*   `<=` Less than or equal to: `4 <= 6` → True

```python
x = 10
y = 20
print(x == y)  # False
print(x != y)  # True
print(x < y)   # True
print(x > y)   # False
```

### 2.3 Logical Operators
Used to combine conditional statements.
*   `and` - Returns True if both conditions are True
*   `or` - Returns True if at least one condition is True
*   `not` - Reverses the boolean value

```python
age = 17
marks = 85

print(age >= 16 and marks >= 80)  # True
print(age < 15 or marks > 90)     # False
print(not(age < 18))              # False
```

**Truth Tables**:
```
AND Truth Table:
True and True = True
True and False = False
False and True = False
False and False = False

OR Truth Table:
True or True = True
True or False = True
False or True = True
False or False = False

NOT:
not True = False
not False = True
```

### 2.4 Assignment Operators
*   `=` Simple assignment: `x = 5`
*   `+=` Add and assign: `x += 3` (same as `x = x + 3`)
*   `-=` Subtract and assign: `x -= 2`
*   `*=` Multiply and assign: `x *= 4`
*   `/=` Divide and assign: `x /= 2`
*   `//=` Floor divide and assign: `x //= 3`
*   `%=` Modulus and assign: `x %= 5`
*   `**=` Exponent and assign: `x **= 2`

```python
x = 10
x += 5   # x = 15
x -= 3   # x = 12
x *= 2   # x = 24
x /= 4   # x = 6.0
```

### 2.5 Identity Operators
*   `is` - Returns True if both variables point to the same object
*   `is not` - Returns True if variables point to different objects

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)    # True (same values)
print(a is b)    # False (different objects)
print(a is c)    # True (same object)
```

### 2.6 Membership Operators
*   `in` - Returns True if value exists in sequence
*   `not in` - Returns True if value doesn't exist in sequence

```python
fruits = ["apple", "banana", "cherry"]
print("apple" in fruits)      # True
print("mango" not in fruits)  # True

text = "Hello World"
print("Hello" in text)  # True
```

### 2.7 Bitwise Operators
Operate on binary representations of integers.
*   `&` AND
*   `|` OR
*   `^` XOR
*   `~` NOT (complement)
*   `<<` Left shift
*   `>>` Right shift

```python
a = 5   # Binary: 0101
b = 3   # Binary: 0011

print(a & b)   # 1  (0001)
print(a | b)   # 7  (0111)
print(a ^ b)   # 6  (0110)
print(~a)      # -6
print(a << 1)  # 10 (1010)
print(a >> 1)  # 2  (0010)
```

### 2.8 Operator Precedence
Order of operations (highest to lowest):
1. `**` (Exponentiation)
2. `~`, `+`, `-` (Unary operators)
3. `*`, `/`, `//`, `%`
4. `+`, `-`
5. `<<`, `>>`
6. `&`
7. `^`
8. `|`
9. `==`, `!=`, `>`, `<`, `>=`, `<=`, `is`, `is not`, `in`, `not in`
10. `not`
11. `and`
12. `or`

Use parentheses `()` to override precedence:
```python
result = 2 + 3 * 4      # 14
result = (2 + 3) * 4    # 20
```

## 3. Control Structures (Detailed)
Control structures direct the flow of execution in a program.

### 3.1 Conditional Statements

#### if Statement
Executes a block if condition is True.
```python
age = 18
if age >= 18:
    print("You are eligible to vote")
```

#### if-else Statement
Executes one block if True, another if False.
```python
marks = 45
if marks >= 50:
    print("Passed")
else:
    print("Failed")
```

#### if-elif-else Chain
Checks multiple conditions sequentially.
```python
marks = 85
if marks >= 90:
    print("Grade: A+")
elif marks >= 80:
    print("Grade: A")
elif marks >= 70:
    print("Grade: B")
elif marks >= 60:
    print("Grade: C")
else:
    print("Grade: F")
```

#### Nested if Statements
if statements inside other if statements.
```python
age = 20
has_license = True

if age >= 18:
    if has_license:
        print("You can drive")
    else:
        print("Get a license first")
else:
    print("You are too young to drive")
```

#### Ternary Operator (Conditional Expression)
Short-hand if-else in one line.
```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)  # Adult
```

### 3.2 Loops

#### for Loop
Iterates over a sequence (list, tuple, string, range).

**Using range()**:
```python
# range(stop)
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# range(start, stop)
for i in range(2, 7):
    print(i)  # 2, 3, 4, 5, 6

# range(start, stop, step)
for i in range(1, 10, 2):
    print(i)  # 1, 3, 5, 7, 9

# Reverse range
for i in range(10, 0, -1):
    print(i)  # 10, 9, 8, ..., 1
```

**Iterating over sequences**:
```python
# String
for char in "Python":
    print(char)

# List
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# Using enumerate() for index and value
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

#### while Loop
Repeats as long as condition is True.
```python
count = 1
while count <= 5:
    print(count)
    count += 1
```

**Using while for user input**:
```python
password = ""
while password != "secret":
    password = input("Enter password: ")
print("Access granted!")
```

#### Nested Loops
Loops inside loops.
```python
# Multiplication table
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} x {j} = {i*j}")
    print("---")
```

**Pattern printing**:
```python
# Right triangle
for i in range(1, 6):
    for j in range(i):
        print("*", end=" ")
    print()

# Output:
# *
# * *
# * * *
# * * * *
# * * * * *
```

### 3.3 Loop Control Statements

#### break Statement
Exits the loop prematurely.
```python
for i in range(10):
    if i == 5:
        break
    print(i)  # 0, 1, 2, 3, 4
```

#### continue Statement
Skips the current iteration and moves to the next.
```python
for i in range(6):
    if i == 3:
        continue
    print(i)  # 0, 1, 2, 4, 5
```

#### pass Statement
Does nothing; used as a placeholder.
```python
for i in range(5):
    if i == 2:
        pass  # To be implemented later
    print(i)
```

#### else Clause in Loops
Executes when loop completes normally (not via break).
```python
for i in range(5):
    print(i)
else:
    print("Loop completed successfully")

# With break
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("This won't print")  # Doesn't execute due to break
```

## 4. Data Structures (Detailed)
Organizing and storing data efficiently.

### 4.1 Lists
Mutable, ordered sequence that can hold items of different types.

#### Creating Lists
```python
empty_list = []
numbers = [1, 2, 3, 4, 5]
mixed = [1, "Hello", 3.14, True]
nested = [[1, 2], [3, 4], [5, 6]]
```

#### Accessing Elements
```python
fruits = ["apple", "banana", "cherry", "date"]
print(fruits[0])    # apple (first element)
print(fruits[-1])   # date (last element)
print(fruits[1:3])  # ['banana', 'cherry'] (slicing)
print(fruits[:2])   # ['apple', 'banana']
print(fruits[2:])   # ['cherry', 'date']
print(fruits[::2])  # ['apple', 'cherry'] (every 2nd element)
```

#### Modifying Lists
```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "blueberry"  # Change element
print(fruits)  # ['apple', 'blueberry', 'cherry']
```

#### List Methods
```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

# Adding elements
numbers.append(7)           # Add to end: [3,1,4,1,5,9,2,6,7]
numbers.insert(2, 99)       # Insert at index 2
numbers.extend([10, 11])    # Add multiple elements

# Removing elements
numbers.remove(1)           # Remove first occurrence of 1
popped = numbers.pop()      # Remove and return last element
popped = numbers.pop(2)     # Remove and return element at index 2
numbers.clear()             # Remove all elements

# Searching
fruits = ["apple", "banana", "cherry"]
index = fruits.index("banana")  # Returns 1
count = fruits.count("apple")   # Returns 1

# Sorting
numbers = [3, 1, 4, 1, 5]
numbers.sort()              # Sort in-place (ascending)
numbers.sort(reverse=True)  # Descending
sorted_nums = sorted(numbers)  # Returns new sorted list

# Reversing
numbers.reverse()           # Reverse in-place
reversed_nums = list(reversed(numbers))  # Returns new reversed list

# Other operations
length = len(fruits)        # Get length
```

#### List Comprehension
Concise way to create lists.
```python
# Basic syntax: [expression for item in iterable]
squares = [x**2 for x in range(1, 6)]
# Result: [1, 4, 9, 16, 25]

# With condition
evens = [x for x in range(10) if x % 2 == 0]
# Result: [0, 2, 4, 6, 8]

# Nested comprehension
matrix = [[i*j for j in range(1, 4)] for i in range(1, 4)]
# Result: [[1,2,3], [2,4,6], [3,6,9]]
```

### 4.2 Tuples
Immutable, ordered sequence.

#### Creating Tuples
```python
empty_tuple = ()
single = (5,)           # Note the comma
numbers = (1, 2, 3, 4, 5)
mixed = (1, "Hello", 3.14)
nested = ((1, 2), (3, 4))
```

#### Accessing Elements
```python
coords = (10, 20, 30)
print(coords[0])    # 10
print(coords[-1])   # 30
print(coords[1:])   # (20, 30)
```

#### Tuple Operations
```python
t1 = (1, 2, 3)
t2 = (4, 5, 6)

# Concatenation
combined = t1 + t2  # (1, 2, 3, 4, 5, 6)

# Repetition
repeated = t1 * 3   # (1, 2, 3, 1, 2, 3, 1, 2, 3)

# Methods
count = t1.count(2)      # Returns 1
index = t1.index(3)      # Returns 2

# Tuple unpacking
x, y, z = t1
print(x, y, z)  # 1 2 3
```

#### Why Use Tuples?
*   Faster than lists
*   Protect data from modification
*   Can be used as dictionary keys
*   Good for fixed collections

### 4.3 Sets
Mutable, unordered collection of unique elements.

#### Creating Sets
```python
empty_set = set()  # Cannot use {} (that's a dict)
numbers = {1, 2, 3, 4, 5}
mixed = {1, "Hello", 3.14}
from_list = set([1, 2, 2, 3, 3, 4])  # Duplicates removed
```

#### Set Operations
```python
a = {1, 2, 3, 4, 5}
b = {4, 5, 6, 7, 8}

# Union (all elements from both)
print(a | b)  # {1, 2, 3, 4, 5, 6, 7, 8}
print(a.union(b))

# Intersection (common elements)
print(a & b)  # {4, 5}
print(a.intersection(b))

# Difference (in a but not in b)
print(a - b)  # {1, 2, 3}
print(a.difference(b))

# Symmetric difference (in either, not both)
print(a ^ b)  # {1, 2, 3, 6, 7, 8}
print(a.symmetric_difference(b))
```

#### Set Methods
```python
fruits = {"apple", "banana"}

# Adding
fruits.add("cherry")
fruits.update(["date", "elderberry"])

# Removing
fruits.remove("apple")      # Raises error if not found
fruits.discard("mango")     # No error if not found
popped = fruits.pop()       # Remove arbitrary element
fruits.clear()              # Remove all

# Checking membership
print("apple" in fruits)    # True/False
```

### 4.4 Dictionaries
Unordered collection of key-value pairs.

#### Creating Dictionaries
```python
empty_dict = {}
student = {
    "name": "Alice",
    "age": 17,
    "grade": "12th",
    "marks": 95
}

# Using dict() constructor
person = dict(name="Bob", age=20)
```

#### Accessing Values
```python
print(student["name"])        # Alice
print(student.get("age"))     # 17
print(student.get("city", "Not Found"))  # Default value
```

#### Modifying Dictionaries
```python
# Update value
student["age"] = 18

# Add new key-value
student["city"] = "Mumbai"

# Update multiple
student.update({"grade": "11th", "school": "XYZ"})
```

#### Dictionary Methods
```python
student = {"name": "Alice", "age": 17, "grade": "12th"}

# Get all keys, values, items
keys = student.keys()       # dict_keys(['name', 'age', 'grade'])
values = student.values()   # dict_values(['Alice', 17, '12th'])
items = student.items()     # dict_items([('name', 'Alice'), ...])

# Remove items
age = student.pop("age")         # Remove and return value
last_item = student.popitem()    # Remove and return last item
del student["grade"]             # Delete specific key
student.clear()                  # Remove all items

# Checking existence
if "name" in student:
    print("Name exists")
```

#### Iterating Through Dictionaries
```python
student = {"name": "Alice", "age": 17, "grade": "12th"}

# Iterate through keys
for key in student:
    print(key)

# Iterate through values
for value in student.values():
    print(value)

# Iterate through key-value pairs
for key, value in student.items():
    print(f"{key}: {value}")
```

#### Dictionary Comprehension
```python
# Square numbers
squares = {x: x**2 for x in range(1, 6)}
# Result: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Filter dictionary
student = {"name": "Alice", "age": 17, "grade": "12th"}
string_items = {k: v for k, v in student.items() if isinstance(v, str)}
```

#### Nested Dictionaries
```python
school = {
    "student1": {"name": "Alice", "age": 17},
    "student2": {"name": "Bob", "age": 16}
}

print(school["student1"]["name"])  # Alice
```

## 5. Functions (Detailed)
Reusable blocks of code that perform specific tasks.

### 5.1 Why Use Functions?
*   **Code Reusability**: Write once, use multiple times
*   **Organization**: Break complex problems into smaller parts
*   **Maintainability**: Easier to update and debug
*   **Abstraction**: Hide implementation details

### 5.2 Defining and Calling Functions

#### Basic Function
```python
def greet():
    print("Hello, World!")

# Calling the function
greet()
```

#### Function with Parameters
```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")  # Hello, Alice!
greet("Bob")    # Hello, Bob!
```

#### Function with Return Value
```python
def add(a, b):
    return a + b

result = add(5, 3)
print(result)  # 8
```

#### Multiple Return Values
```python
def get_student_info():
    name = "Alice"
    age = 17
    grade = "12th"
    return name, age, grade  # Returns tuple

n, a, g = get_student_info()
print(n, a, g)  # Alice 17 12th
```

### 5.3 Types of Arguments

#### Positional Arguments
Arguments passed in order.
```python
def student_info(name, age, grade):
    print(f"{name} is {age} years old in grade {grade}")

student_info("Alice", 17, "12th")
```

#### Keyword Arguments
Arguments passed by name.
```python
student_info(age=17, name="Alice", grade="12th")
# Order doesn't matter when using keywords
```

#### Default Arguments
Parameters with default values.
```python
def greet(name, message="Hello"):
    print(f"{message}, {name}!")

greet("Alice")              # Hello, Alice!
greet("Bob", "Good morning")  # Good morning, Bob!
```

#### Variable-Length Arguments (*args)
Accept any number of positional arguments.
```python
def sum_all(*numbers):
    total = 0
    for num in numbers:
        total += num
    return total

print(sum_all(1, 2, 3))        # 6
print(sum_all(10, 20, 30, 40)) # 100
```

#### Keyword Variable-Length Arguments (**kwargs)
Accept any number of keyword arguments.
```python
def print_info(**info):
    for key, value in info.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=17, grade="12th")
# Output:
# name: Alice
# age: 17
# grade: 12th
```

#### Combining All Types
```python
def complex_function(a, b, *args, default="value", **kwargs):
    print(f"a={a}, b={b}")
    print(f"args={args}")
    print(f"default={default}")
    print(f"kwargs={kwargs}")

complex_function(1, 2, 3, 4, 5, default="custom", x=10, y=20)
```

### 5.4 Scope of Variables

#### Local Scope
Variables defined inside a function.
```python
def my_func():
    x = 10  # Local variable
    print(x)

my_func()
# print(x)  # Error: x is not defined outside function
```

#### Global Scope
Variables defined outside functions.
```python
x = 10  # Global variable

def my_func():
    print(x)  # Can access global variable

my_func()  # 10
```

#### Modifying Global Variables
```python
x = 10

def modify():
    global x
    x = 20

modify()
print(x)  # 20
```

### 5.5 Lambda Functions
Small anonymous functions defined with `lambda` keyword.

```python
# Regular function
def square(x):
    return x ** 2

# Lambda equivalent
square = lambda x: x ** 2
print(square(5))  # 25

# Lambda with multiple arguments
add = lambda a, b: a + b
print(add(3, 7))  # 10

# Lambda in sorting
students = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
students.sort(key=lambda x: x[1])  # Sort by marks
print(students)
```

### 5.6 Built-in Functions
Python provides many built-in functions.

```python
# Type conversion
int(), float(), str(), bool(), list(), tuple(), set(), dict()

# Math functions
abs(-5)        # 5 (absolute value)
pow(2, 3)      # 8 (power)
round(3.7)     # 4
min(1, 2, 3)   # 1
max(1, 2, 3)   # 3
sum([1,2,3])   # 6

# Input/Output
print(), input()

# Sequence operations
len([1, 2, 3])              # 3
sorted([3, 1, 2])           # [1, 2, 3]
reversed([1, 2, 3])         # [3, 2, 1]
enumerate(['a', 'b', 'c'])  # [(0,'a'), (1,'b'), (2,'c')]
zip([1,2], ['a','b'])       # [(1,'a'), (2,'b')]

# Type checking
type(5)                # <class 'int'>
isinstance(5, int)     # True

# Range
range(5)               # 0, 1, 2, 3, 4

# Map, Filter, Reduce
list(map(lambda x: x**2, [1, 2, 3]))     # [1, 4, 9]
list(filter(lambda x: x > 2, [1, 2, 3, 4]))  # [3, 4]
```

### 5.7 Recursion (Detailed)
A function calling itself to solve a problem.

#### Components of Recursion
1. **Base Case**: Condition to stop recursion
2. **Recursive Case**: Function calls itself with modified argument

#### Factorial Example
```python
def factorial(n):
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive case
    else:
        return n * factorial(n - 1)

print(factorial(5))  # 120
# 5 * factorial(4)
# 5 * 4 * factorial(3)
# 5 * 4 * 3 * factorial(2)
# 5 * 4 * 3 * 2 * factorial(1)
# 5 * 4 * 3 * 2 * 1 = 120
```

#### Fibonacci Series
```python
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)

for i in range(10):
    print(fibonacci(i), end=" ")
# 0 1 1 2 3 5 8 13 21 34
```

#### Sum of Natural Numbers
```python
def sum_natural(n):
    if n == 1:
        return 1
    else:
        return n + sum_natural(n - 1)

print(sum_natural(5))  # 15 (1+2+3+4+5)
```

#### Power Function
```python
def power(base, exp):
    if exp == 0:
        return 1
    else:
        return base * power(base, exp - 1)

print(power(2, 5))  # 32
```

### 5.8 Docstrings
Documentation strings for functions.

```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.
    
    Parameters:
    length (float): The length of the rectangle
    width (float): The width of the rectangle
    
    Returns:
    float: The area of the rectangle
    """
    return length * width

# Access docstring
print(calculate_area.__doc__)
help(calculate_area)
```

### 5.9 Function Best Practices
*   Use descriptive names (verb + noun: `calculate_total`, `get_user_input`)
*   Keep functions small and focused (one task per function)
*   Use docstrings for documentation
*   Avoid global variables when possible
*   Return values instead of printing (more flexible)
*   Use default arguments wisely
