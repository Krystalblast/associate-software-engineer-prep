# Python Notes – Section 7: Input and Output

## 7. Input and Output (Overview)
- Output can be printed for humans or written to files for later use.
- Common ways to format output: **f-strings**, **str.format()**, manual string methods, old `%` formatting.
- Quick debug: `str(obj)` (human‑readable) vs `repr(obj)` (unambiguous, interpreter‑readable).

---

## 7.1 Fancier Output Formatting

### 7.1.1 Formatted String Literals (f-strings)
- Syntax: prefix the string with `f` and put expressions in `{}`.
- Optional **format spec** after `:` controls width/precision/alignment; `!r/!s/!a` apply `repr/str/ascii`.

**Example:**
```python
import math
year, event = 2016, "Referendum"
msg = f"Results of the {year} {event}"
pi_line = f"The value of pi is approximately {math.pi:.3f}."
rows = {"Sjoerd": 4127, "Jack": 4098, "Dcab": 7678}
table = [f"{name:10} ==> {phone:10d}" for name, phone in rows.items()]
show_flags = f"{(bugs := 'roaches')=}, {(count := 13)=}, {(area := 'living room')=}"
print(msg); print(pi_line); print(*table, sep="\n"); print(show_flags)
```

**Result (abridged):**
```
Results of the 2016 Referendum
The value of pi is approximately 3.142.
Sjoerd     ==>       4127
Jack       ==>       4098
Dcab       ==>       7678
bugs='roaches', count=13, area='living room'
```

**Explanation:** `{expr:spec}` formats expressions in place; `= specifier` self-documents `name=value`.

---

### 7.1.2 `str.format()` Method
- Use `{}` placeholders (positional or named); supports rich **Format Specification Mini-Language**.
- Works well with dicts and `**` expansion.

**Example:**
```python
yes_votes, total_votes = 42_572_654, 85_705_149
pct = yes_votes / total_votes
line = "{:-9} YES votes  {:2.2%}".format(yes_votes, pct)
swap = "{1} and {0}".format("spam", "eggs")
named = "This {food} is {adj}.".format(food="spam", adj="absolutely horrible")
tbl = {"Jack": 4098, "Sjoerd": 4127, "Dcab": 8637678}
dict_pos = "Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; Dcab: {0[Dcab]:d}".format(tbl)
dict_kw = "Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}".format(**tbl)
cols = ["{0:2d} {1:3d} {2:4d}".format(x, x*x, x*x*x) for x in range(1, 4)]
print(line, swap, named, dict_pos, dict_kw, *cols, sep="\n")
```

**Result (abridged):**
```
 42572654 YES votes  49.67%
eggs and spam
This spam is absolutely horrible.
Jack: 4098; Sjoerd: 4127; Dcab: 8637678
Jack: 4098; Sjoerd: 4127; Dcab: 8637678
 1   1    1
 2   4    8
 3   9   27
```

**Explanation:** Placeholders can be indexed, named, or dict‑indexed; field specs control padding/width/precision.

---

### 7.1.3 Manual String Formatting
- Use string methods: `str.rjust()`, `ljust()`, `center()`, `zfill()` and concatenation.

**Example:**
```python
rows = ["{0:>2} {1:>3} {2:>4}".format(x, x*x, x*x*x) for x in range(1, 4)]
pad1 = "12".zfill(5)
pad2 = "-3.14".zfill(7)
print(*rows, pad1, pad2, sep="\n")
```

**Result:**
```
 1   1    1
 2   4    8
 3   9   27
00012
-003.14
```

**Explanation:** `rjust/ljust/center` pad with spaces; `zfill` pads numbers with zeros (handles sign).

---

### 7.1.4 Old `%` Formatting
- Legacy but still seen; printf‑style.

**Example:**
```python
import math
print("The value of pi is approximately %5.3f." % math.pi)
```
**Result:** `The value of pi is approximately 3.142.`

**Explanation:** Use only if maintaining old code; prefer f‑strings or `str.format()`.

---

## 7.2 Reading and Writing Files

### Opening Files
- `open(filename, mode, encoding=None)` → returns a file object.
- Common modes: `'r'` read, `'w'` write (truncate), `'a'` append, `'r+'` read/write; add `'b'` for binary.
- **Text mode** reads/writes `str` (with encoding); **binary mode** reads/writes `bytes`.

**Example (safe with context manager):**
```python
with open("workfile.txt", "w", encoding="utf-8") as f:
    f.write("hello\nworld\n")
# f is now closed
```

**Explanation:** `with` guarantees closing even if exceptions occur.

**Warnings:**
- Always close files (or use `with`), or data may not be fully written.
- Use **binary mode** for non‑text data (e.g., images), otherwise corruption can occur.

---

### 7.2.1 Methods of File Objects
- **Read:** `f.read(size)`, `f.readline()`, iterate lines (`for line in f:`), `f.readlines()`.
- **Write:** `f.write(string)` returns number of characters.
- **Positioning:** `f.tell()` (position), `f.seek(offset, whence)` (0=begin, 1=current, 2=end).

**Example (binary seek):**
```python
with open("workfile.bin", "wb+") as f:
    f.write(b"0123456789abcdef")
    f.seek(5)      # go to 6th byte
    one = f.read(1)  # b'5'
    f.seek(-3, 2)  # 3rd byte before end
    last = f.read(1)  # b'd'
print(one, last)
```

**Result:** `b'5' b'd'`

**Explanation:** `seek` moves the cursor; negative offsets require `whence=2` (from end) in binary mode.

---

### 7.2.2 Saving Structured Data with `json`
- Serialize (Python → JSON string/file): `json.dumps(obj)`, `json.dump(obj, file)`.
- Deserialize (JSON → Python): `json.loads(s)`, `json.load(file)`.
- JSON text must be **UTF‑8**; open files with `encoding="utf-8"`.

**Example:**
```python
import json
x = [1, "simple", "list"]
s = json.dumps(x)     # '[1, "simple", "list"]'
with open("data.json", "w", encoding="utf-8") as f:
    json.dump(x, f)

with open("data.json", "r", encoding="utf-8") as f:
    x2 = json.load(f)
print(s, x2)
```

**Result:**  
```
[1, "simple", "list"] [1, 'simple', 'list']
```

**Explanation:** `dumps/dump` produce JSON text; `loads/load` reconstruct Python objects (lists/dicts, etc.).

---

## Quick Reference: `str()` vs `repr()`
```python
s = "Hello, world."
str(s)   # 'Hello, world.'
repr(s)  # "'Hello, world.'"
```
- `str()` → friendly/human-readable
- `repr()` → unambiguous, often valid Python expression

---

## Reference
[Python 3 Tutorial — 7. Input and Output](https://docs.python.org/3/tutorial/inputoutput.html)
