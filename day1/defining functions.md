## Define funtion with `def`
  - Syntax: def name(params):
  - Body must be indented.
  ```python
  def fib(n):                                       # define function named fib with parameter n
      """Print Fibonacci series less than n."""    # docstring
      a, b = 0, 1                                   # initialize first two numbers
      while a < n:                                  # loop until a is less than n
          print(a, end=" ")                         # print current value of a
          a, b = b, a+b                             # update values (Fibonacci formula)
      print()                                       # new line after loop

  fib(20)                                           # call function

  # Result: 0 1 1 2 3 5 8 13
  ```
---
## Docstring
  - First statement inside function body can be a string literal.
  - Used as documentation (`function.__doc__`).
  ```python
  def greet(name):            # function with parameter name
    """Say hello to someone."""  # docstring: describes purpose
    print("Hello,", name)   # print greeting

  print(greet.__doc__)        # access docstring
  # Result: Say hello to someone.
  ```
---
## Local scope
  - Variables inside function are stored in a new local symbol table.
  - Lookup order follows LEGB rule (Local → Enclosing → Global → Built-ins).
  - Cannot assign to global variables directly unless declared with global.

## Scope (LEGB Rule)

Python resolves names following the **LEGB rule**:

- **L = Local** → names defined inside the current function (or lambda)  
- **E = Enclosing** → names in any enclosing function (for nested functions)  
- **G = Global** → names defined at the top level of the script/module  
- **B = Built-in** → names preloaded in Python (e.g., `len`, `print`)  

👉 If a name isn’t found in any of these, Python raises a `NameError`.

### Example
```python
x = "global"        # G

def outer():
    x = "enclosing" # E
    def inner():
        x = "local" # L
        print(x)    # Local
    inner()
    print(x)        # Enclosing

outer()
print(x)            # Global
print(len("hi"))    # Built-in
```
- **Result**
```sql
local
enclosing
global
2
```
