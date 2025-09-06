# Python Notes – Section 8: Errors and Exceptions

## 8.0 Overview
- Two kinds of errors: **Syntax Errors** (detected at parse time) and **Exceptions** (detected at runtime).
- Use `try/except/else/finally` to handle exceptions; use `raise` to generate them.

---

## 8.1 Syntax Errors
**Example:**
```python
while True print('Hello world')
```
**Result (abridged):**
```
SyntaxError: invalid syntax
          ^^^^^  # points near where parser got confused (missing ':')
```
**Explanation:** Parser reports filename/line and points near the error. The arrow may be **after** the true mistake.

---

## 8.2 Exceptions
**Example:**
```python
10 * (1/0)      # ZeroDivisionError
4 + spam*3      # NameError
'2' + 2         # TypeError
```
**Result (types shown):**
```
ZeroDivisionError, NameError, TypeError
```
**Explanation:** Runtime errors raise exceptions; traceback shows call stack and error type/detail.

---

## 8.3 Handling Exceptions (`try` / `except` / `else`)
**Pattern:**
```python
while True:
    try:
        x = int(input("Enter a number: "))
        break
    except ValueError:
        print("Not a valid number")
```
**Multiple handlers & order:**
```python
class B(Exception): pass
class C(B): pass
class D(C): pass

for cls in [B, C, D]:
    try:
        raise cls()
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")
# Output: B, C, D
```
**Explanation:** First matching `except` runs; subclass catches don’t match base-first ordering.

**Binding the exception:**
```python
try:
    raise Exception('spam', 'eggs')
except Exception as inst:
    print(type(inst))   # <class 'Exception'>
    print(inst.args)    # ('spam', 'eggs')
    print(inst)         # ('spam', 'eggs')
```
**Best practice:** Catch **specific** exceptions; allow unexpected ones to propagate (or log then `raise`).

**`else` clause:**
```python
import sys
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except OSError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```
**Explanation:** `else` runs only if `try` succeeded—keeps the protected code tight.

**Errors inside called functions are caught too:**
```python
def this_fails():
    return 1/0

try:
    this_fails()
except ZeroDivisionError as err:
    print('Handling run-time error:', err)
# -> Handling run-time error: division by zero
```

---

## 8.4 Raising Exceptions (`raise`)
**Example:**
```python
raise NameError('HiThere')
raise ValueError          # same as ValueError()
```
**Re-raising current exception:**
```python
try:
    raise NameError('HiThere')
except NameError:
    print('An exception flew by!')
    raise
```
**Explanation:** `raise` with no args re-raises the active exception (preserves traceback).

---

## 8.5 Exception Chaining
**Automatic chaining:**
```python
try:
    open("database.sqlite")
except OSError:
    raise RuntimeError("unable to handle error")
```
**Explicit cause (`from`):**
```python
def func():
    raise ConnectionError

try:
    func()
except ConnectionError as exc:
    raise RuntimeError('Failed to open database') from exc
```
**Disable chaining:**
```python
try:
    open('database.sqlite')
except OSError:
    raise RuntimeError from None
```
**Explanation:** `from exc` sets the direct cause; `from None` hides the original cause.

---

## 8.6 User-defined Exceptions
**Example:**
```python
class MyError(Exception):
    """Custom error."""
    pass

def do_something():
    raise MyError("something went wrong")

try:
    do_something()
except MyError as e:
    print(e)
```
**Explanation:** Derive from `Exception` (directly/indirectly). Keep classes simple and end names with `Error`.

---

## 8.7 Defining Clean-up Actions (`finally`)
**Example:**
```python
def divide(x, y):
    try:
        result = x / y
    except ZeroDivisionError:
        print("division by zero!")
    else:
        print("result is", result)
    finally:
        print("executing finally clause")

divide(2, 1)   # result is 2.0; executing finally clause
divide(2, 0)   # division by zero!; executing finally clause
```
**Explanation:** `finally` runs **always** (before control leaves `try`), even if exceptions occur or `return`/`break`/`continue` happen.

**Gotcha:** A `return` in `finally` overrides earlier returns.

---

## 8.8 Predefined Clean-up Actions (Context Managers)
**Bad:**
```python
for line in open("myfile.txt"):
    print(line, end="")
# file may remain open longer than needed
```
**Good (`with`):**
```python
with open("myfile.txt") as f:
    for line in f:
        print(line, end="")
# file is guaranteed closed
```
**Explanation:** Objects that support context management (`__enter__`/`__exit__`) clean up reliably.

---

## 8.9 Raising & Handling Multiple Unrelated Exceptions (PEP 654)
**Raise an `ExceptionGroup`:**
```python
def f():
    excs = [OSError('error 1'), SystemError('error 2')]
    raise ExceptionGroup('there were problems', excs)
```
**Selective handling with `except*`:**
```python
try:
    f()
except* OSError:
    print("There were OSErrors")
except* SystemError:
    print("There were SystemErrors")
```
**Explanation:** `ExceptionGroup` bundles exceptions; `except*` splits and handles matching types. Items must be **instances**.

---

## 8.10 Enriching Exceptions with Notes
**Example:**
```python
try:
    raise TypeError('bad type')
except Exception as e:
    e.add_note('Add some information')
    e.add_note('Add some more information')
    raise
```
**Collecting with context per error:**
```python
def f(): raise OSError('operation failed')

excs = []
for i in range(3):
    try:
        f()
    except Exception as e:
        e.add_note(f'Happened in Iteration {i+1}')
        excs.append(e)

raise ExceptionGroup('We have some problems', excs)
```
**Explanation:** `add_note()` appends human-friendly notes shown after the traceback.

---

## Reference
[Python 3 Tutorial — 8. Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)
