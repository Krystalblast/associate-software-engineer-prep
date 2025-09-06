# Python Notes — Chapter 11: Brief Tour of the Standard Library (Part II)

## 11.1 Output Formatting
- **reprlib**: Abbreviated `repr()` for large containers.
```python
import reprlib
reprlib.repr(set('supercalifragilisticexpialidocious'))
# Result: "{'a', 'c', 'd', 'e', 'f', 'g', ...}"
```
- **pprint**: Pretty printing with indentation and line breaks.
```python
import pprint
t = [[[['black', 'cyan'], 'white', ['green', 'red']], [['magenta', 'yellow'], 'blue']]]
pprint.pprint(t, width=30)
# Result is formatted nicely with indentation
```
- **textwrap**: Wraps text to a given width.
```python
import textwrap
doc = "The wrap() method is just like fill() except it returns a list of strings."
print(textwrap.fill(doc, width=40))
```
- **locale**: Culture-specific formatting for numbers/currency.
```python
import locale
locale.setlocale(locale.LC_ALL, 'English_United States.1252')
x = 1234567.8
locale.format_string("%d", x, grouping=True)   # '1,234,567'
```

## 11.2 Templating
- **string.Template**: Simplified string substitution with `$`.
```python
from string import Template
t = Template('${village}folk send $$10 to $cause.')
t.substitute(village='Nottingham', cause='the ditch fund')
# 'Nottinghamfolk send $10 to the ditch fund.'
```
- `safe_substitute()` avoids errors if placeholders are missing.

## 11.3 Working with Binary Data (struct)
- **struct**: Pack/unpack binary data.
```python
import struct
data = struct.pack('<IIf', 1, 2, 3.14)
struct.unpack('<IIf', data)
# Result: (1, 2, 3.140000104904175)
```

## 11.4 Multi-threading
- **threading**: Run tasks in background.
```python
import threading

class Worker(threading.Thread):
    def run(self):
        print("Task running in background")

w = Worker()
w.start()
w.join()
```
- Use `queue.Queue` for safer inter-thread communication.

## 11.5 Logging
- Flexible system for log messages.
```python
import logging
logging.warning("Warning: config not found")
logging.error("Error occurred")
```
- Levels: DEBUG, INFO, WARNING, ERROR, CRITICAL.

## 11.6 Weak References
- **weakref**: Track objects without preventing garbage collection.
```python
import weakref, gc
class A: pass
a = A()
d = weakref.WeakValueDictionary()
d['obj'] = a
del a; gc.collect()
# d['obj'] now removed automatically
```

## 11.7 Tools for Lists
- **array**: Compact arrays of numbers.
```python
from array import array
a = array('H', [10, 20, 30])
```
- **collections.deque**: Fast appends/pops from both ends.
```python
from collections import deque
d = deque([1, 2, 3]); d.appendleft(0)
```
- **bisect**: Maintain sorted lists.
```python
import bisect
nums = [1, 3, 5]; bisect.insort(nums, 4)
# [1, 3, 4, 5]
```
- **heapq**: Priority queue with smallest element first.
```python
import heapq
nums = [3, 1, 4]; heapq.heapify(nums)
heapq.heappop(nums)   # 1
```

## 11.8 Decimal Floating-Point Arithmetic
- **decimal.Decimal**: Exact decimal arithmetic.
```python
from decimal import Decimal, getcontext
getcontext().prec = 4
Decimal('1') / Decimal('7')   # Decimal('0.1429')
```
- Useful for finance (avoids floating-point rounding issues).

---
## Reference
[Python 3 Tutorial — 11. Brief Tour of the Standard Library Part II](https://docs.python.org/3/tutorial/stdlib2.html)
