### 1. Classes and Objects

#### Definition:
Classes are blueprints for creating objects. Objects are instances of classes that encapsulate data (attributes) and behaviours (methods).

#### Example:
```python
# Define a class
class Car:
    # Class attribute
    car_count = 0
    
    # Constructor method
    def __init__(self, brand, model):
        # Instance attributes
        self.brand = brand
        self.model = model
        Car.car_count += 1
    
    # Instance method
    def display_info(self):
        print(f"{self.brand} {self.model}")

# Create objects (instances of Car class)
car1 = Car("Toyota", "Corolla")
car2 = Car("Honda", "Civic")

# Access attributes and call methods
car1.display_info()  # Output: Toyota Corolla
car2.display_info()  # Output: Honda Civic

# Access class attribute
print(f"Number of cars created: {Car.car_count}")  # Output: Number of cars created: 2
```

### 2. Inheritance

#### Definition:
Inheritance allows a class (subclass/derived class) to inherit attributes and methods from another class (superclass/base class). It promotes code reusability and allows hierarchical relationships between classes.

#### Example:
```python
# Base class
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        raise NotImplementedError("Subclass must implement abstract method")

# Derived class (inherits from Animal)
class Dog(Animal):
    def speak(self):
        return "Woof!"

# Derived class (inherits from Animal)
class Cat(Animal):
    def speak(self):
        return "Meow!"

# Usage
dog = Dog("Buddy")
cat = Cat("Whiskers")

print(dog.name + ": " + dog.speak())  # Output: Buddy: Woof!
print(cat.name + ": " + cat.speak())  # Output: Whiskers: Meow!
```

### 3. Encapsulation

#### Definition:
Encapsulation refers to restricting direct access to some of an object's components (attributes and methods). It helps in controlling the level of abstraction and hides internal state.

#### Example:
```python
class BankAccount:
    def __init__(self, account_number, balance):
        self.account_number = account_number
        self.__balance = balance  # Private attribute
    
    def deposit(self, amount):
        self.__balance += amount
    
    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient balance")
    
    def get_balance(self):
        return self.__balance

# Usage
acc1 = BankAccount("12345", 1000)
print(acc1.get_balance())  # Output: 1000
acc1.withdraw(500)
print(acc1.get_balance())  # Output: 500
acc1.deposit(200)
print(acc1.get_balance())  # Output: 700
```

### 4. Polymorphism

#### Definition:
Polymorphism means the ability to take multiple forms. In OOP, it allows objects of different classes to be treated as objects of a common superclass. It is achieved through method overriding and method overloading.

#### Example:
```python
# Polymorphism through method overriding
class Bird:
    def sound(self):
        raise NotImplementedError("Subclass must implement abstract method")

class Parrot(Bird):
    def sound(self):
        return "Squawk!"

class Crow(Bird):
    def sound(self):
        return "Caw!"

# Usage
parrot = Parrot()
crow = Crow()

print(parrot.sound())  # Output: Squawk!
print(crow.sound())    # Output: Caw!
```

### 5. Abstraction

#### Definition:
Abstraction focuses on hiding the complex implementation details and showing only the essential features of the object. It is implemented using abstract classes and interfaces.

#### Example:
```python
from abc import ABC, abstractmethod

# Abstract base class
class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

# Concrete classes (implementing Shape)
class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius * self.radius
    
    def perimeter(self):
        return 2 * 3.14 * self.radius

class Square(Shape):
    def __init__(self, side):
        self.side = side
    
    def area(self):
        return self.side * self.side
    
    def perimeter(self):
        return 4 * self.side

# Usage
circle = Circle(5)
square = Square(4)

print("Area of circle:", circle.area())        # Output: Area of circle: 78.5
print("Perimeter of circle:", circle.perimeter())  # Output: Perimeter of circle: 31.400000000000002
print("Area of square:", square.area())        # Output: Area of square: 16
print("Perimeter of square:", square.perimeter())  # Output: Perimeter of square: 16
```

### Conclusion
This knowledge base provides a foundational understanding of Object-Oriented Programming in Python, covering classes, objects, inheritance, encapsulation, polymorphism, and abstraction with examples. These concepts are fundamental to writing efficient, modular, and reusable code in Python and are widely used in real-world applications.