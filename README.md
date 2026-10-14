# 🐍 Python Day 13 — Exception Handling

## 📌 Topics Covered

- What is an Error?
- What is an Exception?
- Why Exception Handling Is Needed
- `try` and `except`
- Handling Multiple Exceptions
- `else` Block
- `finally` Block
- `ZeroDivisionError`
- `ValueError`
- `FileNotFoundError`
- Using Multiple `except` Blocks
- The `raise` Keyword
- Exception Handling with Functions
- Exception Handling with Files
- Practical Cloud/DevOps Examples
- Common Beginner Mistakes

---

## 1. What Is an Error?

An error is a problem in a program that prevents it from working as expected.

Example:

```python
print("Hello"
```

Output:

```text
SyntaxError
```

The closing parenthesis is missing, so Python cannot understand the code.

**Remember:** Syntax errors and exceptions are different. Exception handling is mainly used to handle errors that occur while a program is running.

---

## 2. What Is an Exception?

An exception is an error that occurs while a Python program is running.

Example:

```python
a = 10
b = 0

print(a / b)
```

Output:

```text
ZeroDivisionError: division by zero
```

Python cannot divide a number by zero, so it raises an exception.

Without exception handling, this error stops the normal execution of the program.

---

## 3. Why Do We Need Exception Handling?

Suppose your program reads a file, but the file does not exist.

Without exception handling, the program may stop unexpectedly.

Exception handling helps us handle such problems and display a meaningful message.

For example:

```python
try:
    number = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
```

Output:

```text
Cannot divide by zero
```

The program handles the exception instead of displaying an unhandled error traceback.

---

## 4. The `try` and `except` Blocks

- `try`: Contains code that might raise an exception.
- `except`: Contains code that runs if a matching exception occurs.

### Example

```python
try:
    number = int(input("Enter a number: "))
    print(number)
except ValueError:
    print("Please enter a valid integer")
```

If the user enters:

```text
25
```

Output:

```text
25
```

If the user enters:

```text
hello
```

Output:

```text
Please enter a valid integer
```

**Explanation:** Python cannot convert `"hello"` into an integer, so it raises `ValueError`. The `except` block handles it.

---

## 5. Handling Division Errors

```python
try:
    a = 10
    b = 0

    result = a / b

    print(result)

except ZeroDivisionError:
    print("Division by zero is not allowed")
```

Output:

```text
Division by zero is not allowed
```

The exception is caught, and the program continues after the `try-except` statement.

---

## 6. Handling Multiple Exceptions

A program can produce different types of exceptions.

We can handle them separately.

```python
try:
    a = int(input("Enter first number: "))
    b = int(input("Enter second number: "))

    print(a / b)

except ValueError:
    print("Please enter numbers only")

except ZeroDivisionError:
    print("Second number cannot be zero")
```

### Example 1

Input:

```text
Enter first number: 10
Enter second number: 0
```

Output:

```text
Second number cannot be zero
```

### Example 2

Input:

```text
Enter first number: hello
```

Output:

```text
Please enter numbers only
```

Each `except` block handles a specific exception type.

---

## 7. The `else` Block

The `else` block runs only when the `try` block completes without an exception.

### Example

```python
try:
    number = int(input("Enter a number: "))

except ValueError:
    print("Invalid input")

else:
    print("You entered:", number)
```

If the user enters:

```text
10
```

Output:

```text
You entered: 10
```

If the user enters:

```text
hello
```

Output:

```text
Invalid input
```

**Remember:** `else` runs only when no exception occurs in the associated `try` block.

---

## 8. The `finally` Block

The `finally` block runs whether an exception occurs or not, including when an exception is handled.

It is commonly used for cleanup operations.

### Example

```python
try:
    print("Program started")
    result = 10 / 0

except ZeroDivisionError:
    print("An error occurred")

finally:
    print("Program finished")
```

Output:

```text
Program started
An error occurred
Program finished
```

Even though an exception occurred, the `finally` block executed.

### Simple meaning

```text
try     → Try the code
except  → Handle an exception
else    → Run if no exception occurs
finally → Run cleanup code
```

---

## 9. Understanding `try`, `except`, `else`, and `finally`

```python
try:
    number = int(input("Enter a number: "))

except ValueError:
    print("Invalid number")

else:
    print("Valid number:", number)

finally:
    print("Execution completed")
```

If the user enters `5`:

```text
Valid number: 5
Execution completed
```

If the user enters `hello`:

```text
Invalid number
Execution completed
```

The `else` block is skipped when an exception occurs, but `finally` still runs.

---

## 10. Common Python Exceptions

| Exception | Meaning |
|---|---|
| `ValueError` | A value is unsuitable for an operation, such as converting `"abc"` to an integer |
| `ZeroDivisionError` | Division by zero |
| `FileNotFoundError` | A requested file does not exist |
| `TypeError` | An operation receives an inappropriate type |
| `IndexError` | A list or sequence index is out of range |
| `KeyError` | A dictionary key does not exist |
| `NameError` | A variable name is not defined |

---

## 11. Handling `FileNotFoundError`

Suppose we want to read a file called `server.log`, but it does not exist.

```python
try:
    with open("server.log", "r") as file:
        data = file.read()

    print(data)

except FileNotFoundError:
    print("Server log file was not found")
```

If the file does not exist, output:

```text
Server log file was not found
```

This is useful when Python scripts process log files or configuration files.

---

## 12. Handling `IndexError`

An `IndexError` occurs when we try to access an invalid list index.

```python
servers = ["EC2-1", "EC2-2"]

try:
    print(servers[5])

except IndexError:
    print("Server index does not exist")
```

Output:

```text
Server index does not exist
```

The list has only two items, so index `5` is invalid.

---

## 13. Handling `KeyError`

A `KeyError` occurs when we try to access a dictionary key that does not exist.

```python
server = {
    "name": "EC2-1",
    "status": "Running"
}

try:
    print(server["region"])

except KeyError:
    print("Region information is not available")
```

Output:

```text
Region information is not available
```

Here, the dictionary does not contain the key `"region"`.

**Tip:** If a missing key is an expected possibility, `server.get("region")` is often simpler than handling `KeyError`.

---

## 14. Handling `TypeError`

A `TypeError` can occur when an operation uses incompatible data types.

```python
try:
    result = 10 + "20"
    print(result)

except TypeError:
    print("Cannot add an integer and a string directly")
```

Output:

```text
Cannot add an integer and a string directly
```

We can convert the string to an integer if that is what we intend:

```python
result = 10 + int("20")
print(result)
```

Output:

```text
30
```

---

## 15. Using `raise`

The `raise` keyword allows us to raise an exception intentionally.

### Example

```python
age = -5

if age < 0:
    raise ValueError("Age cannot be negative")
```

Output:

```text
ValueError: Age cannot be negative
```

We use `raise` when a value violates a rule our program requires.

### Practical example

```python
def check_server(status):
    if status not in ["Running", "Stopped"]:
        raise ValueError("Invalid server status")

    return status

print(check_server("Running"))
```

Output:

```text
Running
```

Calling `check_server("Unknown")` raises a `ValueError`.

---

## 16. Exception Handling with Functions

We can place exception handling inside a function.

```python
def divide(a, b):
    try:
        return a / b

    except ZeroDivisionError:
        return "Cannot divide by zero"

print(divide(10, 2))
print(divide(10, 0))
```

Output:

```text
5.0
Cannot divide by zero
```

The function handles the division error and returns a useful result.

---

## 17. Practical Cloud/DevOps Example — Server Status

Suppose we receive server status as user input.

```python
def check_server(status):
    try:
        if status == "Running":
            return "Server is running"

        elif status == "Stopped":
            return "Server is stopped"

        else:
            raise ValueError("Unknown server status")

    except ValueError as error:
        return str(error)

print(check_server("Running"))
print(check_server("Unknown"))
```

Output:

```text
Server is running
Unknown server status
```

This demonstrates input validation and exception handling. It does not connect to AWS or check a real EC2 instance.

---

## 18. Practical Example — Reading a Configuration File

Suppose a script needs to read `config.txt`.

```python
try:
    with open("config.txt", "r") as file:
        configuration = file.read()

except FileNotFoundError:
    print("Configuration file is missing")

else:
    print("Configuration loaded successfully")
    print(configuration)

finally:
    print("Configuration check completed")
```

This program:

1. Tries to read the file.
2. Handles the missing-file exception.
3. Displays the configuration if reading succeeds.
4. Prints a completion message.

The `with` statement automatically closes the file, even if an exception occurs while processing it.

---

## 19. Practical Example — Validate AWS Resource Count

Suppose a script accepts the number of AWS resources to process.

```python
try:
    count = int(input("Enter the number of resources: "))

    if count < 0:
        raise ValueError("Resource count cannot be negative")

except ValueError as error:
    print("Invalid input:", error)

else:
    print("Resources to process:", count)
```

If the user enters `5`:

```text
Resources to process: 5
```

If the user enters `abc`:

```text
Invalid input: invalid literal for int() with base 10: 'abc'
```

If the user enters `-2`:

```text
Invalid input: Resource count cannot be negative
```

This is a basic example of validating data before an automation script uses it.

---

## 20. What Is `except Exception`?

We can use `Exception` to catch many common runtime exceptions.

```python
try:
    result = 10 / 0

except Exception as error:
    print("Something went wrong:", error)
```

Output:

```text
Something went wrong: division by zero
```

However, **prefer catching specific exceptions** such as `ValueError` or `FileNotFoundError` when possible. This makes problems easier to identify and avoids hiding unexpected errors.

Avoid using a bare `except:` unless you have a specific reason, because it can also catch exceptions that normally should not be swallowed.

---

## 21. Common Beginner Mistakes

### Mistake 1: Incorrect indentation

Incorrect:

```python
try:
print(10 / 0)
```

Correct:

```python
try:
    print(10 / 0)
except ZeroDivisionError:
    print("Cannot divide by zero")
```

### Mistake 2: Using the wrong exception type

```python
try:
    number = int("hello")

except ZeroDivisionError:
    print("Error")
```

This does not handle the `ValueError` raised by `int("hello")`.

Correct:

```python
try:
    number = int("hello")

except ValueError:
    print("Invalid number")
```

### Mistake 3: Catching every error without understanding it

Avoid:

```python
try:
    # Program code
    pass

except:
    print("Error")
```

Prefer handling the specific exception you expect.

### Mistake 4: Forgetting that `finally` is for cleanup

Use `finally` for cleanup tasks that should run whether the operation succeeds or fails. For files, `with open()` is usually the simplest approach.

---

## 22. Practice Questions

### Practice 1
Write a program that divides two numbers and handles division by zero.

### Practice 2
Ask the user to enter an integer. Handle invalid input using `ValueError`.

### Practice 3
Try to read a file called `data.txt`. Handle `FileNotFoundError`.

### Practice 4
Create a function that accepts a server status and raises `ValueError` if the status is invalid.

### Practice 5
Write a program using `try`, `except`, `else`, and `finally`.

### Practice 6
Create a list of server names and handle an invalid index using `IndexError`.

---

## 23. Day 13 Summary

Exception handling helps Python programs respond to errors instead of stopping unexpectedly.

### `try`

```python
try:
    print(10 / 2)
```

Contains code that might raise an exception.

### `except`

```python
except ZeroDivisionError:
    print("Cannot divide by zero")
```

Handles a matching exception.

### `else`

```python
else:
    print("No exception occurred")
```

Runs when the `try` block completes without an exception.

### `finally`

```python
finally:
    print("Execution completed")
```

Runs whether an exception occurs or not, including when the exception is handled.

### `raise`

```python
raise ValueError("Invalid value")
```

Raises an exception intentionally.

---

## ✅ Day 13 Checklist

- [ ] Understand errors and exceptions
- [ ] Understand `try` and `except`
- [ ] Handle `ValueError`
- [ ] Handle `ZeroDivisionError`
- [ ] Handle `FileNotFoundError`
- [ ] Handle `IndexError` and `KeyError`
- [ ] Use multiple `except` blocks
- [ ] Understand the `else` block
- [ ] Understand the `finally` block
- [ ] Use the `raise` keyword
- [ ] Handle exceptions inside functions
- [ ] Validate user input
- [ ] Practice file handling with exceptions
- [ ] Apply exception handling to Cloud/DevOps examples

---

## 🚀 Key Takeaway

**Exception handling allows Python programs to detect and handle runtime problems in a controlled way.**

It is especially useful in Cloud/DevOps automation when:

- A log or configuration file is missing.
- User input is invalid.
- Resource information is incomplete.
- An operation fails and needs a useful error message.

The most important pattern to remember is:

```python
try:
    # Code that might fail
    pass

except ValueError:
    # Handle invalid values
    print("Invalid input")
```

## 📅 Day 14 Preview

**Revision + Mini Project**

You will revise Python fundamentals and combine your knowledge of variables, conditions, loops, collections, functions, modules, file handling, and exception handling in a small project.
