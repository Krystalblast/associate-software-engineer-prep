# Python Notes – Section 9: Classes

## 9.0 Overview
- Classes bundle **data (attributes)** and **behavior (methods)**. Instances are created from classes.
- Python supports **single & multiple inheritance**, **method overriding**, and **operator overloading** (via special methods).
- Everything is runtime and dynamic: classes are objects; built-ins can be subclassed.

---

## 9.1 A Word About Names and Objects
- Names are **bindings** to objects (aliasing). Mutables (lists/dicts) show shared changes via aliases.

**Example:**
```python
a = [1, 2]; b = a; b.append(3); print(a is b, a)
```
**Result:** `True [1, 2, 3]`  
**Explanation:** `a` and `b` reference the same list object.

---

## 9.2 Python Scopes and Namespaces
- **Namespace**: mapping of names → objects (module globals, function locals, builtins, attributes).
- Scope lookup order (LEGB-ish): **Local → Enclosing → Global → Builtins**.
- `global` rebinding at module scope; `nonlocal` rebinding in enclosing function scope.

**Example (bindings):**
```python
def scope_test():
    def do_local():    spam = "local spam"
    def do_nonlocal():
        nonlocal spam; spam = "nonlocal spam"
    def do_global():
        global spam; spam = "global spam"

    spam = "test spam"
    do_local();    print("After local:", spam)
    do_nonlocal(); print("After nonlocal:", spam)
    do_global();   print("After global:", spam)

scope_test(); print("In global:", spam)
```
**Result (abridged):**
```
After local: test spam
After nonlocal: nonlocal spam
After global: nonlocal spam
In global: global spam
```
**Explanation:** Local assign doesn’t affect outer; `nonlocal` rebinding affects enclosing; `global` writes module var.

---

## 9.3 A First Look at Classes

### 9.3.1 Class Definition Syntax
- Define with `class Name:`. Body executes creating a new **class object**.

**Example:**
```python
class ClassName:
    pass
```
**Explanation:** Executing the `class` block creates/binds the class object to `ClassName`.

### 9.3.2 Class Objects
- Class attributes & methods are in the class namespace; instantiate with call syntax; initialize via `__init__`.

**Example:**
```python
class MyClass:
    """A simple example class"""
    i = 12345
    def f(self): return "hello world"

x = MyClass()             # instantiation
print(MyClass.i, x.f(), MyClass.__doc__)
```
**Result:** `12345 hello world A simple example class`  
**Explanation:** Attribute access via class/instance; methods are functions bound at access time.

**`__init__` with args:**
```python
class Complex:
    def __init__(self, real, imag):
        self.r = real; self.i = imag
x = Complex(3.0, -4.5); print(x.r, x.i)
```
**Result:** `3.0 -4.5`

### 9.3.3 Instance Objects
- Instances support **attribute references**: data attributes & methods. Data attributes appear on first assignment.

**Example:**
```python
class Counter:
    pass

c = Counter()
c.value = 1
while c.value < 10:
    c.value *= 2
print(c.value); del c.value
```
**Result:** `16`  
**Explanation:** Creating/using/deleting instance data attributes dynamically.

### 9.3.4 Method Objects
- Accessing `x.f` produces a **bound method**; calling `x.f()` == `Class.f(x)`.

**Example:**
```python
class Greeter:
    def hello(self): return "hello"
g = Greeter(); mf = g.hello; print(mf(), Greeter.hello(g))
```
**Result:** `hello hello`  
**Explanation:** The instance is implicitly passed as first argument.

### 9.3.5 Class vs Instance Variables
- Use class variables for shared data; instance variables for per-instance data.
- **Pitfall**: mutable class variables are **shared** across instances.

**Bad (shared list):**
```python
class Dog:
    tricks = []                 # shared!
    def __init__(self, name): self.name = name
    def add_trick(self, t): self.tricks.append(t)

d = Dog("Fido"); e = Dog("Buddy")
d.add_trick("roll over"); e.add_trick("play dead")
print(d.tricks)
```
**Result:** `['roll over', 'play dead']` (shared)  

**Good (per-instance list):**
```python
class Dog:
    def __init__(self, name):
        self.name = name; self.tricks = []
    def add_trick(self, t): self.tricks.append(t)

d = Dog("Fido"); e = Dog("Buddy")
d.add_trick("roll over"); e.add_trick("play dead")
print(d.tricks, e.tricks)
```
**Result:** `['roll over'] ['play dead']`

---

## 9.4 Random Remarks
- Instance attributes shadow class attributes with the same name.
- No enforced access control; underscore `_name` by convention = non-public.
- Methods can be assigned from outside or aliased; `self` is a naming **convention**.
- Methods can call other methods: `self.other()`.

**Example (shadowing):**
```python
class Warehouse: purpose = "storage"; region = "west"
w1 = Warehouse(); w2 = Warehouse(); w2.region = "east"
print(w1.region, w2.region)
```
**Result:** `west east`

---

## 9.5 Inheritance
- Attribute lookup falls back to base classes; overriding works; all methods are effectively **virtual**.
- `isinstance(obj, T)` and `issubclass(S, T)` for type checks.

**Example:**
```python
class A: 
    def ping(self): return "A.ping"
class B(A):
    def ping(self): return "B.ping (override)"
    def call_super(self): return A.ping(self)

b = B(); print(b.ping(), b.call_super(), isinstance(b, A), issubclass(B, A))
```
**Result:** `B.ping (override) A.ping True True`

### 9.5.1 Multiple Inheritance
- Supports multiple bases; Python’s MRO (C3 linearization) enables cooperative `super()` calls.

**Example (cooperative super):**
```python
class X: 
    def who(self): return "X"
class Y(X):
    def who(self): return "Y>" + super().who()
class Z(X):
    def who(self): return "Z>" + super().who()
class M(Y, Z):
    def who(self): return "M>" + super().who()

print(M().who())  # MRO: M → Y → Z → X → object
```
**Result:** `M>Y>Z>X`  
**Explanation:** `super()` follows MRO; each parent runs once.

---

## 9.6 Private Variables (Name Mangling)
- No true private vars; leading `__name` triggers **name mangling** to `_ClassName__name` inside the class.
- Useful to avoid subclass name clashes; still accessible if needed.

**Example:**
```python
class Mapping:
    def __init__(self, it):
        self.items_list = []
        self.__update(it)      # calls private alias
    def update(self, it):
        for item in it: self.items_list.append(item)
    __update = update          # private copy

class MappingSubclass(Mapping):
    def update(self, keys, values):
        for kv in zip(keys, values): self.items_list.append(kv)

m = MappingSubclass(["a"])
print(hasattr(m, "_Mapping__update"))
```
**Result:** `True`

---

## 9.7 Odds and Ends
- Use `@dataclass` for lightweight records.
- Method objects: `m.__self__` (instance), `m.__func__` (underlying function).

**Example (dataclass):**
```python
from dataclasses import dataclass
@dataclass
class Employee: name: str; dept: str; salary: int
john = Employee("john", "computer lab", 1000)
print(john.dept, john.salary)
```
**Result:** `computer lab 1000`

---

## 9.8 Iterators
- `for` calls `iter(obj)` → iterator with `__next__()`; raises `StopIteration` to end.

**Example (custom iterator):**
```python
class Reverse:
    def __init__(self, data): self.data, self.index = data, len(data)
    def __iter__(self): return self
    def __next__(self):
        if self.index == 0: raise StopIteration
        self.index -= 1; return self.data[self.index]

rev = Reverse("spam"); print(list(rev))
```
**Result:** `['m', 'a', 'p', 's']`

---

## 9.9 Generators
- Functions with `yield` create **generators** (stateful iterators) easily.

**Example:**
```python
def reverse(data):
    for i in range(len(data)-1, -1, -1):
        yield data[i]

print(list(reverse("golf")))
```
**Result:** `['f', 'l', 'o', 'g']`

---

## 9.10 Generator Expressions
- Like list comprehensions, but with `()`; lazy and memory-friendly.

**Examples:**
```python
print(sum(i*i for i in range(10)))        # 285
xv, yv = [10,20,30], [7,5,3]
print(sum(x*y for x,y in zip(xv, yv)))    # 260
data = "golf"
print(list(data[i] for i in range(len(data)-1,-1,-1)))  # ['f','l','o','g']
```
**Result (abridged):**
```
285
260
['f', 'l', 'o', 'g']
```

---

## Reference
[Python 3 Tutorial — 9. Classes](https://docs.python.org/3/tutorial/classes.html)
