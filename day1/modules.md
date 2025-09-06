# Python Notes – Section 6: Modules

## 6. Modules (Basics)
- A **module** is a `.py` file containing definitions and statements.
- Use `import` to load it into another program.

**Example:**
```python
# fibo.py
def fib(n):
    a, b = 0, 1
    while a < n:
        print(a, end=" ")
        a, b = b, a+b
    print()
```

```python
import fibo
fibo.fib(20)
```
**Result:**  
```
0 1 1 2 3 5 8 13
```

**Explanation:** `fibo` is imported once, functions are accessed with `fibo.func()`.

---

## 6.1 More on Modules
- You can import functions in different ways.

**Example:**
```python
from fibo import fib
fib(20)
```
**Result:**  
```
0 1 1 2 3 5 8 13
```

**Explanation:** Imports the function directly; no need to prefix with `fibo.`.  
⚠️ `from fibo import *` imports everything — discouraged in real code.

---

## 6.1.1 Executing Modules as Scripts
- Code runs differently depending on `__name__`.

**Example:**
```python
# fibo.py
def fib(n): ...
if __name__ == "__main__":
    fib(10)
```

```bash
python fibo.py
```
**Result:**  
```
0 1 1 2 3 5 8
```

**Explanation:** When run directly, `__name__ == "__main__"`.  
When imported, that block does not run.

---

## 6.1.2 Module Search Path
- Python looks for modules in order:  
  1. Current directory  
  2. `PYTHONPATH` environment variable  
  3. Standard library path  

**Example:**
```python
import sys
print(sys.path)
```

**Result:**  
A list of directories where Python searches for modules.

---

## 6.1.3 Compiled Python Files
- Python caches modules in `__pycache__` as `.pyc` files.

**Example:**  
Run `import fibo` → directory gets:
```
__pycache__/fibo.cpython-311.pyc
```

**Explanation:** This speeds up **loading**, not execution.

---

## 6.2 Standard Modules
- Python has many built-in modules.

**Example:**
```python
import sys
print(sys.version)
```

**Result:**  
```
3.11.x (main, ...)
```

**Explanation:** `sys` is a standard module available everywhere.

---

## 6.3 The `dir()` Function
- Lists names defined in a module or namespace.

**Example:**
```python
import fibo, sys
print(dir(fibo))
print(dir(sys)[:5])
```

**Result:**  
```
['__name__', 'fib', 'fib2']
['__breakpointhook__', '__displayhook__', '__doc__', '__excepthook__', ...]
```

**Explanation:** Useful to discover available functions and attributes.

---

## 6.4 Packages
- A way to organize modules in directories with `__init__.py`.

**Example structure:**
```
sound/
    __init__.py
    effects/
        __init__.py
        echo.py
```

**Usage:**
```python
import sound.effects.echo
sound.effects.echo.echofilter(...)
```

**Explanation:** Dotted names represent submodules inside packages.

---

## 6.4.1 Importing * From a Package
- Controlled by `__all__` in `__init__.py`.

**Example (`sound/effects/__init__.py`):**
```python
__all__ = ["echo", "surround"]
```

```python
from sound.effects import *
```
**Result:** Only `echo` and `surround` are imported.

---

## 6.4.2 Intra-package References
- Relative imports using dots.

**Example (`surround.py`):**
```python
from . import echo
from .. import formats
```

**Explanation:** Leading `.` means “current package,” `..` means “parent package.”

---

## 6.4.3 Packages in Multiple Directories
- A package’s `__path__` can be modified to extend search directories.

**Example:**
```python
import sound
print(sound.__path__)
```

**Result:**  
List of directories where Python looks for submodules of `sound`.

---

## Reference
[Python 3 Tutorial — 6. Modules](https://docs.python.org/3/tutorial/modules.html)
