# Chapter 3: File Handling and Exception Handling

## 1. File Operations
Files are used to permanently store data. Python provides built-in functions to create, read, update, and delete files.

### Opening a File
Use the `open()` function to open a file. It returns a file object.
```python
file = open("filename.txt", "mode")
```

### File Modes
*   `"r"` - Read mode (default). File must exist.
*   `"w"` - Write mode. Creates a new file or overwrites an existing file.
*   `"a"` - Append mode. Adds data to the end of the file.
*   `"r+"` - Read and write mode.
*   `"x"` - Exclusive creation. Fails if file already exists.

### Reading from a File
```python
# Read entire file
file = open("data.txt", "r")
content = file.read()
print(content)
file.close()

# Read line by line
file = open("data.txt", "r")
for line in file:
    print(line)
file.close()

# Read specific number of characters
file = open("data.txt", "r")
content = file.read(10) # Reads first 10 characters
file.close()
```

### Writing to a File
```python
file = open("output.txt", "w")
file.write("Hello, World!\n")
file.write("This is line 2.")
file.close()
```

### Appending to a File
```python
file = open("output.txt", "a")
file.write("\nThis is an appended line.")
file.close()
```

### Closing a File
Always close a file after operations using `file.close()`. This frees up system resources.

### Using `with` Statement (Recommended)
The `with` statement automatically closes the file after the block is executed, even if an error occurs.
```python
with open("data.txt", "r") as file:
    content = file.read()
    print(content)
# File is automatically closed here
```

### File Methods
*   `read()` - Reads the entire file.
*   `readline()` - Reads one line.
*   `readlines()` - Returns a list of all lines.
*   `write(string)` - Writes a string to the file.
*   `writelines(list)` - Writes a list of strings to the file.

## 2. Exception Handling
Exceptions are runtime errors that disrupt the normal flow of a program. Python provides mechanisms to handle these gracefully.

### Common Exceptions
*   `ZeroDivisionError` - Division by zero.
*   `ValueError` - Invalid value conversion (e.g., `int("abc")`).
*   `FileNotFoundError` - File does not exist.
*   `IndexError` - Index out of range.
*   `KeyError` - Key not found in dictionary.
*   `TypeError` - Operation on incompatible types.

### Try-Except Block
```python
try:
    # Code that might raise an exception
    x = int(input("Enter a number: "))
    result = 10 / x
    print(result)
except ZeroDivisionError:
    print("Error: Cannot divide by zero!")
except ValueError:
    print("Error: Invalid input. Please enter a number.")
```

### Multiple Exceptions
```python
try:
    # risky code
except (TypeError, ValueError):
    print("Type or Value error occurred")
```

### Catching All Exceptions
```python
try:
    # code
except Exception as e:
    print(f"An error occurred: {e}")
```

### Else Block
The `else` block runs if no exception is raised in the `try` block.
```python
try:
    x = int(input("Enter a number: "))
except ValueError:
    print("Invalid input!")
else:
    print(f"You entered: {x}")
```

### Finally Block
The `finally` block always executes, regardless of whether an exception occurred or not. It's typically used for cleanup operations.
```python
try:
    file = open("data.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("File not found!")
finally:
    file.close() # This will always execute
    print("File operation complete.")
```

### Raising Exceptions
You can manually raise exceptions using the `raise` keyword.
```python
age = int(input("Enter age: "))
if age < 0:
    raise ValueError("Age cannot be negative!")
```

### Complete Example
```python
try:
    with open("marks.txt", "r") as file:
        marks = int(file.read())
        if marks > 100:
            raise ValueError("Marks cannot exceed 100")
        print(f"Marks: {marks}")
except FileNotFoundError:
    print("Error: File not found")
except ValueError as e:
    print(f"Error: {e}")
finally:
    print("Operation completed")
```
