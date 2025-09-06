#Notes
## Define function with `def`
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
  local      -- printed inside inner() called from outer()
  enclosing  -- printed inside outer() after inner() finishes
  global     -- printed outside, using Global variable x // (print(x))
  2          -- printed using Built-in function len() // print(len("hi"))
  ```
---
## Arguments
  - Passed by object reference (call by value of the reference).
  - Each call creates a new local symbol table.
```python
def add(a, b):               # parameters a, b are local to this call
    return a + b

print(add(2, 3))             # Result: 5
print(add(10, 20))           # Result: 30
# Explanation: Each function call creates a new local symbol table.
# Arguments are passed by object reference (values are references to objects).
```
---
## Functions are objects
  - Function name is bound to a function object.
  - Can assign to another variable (alias) and call from it.
```python
def square(x):              # function to return square
    return x * x

f = square                  # assign function to another variable
print(f(5))                 # call using new name
# Result: 25
```
---
## Return value
- If no return → function returns None.
- return can return any object.
```python
def no_return():            # function with no return
    pass                    # does nothing

print(no_return())          # prints return value
# Result: None              # default return is None
```
---
## Return Fibonacci as list
```python
def fib2(n):
    """Return Fibonacci series up to n as a list."""
    result = []             # create empty list
    a, b = 0, 1
    while a < n:
        result.append(a)    # add current value of a into list
        a, b = b, a+b       # update values
    return result           # return the list

print(fib2(30))             # call and print result
# Result: [0, 1, 1, 2, 3, 5, 8, 13, 21]
```
---
## Method 
```python
numbers = []                # empty list
numbers.append(10)          # call list method append()
numbers.append(20)          # add another element
print(numbers)

# Result: [10, 20]
# Explanation: append() is a method of list objects
```
---
## Global keyword (allow assignment to global var)
```python
x = 5

def set_global():
    global x                 # declare x as global
    x = 100                  # change global x

set_global()
print(x)                     # Result: 100
# Explanation: Without `global`, assignment inside function would create a local x.
```
---
## Reference
- [Python 3 Tutorial — 4.8 Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
