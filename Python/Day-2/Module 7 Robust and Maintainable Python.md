# Python Advanced Concepts: Iterators, Generators, Closures, Decorators, Exception Handling and Debugging

## Study Notes

These notes explain Python iteration, generators, nested functions,
closures, decorators, exception handling, logging, tracebacks, and
debugging. They include definitions, syntax, examples, explanations,
comparisons, practical applications, interview questions, and coding
exercises.

## Contents

1.  [Iterables and Iterators](#1-iterables-and-iterators)
2.  [iter(), next() and StopIteration](#2-iter-next-and-stopiteration)
3.  [Generator Functions and yield](#3-generator-functions-and-yield)
4.  [Generator Expressions](#4-generator-expressions)
5.  [Nested Functions and Closures](#5-nested-functions-and-closures)
6.  [Decorators](#6-decorators)
7.  [Exception Handling](#7-exception-handling)
8.  [try, except, else and finally](#8-try-except-else-and-finally)
9.  [Raising and Creating Custom
    Exceptions](#9-raising-and-creating-custom-exceptions)
10. [Assertions](#10-assertions)
11. [Logging and Log Levels](#11-logging-and-log-levels)
12. [Reading Tracebacks and
    Debugging](#12-reading-tracebacks-and-debugging)
13. [Debugger and Breakpoints](#13-debugger-and-breakpoints)
14. [Complete Practical Example](#14-complete-practical-example)
15. [Important Differences for
    Interviews](#15-important-differences-for-interviews)
16. [Interview Questions and
    Answers](#16-interview-questions-and-answers)
17. [Practical Coding Exercises](#17-practical-coding-exercises)
18. [Recommended Learning Order](#18-recommended-learning-order)

------------------------------------------------------------------------

# 1. Iterables and Iterators

## 1.1 What is an Iterable?

An **iterable** is an object that contains a collection of elements and
allows us to access its elements one at a time.

In simple words, an iterable is any Python object that we can loop
through using a `for` loop.

### Examples of iterables

-   Lists
-   Tuples
-   Strings
-   Dictionaries
-   Sets
-   Files
-   Ranges

### Example 1: List as an iterable

``` python
numbers = [10, 20, 30, 40, 50]

for number in numbers:
    print(number)
```

Output:

``` text
10
20
30
40
50
```

Here:

-   `numbers` is an iterable.
-   The `for` loop accesses each element.
-   Python internally uses an iterator to retrieve elements.

### Example 2: String as an iterable

``` python
name = "Python"

for character in name:
    print(character)
```

Output:

``` text
P
y
t
h
o
n
```

Each character is retrieved individually.

### Example 3: Dictionary as an iterable

``` python
student = {
    "name": "Rahul",
    "age": 22,
    "course": "Python"
}

for key in student:
    print(key)
```

Output:

``` text
name
age
course
```

By default, iterating over a dictionary returns its keys.

To access both keys and values:

``` python
for key, value in student.items():
    print(key, value)
```

Output:

``` text
name Rahul
age 22
course Python
```

## 1.2 What is an Iterator?

An **iterator** is an object that represents a stream of data and
returns one element at a time.

An iterator remembers its current position while iterating.

Unlike a normal list, an iterator does not necessarily store all
elements in memory.

An iterator implements two special methods:

1.  `__iter__()`
2.  `__next__()`

### Example

``` python
numbers = [10, 20, 30, 40]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
print(next(iterator))
```

Output:

``` text
10
20
30
40
```

Explanation:

-   `iter(numbers)` creates an iterator from the list.
-   `next(iterator)` retrieves the next element.
-   Every call moves the iterator forward.
-   The iterator remembers its current position.

## 1.3 Iterable vs Iterator

  -----------------------------------------------------------------------
  Feature                 Iterable                Iterator
  ----------------------- ----------------------- -----------------------
  Meaning                 Object that can be      Object that produces
                          iterated over           elements one at a time

  Methods                 Usually implements      Implements `__iter__()`
                          `__iter__()`            and `__next__()`

  Position tracking       Usually does not track  Tracks current position
                          iteration position      

  Reusability             Can generally create    Usually consumed as
                          multiple independent    elements are retrieved
                          iterators               

  Examples                List, tuple, string,    List iterator,
                          set                     generator
  -----------------------------------------------------------------------

### Example demonstrating the difference

``` python
numbers = [10, 20, 30]

# Creating an iterator
iterator = iter(numbers)

print(next(iterator))
print(next(iterator))

# Creating another iterator
iterator2 = iter(numbers)

print(next(iterator2))
```

Output:

``` text
10
20
10
```

Why?

The list is reusable. Every call to `iter(numbers)` creates a new
iterator starting from the beginning.

However, the original iterator continues from its previous position.

## 1.4 Creating a Custom Iterator

Python allows us to create our own iterator using classes.

A custom iterator must implement:

-   `__iter__()`: Returns the iterator object.
-   `__next__()`: Returns the next value or raises `StopIteration`.

### Example: Custom number iterator

``` python
class NumberIterator:

    def __init__(self, limit):
        self.limit = limit
        self.current = 1

    def __iter__(self):
        return self

    def __next__(self):

        if self.current <= self.limit:
            result = self.current
            self.current += 1
            return result

        else:
            raise StopIteration


numbers = NumberIterator(5)

for number in numbers:
    print(number)
```

Output:

``` text
1
2
3
4
5
```

Explanation:

1.  The constructor initializes the limit and current value.
2.  `__iter__()` returns the iterator itself.
3.  `__next__()` checks whether more values are available.
4.  If a value is available, it returns it and increments the counter.
5.  Otherwise, it raises `StopIteration`.

### Real-world applications

-   Reading large files line by line.
-   Processing large datasets.
-   Handling database records.
-   Streaming API responses.
-   Processing data without loading everything into memory.

------------------------------------------------------------------------

# 2. iter(), next() and StopIteration

These three concepts form the foundation of Python iteration.

## 2.1 iter()

The `iter()` function converts an iterable into an iterator.

### Syntax

``` python
iterator = iter(iterable)
```

### Example

``` python
fruits = ["Apple", "Banana", "Mango"]

fruit_iterator = iter(fruits)

print(type(fruit_iterator))
```

Output:

``` text
<class 'list_iterator'>
```

Here, `iter()` creates a list iterator.

### Another example

``` python
name = "Python"

iterator = iter(name)

print(next(iterator))
print(next(iterator))
```

Output:

``` text
P
y
```

## 2.2 next()

The `next()` function retrieves the next available element from an
iterator.

### Syntax

``` python
next(iterator)
```

### Example

``` python
numbers = [100, 200, 300]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

Output:

``` text
100
200
300
```

Every call to `next()` moves the iterator forward by one position.

### Using next() with a default value

We can provide a default value to avoid an exception when the iterator
is exhausted.

Syntax:

``` python
next(iterator, default_value)
```

Example:

``` python
numbers = [10, 20]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator, "No more elements"))
```

Output:

``` text
10
20
No more elements
```

The default value is returned instead of raising `StopIteration`.

## 2.3 StopIteration

`StopIteration` is a built-in Python exception that indicates that an
iterator has no more elements to return.

### Example

``` python
numbers = [10, 20]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

Output:

``` text
10
20

StopIteration
```

The third `next()` call raises `StopIteration` because the iterator is
exhausted.

### Handling StopIteration

``` python
numbers = [10, 20, 30]

iterator = iter(numbers)

while True:

    try:
        value = next(iterator)
        print(value)

    except StopIteration:
        break
```

Output:

``` text
10
20
30
```

The loop stops when the iterator raises `StopIteration`.

### How does a for loop use iterators internally?

Consider:

``` python
numbers = [10, 20, 30]

for number in numbers:
    print(number)
```

Python internally performs an operation similar to:

``` python
numbers = [10, 20, 30]

iterator = iter(numbers)

while True:

    try:
        number = next(iterator)
        print(number)

    except StopIteration:
        break
```

This is a simplified conceptual equivalent of how iteration works.

**Important:** A `for` loop automatically handles `StopIteration`, so we
generally do not need to handle it manually.

### Difference between iter() and next()

  Function          Purpose
  ----------------- -----------------------------------------------
  `iter()`          Creates an iterator from an iterable
  `next()`          Retrieves the next element from an iterator
  `StopIteration`   Indicates that no more elements are available

------------------------------------------------------------------------

# 3. Generator Functions and yield

## 3.1 What is a Generator?

A **generator** is a special type of iterator that produces values one
at a time instead of storing all values in memory.

Generators are particularly useful when working with large amounts of
data.

Python provides generators through:

1.  Generator functions using `yield`.
2.  Generator expressions.

## 3.2 What is a Generator Function?

A generator function is a function that contains the `yield` keyword.

Unlike a normal function, which generally returns a result and
terminates, a generator function can pause its execution and resume from
where it stopped.

### Normal function example

``` python
def numbers():
    return 10
    return 20
    return 30


print(numbers())
```

Output:

``` text
10
```

The first `return` terminates the function. The remaining statements are
not executed.

### Generator function example

``` python
def numbers():
    yield 10
    yield 20
    yield 30


for number in numbers():
    print(number)
```

Output:

``` text
10
20
30
```

Unlike `return`, `yield` pauses execution and preserves the function's
state.

## 3.3 Understanding yield

The `yield` keyword is used to produce a value from a generator
function.

When Python encounters `yield`:

1.  It returns the current value.
2.  It pauses the function.
3.  It remembers local variables and the execution position.
4.  When requested again, execution resumes from the next statement.

### Example

``` python
def student_names():

    print("Starting generator")

    yield "Rahul"

    print("Resuming generator")

    yield "Priya"

    print("Generator completed")


generator = student_names()

print(next(generator))
print(next(generator))
```

Output:

``` text
Starting generator
Rahul
Resuming generator
Priya
```

Let's understand the execution:

-   Calling `student_names()` creates a generator object. The function
    body has not yet started executing.
-   The first `next()` starts execution and reaches `yield "Rahul"`.
-   The function pauses.
-   The second `next()` resumes execution and reaches `yield "Priya"`.
-   The function pauses again.

If we call `next()` one more time, the function prints
`Generator completed` and raises `StopIteration`.

## 3.4 Difference between return and yield

  -----------------------------------------------------------------------
  Feature                 return                  yield
  ----------------------- ----------------------- -----------------------
  Purpose                 Returns a final result  Produces a value

  Execution               Terminates the function Pauses the function

  State                   Does not preserve       Preserves execution
                          resumable execution     state
                          state                   

  Multiple values         Normally returns one    Can produce multiple
                          result                  values

  Memory                  May require building a  Supports lazy value
                          complete result         generation
  -----------------------------------------------------------------------

## 3.5 Generator Example: Generate numbers

``` python
def generate_numbers(limit):

    number = 1

    while number <= limit:

        yield number

        number += 1


for value in generate_numbers(5):
    print(value)
```

Output:

``` text
1
2
3
4
5
```

This generator produces numbers one at a time.

## 3.6 Generator Example: Fibonacci Series

The Fibonacci series is a sequence in which each number is the sum of
the previous two numbers.

Example:

``` text
0, 1, 1, 2, 3, 5, 8, 13
```

Implementation:

``` python
def fibonacci(limit):

    a, b = 0, 1

    for _ in range(limit):

        yield a

        a, b = b, a + b


for number in fibonacci(8):
    print(number)
```

Output:

``` text
0
1
1
2
3
5
8
13
```

This generator produces Fibonacci numbers without creating a complete
list.

## 3.7 Generator with Large Data

Suppose we need to generate one million numbers.

### Using a list

``` python
numbers = [x for x in range(1000000)]

print(numbers[0])
```

This creates and stores all one million numbers in memory.

### Using a generator

``` python
numbers = (x for x in range(1000000))

print(next(numbers))
print(next(numbers))
```

Output:

``` text
0
1
```

The generator calculates values as needed.

This is called **lazy evaluation**.

## 3.8 Generator Applications

Generators are useful for:

-   Processing large CSV files.
-   Reading huge log files.
-   Streaming data from APIs.
-   Processing database records.
-   Generating infinite sequences.
-   Memory-efficient data pipelines.
-   Machine learning data preprocessing.

------------------------------------------------------------------------

# 4. Generator Expressions

## 4.1 What is a Generator Expression?

A generator expression is a compact way of creating a generator without
defining a separate generator function.

It has a syntax similar to list comprehension but uses parentheses
instead of square brackets.

### Syntax

``` python
generator = (expression for item in iterable)
```

### Example

``` python
numbers = (x for x in range(5))

for number in numbers:
    print(number)
```

Output:

``` text
0
1
2
3
4
```

## 4.2 List Comprehension vs Generator Expression

### List comprehension

``` python
numbers = [x * x for x in range(5)]

print(numbers)
```

Output:

``` text
[0, 1, 4, 9, 16]
```

All values are calculated and stored in a list.

### Generator expression

``` python
numbers = (x * x for x in range(5))

print(numbers)
```

Output is similar to:

``` text
<generator object <genexpr> at ...>
```

The generator object produces values only when requested.

### Comparison

  -----------------------------------------------------------------------
  Feature                 List Comprehension      Generator Expression
  ----------------------- ----------------------- -----------------------
  Syntax                  `[]`                    `()`

  Execution               Eager                   Lazy

  Memory                  Stores all results      Produces values as
                                                  needed

  Reusability             Can iterate multiple    Usually consumed once
                          times                   

  Speed                   Often faster for        Avoids unnecessary
                          repeated access         computation

  Best for                Small collections       Large or streaming data
  -----------------------------------------------------------------------

## 4.3 Generator Expression with Conditions

Example: Generate even numbers.

``` python
even_numbers = (x for x in range(20) if x % 2 == 0)

for number in even_numbers:
    print(number)
```

Output:

``` text
0
2
4
6
8
10
12
14
16
18
```

## 4.4 Generator Expression with sum()

Generator expressions work well with built-in functions.

Example:

``` python
total = sum(x for x in range(1, 101))

print(total)
```

Output:

``` text
5050
```

This calculates the sum without creating a separate list of 100
elements.

Other useful functions include:

``` python
numbers = (x for x in range(10))

print(max(numbers))
```

Output:

``` text
9
```

Other functions:

-   `sum()`
-   `min()`
-   `max()`
-   `any()`
-   `all()`

Remember that these functions consume the generator.

## 4.5 Generator Function vs Generator Expression

  -----------------------------------------------------------------------
  Feature                 Generator Function      Generator Expression
  ----------------------- ----------------------- -----------------------
  Creation                Uses `def` and `yield`  Uses parentheses

  Complexity              Suitable for complex    Suitable for simple
                          logic                   logic

  Multiple statements     Supported               Not supported as a
                                                  sequence of statements

  Readability             Better for complex      Better for simple
                          operations              transformations
  -----------------------------------------------------------------------

Example:

Generator function:

``` python
def squares(limit):
    for x in range(limit):
        yield x * x
```

Generator expression:

``` python
squares = (x * x for x in range(10))
```

------------------------------------------------------------------------

# 5. Nested Functions and Closures

## 5.1 What is a Nested Function?

A nested function is a function defined inside another function.

In Python, we can define functions inside other functions using the
`def` keyword.

### Syntax

``` python
def outer_function():

    def inner_function():
        print("Inside inner function")

    inner_function()


outer_function()
```

Output:

``` text
Inside inner function
```

Here:

-   `outer_function()` is the outer function.
-   `inner_function()` is the nested or inner function.
-   The inner function is called from the outer function.

## 5.2 Why do we use Nested Functions?

Nested functions are useful when:

-   A function is needed only inside another function.
-   We want to organize complex logic.
-   We want to hide implementation details.
-   We want to implement closures.
-   We want to implement decorators.

### Example: Calculation

``` python
def calculate():

    def add(a, b):
        return a + b

    def multiply(a, b):
        return a * b

    print("Addition:", add(10, 20))
    print("Multiplication:", multiply(10, 20))


calculate()
```

Output:

``` text
Addition: 30
Multiplication: 200
```

The inner functions are available within `calculate()` but are not
directly available in the global scope.

## 5.3 Returning a Nested Function

An outer function can return an inner function.

Example:

``` python
def outer_function():

    def inner_function():
        print("Hello from inner function")

    return inner_function


result = outer_function()

result()
```

Output:

``` text
Hello from inner function
```

Notice that we are returning the function itself, not calling it.

-   `return inner_function` returns a function object.
-   `return inner_function()` calls the function and returns its result.

This concept is important for understanding closures and decorators.

## 5.4 What is a Closure?

A **closure** is a nested function that remembers and accesses variables
from its enclosing function even after the outer function has finished
executing.

In simple words, a closure allows an inner function to remember
information from the outer function.

### Example

``` python
def outer_function():

    message = "Hello Python"

    def inner_function():
        print(message)

    return inner_function


my_function = outer_function()

my_function()
```

Output:

``` text
Hello Python
```

Let's understand what happens:

1.  `outer_function()` is called.
2.  The variable `message` is created.
3.  `inner_function()` is defined.
4.  The outer function returns the inner function.
5.  The outer function finishes execution.
6.  We call `my_function()`.
7.  The inner function still remembers the value of `message`.

This behavior is called a closure.

## 5.5 Closure with Parameters

Closures become more useful when the outer function accepts parameters.

Example:

``` python
def multiplier(factor):

    def multiply(number):
        return number * factor

    return multiply


double = multiplier(2)

triple = multiplier(3)

print(double(10))
print(triple(10))
```

Output:

``` text
20
30
```

Explanation:

-   `multiplier(2)` creates a function that remembers `factor = 2`.
-   `multiplier(3)` creates another function that remembers
    `factor = 3`.
-   Both functions maintain their own enclosing values.

## 5.6 Using nonlocal in Closures

Sometimes we want to modify a variable defined in an enclosing function.

For this, Python provides the `nonlocal` keyword.

Example:

``` python
def counter():

    count = 0

    def increment():

        nonlocal count

        count += 1

        return count

    return increment


my_counter = counter()

print(my_counter())
print(my_counter())
print(my_counter())
```

Output:

``` text
1
2
3
```

Explanation:

-   `count` belongs to the outer function.
-   `nonlocal count` allows the inner function to modify it.
-   Every call to `increment()` increases the same variable.

Without `nonlocal`, assigning to `count` inside the inner function would
create a local variable and cause an error when trying to read it before
assignment.

## 5.7 Applications of Closures

Closures are used in:

-   Data hiding and encapsulation.
-   Creating function factories.
-   Maintaining state without using classes.
-   Decorators.
-   Callback functions.
-   Configuration-based functions.

### Important Difference: local, global and nonlocal

  Keyword      Meaning
  ------------ -----------------------------------------------------
  `local`      Variable defined inside the current function
  `global`     Refers to a variable in the module-level scope
  `nonlocal`   Refers to a variable in an enclosing function scope

------------------------------------------------------------------------

# 6. Decorators

## 6.1 What is a Decorator?

A decorator is a function that modifies or extends the behavior of
another function without changing its original source code.

Decorators are widely used in Python frameworks and applications.

Examples include:

-   Authentication.
-   Logging.
-   Execution-time measurement.
-   Access control.
-   Caching.
-   Input validation.

## 6.2 Understanding Functions as First-Class Objects

Python treats functions as first-class objects.

This means we can:

1.  Store functions in variables.
2.  Pass functions as arguments.
3.  Return functions from other functions.
4.  Define functions inside other functions.

Example:

``` python
def greet():
    print("Hello")


message = greet

message()
```

Output:

``` text
Hello
```

Here, `message` refers to the same function as `greet`.

## 6.3 Creating a Simple Decorator

Let's create a decorator that prints a message before and after
executing a function.

``` python
def my_decorator(func):

    def wrapper():

        print("Before function execution")

        func()

        print("After function execution")

    return wrapper


@my_decorator
def greet():
    print("Hello Python")


greet()
```

Output:

``` text
Before function execution
Hello Python
After function execution
```

### Understanding the execution

The decorator syntax:

``` python
@my_decorator
def greet():
    print("Hello Python")
```

Is equivalent to:

``` python
def greet():
    print("Hello Python")


greet = my_decorator(greet)
```

Explanation:

1.  The original `greet()` function is passed to `my_decorator()`.
2.  The decorator creates a `wrapper()` function.
3.  The wrapper calls the original function.
4.  The decorator returns the wrapper.
5.  Calling `greet()` now executes the wrapper.

## 6.4 Decorators with Function Arguments

The previous decorator works only with functions that accept no
arguments.

To support functions with different arguments, we use `*args` and
`**kwargs`.

Example:

``` python
def my_decorator(func):

    def wrapper(*args, **kwargs):

        print("Function is starting")

        result = func(*args, **kwargs)

        print("Function is completed")

        return result

    return wrapper


@my_decorator
def add(a, b):
    return a + b


print(add(10, 20))
```

Output:

``` text
Function is starting
Function is completed
30
```

Here:

-   `*args` accepts positional arguments.
-   `**kwargs` accepts keyword arguments.
-   `result` stores the original function's return value.
-   `return result` ensures that the decorated function preserves its
    result.

## 6.5 Decorator for Execution Time

One practical application is measuring how long a function takes to
execute.

``` python
import time


def calculate_time(func):

    def wrapper(*args, **kwargs):

        start = time.time()

        result = func(*args, **kwargs)

        end = time.time()

        print("Execution time:", end - start, "seconds")

        return result

    return wrapper


@calculate_time
def calculation():

    total = 0

    for i in range(1000000):
        total += i

    return total


print(calculation())
```

Output will contain:

``` text
Execution time: ... seconds
499999500000
```

The exact execution time depends on the computer.

## 6.6 Decorator with Parameters

Sometimes we want to pass arguments to the decorator itself.

This requires an additional function level.

Example:

``` python
def repeat(times):

    def decorator(func):

        def wrapper(*args, **kwargs):

            for _ in range(times):
                func(*args, **kwargs)

        return wrapper

    return decorator


@repeat(3)
def greet():
    print("Hello!")


greet()
```

Output:

``` text
Hello!
Hello!
Hello!
```

Understanding the structure:

-   `repeat(3)` receives the decorator configuration.
-   `decorator(func)` receives the function.
-   `wrapper()` executes the function three times.

## 6.7 functools.wraps

One issue with decorators is that they can replace the original
function's metadata.

For example:

``` python
def my_decorator(func):

    def wrapper():
        print("Executing function")
        func()

    return wrapper


@my_decorator
def greet():
    """This function greets the user."""
    print("Hello")


print(greet.__name__)
```

Output:

``` text
wrapper
```

The decorated function has the name `wrapper`.

To preserve the original function's metadata, Python provides
`functools.wraps`.

### Correct implementation

``` python
from functools import wraps


def my_decorator(func):

    @wraps(func)
    def wrapper(*args, **kwargs):

        print("Executing function")

        return func(*args, **kwargs)

    return wrapper


@my_decorator
def greet():
    """This function greets the user."""
    print("Hello")


print(greet.__name__)
print(greet.__doc__)
```

Output:

``` text
greet
This function greets the user.
```

## 6.8 Multiple Decorators

Python supports applying multiple decorators to a single function.

Example:

``` python
def decorator_one(func):

    def wrapper():
        print("Decorator One - Before")
        func()
        print("Decorator One - After")

    return wrapper


def decorator_two(func):

    def wrapper():
        print("Decorator Two - Before")
        func()
        print("Decorator Two - After")

    return wrapper


@decorator_one
@decorator_two
def greet():
    print("Hello")


greet()
```

Output:

``` text
Decorator One - Before
Decorator Two - Before
Hello
Decorator Two - After
Decorator One - After
```

The decorators are applied from the bottom upward.

## 6.9 Real-world Decorator Examples

### Authentication

A decorator can check whether a user is authenticated before allowing
access to a function.

### Logging

A decorator can automatically record when a function starts and
finishes.

### Caching

A decorator can store previously calculated results to avoid repeated
calculations.

Python provides `functools.lru_cache`:

``` python
from functools import lru_cache


@lru_cache(maxsize=128)
def fibonacci(n):

    if n <= 1:
        return n

    return fibonacci(n - 1) + fibonacci(n - 2)


print(fibonacci(10))
```

Output:

``` text
55
```

### Important interview point

Decorators are closely related to:

-   First-class functions.
-   Nested functions.
-   Closures.
-   Higher-order functions.

------------------------------------------------------------------------

# 7. Exception Handling

## 7.1 What is an Exception?

An exception is an error or unexpected event that occurs during program
execution and interrupts the normal flow of the program.

Examples:

-   Dividing a number by zero.
-   Accessing an invalid list index.
-   Opening a file that does not exist.
-   Converting invalid text into an integer.
-   Accessing a dictionary key that does not exist.

### Example without exception handling

``` python
a = 10
b = 0

result = a / b

print(result)

print("Program completed")
```

Output:

``` text
ZeroDivisionError: division by zero
```

The program terminates before executing the last statement.

Python provides exception handling to manage such situations.

## 7.2 Types of Errors in Python

There are three broad categories worth understanding.

### 1. Syntax Errors

Syntax errors occur when Python code violates language grammar.

Example:

``` python
if x > 10
    print("Greater")
```

Output:

``` text
SyntaxError
```

The colon is missing after the condition.

### 2. Runtime Errors

Runtime errors occur while the program is executing.

Example:

``` python
print(10 / 0)
```

Output:

``` text
ZeroDivisionError
```

### 3. Logical Errors

Logical errors occur when the program executes successfully but produces
an incorrect result.

Example:

``` python
length = 10
width = 5

area = length + width

print(area)
```

Output:

``` text
15
```

The program should multiply length and width, not add them.

Logical errors are usually identified through testing and debugging.

------------------------------------------------------------------------

# 8. try, except, else and finally

Python provides four main blocks for structured exception handling.

-   `try`
-   `except`
-   `else`
-   `finally`

## 8.1 try Block

The `try` block contains code that might generate an exception.

Syntax:

``` python
try:
    # Risky code
    statement
```

Example:

``` python
try:
    result = 10 / 2
    print(result)
```

Output:

``` text
5.0
```

## 8.2 except Block

The `except` block handles exceptions raised inside the corresponding
`try` block.

Syntax:

``` python
try:
    # Risky code

except ExceptionType:
    # Error handling
```

Example:

``` python
try:

    number = int(input("Enter a number: "))

    print(100 / number)

except ZeroDivisionError:
    print("Cannot divide by zero")

except ValueError:
    print("Please enter a valid integer")
```

Possible outputs:

For input `0`:

``` text
Cannot divide by zero
```

For input `abc`:

``` text
Please enter a valid integer
```

For input `5`:

``` text
20.0
```

### Handling multiple exceptions together

``` python
try:

    number = int(input("Enter a number: "))

    result = 100 / number

except (ValueError, ZeroDivisionError) as error:

    print("Error occurred:", error)
```

The `as error` syntax stores the exception object in a variable.

### Generic exception handling

``` python
try:
    result = 10 / 0

except Exception as error:
    print("An error occurred:", error)
```

Output:

``` text
An error occurred: division by zero
```

It is generally better to catch specific exceptions rather than catching
every possible exception.

Avoid unnecessarily using a bare `except:` because it can also catch
exceptions such as `KeyboardInterrupt` and `SystemExit`.

## 8.3 else Block

The `else` block executes only when the `try` block completes
successfully without raising an exception.

Syntax:

``` python
try:
    # Risky code

except Exception:
    # Handle error

else:
    # Executes if no exception occurs
```

Example:

``` python
try:

    number = int(input("Enter a number: "))

    result = 100 / number

except ZeroDivisionError:
    print("Cannot divide by zero")

except ValueError:
    print("Invalid input")

else:
    print("Result:", result)
```

Input:

``` text
5
```

Output:

``` text
Result: 20.0
```

The `else` block is useful for separating successful execution from
error-handling logic.

## 8.4 finally Block

The `finally` block executes whether an exception occurs or not,
including when an exception is handled.

It is commonly used for cleanup operations.

Examples:

-   Closing files.
-   Releasing database connections.
-   Releasing resources.
-   Cleaning up temporary operations.

Syntax:

``` python
try:
    # Risky code

except Exception:
    # Handle error

finally:
    # Cleanup code
```

Example:

``` python
try:

    number = 10 / 0

except ZeroDivisionError:

    print("Cannot divide by zero")

finally:

    print("Program execution completed")
```

Output:

``` text
Cannot divide by zero
Program execution completed
```

Even though an exception occurs, the `finally` block executes.

## 8.5 Complete Example: try, except, else and finally

``` python
try:

    a = int(input("Enter first number: "))
    b = int(input("Enter second number: "))

    result = a / b

except ZeroDivisionError:

    print("Error: Division by zero is not allowed")

except ValueError:

    print("Error: Enter valid numbers")

else:

    print("Division result:", result)

finally:

    print("Calculation operation finished")
```

Possible outputs:

**Successful execution**

``` text
Enter first number: 20
Enter second number: 5
Division result: 4.0
Calculation operation finished
```

**Exception execution**

``` text
Enter first number: 20
Enter second number: 0
Error: Division by zero is not allowed
Calculation operation finished
```

## 8.6 Execution Flow

``` text
                 +----------------+
                 |   try block    |
                 +----------------+
                         |
                Did an exception occur?
                    /          \
                  No            Yes
                  |              |
           +-------------+  +----------------+
           |  else block |  | Matching except|
           +-------------+  +----------------+
                  \              /
                   \            /
                    +----------+
                         |
                  +--------------+
                  | finally block|
                  +--------------+
```

**Important:** If an exception is not handled by any matching `except`
block, it propagates after the `finally` block executes. The `else`
block is skipped.

------------------------------------------------------------------------

# 9. Raising and Creating Custom Exceptions

## 9.1 What is raise?

The `raise` keyword is used to explicitly generate an exception.

Sometimes Python does not automatically identify a business-rule
violation, so we manually raise an exception.

### Syntax

``` python
raise ExceptionType("Error message")
```

### Example

``` python
age = 15

if age < 18:
    raise ValueError("Age must be 18 or above")
```

Output:

``` text
ValueError: Age must be 18 or above
```

Here, the programmer explicitly raises an exception when the condition
is not satisfied.

## 9.2 Raising Built-in Exceptions

Python provides several built-in exceptions.

Examples:

``` python
raise ValueError("Invalid value")

raise TypeError("Incorrect data type")

raise RuntimeError("Runtime problem")

raise ZeroDivisionError("Division by zero")
```

### Example: Validate marks

``` python
def validate_marks(marks):

    if marks < 0 or marks > 100:
        raise ValueError("Marks must be between 0 and 100")

    print("Valid marks")


validate_marks(85)
```

Output:

``` text
Valid marks
```

For:

``` python
validate_marks(120)
```

Output:

``` text
ValueError: Marks must be between 0 and 100
```

## 9.3 Handling Raised Exceptions

We can combine `raise` with `try` and `except`.

``` python
def withdraw(balance, amount):

    try:

        if amount > balance:
            raise ValueError("Insufficient balance")

        balance -= amount

        print("Withdrawal successful")

    except ValueError as error:

        print("Error:", error)


withdraw(5000, 6000)
```

Output:

``` text
Error: Insufficient balance
```

## 9.4 What is a Custom Exception?

A custom exception is an exception class created by the programmer to
represent application-specific errors.

Custom exceptions are useful when built-in exceptions do not clearly
describe the problem.

Custom exceptions generally inherit from the built-in `Exception` class.

### Syntax

``` python
class CustomException(Exception):
    pass
```

### Example: Invalid Age Exception

``` python
class InvalidAgeError(Exception):
    pass


def register_user(age):

    if age < 18:
        raise InvalidAgeError("User must be at least 18 years old")

    print("Registration successful")


try:

    register_user(16)

except InvalidAgeError as error:

    print("Registration failed:", error)
```

Output:

``` text
Registration failed: User must be at least 18 years old
```

Explanation:

1.  `InvalidAgeError` is our custom exception class.
2.  It inherits from `Exception`.
3.  `register_user()` checks the age.
4.  If the age is below 18, it raises `InvalidAgeError`.
5.  The `except` block catches that exception.

## 9.5 Custom Exception with Additional Information

We can also store additional details inside a custom exception.

``` python
class InsufficientBalanceError(Exception):

    def __init__(self, balance, amount):

        self.balance = balance
        self.amount = amount

        message = (
            f"Insufficient balance. "
            f"Available: {balance}, Requested: {amount}"
        )

        super().__init__(message)


def withdraw(balance, amount):

    if amount > balance:
        raise InsufficientBalanceError(balance, amount)

    return balance - amount


try:

    withdraw(5000, 7000)

except InsufficientBalanceError as error:

    print(error)
```

Output:

``` text
Insufficient balance. Available: 5000, Requested: 7000
```

### Real-world applications

Custom exceptions are used in:

-   Banking systems.
-   E-commerce applications.
-   Authentication systems.
-   Payment processing.
-   API validation.
-   Database applications.
-   Enterprise applications.

### Difference between raise and custom exceptions

  -----------------------------------------------------------------------
  raise                               Custom exception
  ----------------------------------- -----------------------------------
  Keyword used to generate an         Programmer-defined exception class
  exception                           

  Can raise built-in exceptions       Defines application-specific error
                                      types

  Used for triggering errors          Used for representing specific
                                      application errors
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 10. Assertions

## 10.1 What is an Assertion?

An assertion is a debugging statement used to check whether a condition
is true.

If the condition is false, Python raises an `AssertionError`.

Assertions are commonly used during development and testing.

### Syntax

``` python
assert condition
```

Or:

``` python
assert condition, "Error message"
```

## 10.2 Basic Assertion Example

``` python
age = 25

assert age >= 18

print("Eligible")
```

Output:

``` text
Eligible
```

The condition is true, so execution continues.

### Example with False Condition

``` python
age = 15

assert age >= 18, "Age must be 18 or above"

print("Eligible")
```

Output:

``` text
AssertionError: Age must be 18 or above
```

The condition is false, so Python raises `AssertionError`.

## 10.3 Assertions in Functions

Assertions can be used to verify assumptions about function inputs.

Example:

``` python
def calculate_square(number):

    assert number >= 0, "Number must be non-negative"

    return number * number


print(calculate_square(5))
```

Output:

``` text
25
```

For:

``` python
print(calculate_square(-5))
```

Output:

``` text
AssertionError: Number must be non-negative
```

## 10.4 Assertions vs Exception Handling

  -----------------------------------------------------------------------
  Feature                 Assertions              Exception Handling
  ----------------------- ----------------------- -----------------------
  Purpose                 Verify assumptions      Handle runtime errors

  Keyword                 `assert`                `try`, `except`,
                                                  `raise`

  Failure                 Raises `AssertionError` Raises or handles
                                                  various exceptions

  Main use                Debugging and testing   Production error
                                                  management

  Can be disabled?        Yes, with Python        Normal exception
                          optimization            handling cannot be
                                                  disabled this way
  -----------------------------------------------------------------------

**Important:** Do not use assertions for validating untrusted user input
or essential business rules. Python can remove assertions when run with
optimization (`python -O`).

For production validation, use explicit conditions and raise appropriate
exceptions.

------------------------------------------------------------------------

# 11. Logging and Log Levels

## 11.1 What is Logging?

Logging is the process of recording information about a program's
execution.

It helps developers understand:

-   What happened during execution.
-   When an error occurred.
-   Which operation was performed.
-   Why a program failed.
-   Whether an application is functioning correctly.

Python provides a built-in `logging` module.

### Why use logging instead of print()?

Consider a large application with thousands of operations.

Using `print()` for every operation becomes difficult to manage.

Logging provides:

-   Different severity levels.
-   Timestamps.
-   File-based logging.
-   Configurable message formats.
-   Better debugging.
-   Easier monitoring.

### Basic logging example

``` python
import logging

logging.basicConfig(level=logging.DEBUG)

logging.debug("This is a debug message")
logging.info("Application started")
logging.warning("Low disk space")
logging.error("An error occurred")
logging.critical("Critical system failure")
```

Possible output:

``` text
DEBUG:root:This is a debug message
INFO:root:Application started
WARNING:root:Low disk space
ERROR:root:An error occurred
CRITICAL:root:Critical system failure
```

## 11.2 Python Logging Levels

Python provides five commonly used standard logging levels.

  ------------------------------------------------------------------------
  Level                                Numeric value Purpose
  --------------------- ---------------------------- ---------------------
  DEBUG                                           10 Detailed diagnostic
                                                     information useful
                                                     during development

  INFO                                            20 Confirms that normal
                                                     application
                                                     operations are
                                                     working

  WARNING                                         30 Indicates an
                                                     unexpected situation
                                                     that does not stop
                                                     execution

  ERROR                                           40 Indicates that an
                                                     operation failed

  CRITICAL                                        50 Indicates a serious
                                                     failure that may
                                                     prevent the
                                                     application from
                                                     continuing
  ------------------------------------------------------------------------

### Logging level hierarchy

``` text
DEBUG       10
INFO        20
WARNING     30
ERROR       40
CRITICAL    50
```

When we configure a logging level, messages at that level and higher are
generally displayed.

Example:

``` python
logging.basicConfig(level=logging.WARNING)
```

This displays:

-   WARNING
-   ERROR
-   CRITICAL

It does not display DEBUG or INFO.

## 11.3 Logging to a File

Instead of displaying messages on the console, we can save them in a
file.

Example:

``` python
import logging

logging.basicConfig(
    filename="application.log",
    level=logging.DEBUG,
    format="%(asctime)s - %(levelname)s - %(message)s"
)

logging.info("Application started")

logging.warning("Low memory")

logging.error("Database connection failed")
```

This creates an `application.log` file.

Example content:

``` text
2026-11-17 10:30:00 - INFO - Application started
2026-11-17 10:30:01 - WARNING - Low memory
2026-11-17 10:30:02 - ERROR - Database connection failed
```

The exact timestamps depend on execution.

## 11.4 Understanding Logging Format

Consider:

``` python
format="%(asctime)s - %(levelname)s - %(message)s"
```

Each placeholder represents:

  Placeholder       Meaning
  ----------------- --------------------
  `%(asctime)s`     Date and time
  `%(levelname)s`   Logging level
  `%(message)s`     Actual log message
  `%(name)s`        Logger name
  `%(filename)s`    Source filename
  `%(lineno)d`      Line number

## 11.5 Logging Exceptions

We can use `logging.exception()` inside an exception handler to log an
error along with its traceback.

Example:

``` python
import logging

logging.basicConfig(level=logging.ERROR)

try:

    result = 10 / 0

except ZeroDivisionError:

    logging.exception("Division error occurred")
```

This records the exception details and traceback.

### Real-world applications

Logging is essential in:

-   Backend development.
-   Django and Flask applications.
-   FastAPI services.
-   Machine learning pipelines.
-   AI agents and RAG applications.
-   Database applications.
-   Production monitoring.

For larger applications, use named loggers and configure handlers
centrally rather than repeatedly calling `basicConfig()` in different
modules.

------------------------------------------------------------------------

# 12. Reading Tracebacks and Debugging

## 12.1 What is a Traceback?

A traceback is a report generated by Python when an exception occurs.

It shows the sequence of function calls that led to the error.

A traceback helps developers identify:

-   The error type.
-   The error message.
-   The file where the error occurred.
-   The line number.
-   The sequence of function calls.

### Example

``` python
def divide(a, b):

    return a / b


def calculate():

    result = divide(10, 0)

    print(result)


calculate()
```

Output:

``` text
Traceback (most recent call last):

  File "main.py", line 13, in <module>
    calculate()

  File "main.py", line 9, in calculate
    result = divide(10, 0)

  File "main.py", line 4, in divide
    return a / b

ZeroDivisionError: division by zero
```

## 12.2 How to Read a Traceback

Let's understand the traceback step by step.

### Step 1: Identify the exception type

``` text
ZeroDivisionError: division by zero
```

This tells us that the program attempted to divide a number by zero.

### Step 2: Identify the file name

``` text
File "main.py"
```

This tells us where the error occurred.

### Step 3: Identify the line number

``` text
line 4
```

The error occurred on line 4.

### Step 4: Identify the failing statement

``` python
return a / b
```

This is the statement that caused the exception.

### Step 5: Understand the function call sequence

``` text
calculate()
    |
    v
divide(10, 0)
    |
    v
return a / b
```

This helps us understand how the program reached the error.

## 12.3 Common Python Exceptions

  -----------------------------------------------------------------------
  Exception               Meaning                 Example
  ----------------------- ----------------------- -----------------------
  `SyntaxError`           Invalid Python syntax   Missing colon

  `NameError`             Variable not defined    `print(x)` when `x`
                                                  does not exist

  `TypeError`             Invalid operation       `"10" + 5`
                          between types           

  `ValueError`            Correct type but        `int("hello")`
                          invalid value           

  `IndexError`            Invalid sequence index  `numbers[10]`

  `KeyError`              Dictionary key missing  `student["salary"]`

  `AttributeError`        Attribute or method     `5.append(10)`
                          does not exist          

  `ZeroDivisionError`     Division by zero        `10 / 0`

  `FileNotFoundError`     File does not exist     Opening missing file

  `ImportError`           Import operation failed Importing unavailable
                                                  names

  `ModuleNotFoundError`   Module cannot be found  Importing an
                                                  uninstalled module
  -----------------------------------------------------------------------

## 12.4 Debugging

Debugging is the process of identifying, analyzing and fixing errors in
a program.

The goal of debugging is not just to identify the line where an error
occurred but also to understand why it occurred.

### Common debugging techniques

1.  Reading error messages.
2.  Reading tracebacks.
3.  Using print statements.
4.  Using logging.
5.  Using breakpoints.
6.  Inspecting variable values.
7.  Executing code step by step.
8.  Testing individual functions.

### Example: Debugging a logical error

Consider:

``` python
def calculate_average(numbers):

    total = 0

    for number in numbers:
        total += number

    average = total / len(numbers) + 1

    return average


print(calculate_average([10, 20, 30]))
```

Expected output:

``` text
20.0
```

Actual output:

``` text
21.0
```

The issue is:

``` python
average = total / len(numbers) + 1
```

The additional `+ 1` creates the logical error.

Correct implementation:

``` python
def calculate_average(numbers):

    total = 0

    for number in numbers:
        total += number

    average = total / len(numbers)

    return average


print(calculate_average([10, 20, 30]))
```

Output:

``` text
20.0
```

A good debugging process involves understanding the expected output,
actual output, and the logic responsible for the difference.

------------------------------------------------------------------------

# 13. Debugger and Breakpoints

## 13.1 What is a Debugger?

A debugger is a tool that allows programmers to execute a program step
by step and inspect its internal state.

Instead of running the entire program at once, we can pause execution
and examine variables.

Python provides a built-in debugger called `pdb`.

Code editors such as VS Code also provide graphical debugging tools.

## 13.2 What is a Breakpoint?

A breakpoint is a point in the program where execution pauses
temporarily.

It allows us to inspect variables and understand program behavior at a
specific line.

### Example

``` python
def calculate(a, b):

    total = a + b

    average = total / 2

    result = average * 10

    return result


answer = calculate(10, 20)

print(answer)
```

Suppose we want to inspect the values of `total` and `average`.

We can place a breakpoint after calculating `total`.

When the program reaches that line, execution pauses and we can inspect
the variables.

## 13.3 Using breakpoint() in Python

Python provides a built-in `breakpoint()` function.

Example:

``` python
def calculate(a, b):

    total = a + b

    breakpoint()

    average = total / 2

    return average


print(calculate(10, 20))
```

When execution reaches `breakpoint()`, Python enters the debugger.

Example debugger session:

``` text
(Pdb) p total
30

(Pdb) n
(Pdb) p average
15.0

(Pdb) c
15.0
```

Explanation of commands:

-   `p total`: Prints the value of `total`.
-   `n`: Executes the next line.
-   `c`: Continues program execution.

## 13.4 Important pdb Commands

  Command         Meaning
  --------------- ----------------------------
  `n`             Execute the next line
  `s`             Step into a function call
  `c`             Continue execution
  `l`             Display nearby source code
  `p variable`    Print a variable's value
  `pp variable`   Pretty-print a variable
  `w`             Display the current stack
  `b`             Set a breakpoint
  `cl`            Clear a breakpoint
  `q`             Quit the debugger

## 13.5 Debugging in VS Code

Visual Studio Code provides an interactive graphical debugger for
Python.

### Step 1: Open your Python file

Open your Python program in VS Code.

### Step 2: Set a breakpoint

Click to the left of a line number.

A red dot appears, indicating that a breakpoint has been set.

### Step 3: Start debugging

-   Open the Run and Debug panel.
-   Select the Python debugger.
-   Start debugging using F5.

### Step 4: Inspect variables

When execution pauses, you can inspect:

-   Local variables.
-   Global variables.
-   Function arguments.
-   Call stack.
-   Watch expressions.

### Step 5: Use debugging controls

  -----------------------------------------------------------------------
  Action                  Typical shortcut        Purpose
  ----------------------- ----------------------- -----------------------
  Continue                F5                      Continue execution
                                                  until the next
                                                  breakpoint

  Step Over               F10                     Execute the current
                                                  line without entering
                                                  called functions

  Step Into               F11                     Enter a function call
                                                  and debug its internal
                                                  statements

  Step Out                Shift + F11             Finish the current
                                                  function and return to
                                                  its caller

  Stop                    Shift + F5              Stop the debugging
                                                  session
  -----------------------------------------------------------------------

Keyboard shortcuts can vary depending on the operating system and VS
Code keymap.

## 13.6 Debugger vs print()

  -----------------------------------------------------------------------
  Feature                 print()                 Debugger
  ----------------------- ----------------------- -----------------------
  Purpose                 Displays values         Examines program
                                                  execution

  Execution control       Cannot pause execution  Can pause and resume
                          by itself               execution

  Variable inspection     Manual                  Interactive

  Step-by-step execution  Not available           Available

  Call stack              Not directly available  Available

  Best use                Simple checks           Complex debugging
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 14. Complete Practical Example: Combining Multiple Concepts

Let's combine generators, decorators, exception handling and logging
into one practical example.

**Scenario:** Create a student marks processing system.

Requirements:

1.  Generate student marks using a generator.
2.  Validate marks.
3.  Use a custom exception for invalid marks.
4.  Use a decorator to log function execution.
5.  Use Python logging to record errors.

### Complete program

``` python
import logging
from functools import wraps


# Configure logging
logging.basicConfig(
    level=logging.INFO,
    format="%(levelname)s - %(message)s"
)


# Custom exception
class InvalidMarksError(Exception):
    pass


# Decorator
def log_execution(func):

    @wraps(func)
    def wrapper(*args, **kwargs):

        logging.info(f"Executing {func.__name__}")

        try:
            result = func(*args, **kwargs)
            return result

        except Exception:
            logging.exception("Function execution failed")
            raise

    return wrapper


# Generator
def generate_marks():

    marks = [85, 90, 75, 110, 65]

    for mark in marks:
        yield mark


# Processing function
@log_execution
def process_marks():

    for mark in generate_marks():

        if mark < 0 or mark > 100:
            raise InvalidMarksError(
                f"Invalid marks: {mark}"
            )

        print("Valid marks:", mark)


# Main program
try:

    process_marks()

except InvalidMarksError as error:

    print("Error:", error)

finally:

    print("Student marks processing completed")
```

Possible output:

``` text
INFO - Executing process_marks
Valid marks: 85
Valid marks: 90
Valid marks: 75
ERROR - Function execution failed
Traceback ...
InvalidMarksError: Invalid marks: 110
Error: Invalid marks: 110
Student marks processing completed
```

### Concepts used

  Concept            Application
  ------------------ ------------------------------------
  Generator          Produces marks one at a time
  `yield`            Returns each mark
  Custom exception   Represents invalid marks
  `raise`            Raises the invalid marks exception
  Decorator          Adds logging behavior
  `@wraps`           Preserves function metadata
  Logging            Records execution and errors
  try-except         Handles invalid marks
  finally            Executes final cleanup message

------------------------------------------------------------------------

# 15. Important Differences for Interviews

These comparisons are particularly important for Python interviews.

## 15.1 Iterable vs Iterator vs Generator

  ------------------------------------------------------------------------
  Feature           Iterable          Iterator          Generator
  ----------------- ----------------- ----------------- ------------------
  Purpose           Provides elements Returns elements  Generates elements
                    for iteration     one by one        lazily

  `__iter__()`      Yes, for standard Yes               Yes
                    iterables                           

  `__next__()`      Not necessarily   Yes               Yes

  Memory            Depends on        Depends on        Generally
                    implementation    implementation    memory-efficient

  Creation          List, tuple,      `iter()` or       `yield` or
                    string, etc.      custom class      generator
                                                        expression
  ------------------------------------------------------------------------

## 15.2 yield vs return

  yield                       return
  --------------------------- ---------------------------------------
  Produces a value            Returns a result
  Pauses function execution   Terminates function execution
  Preserves generator state   Does not create a resumable generator
  Supports multiple yields    Function normally returns once

## 15.3 Nested Function vs Closure

  -----------------------------------------------------------------------
  Nested Function                     Closure
  ----------------------------------- -----------------------------------
  Function defined inside another     Inner function that retains access
  function                            to enclosing variables

  Does not necessarily retain         Retains access to captured
  variables after the outer function  variables
  ends                                

  Used for organizing code            Used for state preservation and
                                      data hiding
  -----------------------------------------------------------------------

## 15.4 Decorator vs Closure

  -----------------------------------------------------------------------
  Decorator                           Closure
  ----------------------------------- -----------------------------------
  Modifies or extends function        Retains access to enclosing
  behavior                            variables

  Usually implemented using nested    Uses nested functions
  functions                           

  Uses functions as arguments and     Uses an enclosing scope
  return values                       

  Can be implemented using a closure  Often provides the mechanism used
                                      by a decorator
  -----------------------------------------------------------------------

## 15.5 Exception vs Assertion

  -----------------------------------------------------------------------
  Exception                           Assertion
  ----------------------------------- -----------------------------------
  Handles unexpected runtime          Checks assumptions
  conditions                          

  Used in production error handling   Mainly used in development and
                                      testing

  Can be raised explicitly            Uses `assert`

  Supports many exception types       Raises `AssertionError` when false
  -----------------------------------------------------------------------

## 15.6 Logging vs Debugging

  -----------------------------------------------------------------------
  Logging                             Debugging
  ----------------------------------- -----------------------------------
  Records application events          Investigates program behavior

  Can work continuously in production Often performed during development

  Uses log levels                     Uses breakpoints and stepping

  Helps monitor applications          Helps locate and fix bugs
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 16. Interview Questions and Answers

Here are important questions based on these topics.

### Q1. What is the difference between an iterable and an iterator?

An iterable is an object that can be looped through, whereas an iterator
is an object that retrieves elements one at a time and maintains its
current iteration position.

### Q2. What is the purpose of iter()?

`iter()` converts an iterable into an iterator.

### Q3. What does next() do?

`next()` retrieves the next element from an iterator.

### Q4. What is StopIteration?

It is a built-in exception raised when an iterator has no more elements
to return.

### Q5. What is a generator?

A generator is a special iterator that produces values one at a time
using `yield` or a generator expression.

### Q6. Why are generators memory-efficient?

Generators use lazy evaluation. They produce values only when requested
instead of storing all generated values in memory.

### Q7. What is the difference between yield and return?

`return` terminates a function, whereas `yield` pauses a generator
function and allows it to resume later.

### Q8. What is a generator expression?

It is a concise way to create a generator using parentheses.

Example:

``` python
squares = (x * x for x in range(10))
```

### Q9. What is a nested function?

A function defined inside another function is called a nested function.

### Q10. What is a closure?

A closure is an inner function that retains access to variables from its
enclosing scope even after the outer function has completed.

### Q11. What is the purpose of nonlocal?

`nonlocal` allows an inner function to modify a variable belonging to an
enclosing function.

### Q12. What is a decorator?

A decorator is a function that modifies or extends another function's
behavior without changing its original source code.

### Q13. Why do we use \*args and \*\*kwargs in decorators?

They allow decorators to support functions with different positional and
keyword arguments.

### Q14. What is functools.wraps?

It preserves the original function's metadata, such as its name and
documentation, when using decorators.

### Q15. What is the purpose of finally?

The `finally` block executes whether an exception occurs or not, making
it useful for cleanup operations.

### Q16. What is the difference between raise and except?

`raise` explicitly generates an exception, whereas `except` catches and
handles an exception.

### Q17. What is a custom exception?

A custom exception is a programmer-defined exception class that usually
inherits from `Exception`.

### Q18. What is an assertion?

An assertion checks whether a condition is true. If it is false, Python
raises `AssertionError`.

### Q19. What are the five logging levels?

-   DEBUG
-   INFO
-   WARNING
-   ERROR
-   CRITICAL

### Q20. What is a traceback?

A traceback is a report showing the sequence of function calls that led
to an exception.

### Q21. What is debugging?

Debugging is the process of identifying, analyzing and fixing errors in
a program.

### Q22. What is a breakpoint?

A breakpoint is a point where program execution pauses so that variables
and execution flow can be inspected.

### Q23. What is pdb?

`pdb` is Python's built-in interactive debugger.

### Q24. Can a generator be reused?

Generally, a generator object is consumed once. After it is exhausted,
it cannot produce its values again. A new generator must be created.

### Q25. Can we use multiple decorators on one function?

Yes. Python supports multiple decorators, and they are applied from
bottom to top.

------------------------------------------------------------------------

# 17. Practical Coding Exercises

Practice the following programs to strengthen your understanding.

## Beginner

1.  Create an iterator that prints numbers from 1 to 10.
2.  Write a generator that produces even numbers up to 100.
3.  Create a generator expression that produces squares of numbers.
4.  Write a nested function to perform addition and subtraction.
5.  Create a closure that remembers a user's name.

## Intermediate

6.  Create a custom iterator for odd numbers.
7.  Write a Fibonacci generator.
8.  Create a decorator that prints the execution time of a function.
9.  Create a decorator that executes a function three times.
10. Write a program using `try`, `except`, `else` and `finally`.
11. Create a custom exception for invalid password length.
12. Use assertions to validate a function's assumptions.
13. Configure logging to save messages into a file.

## Advanced

14. Create a generator that reads a large text file line by line.
15. Create a closure-based counter that maintains state.
16. Implement multiple decorators on one function.
17. Build a banking application using custom exceptions.
18. Implement a student result processing system using generators and
    logging.
19. Debug a program using `pdb` and breakpoints.
20. Create a data processing pipeline using generators and exception
    handling.

------------------------------------------------------------------------

# 18. Recommended Learning Order

For better understanding and practical implementation, follow this
sequence:

1.  **Iteration fundamentals:** Iterable, iterator, `iter()`, `next()`,
    `StopIteration`.
2.  **Generators:** Generator functions, `yield`, generator expressions.
3.  **Functions advanced concepts:** Nested functions, closures,
    `nonlocal`.
4.  **Decorators:** Function wrapping, arguments, multiple decorators,
    `functools.wraps`.
5.  **Exception handling:** `try`, `except`, `else`, `finally`, `raise`,
    custom exceptions, assertions.
6.  **Logging and debugging:** Logging levels, tracebacks, `pdb`,
    breakpoints and VS Code debugging.

## Final Study Recommendation

Do not just memorize the definitions. Write and execute the examples in
VS Code, modify the inputs, deliberately introduce errors, and observe
the outputs. This will help you understand how Python behaves internally
and prepare you for practical coding interviews.
