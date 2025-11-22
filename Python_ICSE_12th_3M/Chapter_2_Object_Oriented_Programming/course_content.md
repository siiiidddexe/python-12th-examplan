# Chapter 2: Object-Oriented Programming (OOP)

## Introduction to OOP

### What is Object-Oriented Programming?
Object-Oriented Programming (OOP) is a programming paradigm that organizes code around "objects" rather than functions and logic. It helps structure programs to make them more modular, reusable, and easier to maintain.

### Why OOP?
*   **Real-world Modeling**: Represents real-world entities naturally
*   **Code Reusability**: Write once, use multiple times through inheritance
*   **Modularity**: Break complex problems into manageable pieces
*   **Data Security**: Encapsulation protects data from unauthorized access
*   **Maintainability**: Easier to update and debug
*   **Scalability**: Easy to extend functionality

### Core OOP Principles
1.  **Encapsulation**: Bundling data and methods together; hiding internal details
2.  **Inheritance**: Creating new classes from existing ones
3.  **Polymorphism**: Same interface, different implementations
4.  **Abstraction**: Hiding complex implementation details

## 1. Classes and Objects (Detailed)

### Fundamental Concepts
*   **Class**: A blueprint or template for creating objects. It defines:
    - **Attributes** (data/properties): What the object knows
    - **Methods** (behaviors/functions): What the object can do
    
*   **Object**: An instance of a class. A concrete entity created from the class blueprint.

**Real-world Analogy**:
- **Class**: "Car" blueprint (design specifications)
- **Object**: Specific cars like "Honda Civic 2024", "Toyota Camry 2023"

### Creating a Class
```python
class Student:
    # The __init__ method is the constructor
    def __init__(self, name, grade):
        self.name = name   # Attribute
        self.grade = grade # Attribute

    # Method
    def display_info(self):
        print(f"Student: {self.name}, Grade: {self.grade}")
```

### Creating an Object (Instantiation)
```python
s1 = Student("Rohan", 12)
s2 = Student("Priya", 11)

s1.display_info() # Output: Student: Rohan, Grade: 12
```

### The `self` Parameter (Detailed)
*   `self` represents the instance of the class
*   It must be the first parameter of instance methods
*   Used to access attributes and methods of the class
*   Can be named anything, but `self` is conventional

```python
class Example:
    def __init__(self, value):
        self.value = value  # instance attribute
    
    def show(self):
        print(self.value)  # accessing instance attribute

obj = Example(10)
obj.show()  # Output: 10
```

### Class Variables vs Instance Variables (Detailed)

#### Instance Variables
Variables unique to each object instance.
```python
class Student:
    def __init__(self, name, roll_no):
        self.name = name        # Instance variable
        self.roll_no = roll_no  # Instance variable

s1 = Student("Alice", 101)
s2 = Student("Bob", 102)
print(s1.name)  # Alice
print(s2.name)  # Bob (different for each object)
```

#### Class Variables
Variables shared by all instances of a class.
```python
class Student:
    school_name = "ABC School"  # Class variable
    
    def __init__(self, name):
        self.name = name  # Instance variable

s1 = Student("Alice")
s2 = Student("Bob")

print(s1.school_name)  # ABC School
print(s2.school_name)  # ABC School (same for all objects)

# Changing class variable affects all instances
Student.school_name = "XYZ School"
print(s1.school_name)  # XYZ School
print(s2.school_name)  # XYZ School
```

### Types of Methods

#### Instance Methods
Operate on instance data; require `self` parameter.
```python
class Calculator:
    def __init__(self, value):
        self.value = value
    
    def add(self, num):  # Instance method
        self.value += num
        return self.value

calc = Calculator(10)
print(calc.add(5))  # 15
```

#### Class Methods
Operate on class data; use `@classmethod` decorator and `cls` parameter.
```python
class Student:
    student_count = 0  # Class variable
    
    def __init__(self, name):
        self.name = name
        Student.student_count += 1
    
    @classmethod
    def get_student_count(cls):  # Class method
        return cls.student_count

s1 = Student("Alice")
s2 = Student("Bob")
print(Student.get_student_count())  # 2
```

#### Static Methods
Don't access instance or class data; use `@staticmethod` decorator.
```python
class MathOperations:
    @staticmethod
    def add(a, b):  # Static method
        return a + b
    
    @staticmethod
    def multiply(a, b):
        return a * b

print(MathOperations.add(5, 3))       # 8
print(MathOperations.multiply(4, 6))  # 24
```

### Special Methods (Magic Methods / Dunder Methods)

#### `__str__()` Method
Returns a readable string representation of the object.
```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __str__(self):
        return f"Student: {self.name}, Age: {self.age}"

s = Student("Alice", 17)
print(s)  # Student: Alice, Age: 17
```

#### `__repr__()` Method
Returns an official string representation (for developers/debugging).
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __repr__(self):
        return f"Point({self.x}, {self.y})"

p = Point(3, 4)
print(repr(p))  # Point(3, 4)
print(p)        # Point(3, 4)
```

#### Other Special Methods
```python
class Number:
    def __init__(self, value):
        self.value = value
    
    def __add__(self, other):  # Overload + operator
        return Number(self.value + other.value)
    
    def __eq__(self, other):  # Overload == operator
        return self.value == other.value
    
    def __len__(self):  # Make object work with len()
        return self.value

n1 = Number(10)
n2 = Number(20)
n3 = n1 + n2
print(n3.value)  # 30
```

### Encapsulation (Data Hiding)

#### Public Attributes
Accessible from anywhere (default).
```python
class Person:
    def __init__(self, name):
        self.name = name  # Public attribute

p = Person("Alice")
print(p.name)  # Accessible
p.name = "Bob"  # Modifiable
```

#### Protected Attributes
Convention: prefix with single underscore `_` (not enforced).
```python
class Person:
    def __init__(self, name):
        self._name = name  # Protected (by convention)

p = Person("Alice")
print(p._name)  # Still accessible but indicates "use carefully"
```

#### Private Attributes
Prefix with double underscore `__` (name mangling).
```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private attribute
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
    
    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
# print(account.__balance)  # Error: can't access directly
print(account.get_balance())  # 1000 (access via method)
account.deposit(500)
print(account.get_balance())  # 1500
```

### Getters and Setters

#### Traditional Approach
```python
class Student:
    def __init__(self, name, age):
        self.__name = name
        self.__age = age
    
    def get_name(self):  # Getter
        return self.__name
    
    def set_name(self, name):  # Setter
        self.__name = name
    
    def get_age(self):
        return self.__age
    
    def set_age(self, age):
        if age > 0:
            self.__age = age
        else:
            print("Age must be positive")

s = Student("Alice", 17)
print(s.get_name())  # Alice
s.set_age(18)
print(s.get_age())   # 18
```

#### Using Property Decorators (Pythonic Way)
```python
class Student:
    def __init__(self, name, age):
        self.__name = name
        self.__age = age
    
    @property
    def name(self):  # Getter
        return self.__name
    
    @name.setter
    def name(self, value):  # Setter
        self.__name = value
    
    @property
    def age(self):
        return self.__age
    
    @age.setter
    def age(self, value):
        if value > 0:
            self.__age = value
        else:
            raise ValueError("Age must be positive")

s = Student("Alice", 17)
print(s.name)  # Alice (looks like attribute access)
s.name = "Bob"  # Uses setter
print(s.name)  # Bob
s.age = 18
print(s.age)   # 18
```

## 2. Inheritance (Detailed)
Inheritance allows a class (Child/Derived/Subclass) to derive or inherit properties and methods from another class (Parent/Base/Superclass).

### Benefits of Inheritance
*   **Code Reusability**: Write code once in parent, use in all children
*   **Extensibility**: Add new features without modifying existing code
*   **Organization**: Create hierarchical classification of classes
*   **Maintainability**: Update parent class to affect all children
*   **Polymorphism**: Same interface, different implementations

### Basic Inheritance Syntax
```python
class ParentClass:
    # Parent class body
    pass

class ChildClass(ParentClass):
    # Child class body (inherits from ParentClass)
    pass
```

### Simple Inheritance Example
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def eat(self):
        print(f"{self.name} is eating")
    
    def sleep(self):
        print(f"{self.name} is sleeping")

class Dog(Animal):  # Dog inherits from Animal
    def bark(self):
        print(f"{self.name} is barking")

# Create Dog object
dog = Dog("Bruno")
dog.eat()    # Inherited method
dog.sleep()  # Inherited method
dog.bark()   # Own method
```

### Types of Inheritance (Detailed)

#### 1. Single Inheritance
One child class inherits from exactly one parent class.
```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand
    
    def show_brand(self):
        print(f"Brand: {self.brand}")

class Car(Vehicle):
    def __init__(self, brand, model):
        super().__init__(brand)
        self.model = model
    
    def show_details(self):
        print(f"Brand: {self.brand}, Model: {self.model}")

car = Car("Toyota", "Camry")
car.show_brand()    # Inherited method
car.show_details()  # Own method
```

#### 2. Multiple Inheritance
One child class inherits from multiple parent classes.
```python
class Father:
    def skills(self):
        print("Gardening, Cooking")

class Mother:
    def skills_m(self):
        print("Programming, Painting")

class Child(Father, Mother):
    def my_skills(self):
        print("Sports, Music")

child = Child()
child.skills()      # From Father
child.skills_m()    # From Mother
child.my_skills()   # Own method
```

#### 3. Multilevel Inheritance
Chain of inheritance: Child becomes parent for another child.
```python
class Grandparent:
    def show_gp(self):
        print("This is Grandparent")

class Parent(Grandparent):
    def show_p(self):
        print("This is Parent")

class Child(Parent):
    def show_c(self):
        print("This is Child")

child = Child()
child.show_gp()  # From Grandparent
child.show_p()   # From Parent
child.show_c()   # Own method
```

#### 4. Hierarchical Inheritance
Multiple children inherit from one parent.
```python
class Animal:
    def eat(self):
        print("Animal eats")

class Dog(Animal):
    def bark(self):
        print("Dog barks")

class Cat(Animal):
    def meow(self):
        print("Cat meows")

dog = Dog()
dog.eat()   # From Animal
dog.bark()  # Own method

cat = Cat()
cat.eat()   # From Animal
cat.meow()  # Own method
```

#### 5. Hybrid Inheritance
Combination of multiple inheritance types.
```python
class School:
    def school_info(self):
        print("School information")

class Student(School):
    def student_info(self):
        print("Student information")

class Teacher(School):
    def teacher_info(self):
        print("Teacher information")

class Coordinator(Student, Teacher):
    def coordinator_info(self):
        print("Coordinator information")

coord = Coordinator()
coord.school_info()       # From School
coord.student_info()      # From Student
coord.teacher_info()      # From Teacher
coord.coordinator_info()  # Own method
```

### Method Overriding (Detailed)
Child class provides specific implementation of parent's method.

```python
class Animal:
    def sound(self):
        print("Animal makes a sound")

class Dog(Animal):
    def sound(self):  # Override parent method
        print("Dog barks")

class Cat(Animal):
    def sound(self):  # Override parent method
        print("Cat meows")

# Polymorphism in action
animals = [Animal(), Dog(), Cat()]
for animal in animals:
    animal.sound()
# Output:
# Animal makes a sound
# Dog barks
# Cat meows
```

#### Calling Parent Method After Override
```python
class Parent:
    def show(self):
        print("Parent method")

class Child(Parent):
    def show(self):
        super().show()  # Call parent method
        print("Child method")

child = Child()
child.show()
# Output:
# Parent method
# Child method
```

### `super()` Function (Detailed)
Returns a proxy object that allows calling parent class methods.

#### Basic Usage
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def display(self):
        print(f"Name: {self.name}, Age: {self.age}")

class Student(Person):
    def __init__(self, name, age, roll_no):
        super().__init__(name, age)  # Call parent constructor
        self.roll_no = roll_no
    
    def display(self):
        super().display()  # Call parent method
        print(f"Roll No: {self.roll_no}")

student = Student("Alice", 17, 101)
student.display()
# Output:
# Name: Alice, Age: 17
# Roll No: 101
```

#### super() in Multiple Inheritance
```python
class A:
    def __init__(self):
        print("A initialized")
        super().__init__()

class B:
    def __init__(self):
        print("B initialized")
        super().__init__()

class C(A, B):
    def __init__(self):
        print("C initialized")
        super().__init__()

c = C()
# Output (Method Resolution Order):
# C initialized
# A initialized
# B initialized
```

### Method Resolution Order (MRO)
Order in which Python searches for methods in inheritance hierarchy.
```python
class A:
    def method(self):
        print("A method")

class B(A):
    def method(self):
        print("B method")

class C(A):
    def method(self):
        print("C method")

class D(B, C):
    pass

d = D()
d.method()  # B method (searches B before C)

# View MRO
print(D.mro())
# [<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>]
```

### Polymorphism
Same interface, different implementations.

#### Method Overloading (Achieved through default arguments)
```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c

calc = Calculator()
print(calc.add(5))        # 5
print(calc.add(5, 10))    # 15
print(calc.add(5, 10, 15)) # 30
```

#### Method Overriding (Runtime Polymorphism)
```python
class Shape:
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width
    
    def area(self):
        return self.length * self.width

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius ** 2

shapes = [Rectangle(5, 3), Circle(7)]
for shape in shapes:
    print(f"Area: {shape.area()}")
```

### Abstract Base Classes (Introduction)
Classes that cannot be instantiated; used as templates.
```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        print("Bark")

# animal = Animal()  # Error: Can't instantiate abstract class
dog = Dog()
dog.sound()  # Bark
```

### Composition vs Inheritance
**Composition**: "Has-a" relationship (preferred over deep inheritance).
```python
# Inheritance (Is-a): Car IS-A Vehicle
class Vehicle:
    pass

class Car(Vehicle):
    pass

# Composition (Has-a): Car HAS-AN Engine
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()  # Composition
    
    def start(self):
        self.engine.start()

car = Car()
car.start()
```
