### Python Concepts

#### 1. Basic Syntax and Variables

- **Concept:** Python syntax and variable assignment.
- **Example:**
  ```python
  # Variable assignment
  x = 10
  y = "Hello, World!"
  z = 3.14
  
  print(x)  # Output: 10
  print(y)  # Output: Hello, World!
  print(z)  # Output: 3.14
  ```

#### 2. Data Types

- **Concept:** Python supports various data types such as integers, floats, strings, lists, tuples, sets, and dictionaries.
- **Example:**
  ```python
  integer_var = 42
  float_var = 3.14159
  string_var = "Python"
  list_var = [1, 2, 3, 4]
  tuple_var = (1, 2, 3, 4)
  set_var = {1, 2, 3, 4}
  dict_var = {"a": 1, "b": 2}
  
  print(type(integer_var))  # Output: <class 'int'>
  print(type(float_var))    # Output: <class 'float'>
  print(type(string_var))   # Output: <class 'str'>
  print(type(list_var))     # Output: <class 'list'>
  print(type(tuple_var))    # Output: <class 'tuple'>
  print(type(set_var))      # Output: <class 'set'>
  print(type(dict_var))     # Output: <class 'dict'>
  ```

#### 3. Control Flow

- **Concept:** Python supports `if`, `elif`, and `else` for conditional statements, and `for` and `while` loops for iteration.
- **Example:**
  ```python
  # Conditional statements
  x = 10
  if x > 0:
      print("x is positive")
  elif x == 0:
      print("x is zero")
  else:
      print("x is negative")

  # For loop
  for i in range(5):
      print(i)  # Output: 0 1 2 3 4

  # While loop
  count = 0
  while count < 5:
      print(count)  # Output: 0 1 2 3 4
      count += 1
  ```

#### 4. Functions

- **Concept:** Functions are defined using the `def` keyword. They can take parameters and return values.
- **Example:**
  ```python
  def add(a, b):
      return a + b
  
  result = add(5, 3)
  print(result)  # Output: 8
  ```

#### 5. Classes and Objects

- **Concept:** Python supports object-oriented programming. Classes are defined using the `class` keyword.
- **Example:**
  ```python
  class Person:
      def __init__(self, name, age):
          self.name = name
          self.age = age

      def greet(self):
          return f"Hello, my name is {self.name} and I am {self.age} years old."

  person = Person("Alice", 30)
  print(person.greet())  # Output: Hello, my name is Alice and I am 30 years old.
  ```

### Data Structures

#### 1. Lists

- **Concept:** Lists are ordered, mutable collections of items.
- **Example:**
  ```python
  fruits = ["apple", "banana", "cherry"]
  fruits.append("date")
  print(fruits)  # Output: ['apple', 'banana', 'cherry', 'date']
  print(fruits[1])  # Output: banana
  ```

#### 2. Tuples

- **Concept:** Tuples are ordered, immutable collections of items.
- **Example:**
  ```python
  dimensions = (1920, 1080)
  print(dimensions)  # Output: (1920, 1080)
  print(dimensions[0])  # Output: 1920
  ```

#### 3. Sets

- **Concept:** Sets are unordered collections of unique items.
- **Example:**
  ```python
  unique_numbers = {1, 2, 3, 4, 4, 2}
  print(unique_numbers)  # Output: {1, 2, 3, 4}
  unique_numbers.add(5)
  print(unique_numbers)  # Output: {1, 2, 3, 4, 5}
  ```

#### 4. Dictionaries

- **Concept:** Dictionaries are collections of key-value pairs.
- **Example:**
  ```python
  student = {"name": "John", "age": 21, "major": "Computer Science"}
  print(student["name"])  # Output: John
  student["age"] = 22
  print(student)  # Output: {'name': 'John', 'age': 22, 'major': 'Computer Science'}
  ```

#### 5. List Comprehensions

- **Concept:** List comprehensions provide a concise way to create lists.
- **Example:**
  ```python
  squares = [x**2 for x in range(10)]
  print(squares)  # Output: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
  ```

### Advanced Python Concepts

#### 1. Generators

- **Concept:** Generators are iterators that yield items one at a time using the `yield` keyword.
- **Example:**
  ```python
  def count_up_to(max):
      count = 1
      while count <= max:
          yield count
          count += 1
  
  counter = count_up_to(5)
  for num in counter:
      print(num)  # Output: 1 2 3 4 5
  ```

#### 2. Decorators

- **Concept:** Decorators are functions that modify the behavior of other functions or methods.
- **Example:**
  ```python
  def decorator_func(func):
      def wrapper():
          print("Something is happening before the function is called.")
          func()
          print("Something is happening after the function is called.")
      return wrapper

  @decorator_func
  def say_hello():
      print("Hello!")

  say_hello()
  # Output:
  # Something is happening before the function is called.
  # Hello!
  # Something is happening after the function is called.
  ```

#### 3. Lambda Functions

- **Concept:** Lambda functions are small anonymous functions defined with the `lambda` keyword.
- **Example:**
  ```python
  add = lambda x, y: x + y
  print(add(2, 3))  # Output: 5
  ```

#### 4. Exception Handling

- **Concept:** Exception handling is done using `try`, `except`, `else`, and `finally` blocks.
- **Example:**
  ```python
  try:
      result = 10 / 0
  except ZeroDivisionError:
      print("Cannot divide by zero.")
  else:
      print("Division successful.")
  finally:
      print("Execution complete.")
  # Output:
  # Cannot divide by zero.
  # Execution complete.
  ```

#### 5. File I/O

- **Concept:** Reading from and writing to files.
- **Example:**
  ```python
  # Writing to a file
  with open('example.txt', 'w') as file:
      file.write("Hello, World!")
  
  # Reading from a file
  with open('example.txt', 'r') as file:
      content = file.read()
      print(content)  # Output: Hello, World!
  ```

This knowledge base covers fundamental and advanced Python concepts and data structures, providing a comprehensive overview for assessing a candidate's Python proficiency in a data engineering interview.