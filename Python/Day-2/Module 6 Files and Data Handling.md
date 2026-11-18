# Python Files and Data Handling – Complete In-Depth Tutorial

Files and data handling are important Python concepts used to store, retrieve, process, and manage information.

In real-world applications, programs often need to:
* Read information from text files.
* Write output into files.
* Store structured data in JSON format.
* Process Excel-compatible CSV files.
* Handle dates, times, and durations.
* Access configuration values through environment variables.
* Manage files and folders using Python.

For example, in an AI application such as a resume analyzer, Python might read an uploaded resume, extract its contents, store extracted information in JSON, process job data from CSV files, and use environment variables to access API keys.

Let's understand each topic step by step.

---

## 1. Opening, Reading and Writing Files

### 1.1 What is a file?
A file is a collection of data stored permanently on a computer. Unlike variables, which generally exist only while a program is running, files allow us to store information even after the program terminates.

**Examples of files:**

| File | Purpose |
| :--- | :--- |
| `student.txt` | Stores student information |
| `data.csv` | Stores tabular data |
| `config.json` | Stores structured configuration |
| `report.pdf` | Stores documents |
| `image.png` | Stores image data |
| `program.py` | Stores Python source code |

Python provides built-in functions to work with files. The most commonly used function is:

```python
open()
```

### 1.2 Opening a file
The `open()` function is used to open an existing file or create a new file, depending on the selected mode.

**Syntax:**
```python
file_object = open("filename", "mode")
```

**Parameters:**
* `filename`: Name or path of the file.
* `mode`: Specifies how the file should be opened.

**Example:**
```python
file = open("student.txt", "r")
```
This opens `student.txt` in read mode. If the file does not exist, Python raises a `FileNotFoundError`.

### 1.3 Writing data into a file
Python provides the `write()` method to write data into a file.

**Example:**
```python
file = open("student.txt", "w")
file.write("Welcome to Python Programming")
file.close()
```

**Explanation:**
* `open()` opens the file in write mode.
* `write()` writes the specified text.
* `close()` closes the file and releases associated resources.

If `student.txt` does not exist, Python creates it. If it already exists, its previous contents are overwritten.

**To write multiple lines:**
```python
file = open("student.txt", "w")
file.write("Name: Rahul\n")
file.write("Age: 22\n")
file.write("Course: Python Programming\n")
file.close()
```

**Output stored in the file:**
```text
Name: Rahul
Age: 22
Course: Python Programming
```

> **Important:** The `write()` method does not automatically add a newline. Use `\n` when you want to move to the next line.

### 1.4 Reading data from a file
Python provides different methods to read file contents.

#### A. `read()`
Reads the entire file content as a string.

```python
file = open("student.txt", "r")
content = file.read()
print(content)
file.close()
```

**Output:**
```text
Name: Rahul
Age: 22
Course: Python Programming
```

You can also specify the number of characters to read:
```python
file = open("student.txt", "r")
content = file.read(10)
print(content)
file.close()
```
This reads the first 10 characters.

#### B. `readline()`
Reads one line at a time.

```python
file = open("student.txt", "r")
line1 = file.readline()
line2 = file.readline()
print(line1)
print(line2)
file.close()
```

If the file contains:
```text
Name: Rahul
Age: 22
Course: Python Programming
```

**Output:**
```text
Name: Rahul

Age: 22
```
Each call to `readline()` reads the next line.

#### C. `readlines()`
Reads all lines and returns them as a list of strings.

```python
file = open("student.txt", "r")
lines = file.readlines()
print(lines)
file.close()
```

**Output:**
```python
[
    'Name: Rahul\n',
    'Age: 22\n',
    'Course: Python Programming\n'
]
```

#### Difference between `read()`, `readline()` and `readlines()`

| Method | Description | Return type |
| :--- | :--- | :--- |
| `read()` | Reads the entire file or a specified number of characters | String |
| `readline()` | Reads one line | String |
| `readlines()` | Reads all lines into a list | List |

### 1.5 Reading a file using a loop
When processing large files, reading line by line is often more memory-efficient than loading the entire file into memory.

```python
file = open("student.txt", "r")
for line in file:
    print(line.strip())
file.close()
```

**Output:**
```text
Name: Rahul
Age: 22
Course: Python Programming
```

Here:
* `for line in file` iterates over each line.
* `strip()` removes leading and trailing whitespace, including newline characters.

### 1.6 Appending data to a file
Sometimes we want to add new content without deleting existing content. For this, we use append mode (`a`).

```python
file = open("student.txt", "a")
file.write("City: Hyderabad\n")
file.close()
```
The new content is added at the end of the file.

### 1.7 Closing a file
After completing file operations, we should close the file.

```python
file.close()
```

**Why is closing important?**
* Releases system resources.
* Helps ensure buffered data is written.
* Prevents unnecessary open file handles.
* Reduces the possibility of file access problems.

A better approach is using a context manager, which we will discuss in Section 3.

---

## 2. File Modes and Text/Binary Files

### 2.1 What are file modes?
File modes determine how Python interacts with a file. For example, a file can be opened for reading, writing, appending, reading and writing, or binary operations.

### 2.2 Common file modes

| Mode | Description |
| :--- | :--- |
| `r` | Read mode; file must exist |
| `w` | Write mode; creates or overwrites a file |
| `a` | Append mode; creates or adds to the end of a file |
| `x` | Exclusive creation; fails if the file already exists |
| `r+` | Read and write; file must exist |
| `w+` | Read and write; overwrites or creates the file |
| `a+` | Read and append; creates the file if needed |

**Example: Read mode (`r`)**
```python
file = open("data.txt", "r")
print(file.read())
file.close()
```
If the file does not exist, Python raises `FileNotFoundError`.

**Example: Write mode (`w`)**
```python
file = open("data.txt", "w")
file.write("Python Programming")
file.close()
```
If the file already contains data, that data is erased.

**Example: Append mode (`a`)**
```python
file = open("data.txt", "a")
file.write("\nLearning File Handling")
file.close()
```
Existing content is preserved.

**Example: Exclusive creation mode (`x`)**
```python
file = open("newfile.txt", "x")
file.write("This is a new file.")
file.close()
```
If `newfile.txt` already exists, Python raises `FileExistsError`.

### 2.3 Combining file modes
File modes can be combined with `+`, `b`, and `t`.

| Mode | Meaning |
| :--- | :--- |
| `rb` | Read binary |
| `wb` | Write binary |
| `ab` | Append binary |
| `r+` | Read and write text |
| `rb+` | Read and write binary |
| `w+` | Read and write, overwriting existing content |
| `a+` | Read and append |

The default mode is `rt`, meaning read text.

### 2.4 Text files
Text files store information as readable characters (e.g., `.txt`, `.csv`, `.json`, `.py`, `.html`).

**Writing:**
```python
with open("message.txt", "w", encoding="utf-8") as file:
    file.write("Hello, Python!")
```

**Reading:**
```python
with open("message.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)
```

**Output:**
```text
Hello, Python!
```

#### What is encoding?
Encoding defines how characters are converted into bytes for storage. A commonly used encoding is UTF-8:

```python
open("data.txt", "r", encoding="utf-8")
```

UTF-8 supports English characters, Indian languages, special symbols, and most Unicode characters. It is good practice to specify the encoding explicitly when working with text files.

### 2.5 Binary files
Binary files store data as bytes rather than directly readable text (e.g., `.jpg`, `.png`, `.mp3`, `.mp4`, `.pdf`, executables). To work with binary files, use the `b` mode.

```python
with open("image.png", "rb") as file:
    content = file.read()
    print(type(content))
```

**Output:**
```text
<class 'bytes'>
```

#### Copying a binary file
```python
with open("image.png", "rb") as source:
    data = source.read()

with open("image_copy.png", "wb") as destination:
    destination.write(data)
```

For large files, copy in chunks instead of loading the entire file into memory:
```python
with open("large_file.pdf", "rb") as source:
    with open("copy.pdf", "wb") as destination:
        while True:
            chunk = source.read(4096)
            if not chunk:
                break
            destination.write(chunk)
```
Here, `4096` represents the number of bytes read in each iteration.

### 2.6 Difference between text and binary files

| Feature | Text files | Binary files |
| :--- | :--- | :--- |
| **Storage** | Encoded characters | Bytes |
| **Readability** | Human-readable | Usually not directly readable |
| **Mode** | `r`, `w`, `a` | `rb`, `wb`, `ab` |
| **Encoding** | Uses character encoding | No text encoding conversion |
| **Examples** | TXT, CSV, JSON | Images, videos, PDFs |
| **Read result** | `str` | `bytes` |

**Important distinction:**
```python
# Text mode
with open("data.txt", "r") as file:
    print(type(file.read()))  # <class 'str'>

# Binary mode
with open("data.txt", "rb") as file:
    print(type(file.read()))  # <class 'bytes'>
```

---

## 3. Context Managers and the `with` Statement

### 3.1 What is a context manager?
A context manager is a Python mechanism that manages resources automatically (such as files, database connections, network connections, locks, and temporary resources). Instead of manually calling `close()`, Python provides the `with` statement.

### 3.2 Traditional file handling
```python
file = open("data.txt", "r")
content = file.read()
print(content)
file.close()
```
*Potential problem:* If an exception occurs before `file.close()`, the file may remain open.

### 3.3 File handling using `with`
```python
with open("data.txt", "r") as file:
    content = file.read()
    print(content)
```
Python automatically closes the file when execution leaves the `with` block, including when an exception occurs. This makes file handling safer and cleaner.

### 3.4 Syntax
```python
with expression as variable:
    statements
```
* `with`: Starts the context manager.
* `expression`: Usually creates or obtains a resource.
* `as variable`: Assigns the resource to a variable.
* `statements`: Execute while the resource is active.

### 3.5 Writing using `with`
```python
with open("student.txt", "w", encoding="utf-8") as file:
    file.write("Name: Rahul\n")
    file.write("Age: 22\n")
    file.write("Course: Python")
```
No explicit `close()` is required.

### 3.6 Reading line by line using `with`
```python
with open("student.txt", "r", encoding="utf-8") as file:
    for line in file:
        print(line.strip())
```

### 3.7 Multiple context managers
We can manage multiple resources in one `with` statement:
```python
with open("source.txt", "r") as source, \
     open("destination.txt", "w") as destination:
    for line in source:
        destination.write(line)
```

### 3.8 Exception handling with file operations
Sometimes a file may not exist, or Python may not have permission to access it. We can use `try-except`:

```python
try:
    with open("data.txt", "r") as file:
        content = file.read()
        print(content)
except FileNotFoundError:
    print("File does not exist.")
except PermissionError:
    print("You do not have permission to access this file.")
```

### 3.9 How does a context manager work internally?
Python context managers implement two special methods:
* `__enter__()`: Runs when entering the `with` block.
* `__exit__()`: Runs when leaving the block.

**Simplified custom context manager:**
```python
class MyContextManager:
    def __enter__(self):
        print("Entering the context")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting the context")

with MyContextManager():
    print("Inside the context")
```

**Output:**
```text
Entering the context
Inside the context
Exiting the context
```

---

## 4. `pathlib`

### 4.1 What is `pathlib`?
`pathlib` is a Python standard library module used to work with file and directory paths. It provides an object-oriented approach to handling paths using the `Path` class instead of manually joining strings.

```python
from pathlib import Path
```

### 4.2 Creating a path
```python
from pathlib import Path

file_path = Path("data.txt")
print(file_path)  # data.txt
```

### 4.3 Getting the current working directory
```python
from pathlib import Path

current_directory = Path.cwd()
print(current_directory)
```

### 4.4 Getting the home directory
```python
from pathlib import Path

home_directory = Path.home()
print(home_directory)
```

### 4.5 Joining paths
Traditionally, developers might use string concatenation (`"data" + "/" + "student.txt"`). With `pathlib`, use the `/` operator:

```python
from pathlib import Path

file_path = Path("data") / "student.txt"
print(file_path)  # data/student.txt
```
`pathlib` automatically handles platform-specific path separators (`\` on Windows, `/` on Linux/macOS).

### 4.6 Checking whether a file exists
```python
from pathlib import Path

file_path = Path("student.txt")

if file_path.exists():
    print("File exists")
else:
    print("File does not exist")

print(file_path.is_file())  # Check if it's a file
print(file_path.is_dir())   # Check if it's a directory
```

### 4.7 Creating directories
Use `mkdir()`:
```python
from pathlib import Path

folder = Path("students")
folder.mkdir()
```

To create nested directories:
```python
folder = Path("data/students/records")
folder.mkdir(parents=True, exist_ok=True)
```
* `parents=True`: Creates missing parent directories.
* `exist_ok=True`: Does not raise an error if the directory already exists.

### 4.8 Reading files using `pathlib`
```python
from pathlib import Path

file_path = Path("student.txt")
content = file_path.read_text(encoding="utf-8")
print(content)
```

### 4.9 Writing files using `pathlib`
```python
from pathlib import Path

file_path = Path("student.txt")
file_path.write_text("Welcome to Python", encoding="utf-8")
```
This creates the file if necessary and overwrites it if it already exists.

**For binary files:**
```python
file_path = Path("image.png")
data = file_path.read_bytes()
print(type(data))

file_path.write_bytes(b"Python")
```

### 4.10 Getting file information
Assume the path is `data/student.txt`:
```python
from pathlib import Path

file_path = Path("data/student.txt")

print(file_path.name)    # student.txt
print(file_path.stem)    # student
print(file_path.suffix)  # .txt
print(file_path.parent)  # data
```

| Property | Description |
| :--- | :--- |
| `name` | File name with extension |
| `stem` | File name without extension |
| `suffix` | File extension |
| `parent` | Parent directory |

### 4.11 Listing files in a directory
```python
from pathlib import Path

folder = Path("data")

# List all items
for file in folder.iterdir():
    print(file)

# List only Python files
for file in folder.glob("*.py"):
    print(file)

# Search recursively
for file in folder.rglob("*.py"):
    print(file)
```

### 4.12 Renaming and deleting files
```python
from pathlib import Path

# Rename
old_path = Path("old.txt")
new_path = Path("new.txt")
old_path.rename(new_path)

# Delete a file
file_path = Path("new.txt")
file_path.unlink()

# Delete an empty directory
folder = Path("students")
folder.rmdir()
```
> **Warning:** Deleting files and directories is a destructive operation.

**When should you use `pathlib`?**
* Building file paths.
* Checking whether files exist.
* Creating directories.
* Searching for files.
* Reading or writing simple files.
* Developing cross-platform applications.

---

## 5. JSON Serialization and Deserialization

### 5.1 What is JSON?
JSON stands for **JavaScript Object Notation**. It is a lightweight data-interchange format used to store and exchange structured data in REST APIs, web applications, configuration files, ML applications, and database exports.

**Example JSON:**
```json
{
    "name": "Rahul",
    "age": 22,
    "course": "Python",
    "skills": ["Java", "Python", "SQL"]
}
```

**JSON basic data types:**

| JSON type | Example |
| :--- | :--- |
| String | `"Rahul"` |
| Number | `22`, `85.5` |
| Boolean | `true`, `false` |
| Null | `null` |
| Array | `[10, 20, 30]` |
| Object | `{"name": "Rahul"}` |

Note that JSON uses lowercase `true`, `false`, and `null`.

### 5.2 What is serialization?
Serialization is the process of converting a Python object into a format that can be stored or transmitted (e.g., converting a Python dictionary into a JSON string using `json.dumps()`).

### 5.3 What is deserialization?
Deserialization is the reverse process—converting JSON data back into Python objects (e.g., using `json.loads()`).

### 5.4 The `json` module
Python provides a built-in module named `json`:

```python
import json
```

| Method | Purpose |
| :--- | :--- |
| `json.dumps()` | Python object $\rightarrow$ JSON string |
| `json.loads()` | JSON string $\rightarrow$ Python object |
| `json.dump()` | Python object $\rightarrow$ JSON file |
| `json.load()` | JSON file $\rightarrow$ Python object |

### 5.5 Using `json.dumps()`
Converts a Python object into a JSON string.

```python
import json

student = {
    "name": "Rahul",
    "age": 22,
    "course": "Python"
}

json_data = json.dumps(student)
print(json_data)
print(type(json_data))
```

**Output:**
```text
{"name": "Rahul", "age": 22, "course": "Python"}
<class 'str'>
```

#### Pretty-printing JSON
For readable formatting, use `indent` (and optionally `sort_keys`):
```python
json_data = json.dumps(student, indent=4, sort_keys=True)
print(json_data)
```

### 5.6 Using `json.loads()`
Converts a JSON string into a Python object.

```python
import json

json_data = '''
{
    "name": "Rahul",
    "age": 22,
    "course": "Python"
}
'''

student = json.loads(json_data)
print(student)
print(type(student))
print(student["name"])
print(student["age"])
```

### 5.7 Writing JSON data into a file using `json.dump()`
The `dump()` method writes a Python object directly into a JSON file.

```python
import json

student = {
    "name": "Rahul",
    "age": 22,
    "course": "Python",
    "skills": ["Java", "Python", "SQL"]
}

with open("student.json", "w", encoding="utf-8") as file:
    json.dump(student, file, indent=4)
```

### 5.8 Reading JSON data from a file using `json.load()`
```python
import json

with open("student.json", "r", encoding="utf-8") as file:
    student = json.load(file)

print(student)
print(student["name"])
print(student["skills"])
```

### 5.9 Python-to-JSON type conversion

| Python type | JSON type |
| :--- | :--- |
| `dict` | Object |
| `list`, `tuple` | Array |
| `str` | String |
| `int`, `float` | Number |
| `True` | `true` |
| `False` | `false` |
| `None` | `null` |

> **Note:** A Python `set` is not directly JSON-serializable. You must convert it to a supported type, such as a `list`:
> ```python
> skills = {"Python", "Java", "SQL"}
> json_data = json.dumps(list(skills))
> ```

### 5.10 Handling JSON errors
Invalid JSON strings raise `JSONDecodeError`:
```python
import json

data = '{"name": "Rahul", "age": }'

try:
    student = json.loads(data)
except json.JSONDecodeError:
    print("Invalid JSON format")
```

### 5.11 Practical example: Student management system
```python
import json

students = [
    {"id": 1, "name": "Rahul", "marks": 85},
    {"id": 2, "name": "Priya", "marks": 92}
]

# Store student records
with open("students.json", "w", encoding="utf-8") as file:
    json.dump(students, file, indent=4)

# Read student records
with open("students.json", "r", encoding="utf-8") as file:
    data = json.load(file)

# Display student information
for student in data:
    print(student["name"], student["marks"])
```

> **Real-world application:** In an AI project like CareerMind, JSON can be used to store extracted resume information, skill lists, job-matching results, and structured outputs from AI agents.

---

## 6. CSV Files

### 6.1 What is CSV?
CSV stands for **Comma-Separated Values**. It is a file format used to store tabular data where each line represents a row and values are usually separated by commas.

**Example `students.csv`:**
```csv
id,name,age,marks
1,Rahul,22,85
2,Priya,23,92
3,Arjun,21,78
```

Python provides a built-in module named `csv`:
```python
import csv
```

### 6.2 Reading CSV files using `csv.reader()`
```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

**Output:**
```python
['id', 'name', 'age', 'marks']
['1', 'Rahul', '22', '85']
['2', 'Priya', '23', '92']
['3', 'Arjun', '21', '78']
```
Each row is returned as a list of strings.

### 6.3 Skipping the header
Use `next()` to skip the header row:
```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file)
    next(reader)
    for row in reader:
        print(row)
```

### 6.4 Reading CSV using `csv.DictReader()`
`DictReader()` reads each row as a dictionary, using the header names as keys.

```python
import csv

with open("students.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row["name"], row)
```
> **Note:** The values are still strings. Convert them (`int()`, `float()`) when numerical operations are required.

### 6.5 Writing CSV files using `csv.writer()`
```python
import csv

with open("students.csv", "w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)
    writer.writerow(["id", "name", "age", "marks"])
    writer.writerow([1, "Rahul", 22, 85])
    writer.writerow([2, "Priya", 23, 92])
    writer.writerow([3, "Arjun", 21, 78])
```

#### `writerow()` vs `writerows()`
* `writerow()` writes one row: `writer.writerow([1, "Rahul", 22])`
* `writerows()` writes multiple rows at once:
  ```python
  rows = [
      [1, "Rahul", 22],
      [2, "Priya", 23],
      [3, "Arjun", 21]
  ]
  writer.writerows(rows)
  ```

### 6.6 Writing CSV using `csv.DictWriter()`
`DictWriter()` allows us to write dictionaries directly:
```python
import csv

students = [
    {"id": 1, "name": "Rahul", "marks": 85},
    {"id": 2, "name": "Priya", "marks": 92},
    {"id": 3, "name": "Arjun", "marks": 78}
]

with open("students.csv", "w", newline="", encoding="utf-8") as file:
    fieldnames = ["id", "name", "marks"]
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(students)
```

### 6.7 Appending data to a CSV file
Use append mode (`a`):
```python
import csv

with open("students.csv", "a", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)
    writer.writerow([4, "Sneha", 88])
```

### 6.8 Handling different delimiters
CSV files sometimes use semicolons (`;`), tabs (`\t`), or pipes (`|`):
```python
import csv

with open("data.csv", "r", newline="", encoding="utf-8") as file:
    reader = csv.reader(file, delimiter=";")
    for row in reader:
        print(row)
```

### 6.9 Handling quoted values
CSV fields may contain commas inside quoted values:
```csv
name,address
Rahul,"Hyderabad, Telangana"
Priya,"Chennai, Tamil Nadu"
```
The `csv` module handles this automatically. Avoid manually splitting CSV rows with `line.split(",")`, because commas inside quoted fields will break the parsing.

### 6.10 CSV vs JSON

| Feature | CSV | JSON |
| :--- | :--- | :--- |
| **Structure** | Rows and columns | Nested objects and arrays |
| **Data representation** | Tabular | Hierarchical |
| **Human readability** | Simple | Simple |
| **Supports nested data** | Not naturally | Yes |
| **Common use** | Spreadsheets and datasets | APIs and application data |
| **Python module** | `csv` | `json` |

---

## 7. `datetime`, `date`, `time` and `timedelta`

### 7.1 What is `datetime`?
Python provides the `datetime` module to work with dates and times.

```python
from datetime import datetime, date, time, timedelta
```

| Class | Purpose |
| :--- | :--- |
| `date` | Represents a calendar date |
| `time` | Represents a time of day |
| `datetime` | Represents both date and time |
| `timedelta` | Represents a duration or difference |

### 7.2 Working with `date`
```python
from datetime import date

today = date.today()
print(today)  # e.g., 2026-11-17

birthday = date(2002, 5, 15)
print(birthday.year, birthday.month, birthday.day)  # 2002 5 15
```

#### Getting the weekday
`weekday()` returns `0` for Monday through `6` for Sunday. To get the weekday name:
```python
print(today.strftime("%A"))
```

### 7.3 Working with `time`
Represents a clock time (not an elapsed duration):
```python
from datetime import time

meeting_time = time(14, 30, 45)
print(meeting_time)  # 14:30:45
print(meeting_time.hour, meeting_time.minute, meeting_time.second)
```

### 7.4 Working with `datetime`
Combines a date and time:
```python
from datetime import datetime

current = datetime.now()
print(current)

event = datetime(2026, 11, 20, 10, 30, 0)
print(event)
```

### 7.5 Working with `timedelta`
`timedelta` represents a duration or difference between dates and times.

```python
from datetime import datetime, date, timedelta

today = datetime.now()
future_date = today + timedelta(days=7)
past_date = date.today() - timedelta(days=5)
future_time = today + timedelta(hours=2, minutes=30)

# Difference between two dates
start_date = date(2026, 1, 1)
end_date = date(2026, 11, 17)
difference = end_date - start_date
print(difference.days)  # 320
```

### 7.6 Calculating age
```python
from datetime import date

birth_date = date(2002, 5, 15)
today = date.today()

age = today.year - birth_date.year
if (today.month, today.day) < (birth_date.month, birth_date.day):
    age -= 1

print("Age:", age)
```

### 7.7 Comparing dates
```python
from datetime import date

date1 = date(2026, 11, 17)
date2 = date(2026, 12, 1)

if date1 < date2:
    print("Date1 is earlier")
else:
    print("Date1 is later")
```

### 7.8 Difference between `date`, `time`, `datetime` and `timedelta`

| Class | Example | Represents |
| :--- | :--- | :--- |
| `date` | `2026-11-17` | Calendar date |
| `time` | `15:30:00` | Clock time |
| `datetime` | `2026-11-17 15:30:00` | Date and time |
| `timedelta` | `7 days, 0:00:00` | Duration |

---

## 8. Date Formatting and Parsing

### 8.1 What is date formatting?
Date formatting converts a Python `date` or `datetime` object into a readable string using `strftime()` (*string format time*).

```python
from datetime import datetime

current = datetime.now()
formatted = current.strftime("%d-%m-%Y")
print(formatted)  # e.g., 17-11-2026
```

### 8.2 Common `strftime` directives

| Directive | Meaning | Example |
| :--- | :--- | :--- |
| `%Y` | Four-digit year | `2026` |
| `%y` | Two-digit year | `26` |
| `%m` | Month number | `11` |
| `%B` | Full month name | `November` |
| `%b` | Short month name | `Nov` |
| `%d` | Day of month | `17` |
| `%A` | Full weekday name | `Tuesday` |
| `%a` | Short weekday name | `Tue` |
| `%H` | Hour in 24-hour format | `15` |
| `%I` | Hour in 12-hour format | `03` |
| `%M` | Minute | `20` |
| `%S` | Second | `30` |
| `%p` | AM/PM | `PM` |
| `%f` | Microsecond | `123456` |
| `%j` | Day of year | `321` |
| `%z` | UTC offset | `+0530` |
| `%Z` | Time zone name | `IST` (if available) |
| `%%` | Literal percent sign | `%` |

### 8.3 Different date formats
```python
from datetime import datetime

current = datetime.now()

print(current.strftime("%d-%m-%Y"))          # 17-11-2026
print(current.strftime("%Y/%m/%d"))          # 2026/11/17
print(current.strftime("%B %d, %Y"))         # November 17, 2026
print(current.strftime("%A, %B %d, %Y"))     # Tuesday, November 17, 2026
print(current.strftime("%I:%M %p"))          # 03:20 PM
```

### 8.4 What is date parsing?
Date parsing converts a date string into a Python `datetime` object using `strptime()` (*string parse time*). The format passed to `strptime()` must match the input string.

```python
from datetime import datetime

date_string = "17-11-2026"
date_object = datetime.strptime(date_string, "%d-%m-%Y")

print(date_object)        # 2026-11-17 00:00:00
print(type(date_object))  # <class 'datetime.datetime'>
```

### 8.5 Different parsing examples
```python
from datetime import datetime

# DD-MM-YYYY
d1 = datetime.strptime("17-11-2026", "%d-%m-%Y")

# YYYY/MM/DD
d2 = datetime.strptime("2026/11/17", "%Y/%m/%d")

# Date and time
d3 = datetime.strptime("17-11-2026 03:30 PM", "%d-%m-%Y %I:%M %p")
```

### 8.6 Difference between `strftime()` and `strptime()`

| Feature | `strftime()` | `strptime()` |
| :--- | :--- | :--- |
| **Purpose** | Formatting | Parsing |
| **Input** | Date/datetime object | Date string |
| **Output** | String | Datetime object |
| **Direction** | Object $\rightarrow$ String | String $\rightarrow$ Object |

### 8.7 Handling invalid date strings
```python
from datetime import datetime

date_string = "35-15-2026"

try:
    result = datetime.strptime(date_string, "%d-%m-%Y")
    print(result)
except ValueError:
    print("Invalid date format or date value")
```

### 8.8 Working with time zones
A `datetime` can be **naive** (no time-zone info) or **aware** (includes time-zone info).

```python
from datetime import datetime, timezone
from zoneinfo import ZoneInfo

# UTC aware
current_utc = datetime.now(timezone.utc)
print(current_utc)

# Specific time zone
india_time = datetime.now(ZoneInfo("Asia/Kolkata"))
print(india_time)
```
> **Important:** Avoid assuming that a naive datetime is UTC or local time. Be explicit about time zones when handling international events, deadlines, and API timestamps.

---

## 9. Environment Variables

### 9.1 What are environment variables?
Environment variables are named values stored outside the source code and made available to running applications (e.g., API keys, database credentials, server ports, debug flags).

**Why use environment variables?**
* Prevents accidental credential leaks to GitHub.
* Allows different configurations across environments (dev, staging, prod).
* Updates configuration without modifying source code.

### 9.2 Accessing environment variables using `os`
```python
import os

api_key = os.environ.get("API_KEY")
print(api_key)  # Returns None if not defined
```

### 9.3 Setting environment variables in Python
```python
import os

os.environ["APP_NAME"] = "CareerMind"
print(os.environ.get("APP_NAME"))  # CareerMind
```
*(Note: This only affects the current process and its child processes.)*

### 9.4 Difference between `os.environ` and `os.getenv()`

| Feature | `os.getenv()` | `os.environ[]` |
| :--- | :--- | :--- |
| **Access** | Returns variable value | Returns variable value |
| **Missing variable** | Returns `None` by default | Raises `KeyError` |
| **Default value** | Supported (`os.getenv("KEY", "default")`) | Can use `.get()` |
| **Use case** | Optional configuration | Required configuration |

### 9.5 Setting environment variables in the terminal
* **Windows Command Prompt:** `set API_KEY=my_secret_key`
* **Windows PowerShell:** `$env:API_KEY = "my_secret_key"`
* **Linux/macOS:** `export API_KEY="my_secret_key"`

### 9.6 Using a `.env` file
A `.env` file stores environment configuration locally:
```env
API_KEY=my_secret_key
DATABASE_URL=postgresql://localhost:5432/mydb
DEBUG=True
APP_NAME=CareerMind
```

Install `python-dotenv` to load `.env` files into Python:
```bash
pip install python-dotenv
```

```python
from dotenv import load_dotenv
import os

load_dotenv()

api_key = os.getenv("API_KEY")
database_url = os.getenv("DATABASE_URL")
```

### 9.7 Protecting environment variables
1. Add `.env` to your `.gitignore` file so secrets are never pushed to version control:
   ```gitignore
   .env
   ```
2. Commit a `.env.example` file with placeholder values for other developers:
   ```env
   API_KEY=your_api_key_here
   DATABASE_URL=your_database_url_here
   DEBUG=False
   ```

> **Security Note:** Environment variables reduce accidental hardcoding, but they are not a complete secret-management system. Protect access to the machine, deployment environment, logs, and process configuration, and use a dedicated secret manager for sensitive production credentials.

### 9.8 Practical example: Using an API key
```python
import os
from dotenv import load_dotenv

load_dotenv()

api_key = os.getenv("GROQ_API_KEY")

if not api_key:
    raise ValueError("GROQ_API_KEY is not configured")

print("API key loaded successfully")
```

---

## 10. Integrated Practical Project: Student Record Management System

### Project structure
```text
StudentManagement/
│
├── main.py
├── data/
│   ├── students.json
│   └── students.csv
├── .env
└── .gitignore
```

### Complete Python program (`main.py`)
```python
import json
import csv
import os
from pathlib import Path
from datetime import datetime
from dotenv import load_dotenv

# Load environment variables
load_dotenv()
APP_NAME = os.getenv("APP_NAME", "Student Management System")

# Create project directory
DATA_DIR = Path("data")
DATA_DIR.mkdir(parents=True, exist_ok=True)

JSON_FILE = DATA_DIR / "students.json"
CSV_FILE = DATA_DIR / "students.csv"

# Student records
students = [
    {"id": 1, "name": "Rahul", "age": 22, "marks": 85},
    {"id": 2, "name": "Priya", "age": 23, "marks": 92},
    {"id": 3, "name": "Arjun", "age": 21, "marks": 78}
]

# Save records in JSON
with open(JSON_FILE, "w", encoding="utf-8") as file:
    json.dump(students, file, indent=4)

# Read records from JSON
with open(JSON_FILE, "r", encoding="utf-8") as file:
    records = json.load(file)

# Export records to CSV
with open(CSV_FILE, "w", newline="", encoding="utf-8") as file:
    fieldnames = ["id", "name", "age", "marks"]
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(records)

# Display records
print("Application:", APP_NAME)
print("\nStudent Records:")
for student in records:
    print(student["id"], student["name"], student["age"], student["marks"])

# Display current date and time
current_time = datetime.now()
print("\nGenerated on:", current_time.strftime("%d-%m-%Y %I:%M %p"))
print("\nFiles created successfully!")
```

---

## 11. Important Differences – Quick Revision

| Concept | Main purpose | Important methods |
| :--- | :--- | :--- |
| **File handling** | Read and write files | `open()`, `read()`, `write()` |
| **File modes** | Control file access | `r`, `w`, `a`, `x`, `rb`, `wb` |
| **Context manager** | Manage resources automatically | `with`, `__enter__()`, `__exit__()` |
| **`pathlib`** | Manage file and directory paths | `Path()`, `exists()`, `mkdir()`, `glob()` |
| **JSON** | Store structured data | `dump()`, `load()`, `dumps()`, `loads()` |
| **CSV** | Work with tabular data | `reader()`, `writer()`, `DictReader()` |
| **`datetime`** | Work with dates and times | `now()`, `today()` |
| **`timedelta`** | Calculate durations | `days`, `seconds`, arithmetic |
| **Date formatting** | Convert date objects to strings | `strftime()` |
| **Date parsing** | Convert strings to datetime objects | `strptime()` |
| **Environment variables** | Manage configuration | `os.getenv()`, `os.environ` |

---

## 12. Common Mistakes Beginners Should Avoid

| Mistake | Correct approach |
| :--- | :--- |
| Forgetting to close files | Use `with open(...)` |
| Using `w` when you want to preserve content | Use `a` |
| Reading a nonexistent file | Check existence or handle `FileNotFoundError` |
| Reading images in text mode | Use binary mode (`rb`) |
| Assuming `write()` adds newlines | Add `\n` explicitly |
| Using `json.loads()` on a file object | Use `json.load()` |
| Using `json.load()` on a string | Use `json.loads()` |
| Splitting CSV rows using commas manually | Use the `csv` module |
| Passing the wrong date format to `strptime()` | Match the format to the input |
| Hardcoding API keys | Use environment variables |
| Assuming `.env` loads automatically | Use `python-dotenv` or another loader |

---

## 13. Interview Questions and Answers

1. **What is file handling in Python?**  
   File handling is the process of creating, opening, reading, writing, appending, and closing files using Python.
2. **What is the difference between `w` and `a` modes?**  
   `w` overwrites existing content, whereas `a` preserves existing content and adds new content at the end.
3. **What is the difference between `read()` and `readline()`?**  
   `read()` reads the entire file or a specified number of characters, while `readline()` reads one line at a time.
4. **Why is the `with` statement used?**  
   It automatically manages resources and ensures that files are closed after the block finishes, even if an exception occurs.
5. **What is `pathlib`?**  
   `pathlib` is a standard library module that provides an object-oriented way to work with file and directory paths.
6. **What is JSON serialization?**  
   Serialization converts Python objects into JSON-compatible data, commonly represented as a JSON string or stored in a JSON file.
7. **What is the difference between `dump()` and `dumps()`?**  
   `dump()` writes JSON data to a file; `dumps()` converts Python data into a JSON string.
8. **What is the difference between `load()` and `loads()`?**  
   `load()` reads JSON data from a file-like object; `loads()` parses a JSON string.
9. **What is the difference between CSV and JSON?**  
   CSV represents flat tabular data, while JSON supports nested structured data.
10. **What is the difference between `strftime()` and `strptime()`?**  
    `strftime()` converts datetime objects into formatted strings; `strptime()` converts formatted strings into datetime objects.
11. **What is `timedelta`?**  
    `timedelta` represents a duration or difference between two dates or datetime values.
12. **What are environment variables?**  
    Environment variables are external configuration values made available to applications at runtime.
13. **What is the difference between `os.getenv()` and `os.environ[]`?**  
    `os.getenv()` returns `None` by default if a variable is missing, whereas accessing a missing key through `os.environ[]` raises a `KeyError`.
14. **Why should API keys not be hardcoded?**  
    Hardcoded credentials can accidentally be exposed through source code, repositories, or shared files. Environment variables and secret-management systems provide safer configuration practices.

---

## 14. Practical Exercises

- [ ] **1. Write and read a text file:** Create a file named `notes.txt`, write five lines into it, and read the contents.
- [ ] **2. Count words in a file:** Read a text file and calculate the total number of words.
- [ ] **3. Copy a file:** Copy the contents of one text file into another using a context manager.
- [ ] **4. Student JSON records:** Create a list of five student dictionaries and save them into `students.json`. Read and display them.
- [ ] **5. CSV marks analysis:** Read student marks from a CSV file and calculate the average marks.
- [ ] **6. File and folder management:** Use `pathlib` to create a folder, check whether a file exists, and list all `.txt` files.
- [ ] **7. Date calculator:** Ask the user for a date of birth and calculate their age.
- [ ] **8. Date formatting:** Convert a date string in `DD-MM-YYYY` format into `YYYY/MM/DD` format.
- [ ] **9. Environment configuration:** Read `APP_NAME` and `DEBUG` from environment variables and display their values.
- [ ] **10. Mini project:** Build a student record manager that saves data in JSON and exports it to CSV.

---

## 15. Recommended Learning Order

1. **File basics:** Understand `open()`, `read()`, `write()`, `close()`, and file modes.
2. **Context managers:** Learn why `with` is preferred and how exceptions are handled.
3. **Path management:** Practice `pathlib` for working with files and folders.
4. **Structured data:** Learn JSON serialization/deserialization and CSV processing.
5. **Date and time:** Understand `date`, `time`, `datetime`, `timedelta`, formatting, and parsing.
6. **Application configuration:** Learn environment variables and `.env` files.
7. **Mini project:** Build a file-based student management system using JSON, CSV, and `pathlib`.

> **Final takeaway:** These topics are essential for backend development, data science, automation, and AI application development. Once you understand them, you can build Python programs that read real-world data, process it, store results, and securely manage application configuration.