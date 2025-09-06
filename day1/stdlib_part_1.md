# Python Notes – Chapter 10: Brief Tour of the Standard Library

## 10.1 Operating System Interface
- Use `os` for interacting with the operating system.
```python
import os
os.getcwd()       # current working directory
# 'C:\\Python313'

os.chdir('/server/accesslogs')  # change directory
os.system('mkdir today')        # run system command
# 0
```
⚡ Use `import os` instead of `from os import *` to avoid conflicts.

- `shutil` provides higher-level file operations:
```python
import shutil
shutil.copyfile('data.db', 'archive.db')
# 'archive.db'

shutil.move('/build/executables', 'installdir')
# 'installdir'
```

---

## 10.2 File Wildcards
- Use `glob` to find files by pattern:
```python
import glob
glob.glob('*.py')
# ['primes.py', 'random.py', 'quote.py']
```

---

## 10.3 Command Line Arguments
- Command-line arguments are in `sys.argv`:
```python
# demo.py
import sys
print(sys.argv)
# ['demo.py', 'one', 'two', 'three']
```

- Use `argparse` for more complex parsing:
```python
import argparse

parser = argparse.ArgumentParser(prog='top', description='Show top lines')
parser.add_argument('filenames', nargs='+')
parser.add_argument('-l', '--lines', type=int, default=10)
args = parser.parse_args()
print(args)
```
Run: `python top.py --lines=5 alpha.txt beta.txt`  
→ `args.lines=5, args.filenames=['alpha.txt','beta.txt']`

---

## 10.4 Error Output & Program Termination
```python
import sys
sys.stderr.write('Warning, log file not found\n')
# Warning, log file not found
sys.exit()   # exits program
```

---

## 10.5 String Pattern Matching
- `re` for regex:
```python
import re
re.findall(r'\bf[a-z]*', 'which foot or hand fell fastest')
# ['foot', 'fell', 'fastest']

re.sub(r'(\b[a-z]+) \1', r'\1', 'cat in the the hat')
# 'cat in the hat'
```
- For simple tasks, prefer string methods:
```python
'tea for too'.replace('too', 'two')
# 'tea for two'
```

---

## 10.6 Mathematics
- `math` module:
```python
import math
math.cos(math.pi/4)
# 0.7071
math.log(1024, 2)
# 10.0
```

- `random` module:
```python
import random
random.choice(['apple','pear','banana'])
# 'apple'

random.sample(range(100), 5)
# [10, 35, 77, 56, 8]

random.random()   # float [0.0,1.0)
# 0.42

random.randrange(6)  # int from 0-5
# 4
```

- `statistics` module:
```python
import statistics
data=[2.75,1.75,1.25,0.25,0.5,1.25,3.5]
statistics.mean(data)     # 1.6071
statistics.median(data)   # 1.25
statistics.variance(data) # 1.372
```

---

## 10.7 Internet Access
```python
from urllib.request import urlopen
with urlopen('http://worldtimeapi.org/api/timezone/etc/UTC.txt') as r:
    for line in r:
        if line.decode().startswith('datetime'):
            print(line.decode().strip())
# datetime: 2022-01-01T01:36:47+00:00
```

```python
import smtplib
server = smtplib.SMTP('localhost')
server.sendmail('a@example.org','b@example.org',
"""To: b@example.org
From: a@example.org

Test message
""")
server.quit()
```

---

## 10.8 Dates and Times
```python
from datetime import date
now = date.today()
# datetime.date(2003, 12, 2)

now.strftime("%m-%d-%y. %d %b %Y is a %A")
# '12-02-03. 02 Dec 2003 is a Tuesday'

birthday = date(1964, 7, 31)
age = now - birthday
age.days
# 14368
```

---

## 10.9 Data Compression
```python
import zlib
s = b'witch which has which witches wrist watch'
t = zlib.compress(s)
zlib.decompress(t)
# b'witch which has which witches wrist watch'
zlib.crc32(s)
# 226805979
```

---

## 10.10 Performance Measurement
```python
from timeit import Timer
Timer('t=a; a=b; b=t','a=1; b=2').timeit()
# ~0.57

Timer('a,b=b,a','a=1; b=2').timeit()
# ~0.55
```

- For larger profiling: use `profile` and `pstats`.

---

## 10.11 Quality Control
- `doctest` validates examples in docstrings:
```python
def average(values):
    """Return mean.

    >>> average([20,30,70])
    40.0
    """
    return sum(values)/len(values)

import doctest
doctest.testmod()
```

- `unittest` for full testing:
```python
import unittest

class TestAvg(unittest.TestCase):
    def test_average(self):
        self.assertEqual(average([20,30,70]),40.0)
        with self.assertRaises(ZeroDivisionError):
            average([])

unittest.main()
```

---

## 10.12 Batteries Included
- Python comes with many useful modules/packages:
  - `xmlrpc.client`, `xmlrpc.server`
  - `email` package
  - `json`, `csv`, `xml.etree.ElementTree`
  - `sqlite3` for databases
  - `gettext`, `locale`, `codecs` for internationalization

---

## Reference
Python 3 Tutorial — 10. Brief Tour of the Standard Library  
https://docs.python.org/3/tutorial/stdlib.html
