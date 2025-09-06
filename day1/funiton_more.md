# Notes: More on Defining Functions

## Defaul Argument Value
  - You can give parameters default values → function can be called with fewer arguments.
  - **Defaults are evaluated at definition time**, not call time.
  - Be careful with mutable defaults (`[]`, `{}`) → they persist across calls.

### Basic Example
```python
def ask_ok(prompt, retries=4, reminder='Please try again!'):
    while True:
        reply = input(prompt)
        if reply in {'y', 'yes'}:
            return True
        if reply in {'n', 'no'}:
            return False
        retries -= 1
        if retries < 0:
            raise ValueError('invalid user response')
        print(reminder)

# Different ways to call
ask_ok('Continue?')                           # only required arg
ask_ok('Continue?', 2)                        # with retries
ask_ok('Continue?', 2, 'Yes or No only!')    # all args
```

### Mutable Default Warning ⚠️
```python
# DON'T DO THIS - mutable default
def bad_function(a, L=[]):
    L.append(a)
    return L

print(bad_function(1))    # [1]
print(bad_function(2))    # [1, 2] - shared list!

# DO THIS INSTEAD
def good_function(a, L=None):
    if L is None:
        L = []
    L.append(a)
    return L
```

---

## Keyword Arguments
- Call functions with `kw=value`.
- Positional args must come first.
- No parameter can be assigned more than once.
- Extra args: `*args` (tuple), `**kwargs` (dict).
  
### Basic Usage
```python
def parrot(voltage, state='stiff', action='voom', type='Blue'):
    print(f"Voltage: {voltage}")
    print(f"State: {state}")
    print(f"Action: {action}")
    print(f"Type: {type}")

# Valid calls
parrot(1000)                                    # positional
parrot(voltage=1000)                           # keyword
parrot(1000, action='BOOM')                    # mixed
parrot(action='BOOM', voltage=1000)            # order doesn't matter
```

### *args and **kwargs
```python
def cheeseshop(kind, *arguments, **keywords):
    print(f"Kind: {kind}")
    for arg in arguments:
        print(f"Extra: {arg}")
    for key, value in keywords.items():
        print(f"{key}: {value}")

cheeseshop("Cheddar", 
          "Very sharp", 
          "Aged 5 years",
          brand="Fancy",
          price=15.99)
```

---

## Parameter Types
  - `/` → positional-only params.
  - `*` → keyword-only params.
    
### Syntax Overview
```python
def function(pos_only, /, pos_or_kwd, *, kwd_only):
    pass
#            |           |              |
#   Positional only   |         Keyword only
#                Positional or keyword
```

### Examples
```python
def pos_only(arg, /):
    print(arg)

def kwd_only(*, arg):
    print(arg)

def combined(pos_only, /, standard, *, kwd_only):
    print(pos_only, standard, kwd_only)

# Usage
pos_only(1)                           # ✓ Works
# pos_only(arg=1)                     # ✗ Error

# kwd_only(1)                         # ✗ Error  
kwd_only(arg=1)                       # ✓ Works

combined(1, 2, kwd_only=3)            # ✓ Works
combined(1, standard=2, kwd_only=3)   # ✓ Works
```

---

###Arbitrary Argument Lists
  - Use `*args` for any number of positional arguments.
  - Keyword-only arguments can follow.

```python
def concat(*args, sep="/"):
    return sep.join(args)

print(concat("earth", "mars", "venus"))       # earth/mars/venus
print(concat("earth", "mars", "venus", sep="."))  # earth.mars.venus

```
---

## Argument Unpacking
  - Use `*` to unpack sequences, `**` to unpack dictionaries.
    
### List/Tuple Unpacking
```python
def greet(first, last):
    print(f"Hello {first} {last}")

names = ["John", "Doe"]
greet(*names)  # Same as greet("John", "Doe")

# Range example
args = [3, 6]
list(range(*args))  # [3, 4, 5]
```

### Dictionary Unpacking
```python
def parrot(voltage, state='stiff', action='voom'):
    print(f"Voltage: {voltage}, State: {state}, Action: {action}")

params = {"voltage": 1000, "state": "dead", "action": "VOOM"}
parrot(**params)
```

---

## Lambda Functions
  - Anonymous, single-expression functions.
  - Useful as short functions or sort keys.
    
### Basic Lambda
```python
# Regular function
def add(a, b):
    return a + b

# Lambda equivalent
add_lambda = lambda a, b: a + b

print(add_lambda(5, 3))  # 8
```

### Common Use Cases
```python
# With sort()
pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
pairs.sort(key=lambda x: x[1])  # Sort by second element
print(pairs)  # [(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]

# With map()
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# Closure example
def make_incrementor(n):
    return lambda x: x + n

add_10 = make_incrementor(10)
print(add_10(5))  # 15
```

---

## Function Annotations
  - Stored in `__annotations__`.
  - No runtime effect.
    
### Type Hints
```python
def greet(name: str, age: int = 25) -> str:
    return f"Hello {name}, you are {age} years old"

def calculate(x: float, y: float) -> float:
    return x * y

# Annotations are stored in __annotations__
print(greet.__annotations__)
# {'name': <class 'str'>, 'age': <class 'int'>, 'return': <class 'str'>}
```

---

## Documentation Strings
Multi-line strings that document what your function does.
  - First line: short summary.
  - Second line blank.
  - More detail follows.
  - 
### Docstring Format
```python
def calculate_area(radius):
    """Calculate the area of a circle.
    
    Args:
        radius (float): The radius of the circle
        
    Returns:
        float: The area of the circle
        
    Raises:
        ValueError: If radius is negative
    """
    if radius < 0:
        raise ValueError("Radius cannot be negative")
    return 3.14159 * radius ** 2

print(calculate_area(5))  # 78.53975

# Access docstring
print(calculate_area.__doc__)
# Output:
# Calculate the area of a circle.
# 
#     Args:
#         radius (float): The radius of the circle
#         
#     Returns:
#         float: The area of the circle
#         
#     Raises:
#         ValueError: If radius is negative
```

---

## Intermezzo: Coding Style (PEP 8 Key Points)

  - Indentation: **4 spaces**, no tabs.
  - Line length ≤ **79 chars**.
  - Use blank lines between functions, classes, and large code blocks.
  - Comments should be on their own line.
  - Use **docstrings**.
  - Spaces around operators and after commas: `a = f(1, 2) + g(3, 4)`.
  - Naming:
    - Classes → `UpperCamelCase`
    - Functions/variables → `lowercase_with_underscores`
    - First arg in methods → `self`
  - Use UTF-8/ASCII for code; avoid non-ASCII identifiers in shared projects.
---

## Reference
- [Python 3 Tutorial — More on Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#more-on-defining-functions)

