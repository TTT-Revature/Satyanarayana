# Python Functions, Functional Programming and Modules – In-Depth Explanation

Functions are one of the most important concepts in Python programming. They help us divide large programs into smaller, reusable, organized, and manageable blocks of code.

In Python, functions allow us to:
* Avoid writing the same code repeatedly.
* Divide complex problems into smaller tasks.
* Improve code readability and maintainability.
* Accept input through parameters.
* Return results using the `return` statement.
* Build reusable applications and modules.

This tutorial covers topics from basic function creation to advanced concepts such as `*args`, `**kwargs`, lambda functions, functional programming, modules, and the `__name__` variable.

---

## 1. Defining and Calling Functions

### 1.1 What is a Function?
A function is a reusable block of code designed to perform a particular task.

For example, imagine that we want to calculate the sum of two numbers multiple times. Without a function, we might write:

```python
a = 10
b = 20
print(a + b)

x = 30
y = 40
print(x + y)

p = 50
q = 60
print(p + q)
```

This approach repeats the same logic. Instead, we can create a function and reuse it whenever required.

### 1.2 Defining a Function
In Python, we define a function using the `def` keyword.

**Syntax:**
```python
def function_name(parameters):
    # Function body
    statements
```

**Explanation:**

| Component | Description |
| :--- | :--- |
| `def` | Keyword used to define a function |
| `function_name` | Name of the function |
| `parameters` | Input variables accepted by the function |
| `:` | Indicates the beginning of the function body |
| Indentation | Defines the function body |
| `statements` | Instructions executed when called |

**Example: Creating a simple function**
```python
def greet():
    print("Hello, welcome to Python programming!")
```
Here, we have defined a function called `greet()`. However, defining a function does not automatically execute it—we must call the function.

### 1.3 Calling a Function
A function call executes the statements inside the function.

```python
def greet():
    print("Hello, welcome to Python programming!")

greet()
```

**Output:**
```text
Hello, welcome to Python programming!
```

**Execution order:**
1. Program starts.
2. Define `greet()` (function body is stored, not executed yet).
3. Call `greet()`.
4. Execute function body and print greeting message.

### 1.4 Functions with Parameters
A function can accept input values called parameters.

```python
def greet(name):
    print("Hello", name)

greet("Rahul")
greet("Priya")
```

**Output:**
```text
Hello Rahul
Hello Priya
```
Here, `name` is a parameter, and `"Rahul"` and `"Priya"` are arguments.

### 1.5 Functions with Multiple Parameters
```python
def add(a, b):
    result = a + b
    print("Sum:", result)

add(10, 20)
add(50, 60)
```

**Output:**
```text
Sum: 30
Sum: 110
```

### 1.6 Functions Without Parameters vs. With Parameters

| Without Parameters | With Parameters |
| :--- | :--- |
| Does not accept input values | Accepts input values |
| Performs predefined operations | Performs operations based on supplied inputs |
| `def greet():` | `def greet(name):` |

### 1.7 Types of Functions in Python
1. **Built-in functions:** Predefined functions provided by Python that we can directly use:
   ```python
   print("Hello")
   len("Python")
   max(10, 20, 30)
   min(10, 20, 30)
   sum([10, 20, 30])
   type(100)
   ```
2. **User-defined functions:** Functions created by programmers to perform specific tasks:
   ```python
   def square(number):
       print(number * number)

   square(5)  # Output: 25
   ```

---

## 2. Parameters and Arguments

### 2.1 What are Parameters?
Parameters are variables defined inside a function declaration that receive values when the function is called.

```python
def add(a, b):  # a and b are parameters
    print(a + b)
```

### 2.2 What are Arguments?
Arguments are the actual values passed to a function when calling it.

```python
add(10, 20)  # 10 and 20 are arguments (Output: 30)
```

### 2.3 Parameters vs. Arguments

| Parameters | Arguments |
| :--- | :--- |
| Defined in function declaration | Passed during function call |
| Act as placeholders | Represent actual values or objects |
| Example: `a, b` | Example: `10, 20` |

### 2.4 Types of Arguments
* Positional arguments
* Keyword arguments
* Default arguments
* Variable-length positional arguments (`*args`)
* Variable-length keyword arguments (`**kwargs`)

---

## 3. Positional, Keyword and Default Arguments

### 3.1 Positional Arguments
Positional arguments are values passed to a function according to the position of parameters.

```python
def student(name, age):
    print("Name:", name)
    print("Age:", age)

student("Rahul", 21)
```

**Output:**
```text
Name: Rahul
Age: 21
```

The order matters—passing `student(21, "Rahul")` prints `21 Rahul` because Python assigns values strictly by position.

### 3.2 Keyword Arguments
Keyword arguments pass values using parameter names, meaning order does not matter.

```python
def student(name, age):
    print("Name:", name)
    print("Age:", age)

student(age=21, name="Rahul")
```

**Output:**
```text
Name: Rahul
Age: 21
```

#### Mixing positional and keyword arguments
```python
def student(name, age, course):
    print(name, age, course)

student("Rahul", age=21, course="Python")
```
> **Important rule:** Positional arguments must come before keyword arguments. Writing `student(name="Rahul", 21, "Python")` causes a `SyntaxError`.

### 3.3 Default Arguments
Default arguments are parameters with predefined values used if the caller omits them.

```python
def greet(name="Student"):
    print("Hello", name)

greet()         # Hello Student
greet("Rahul")  # Hello Rahul
```

**Multiple default arguments:**
```python
def employee(name, department="IT", salary=30000):
    print(f"Name: {name}, Department: {department}, Salary: {salary}")

employee("Rahul")
employee("Priya", "AI")
employee("Arjun", "HR", 40000)
```

> **Important rule:** Parameters without default values must appear before parameters with default values. Writing `def add(a=10, b):` produces a `SyntaxError`.

### 3.4 Mutable Default Argument Problem
Consider this common Python interview pitfall:

```python
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item(10))  # [10]
print(add_item(20))  # [10, 20]
print(add_item(30))  # [10, 20, 30]
```
**Why does this happen?** Python creates the default list only once when the function is defined, so subsequent calls reuse the same list.

**Recommended solution:** Use `None` as the default value:
```python
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

print(add_item(10))  # [10]
print(add_item(20))  # [20]
print(add_item(30))  # [30]
```

### 3.5 Comparison of Argument Types

| Type | Meaning | Example |
| :--- | :--- | :--- |
| Positional | Assigned by position | `add(10, 20)` |
| Keyword | Assigned by parameter name | `add(a=10, b=20)` |
| Default | Uses predefined value if omitted | `greet()` |
| `*args` | Accepts extra positional arguments | `add(1, 2, 3)` |
| `**kwargs` | Accepts extra keyword arguments | `student(name="Rahul")` |

---

## 4. Return Values and Multiple Returns

### 4.1 What is a Return Statement?
The `return` statement sends a result from a function back to the calling code and terminates the function's execution.

```python
def add(a, b):
    result = a + b
    return result

answer = add(10, 20)
print(answer)  # 30
```

### 4.2 Difference Between `print()` and `return`

**Using `print()`:**
```python
def add(a, b):
    print(a + b)

result = add(10, 20)
print("Result:", result)  # Output: 30 \n Result: None
```
`print()` displays a value on the console, whereas Python automatically returns `None` if a function has no `return` statement.

**Using `return`:**
```python
def add(a, b):
    return a + b

result = add(10, 20)
print("Result:", result)  # Output: Result: 30
```

| `print()` | `return` |
| :--- | :--- |
| Displays output | Sends a value back |
| Does not return the displayed value | Returns the specified object |
| Used for displaying information | Used for calculations and reusable results |
| Does not end the function by itself | Ends current function execution |

### 4.3 Returning Multiple Values
Python packs multiple comma-separated return values into a tuple.

```python
def calculate(a, b):
    return a + b, a - b, a * b

result = calculate(20, 10)
print(result)  # (30, 10, 200)
```

### 4.4 Unpacking Multiple Return Values
```python
add, sub, mul = calculate(20, 10)
print("Addition:", add)        # 30
print("Subtraction:", sub)     # 10
print("Multiplication:", mul)  # 200
```

### 4.5 Returning Different Data Structures
Functions can return lists, tuples, dictionaries, sets, or custom objects:
```python
def get_student():
    return {"name": "Rahul", "age": 21, "marks": 90}
```

### 4.6 Returning Early from a Function
```python
def check_number(number):
    if number < 0:
        return "Negative number"
    return "Positive number or zero"
```

---

## 5. Variable Scope

### 5.1 What is Variable Scope?
Variable scope defines where a variable can be accessed in a Python program. Python resolves unqualified names using the **LEGB rule**:

1. **L – Local:** Inside the current function.
2. **E – Enclosing:** Inside an outer enclosing function.
3. **G – Global:** At the module level.
4. **B – Built-in:** Python-provided names such as `len()`, `print()`.

### 5.2 Local Variables
Created inside a function and accessible only within that function. Trying to access a local variable outside raises a `NameError`.

### 5.3 Global Variables
Defined outside all functions at the module level and readable inside functions.

```python
name = "Rahul"

def greet():
    print("Hello", name)

greet()  # Hello Rahul
```

### 5.4 Modifying Global Variables
To reassign a global variable inside a function, use the `global` keyword:

```python
count = 10

def update():
    global count
    count = 20

update()
print(count)  # 20
```

### 5.5 Enclosing Scope & 5.6 The `nonlocal` Keyword
An enclosing variable belongs to an outer function containing a nested function. Use `nonlocal` inside the inner function to modify it:

```python
def outer():
    count = 10

    def inner():
        nonlocal count
        count = 20

    inner()
    print(count)  # 20

outer()
```

### 5.7 Built-in Scope
Built-in names (`print`, `len`, `max`, `sum`) are available throughout the program.

#### `global` vs. `nonlocal`

| `global` | `nonlocal` |
| :--- | :--- |
| Refers to a module-level variable | Refers to an enclosing function variable |
| Used in nested and normal functions | Used only in nested functions |
| Reassigns global name | Reassigns nearest enclosing binding |
| Cannot refer to an outer function's local variable | Cannot refer to a global variable |

---

## 6. `*args` and `**kwargs`

### 6.1 What is `*args`?
`*args` allows a function to accept any number of positional arguments, collecting them into a **tuple**.

```python
def add(*args):
    return sum(args)

print(add(10, 20))          # 30
print(add(10, 20, 30, 40))  # 100
```
*(Note: The `*` enables variable collection; `args` is just a convention.)*

### 6.2 Practical Example: Finding the Average
```python
def average(*args):
    if not args:
        return 0
    return sum(args) / len(args)
```

### 6.3 What is `**kwargs`?
`**kwargs` allows a function to accept any number of keyword arguments, collecting them into a **dictionary**.

```python
def student(**kwargs):
    for key, value in kwargs.items():
        print(f"{key} : {value}")

student(name="Rahul", age=21, course="Python", marks=90)
```

### 6.4 Practical Example: Employee Information
```python
def employee(**details):
    print("Employee Details")
    for key, value in details.items():
        print(f"{key} : {value}")
```

### 6.5 Using `*args` and `**kwargs` Together & 6.6 Combining Regular Parameters
```python
def student(name, *marks, **details):
    print("Name:", name)
    print("Marks:", marks)
    print("Other Details:", details)

student("Rahul", 85, 90, 95, age=21, course="M.Tech")
```

### 6.7 Argument Unpacking
Use `*` to unpack lists/tuples and `**` to unpack dictionaries during function calls:

```python
def add(a, b, c):
    return a + b + c

numbers = [10, 20, 30]
print(add(*numbers))  # 60

def student(name, age):
    print(name, age)

details = {"name": "Rahul", "age": 21}
student(**details)    # Rahul 21
```

#### `*args` vs. `**kwargs`

| Feature | `*args` | `**kwargs` |
| :--- | :--- | :--- |
| **Accepts** | Positional arguments | Keyword arguments |
| **Stores values in** | Tuple | Dictionary |
| **Example** | `10, 20, 30` | `name="Rahul"` |
| **Symbol** | `*` | `**` |

**Standard parameter ordering:** `def example(a, b=10, *args, **kwargs):`

---

## 7. Function Documentation and Type Hints

### 7.1 What is a Docstring?
A docstring is a documentation string written inside triple quotes at the start of a function, class, or module. It is accessible via `function.__doc__` or `help(function)`.

```python
def add(a, b):
    """
    This function adds two numbers.

    Parameters:
        a: First number
        b: Second number

    Returns:
        Sum of the two numbers.
    """
    return a + b
```

### 7.2 What are Type Hints?
Type hints specify the expected data types of parameters and return values.

```python
def add(a: int, b: int) -> int:
    return a + b
```
> **Important:** Python does not enforce ordinary type hints at runtime. They are used by IDEs, static type checkers (like `mypy`), and documentation tools.

### 7.3 & 7.4 Type Hints with Collections and Unions
```python
def get_numbers() -> list[int]:
    return [10, 20, 30]

def get_student() -> dict[str, int]:
    return {"Rahul": 85, "Priya": 95}

def find_student(student_id: int) -> str | None:
    return "Rahul" if student_id == 101 else None
```

### 7.6 Docstrings vs. Type Hints (Best Practice: Use Both)
```python
def calculate_area(radius: float) -> float:
    """
    Calculate the area of a circle.

    Args:
        radius: Radius of the circle.

    Returns:
        Area of the circle.
    """
    return 3.14159 * radius ** 2
```

---

## 8. Lambda Functions

### 8.1 What is a Lambda Function?
A lambda function is a small anonymous function defined using the `lambda` keyword for short, single-expression operations.

```python
# Normal function
def square(number):
    return number ** 2

# Equivalent lambda function
square = lambda number: number ** 2
print(square(5))  # 25
```

### 8.2 Lambda Syntax
```python
lambda arguments: expression
```
A lambda expression can contain conditional expressions and function calls, but cannot contain statements like `return`, `for`, or `while`.

### 8.3–8.8 Practical Lambda Examples
```python
# Multiple arguments
add = lambda a, b: a + b

# Conditional expression
check = lambda number: "Even" if number % 2 == 0 else "Odd"

# No arguments
greet = lambda: "Hello Python"

# Sorting strings by length
names = ["Python", "Java", "C", "JavaScript"]
print(sorted(names, key=lambda name: len(name)))  # ['C', 'Java', 'Python', 'JavaScript']

# Sorting dictionaries
students = [
    {"name": "Rahul", "marks": 85},
    {"name": "Priya", "marks": 95},
    {"name": "Arjun", "marks": 75}
]
result = sorted(students, key=lambda s: s["marks"], reverse=True)
```

### 8.9 Normal Function vs. Lambda Function

| Normal Function | Lambda Function |
| :--- | :--- |
| Uses `def` | Uses `lambda` |
| Can contain multiple statements | Contains a single expression |
| Named definition | Usually anonymous |
| Supports docstrings | No normal docstring syntax |
| Suitable for complex logic | Suitable for short inline operations |

---

## 9. `map()`, `filter()` and `sorted(key=...)`

### 9.1 What is `map()`?
`map(function, iterable)` applies a function to every item of an iterable and returns a map iterator.

```python
numbers = [1, 2, 3, 4, 5]
squares = list(map(lambda n: n ** 2, numbers))
print(squares)  # [1, 4, 9, 16, 25]

# Multiple iterables
a = [10, 20, 30]
b = [1, 2, 3]
print(list(map(lambda x, y: x + y, a, b)))  # [11, 22, 33]
```

### 9.2 What is `filter()`?
`filter(function, iterable)` selects elements for which the function evaluates to `True` and returns a filter iterator.

```python
numbers = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda n: n % 2 == 0, numbers))
print(evens)  # [2, 4, 6]
```

### 9.3 What is `sorted(key=...)`?
`sorted(iterable, key=None, reverse=False)` returns a new sorted list.

```python
# Sort by multiple criteria: marks descending, then name ascending
students = [
    {"name": "Rahul", "marks": 85},
    {"name": "Priya", "marks": 95},
    {"name": "Arjun", "marks": 85},
    {"name": "Sneha", "marks": 95}
]

result = sorted(students, key=lambda s: (-s["marks"], s["name"]))
```

### 9.4 `map()` vs. `filter()` vs. `sorted()`

| Feature | `map()` | `filter()` | `sorted()` |
| :--- | :--- | :--- | :--- |
| **Purpose** | Transform elements | Select elements | Arrange elements |
| **Function** | Transformation function | Condition function | Sorting key function |
| **Output** | Map iterator | Filter iterator | New list |
| **Mutates original?** | No | No | No |

### Combined Practical Example
```python
marks = [35, 85, 40, 90, 25, 75, 60]

passed = filter(lambda mark: mark >= 40, marks)
updated = map(lambda mark: mark + 5, passed)
result = sorted(updated, reverse=True)

print(result)  # [95, 90, 80, 65, 45]
```
> **Note:** `map()` and `filter()` return iterators that exhaust after one pass. Convert them with `list()` if you need to reuse the data.

---

## 10. Creating and Importing Modules

### 10.1 What is a Module?
A module is a `.py` file containing reusable variables, functions, classes, and statements that helps organize large projects into logical files.

### 10.2 Creating & 10.3 Importing a Module

**`calculator.py`:**
```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
```

**`main.py`:**
```python
import calculator

print(calculator.add(10, 20))       # 30
print(calculator.subtract(20, 10))  # 10
```

---

## 11. `import` and `from ... import`

* **Import whole module:** `import math` $\rightarrow$ `math.sqrt(25)`
* **Import specific names:** `from math import sqrt, pi` $\rightarrow$ `sqrt(25)`
* **Module/Function aliases:** `import math as m` or `from math import factorial as fact`
* **Wildcard import (`from math import *`):** Generally discouraged in large projects because it pollutes the namespace and obscures where names originate.

### Commonly Used Python Standard Library Modules

| Module | Purpose | Example |
| :--- | :--- | :--- |
| `math` | Mathematical operations | `math.sqrt(25)` |
| `random` | Random number generation | `random.randint(1, 10)` |
| `datetime` | Date and time handling | `datetime.date.today()` |
| `os` | Operating system operations | `os.getcwd()` |
| `sys` | Python runtime information | `sys.version` |
| `json` | JSON processing | `json.dumps()` |
| `re` | Regular expressions | `re.search()` |
| `statistics` | Statistical calculations | `statistics.mean()` |
| `collections` | Specialized data structures | `Counter()` |
| `pathlib` | File system paths | `Path()` |

---

## 12. `__name__` and `if __name__ == '__main__'`

### 12.1–12.3 How `__name__` Works
`__name__` is a special built-in variable in every Python module:
* When a file is **executed directly**, `__name__` is set to `"__main__"`.
* When a file is **imported as a module**, `__name__` is set to the module's filename (e.g., `"calculator"`).

### 12.4–12.7 Using `if __name__ == "__main__":`
This guard ensures that script-level or test code runs only when the file is executed directly, not when imported elsewhere:

```python
def add(a, b):
    return a + b

if __name__ == "__main__":
    print("Running directly:", add(10, 20))
```

---

## 13. Advanced Concepts Related to Functions

### 13.1–13.3 First-Class Functions
Functions in Python are first-class objects: they can be assigned to variables, stored in data structures, passed as arguments, and returned from other functions.

### 13.4 Closures
A closure is an inner function that remembers and accesses variables from its enclosing scope even after the outer function has finished executing.

```python
def multiplier(factor):
    def multiply(number):
        return number * factor
    return multiply

double = multiplier(2)
triple = multiplier(3)

print(double(10))  # 20
print(triple(10))  # 30
```

### 13.5 Recursion
Recursion occurs when a function calls itself until reaching a base case.
Mathematical definition: $n! = n \times (n-1)!$, with base case $0! = 1$.

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # 120
```

### 13.6 Positional-Only and Keyword-Only Arguments
* **Positional-only (`/`):** Parameters before `/` cannot be passed as keyword arguments (`def add(a, b, /):`).
* **Keyword-only (`*`):** Parameters after `*` must be passed as keyword arguments (`def student(name, *, age):`).

---

## 14. Complete Practical Program – Student Management System

```python
def calculate_average(*marks: int) -> float:
    """Calculate the average of the given marks."""
    if not marks:
        return 0.0
    return sum(marks) / len(marks)


def add_student(students: list[dict], name: str, *marks: int) -> None:
    """Add a student and their marks to the collection."""
    average = calculate_average(*marks)
    student = {
        "name": name,
        "marks": list(marks),
        "average": average
    }
    students.append(student)


def display_students(students: list[dict]) -> None:
    """Display all student details."""
    for student in students:
        print(f"Name: {student['name']}")
        print(f"Marks: {student['marks']}")
        print(f"Average: {student['average']}\n")


def sort_students(students: list[dict]) -> list[dict]:
    """Sort students by average marks in descending order."""
    return sorted(
        students,
        key=lambda student: student["average"],
        reverse=True
    )


if __name__ == "__main__":
    students = []

    add_student(students, "Rahul", 85, 90, 88)
    add_student(students, "Priya", 95, 92, 98)
    add_student(students, "Arjun", 70, 75, 80)

    print("Student Details:")
    display_students(students)

    print("Students Sorted by Average:")
    sorted_students = sort_students(students)
    display_students(sorted_students)
```

---

## 15. Important Interview Questions

### Basic Function Questions
* What is a function in Python, and why do we use functions?
* How do you define and call a function?
* What is the difference between built-in and user-defined functions?
* What is the difference between parameters and arguments?
* Can a function return multiple values?

### Arguments and Return Questions
* Explain positional, keyword, and default arguments.
* What is the mutable default argument problem, and how do you fix it?
* What is the difference between `print()` and `return`?
* What happens when a function does not have a `return` statement?

### Scope Questions
* Explain the LEGB scope resolution rule.
* What is the difference between `global` and `nonlocal`?

### Advanced & Functional Programming Questions
* What is the difference between `*args` and `**kwargs`?
* How do you unpack lists and dictionaries into function arguments?
* Are Python type hints enforced at runtime?
* What is the difference between a lambda function and a normal function?
* What are first-class functions, closures, and recursion?
* What is the difference between `map()`, `filter()`, and `sorted(key=...)`?
* Why do `map()` and `filter()` return iterators?

### Module Questions
* What is the difference between `import module` and `from module import item`?
* What is `__name__`, and why is `if __name__ == "__main__":` important?

---

## 16. Practice Coding Exercises

- [ ] **1.** Create a function that accepts two numbers and returns their sum, difference, product, and division.
- [ ] **2.** Write a function that checks whether a given number is prime.
- [ ] **3.** Create a function that accepts any number of integers using `*args` and returns the largest number.
- [ ] **4.** Write a function using `**kwargs` to display employee information.
- [ ] **5.** Create a function that uses a global variable and modifies its value.
- [ ] **6.** Write a lambda function to find the cube of a number.
- [ ] **7.** Use `map()` to convert a list of temperatures from Celsius to Fahrenheit.
- [ ] **8.** Use `filter()` to extract numbers divisible by both 3 and 5.
- [ ] **9.** Sort a list of dictionaries containing employee names and salaries by salary.
- [ ] **10.** Create a module containing arithmetic functions and import it into another Python file.
- [ ] **11.** Write a Python file that prints a message only when executed directly.
- [ ] **12.** Create a closure that remembers a number and adds it to any supplied value.

---

## 17. Final Revision – Quick Reference

| Concept | Important Syntax |
| :--- | :--- |
| Define function | `def greet():` |
| Call function | `greet()` |
| Parameter | `def add(a, b):` |
| Positional arguments | `add(10, 20)` |
| Keyword arguments | `add(a=10, b=20)` |
| Default arguments | `def greet(name="Student"):` |
| Return statement | `return result` |
| Multiple returns | `return a, b, c` |
| Global / Nonlocal | `global count` / `nonlocal count` |
| Variable arguments | `*args` / `**kwargs` |
| Docstring | `"""Function description"""` |
| Type hints | `def add(a: int) -> int:` |
| Lambda | `lambda x: x * 2` |
| Map / Filter | `map(fn, iter)` / `filter(fn, iter)` |
| Sorting | `sorted(data, key=...)` |
| Import module | `import math` / `from math import sqrt` |
| Main guard | `if __name__ == "__main__":` |

### Recommended Teaching and Learning Sequence
1. **Function fundamentals:** Definition, calls, parameters, arguments, and return values.
2. **Argument handling:** Positional, keyword, default arguments, `*args`, and `**kwargs`.
3. **Scope and documentation:** Local, global, enclosing scopes (LEGB), docstrings, and type hints.
4. **Functional programming:** Lambda functions, `map()`, `filter()`, and sorting with custom keys.
5. **Modules:** Creating `.py` files, importing modules, aliases, and `if __name__ == "__main__":`.
6. **Hands-on implementation:** Build a calculator, student management system, and employee management program.

> **Recommendation:** Spend extra practice time on `return` vs. `print()`, mutable default arguments, LEGB scope, `*args` and `**kwargs`, closures, `map()` vs. `filter()`, and `if __name__ == "__main__":`.