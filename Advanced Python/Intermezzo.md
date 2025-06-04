# Intermezzo: Coding Style in Python

When you start writing longer, more complex Python programs, adopting a consistent coding style is key to making your code readable and maintainable. The **Intermezzo: Coding Style** section in the Python tutorial summarizes many of the best practices that have evolved into the widely accepted [PEP 8 – Style Guide for Python Code](https://peps.python.org/pep-0008/) standards.

Below are the main guidelines with examples to help you understand and apply them in your own code.

---

## 1. Indentation

- **Use 4-space indentation:**  
  Always indent blocks of code with 4 spaces. Do not use tabs, and avoid mixing tabs and spaces.

**Example:**
```python
def greet(name):
    if name:
        print("Hello, " + name)
    else:
        print("Hello, world!")
```

---

## 2. Maximum Line Length

- **Wrap lines to a maximum of 79 characters:**  
  This helps users with small displays and makes side-by-side file comparison easier.

**Example:**
```python
def long_function_name(argument_one, argument_two, argument_three,
                       argument_four):
    # Function body goes here
    pass
```

---

## 3. Blank Lines

- **Separate functions and classes with blank lines:**  
  Use blank lines to visually separate different parts of your code for better readability.

**Example:**
```python
class MyClass:
    
    def method_one(self):
        # Implementation of method one
        pass

    def method_two(self):
        # Implementation of method two
        pass
```

---

## 4. Comments and Docstrings

- **Use comments on their own lines:**  
  Write clear comments to explain why something is done.
  
- **Use docstrings for modules, functions, and classes:**  
  Docstrings help others understand your code’s purpose and usage.

**Example:**
```python
def add(a, b):
    """
    Return the sum of a and b.

    Parameters:
        a (int): The first number.
        b (int): The second number.

    Returns:
        int: The sum of a and b.
    """
    return a + b
```

---

## 5. Whitespace Around Operators and Commas

- **Use spaces around operators and after commas:**  
  This makes expressions easier to read.
- **Avoid extra spaces inside parentheses:**  
  Do not add spaces just after an opening or before a closing bracket.

**Example:**
```python
# Good:
result = (1, 2, 3)
total = 4 + 5

# Not recommended:
bad_tuple = ( 1, 2, 3 )
bad_expression = 4+5
```

---

## 6. Naming Conventions

- **Classes:** Use `CamelCase` (also known as CapWords).
- **Functions and Methods:** Use `lower_case_with_underscores`.
- **Instance Methods:** Always use `self` as the first parameter.

**Example:**
```python
class Person:
    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name

    def full_name(self):
        return f"{self.first_name} {self.last_name}"
```

---

## 7. Avoid Non-ASCII Characters in Identifiers

- **Stick to plain ASCII:**  
  This ensures your code remains universally understandable and avoids issues with different character encodings.

---

## Conclusion

Following these Intermezzo coding style guidelines helps you write Python code that is clean, consistent, and easy for others (and future you) to read and maintain. For more in-depth details, be sure to check out the [official PEP 8 document](https://peps.python.org/pep-0008/) and the Python tutorial's [Intermezzo: Coding Style](https://docs.python.org/3/tutorial/controlflow.html#intermezzo-coding-style).

Happy coding!

