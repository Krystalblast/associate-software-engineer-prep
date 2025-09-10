# Python Debugging Cheat Sheet

> Quick reference for debugging techniques in Python, with official documentation links.

---

## 1. Print & Logging

### Print debugging
```python
x = 10
y = 0
print("x =", x, "y =", y)
```

### Logging (better for real projects)
```python
import logging
logging.basicConfig(level=logging.DEBUG)
logging.debug("x=%s y=%s", x, y)
```

**Reference:** [logging docs](https://docs.python.org/3/library/logging.html)

---

## 2. Built-in Debugger (`pdb`)

Insert a breakpoint:
```python
def divide(a, b):
    breakpoint()   # or: import pdb; pdb.set_trace()
    return a / b
```

### Common pdb commands
- `n` → next line  
- `s` → step into function  
- `c` → continue execution  
- `p var` → print variable  
- `pp var` → pretty-print variable  
- `b 12` → set breakpoint at line 12  
- `w` → show stack trace  
- `q` → quit

Run script with pdb:
```bash
python -m pdb script.py
```

**Reference:** [pdb docs](https://docs.python.org/3/library/pdb.html)

---

## 3. Post-mortem Debugging

Debug after exception:
```python
try:
    risky()
except Exception:
    import pdb; pdb.pm()
```

---

## 4. Tracebacks

Capture and print detailed error info:
```python
import traceback
try:
    1/0
except Exception:
    traceback.print_exc()
```

**Reference:** [traceback docs](https://docs.python.org/3/library/traceback.html)

---

## 5. faulthandler (for crashes)

Enable crash tracebacks:
```python
import faulthandler
faulthandler.enable()
```

Or run with:
```bash
python -X faulthandler script.py
```

**Reference:** [faulthandler docs](https://docs.python.org/3/library/faulthandler.html)

---

## 6. IDE Debuggers

- **VS Code** → breakpoints, call stack, watch variables ([docs](https://code.visualstudio.com/docs/editor/debugging))  
- **PyCharm** → advanced debugger ([docs](https://www.jetbrains.com/help/pycharm/debugging-code.html))

---

## 7. Performance Debugging

### cProfile (profile whole program)
```bash
python -m cProfile script.py
```

### timeit (benchmark small snippets)
```python
import timeit
print(timeit.timeit("sum(range(1000))", number=10000))
```

**Reference:** [profile & cProfile docs](https://docs.python.org/3/library/profile.html) | [timeit docs](https://docs.python.org/3/library/timeit.html)

---

## ✅ Summary

- Use `logging` instead of plain `print()` for scalable debugging.  
- Use `breakpoint()` / `pdb` for interactive step-through.  
- Use `traceback` / `faulthandler` for exception and crash analysis.  
- Use **IDE debuggers** for productivity.  
- Use `cProfile` / `timeit` for performance bottlenecks.

---
