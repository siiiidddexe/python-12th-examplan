# Quiz: File Handling and Exception Handling

**Instructions**: Answer the following questions to test your understanding of Chapter 3.

## Section A: Multiple Choice Questions (1 Mark each)

1.  Which mode opens a file for reading?
    a) `"w"`
    b) `"r"`
    c) `"a"`
    d) `"x"`

2.  What does the `"a"` mode do?
    a) Reads the file
    b) Overwrites the file
    c) Appends to the file
    d) Deletes the file

3.  Which method reads the entire file content as a string?
    a) `readline()`
    b) `readlines()`
    c) `read()`
    d) `readall()`

4.  Which exception is raised when dividing by zero?
    a) `ValueError`
    b) `ZeroDivisionError`
    c) `TypeError`
    d) `IndexError`

5.  Which block always executes, whether an exception occurs or not?
    a) `try`
    b) `except`
    c) `else`
    d) `finally`

## Section B: Short Answer Questions (2 Marks each)

6.  What is the purpose of the `with` statement in file handling?
7.  Differentiate between `"w"` and `"a"` file modes.
8.  What is an Exception? Name any three built-in exceptions in Python.
9.  Explain the role of the `else` block in exception handling.
10. Why should we always close a file after performing operations on it?

## Section C: Programming Questions (5 Marks each)

11. Write a program to read a text file and count the number of lines, words, and characters in it.
12. Create a program that writes a list of 5 student names to a file called `students.txt`, then reads and displays them.
13. Write a program that asks the user for two numbers and divides them. Handle `ZeroDivisionError` and `ValueError` exceptions appropriately.
14. Write a function `safe_divide(a, b)` that takes two numbers and returns their division. If `b` is zero, it should raise a custom exception message instead of crashing. Use try-except-finally blocks.

---
**Answer Key (Section A)**
1. b
2. c
3. c
4. b
5. d
