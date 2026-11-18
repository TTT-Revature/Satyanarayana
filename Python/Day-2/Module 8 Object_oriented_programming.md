# Python Object-Oriented Programming (OOP) – In-Depth Guide

Object-Oriented Programming (OOP) is one of the most important concepts in Python. It allows developers to organize programs using classes and objects, making applications easier to develop, maintain, reuse, and extend.

This guide explains each topic from a teaching perspective, starting with fundamental concepts and progressing to advanced OOP concepts, with definitions, syntax, practical examples, outputs, and real-world applications.

---

## 1. Classes and Objects

### 1.1 What is Object-Oriented Programming?
Object-Oriented Programming is a programming approach in which programs are organized around objects rather than only functions and instructions.

An object represents a real-world or logical entity containing:
* **Data (Attributes):** Information associated with the object.
* **Behavior (Methods):** Actions that the object can perform.

For example, consider a student:
* **Attributes:** Name, Roll number, Age, Department.
* **Methods:** Attend classes, Write examinations, Display details, Calculate marks.

In OOP, we represent this student using a class and an object.

### 1.2 What is a Class?
A class is a blueprint or template used to create objects. It defines the attributes and methods that its objects will have.

**Syntax:**
```python
class ClassName:
    # Attributes

    # Methods
    def method_name(self):
        statements
```

**Example:**
```python
class Student:
    def display(self):
        print("Welcome to Python OOP")
```
Here:
* `class` is the keyword used to define a class.
* `Student` is the class name.
* `display()` is a method defined inside the class.

### 1.3 What is an Object?
An object is an instance of a class. When we create an object, Python allocates an instance and allows us to access its attributes and methods.

```python
class Student:
    def display(self):
        print("Welcome to Python OOP")

# Creating an object
student1 = Student()

# Calling the method
student1.display()
```

**Output:**
```text
Welcome to Python OOP
```

### 1.4 Creating Multiple Objects
A single class can be used to create multiple objects:
```python
class Student:
    def display(self):
        print("Student details")

student1 = Student()
student2 = Student()
student3 = Student()

student1.display()
student2.display()
student3.display()
```

**Output:**
```text
Student details
Student details
Student details
```
Each object is a separate instance of the same class.

### 1.5 Real-World Example
```python
class Employee:
    def display(self):
        print("Employee information")

emp1 = Employee()
emp2 = Employee()

emp1.display()
emp2.display()
```
The same `Employee` class can represent thousands of employees in an organization.

### 1.6 Advantages of Classes and Objects
* **Code reusability:** A class can be reused to create multiple objects.
* **Modularity:** Programs can be divided into independent classes.
* **Maintainability:** Changes can be made to a class without rewriting the entire application.
* **Data organization:** Related data and functionality are grouped together.
* **Scalability:** OOP makes it easier to develop large applications.

---

## 2. Attributes, Methods, `__init__()` and `self`

### 2.1 Attributes
Attributes are variables associated with a class or an object that store information.

#### A. Instance Attributes
Instance attributes belong to individual objects and are commonly created using `self`. Each object can have its own values.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

student1 = Student("Rahul", 22)
student2 = Student("Priya", 23)

print(student1.name, student1.age)  # Rahul 22
print(student2.name, student2.age)  # Priya 23
```

#### B. Class Attributes
Class attributes are defined directly inside the class but outside its methods. They are shared by all instances unless an instance overrides the attribute with its own value.

```python
class Student:
    college = "JNTUH"

    def __init__(self, name):
        self.name = name

student1 = Student("Rahul")
student2 = Student("Priya")

print(student1.college)  # JNTUH
print(student2.college)  # JNTUH
print(Student.college)   # JNTUH
```

### 2.2 Difference Between Instance and Class Attributes

| Instance Attributes | Class Attributes |
| :--- | :--- |
| Belong to individual objects | Belong to the class |
| Usually defined using `self` | Defined directly inside the class |
| Each object can have different values | Shared by instances by default |
| Accessed through an object | Accessed through class or object |
| Changes generally affect one instance | Changes to the class attribute affect instances that do not shadow it |

### 2.3 Methods
Methods are functions defined inside a class representing the actions an object can perform.

```python
class Calculator:
    def add(self, a, b):
        return a + b

    def subtract(self, a, b):
        return a - b

calc = Calculator()
print(calc.add(10, 20))       # 30
print(calc.subtract(30, 10))  # 20
```

### 2.4 What is `__init__()`?
`__init__()` is a special method in Python known as an **initializer**. It is automatically called after a new object has been created to initialize its attributes.

**Syntax:**
```python
class ClassName:
    def __init__(self, parameters):
        self.attribute = parameters
```

**Example:**
```python
class Student:
    def __init__(self, name, age, department):
        self.name = name
        self.age = age
        self.department = department

student1 = Student("Rahul", 22, "CSE")
print(student1.name, student1.age, student1.department)  # Rahul 22 CSE
```

**How does it work?**
1. Python creates a new `Student` object.
2. Python automatically invokes `__init__()`.
3. The supplied arguments are passed to the initializer.
4. `self.name`, `self.age`, and `self.department` are assigned their respective values.

> **Important:** Technically, `__new__()` creates the object, while `__init__()` initializes it. Therefore, `__init__()` is not the constructor in the strict technical sense, although it is commonly called the constructor in introductory Python teaching.

### 2.5 What is `self`?
`self` refers to the current instance of a class, allowing methods to access and modify attributes and other methods belonging to that specific object.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print("Student name:", self.name)

student1 = Student("Rahul")
student2 = Student("Priya")

student1.display()  # Internally behaves like Student.display(student1)
student2.display()  # Internally behaves like Student.display(student2)
```

**Important points about `self`:**
* `self` is not a Python keyword; it is a conventional parameter name.
* It is automatically passed when an instance method is called through an object.
* Technically another name could be used, but `self` is strongly recommended by PEP 8.

### 2.6 Complete Example
```python
class Employee:
    company = "Tech Solutions"

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print("Employee:", self.name)
        print("Salary:", self.salary)
        print("Company:", self.company)

emp1 = Employee("Rahul", 50000)
emp2 = Employee("Priya", 60000)

emp1.display()
print("----------------")
emp2.display()
```

**Output:**
```text
Employee: Rahul
Salary: 50000
Company: Tech Solutions
----------------
Employee: Priya
Salary: 60000
Company: Tech Solutions
```

---

## 3. Encapsulation and Properties

### 3.1 What is Encapsulation?
Encapsulation is one of the four major principles of OOP. It means combining data and the methods that operate on that data into a single unit (usually a class) while controlling how internal data is accessed or modified.

### 3.2 Access Modifiers in Python
Python uses naming conventions rather than strict access keywords:

#### A. Public Attributes
Accessible from anywhere:
```python
class Student:
    def __init__(self, name):
        self.name = name

student = Student("Rahul")
print(student.name)  # Rahul
```

#### B. Protected Attributes
Indicated by a single underscore (`_`). Intended for internal use within a class and its subclasses (convention only; Python does not block direct access):
```python
class Student:
    def __init__(self, name):
        self._name = name
```

#### C. Private Attributes
Indicated by double underscores (`__`). Python applies **name mangling** to these attributes:
```python
class Student:
    def __init__(self, name):
        self.__name = name

student = Student("Rahul")
# print(student.__name)        # Raises AttributeError
print(student._Student__name)  # Rahul (accessed via mangled name)
```
> **Note:** Private attributes provide name protection against accidental access or collision in subclasses, not absolute security.

### 3.3 Implementing Encapsulation
```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            print("Deposit successful")
        else:
            print("Invalid deposit amount")

    def withdraw(self, amount):
        if amount > self.__balance:
            print("Insufficient balance")
        elif amount <= 0:
            print("Invalid withdrawal amount")
        else:
            self.__balance -= amount
            print("Withdrawal successful")

    def display_balance(self):
        print("Balance:", self.__balance)

account = BankAccount(10000)
account.deposit(5000)
account.withdraw(3000)
account.display_balance()  # Balance: 12000
```

### 3.4–3.7 Properties (`@property`, Setter, and Deleter)
Properties provide a Pythonic way to add validation, compute values dynamically, and maintain backward compatibility without changing attribute access syntax.

```python
class Student:
    def __init__(self, name, age):
        self.__name = name
        self.__age = age

    @property
    def name(self):
        return self.__name

    @name.deleter
    def name(self):
        del self.__name

    @property
    def age(self):
        return self.__age

    @age.setter
    def age(self, value):
        if value > 0:
            self.__age = value
        else:
            raise ValueError("Age must be positive")

student = Student("Rahul", 22)
print(student.age)  # 22
student.age = 23
print(student.age)  # 23
# student.age = -5  # Raises ValueError: Age must be positive
del student.name
```

### 3.8 Real-World Applications of Encapsulation
* **Banking applications:** Protecting account balances.
* **E-commerce:** Controlling product prices and stock quantities.
* **Employee management:** Validating salaries and employee information.
* **Authentication systems:** Managing passwords and credentials.
* **Healthcare applications:** Controlling access to patient records.

---

## 4. Instance, Class and Static Methods

### 4.1 Instance Methods
* Take `self` as the first parameter.
* Can access and modify both instance and class state.

### 4.2 Class Methods
* Decorated with `@classmethod` and take `cls` (the class itself) as the first parameter.
* Can access/modify class attributes and serve as factory methods.

### 4.3 Static Methods
* Decorated with `@staticmethod`; do not receive `self` or `cls` automatically.
* Used for utility functions logically grouped within the class namespace.

### 4.4 Practical Example Using All Three Methods
```python
class Employee:
    company = "ABC Technologies"

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    # Instance method
    def display(self):
        print(self.name, self.salary)

    # Class method
    @classmethod
    def change_company(cls, company):
        cls.company = company

    # Static method
    @staticmethod
    def is_valid_salary(salary):
        return salary > 0

emp = Employee("Rahul", 50000)
emp.display()                           # Rahul 50000
Employee.change_company("XYZ Tech")
print(Employee.company)                 # XYZ Tech
print(Employee.is_valid_salary(50000))  # True
```

### 4.5 Difference Between Instance, Class and Static Methods

| Feature | Instance Method | Class Method | Static Method |
| :--- | :--- | :--- | :--- |
| **Decorator** | Not required | `@classmethod` | `@staticmethod` |
| **First parameter** | `self` | `cls` | No automatic parameter |
| **Access instance attributes** | Yes | No direct access | No direct access |
| **Access class attributes** | Yes | Yes | Only via explicit class/object reference |
| **Modify instance state** | Yes | Not directly | Not automatically |
| **Modify class state** | Yes | Yes | Possible via explicit reference |
| **Main purpose** | Object-specific operations | Class-level operations | Utility operations |

### 4.6 Factory Methods Using Class Methods
```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_string(cls, data):
        name, age = data.split(",")
        return cls(name, int(age))

student = Student.from_string("Rahul,22")
print(student.name, student.age)  # Rahul 22
```

---

## 5. Inheritance and Method Overriding

### 5.1 What is Inheritance?
Inheritance allows a **child class (derived/subclass)** to acquire the attributes and methods of a **parent class (base/superclass)**, promoting code reusability.

```python
class Parent:
    pass

class Child(Parent):
    pass
```

### 5.2 Simple Inheritance Example
```python
class Animal:
    def eat(self):
        print("Animals can eat")

class Dog(Animal):
    def bark(self):
        print("Dog can bark")

dog = Dog()
dog.eat()   # Animals can eat
dog.bark()  # Dog can bark
```

### 5.3 Types of Inheritance in Python

1. **Single Inheritance:** One child inherits from one parent (`class Dog(Animal):`).
2. **Multiple Inheritance:** One child inherits from multiple parents (`class Child(Father, Mother):`).
3. **Multilevel Inheritance:** A chain of inheritance (`Grandparent` $\rightarrow$ `Parent` $\rightarrow$ `Child`).
4. **Hierarchical Inheritance:** Multiple children inherit from a single parent (`Dog(Animal)` and `Cat(Animal)`).
5. **Hybrid Inheritance:** A combination of two or more inheritance types (e.g., hierarchical + multiple inheritance).

### 5.4 & 5.5 Method Overriding
Method overriding occurs when a child class provides its own implementation of a method already defined in its parent class, enabling runtime polymorphism.

```python
class Animal:
    def sound(self):
        print("Animal makes a sound")

class Dog(Animal):
    def sound(self):
        print("Dog barks")

class Cat(Animal):
    def sound(self):
        print("Cat meows")

for animal in [Animal(), Dog(), Cat()]:
    animal.sound()
```

**Output:**
```text
Animal makes a sound
Dog barks
Cat meows
```

### 5.6 Overriding vs Overloading

| Method Overriding | Method Overloading |
| :--- | :--- |
| Occurs between parent and child classes | Traditionally means multiple methods with the same name and different signatures |
| Child redefines an inherited method | Same method name supports different argument combinations |
| Used for runtime polymorphism | Commonly associated with compile-time polymorphism |
| Directly supported in Python | Python does not support traditional signature-based overloading (simulated via default args or `*args`) |

---

## 6. `super()` in Python

### 6.1–6.4 Using `super()`
`super()` is a built-in function used to access methods and attributes through the Method Resolution Order (MRO) of a class hierarchy without hardcoding the parent class name.

```python
class Parent:
    def __init__(self, name):
        self.name = name
        print("Parent constructor called")

class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)
        self.age = age
        print("Child constructor called")

obj = Child("Rahul", 22)
print(obj.name, obj.age)
```

> **Note:** If a child class defines its own `__init__()`, the parent's `__init__()` is not called automatically—you must invoke `super().__init__(...)` to initialize inherited attributes.

### 6.5 Method Resolution Order (MRO)
MRO determines the order in which Python searches for methods and attributes using the **C3 linearization algorithm**. Inspect it via `ClassName.mro()` or `ClassName.__mro__`.

### 6.6 `super()` in Cooperative Multiple Inheritance
```python
class Base:
    def process(self):
        print("Base process")

class A(Base):
    def process(self):
        print("A process")
        super().process()

class B(Base):
    def process(self):
        print("B process")
        super().process()

class C(A, B):
    def process(self):
        print("C process")
        super().process()

obj = C()
obj.process()
```

**Output:**
```text
C process
A process
B process
Base process
```

---

## 7. Polymorphism and Duck Typing

### 7.1–7.3 Polymorphism
Polymorphism ("many forms") allows the same method name or interface to behave differently depending on the object—either through inheritance/method overriding or across unrelated classes sharing a common method name.

### 7.4–7.7 Duck Typing
*"If it walks like a duck and quacks like a duck, it can be treated like a duck."*

In Python, duck typing focuses on whether an object supports the required behavior/methods rather than checking its explicit class type (`isinstance`).

```python
class Duck:
    def speak(self):
        print("Quack Quack")

class Person:
    def speak(self):
        print("Hello")

class Robot:
    def speak(self):
        print("Beep Beep")

def make_sound(obj):
    obj.speak()

for entity in [Duck(), Person(), Robot()]:
    make_sound(entity)
```

| Polymorphism | Duck Typing |
| :--- | :--- |
| An OOP concept | A programming approach used in Python |
| Same interface can have different implementations | Focuses on available behavior rather than actual type |
| Can use inheritance and overriding | Does not require inheritance |
| Describes flexible behavior | Describes how compatible objects are accepted |

---

## 8. `__str__`, `__repr__`, `__len__` and `__eq__`

Special methods (also called **dunder** or **magic methods**) allow custom objects to integrate with Python's built-in functions and operators.

### 8.2–8.4 `__str__()` vs `__repr__()`

| `__str__()` | `__repr__()` |
| :--- | :--- |
| Human-readable representation | Developer-oriented representation |
| Used by `str()` and `print()` | Used by `repr()`, debuggers, and container displays |
| Focuses on readability | Focuses on clarity and unambiguity |
| Need not be executable | Ideally provides enough info to recreate the object |

*(If `__str__()` is not defined, Python falls back to `__repr__()`.)*

### 8.5–8.7 Complete Example Using All Four Methods
```python
class Product:
    def __init__(self, name, price, items):
        self.name = name
        self.price = price
        self.items = items

    def __str__(self):
        return f"{self.name} costs Rs. {self.price}"

    def __repr__(self):
        return f"Product(name={self.name!r}, price={self.price!r}, items={self.items!r})"

    def __len__(self):
        return len(self.items)

    def __eq__(self, other):
        if not isinstance(other, Product):
            return NotImplemented
        return self.name == other.name and self.price == other.price

p1 = Product("Laptop", 50000, ["Mouse", "Bag"])
p2 = Product("Laptop", 50000, ["Mouse", "Bag"])

print(str(p1))    # Laptop costs Rs. 50000
print(repr(p1))   # Product(name='Laptop', price=50000, items=['Mouse', 'Bag'])
print(len(p1))    # 2
print(p1 == p2)   # True
```

### 8.8 Other Important Dunder Methods

| Method | Purpose | Method | Purpose |
| :--- | :--- | :--- | :--- |
| `__init__()` | Initialize an object | `__lt__()`, `__gt__()` | Define `<` and `>` |
| `__new__()` | Create an object | `__contains__()` | Define membership (`in`) |
| `__del__()` | Finalization hook | `__iter__()`, `__next__()` | Iteration protocol |
| `__add__()`, `__sub__()` | Define `+` and `-` | `__call__()` | Make an object callable |
| `__mul__()`, `__truediv__()` | Define `*` and `/` | `__getitem__()` | Support indexing (`obj[i]`) |

---

## 9. Dataclasses

### 9.1–9.5 `@dataclass` Overview
Introduced in Python 3.7, `@dataclass` automatically generates boilerplate methods (`__init__()`, `__repr__()`, and `__eq__()`) based on class type annotations.

```python
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int
    department: str = "CSE"

s1 = Student("Rahul", 22)
print(s1)  # Student(name='Rahul', age=22, department='CSE')
```

### 9.6 Mutable Defaults with `field(default_factory=...)`
Never assign a raw mutable object (like `[]`) as a default in a dataclass; use `field(default_factory=list)` so each instance gets its own list:

```python
from dataclasses import dataclass, field

@dataclass
class Student:
    name: str
    subjects: list = field(default_factory=list)
```

### 9.7–9.9 Frozen and Ordered Dataclasses
* `@dataclass(frozen=True)` prevents normal attribute reassignment after creation (raises `FrozenInstanceError`), though nested mutable objects inside it can still be mutated.
* `@dataclass(order=True)` generates comparison methods (`__lt__`, `__le__`, `__gt__`, `__ge__`) based on field order.

---

## 10. Objects, References and Mutation

### 10.1–10.6 References, Mutable vs. Immutable Objects, and Reassignment
Every Python object has an **identity** (`id()`), a **type** (`type()`), and a **value**.

| Mutable Objects | Immutable Objects |
| :--- | :--- |
| Can be modified in place after creation | Cannot be modified after creation |
| Examples: `list`, `dict`, `set`, most custom objects | Examples: `int`, `float`, `str`, `tuple`, `bool`, `bytes` |
| Shared references reflect in-place mutations | Operations create new objects; reassignment rebinds the variable |

### 10.7 `==` vs `is`
* `==` checks **value equality** (invokes `__eq__`).
* `is` checks **object identity** (whether two variables point to the exact same object in memory). Always use `is None` / `is not None` when checking for `None`.

### 10.8 Objects as Function Arguments (Call by Sharing)
Python passes object references to functions. Mutating a mutable argument inside a function affects the caller's object, whereas reassigning the parameter inside the function only rebinds the local name.

---

## 11. Shallow Copy, Deep Copy and Garbage Collection

### 11.1–11.7 Shallow Copy vs Deep Copy

| Feature | Shallow Copy (`copy.copy()`) | Deep Copy (`copy.deepcopy()`) |
| :--- | :--- | :--- |
| **New outer object** | Yes | Yes |
| **Copies nested objects recursively** | No | Yes |
| **Shares nested mutable objects** | Yes | No |
| **Performance & Memory** | Faster, lower memory | Slower, higher memory |

```python
import copy

original = [10, 20, [30, 40]]
shallow = copy.copy(original)
deep = copy.deepcopy(original)

shallow[2].append(50)
print(original)  # [10, 20, [30, 40, 50]] (affected by shallow copy)
print(deep)      # [10, 20, [30, 40]]     (independent)
```

### 11.8–11.16 Garbage Collection & `__del__()`
CPython manages memory automatically using:
1. **Reference Counting:** Tracks the number of references to an object (`sys.getrefcount()`). When references drop to zero, the object is immediately deallocated.
2. **Cyclic Garbage Collector (`gc` module):** Detects and reclaims unreachable reference cycles (e.g., two objects referencing each other) that reference counting alone cannot free.

> **Best Practice:** Do not rely on `__del__()` (finalizers) for closing files or releasing external resources—timing is not guaranteed. Always use context managers (`with open(...)`).

---

## 12. Important Differences – Quick Revision

### 12.1 Class vs Object
* **Class:** Blueprint defining attributes and methods (`class Student:`).
* **Object:** Concrete instance created by calling the class (`Student()`).

### 12.2 The Four Pillars of OOP
* **Encapsulation:** Bundling data and methods while controlling access (e.g., `BankAccount`).
* **Inheritance:** Reusing features from a parent class (e.g., `Dog` inherits `Animal`).
* **Polymorphism:** Same interface, different behaviors (e.g., `sound()`).
* **Abstraction:** Hiding implementation complexity and exposing essential interfaces.

### 12.3 `self` vs `cls`
* `self`: Refers to the current instance (used in instance methods).
* `cls`: Refers to the class itself (used in `@classmethod`).

### 12.4 `super()` vs Direct Parent Call
* `super()` follows the dynamic MRO and enables cooperative multiple inheritance.
* Direct parent calls (`Parent.method(self)`) bypass the MRO.

### 12.5 Dataclass vs Normal Class
* `@dataclass` eliminates boilerplate for data-centric models; standard classes offer full manual control over complex behavior.

---

## 13. Practical Python OOP Project: Student Management System

```python
from dataclasses import dataclass

# Base class
class Person:
    college = "JNTUH"

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)

    def role(self):
        print("Person")


# Derived class
class Student(Person):
    def __init__(self, name, age, roll_no, marks):
        super().__init__(name, age)
        self.roll_no = roll_no
        self.__marks = marks

    @property
    def marks(self):
        return self.__marks

    @marks.setter
    def marks(self, value):
        if 0 <= value <= 100:
            self.__marks = value
        else:
            raise ValueError("Marks must be between 0 and 100")

    def role(self):
        print("Student")

    def display(self):
        super().display()
        print("Roll Number:", self.roll_no)
        print("Marks:", self.__marks)
        print("College:", self.college)

    def __str__(self):
        return f"{self.name} - {self.roll_no}"

    def __eq__(self, other):
        if not isinstance(other, Student):
            return NotImplemented
        return self.roll_no == other.roll_no


# Dataclass
@dataclass
class Course:
    course_name: str
    duration: int


if __name__ == "__main__":
    student1 = Student("Rahul", 22, 101, 85)
    student2 = Student("Priya", 23, 102, 90)

    student1.display()
    print("----------------")
    student2.display()

    # Property update
    student1.marks = 95
    print("Updated Marks:", student1.marks)

    # Polymorphism
    people = [Person("Arun", 40), student1, student2]
    for person in people:
        person.role()

    # Special methods
    print(student1)
    print(student1 == student2)

    # Dataclass
    course = Course("Python Programming", 3)
    print(course)
```

---

## 14. Important Interview Questions

- [ ] **1.** What is the difference between a class and an object?
- [ ] **2.** Why is `self` used in Python?
- [ ] **3.** Is `__init__()` a constructor?
- [ ] **4.** What is encapsulation?
- [ ] **5.** Does Python support private variables?
- [ ] **6.** What is the difference between `classmethod` and `staticmethod`?
- [ ] **7.** What is method overriding?
- [ ] **8.** Why do we use `super()`?
- [ ] **9.** What is duck typing?
- [ ] **10.** What is the difference between `__str__` and `__repr__`?
- [ ] **11.** Why are dataclasses used?
- [ ] **12.** What is the difference between `==` and `is`?
- [ ] **13.** What is mutation?
- [ ] **14.** What is the difference between shallow and deep copy?
- [ ] **15.** How does Python garbage collection work?

---

## 15. Recommended Learning and Practice Order

| Stage | Topics | Practice |
| :--- | :--- | :--- |
| **1. Fundamentals** | Classes, objects, attributes, methods, `self`, `__init__` | `Student` class |
| **2. Data protection** | Encapsulation, properties | Bank account |
| **3. Method types** | Instance, class, static methods | Employee management |
| **4. Reusability** | Inheritance, overriding, `super()` | Animal hierarchy |
| **5. Advanced behavior** | Polymorphism, duck typing | Payment system |
| **6. Special methods** | `__str__`, `__repr__`, `__len__`, `__eq__` | Shopping cart |
| **7. Data modeling** | Dataclasses | Student/course records |
| **8. Memory management** | References, mutation, copying, garbage collection | Nested list experiments |

---

## 16. Practice Assignments

1. **Bank Account Management:** Create a `BankAccount` class with deposit, withdrawal, balance validation, and transaction history.
2. **Employee Management:** Create an `Employee` class with employee details, salary calculation, and class-level company information.
3. **Vehicle Inheritance:** Create a `Vehicle` parent class and `Car`, `Bike`, and `Bus` child classes. Override a common method.
4. **Library Management:** Create `Book` and `Library` classes with methods for adding, borrowing, returning, and displaying books.
5. **Shopping Cart:** Implement a `ShoppingCart` class using `__init__()`, `__str__()`, `__len__()`, and `__eq__()`.
6. **Student Management:** Use dataclasses to store student information and calculate average marks.
7. **Copying Experiments:** Create nested lists and demonstrate the difference between assignment, shallow copy, and deep copy.
8. **Duck Typing:** Create different classes such as `PDFReader`, `WordReader`, and `TextReader` that implement a common `read()` method.

> **Recommendation:** Before moving to advanced Python topics such as multithreading, asynchronous programming, and design patterns, ensure you can independently implement the **Bank Account**, **Employee Management**, and **Library Management** projects. These build a strong foundation for using OOP in Django, Flask, FastAPI, LangChain, and other Python frameworks.