## The del Statement
	- `del` removes items from a list by index, unlike `pop()` which also returns the value.
	- It can delete slices, clear lists, or even delete entire variables.

	**Example:**

	```python
	a = [-1, 1, 66.25, 333, 333, 1234.5]
	del a[0]
	print(a)         # [1, 66.25, 333, 333, 1234.5]

	del a[2:4]
	print(a)         # [1, 66.25, 1234.5]

	del a[:]         
	print(a)         # []

	del a
	# now 'a' is undefined → NameError if accessed
	```
---

## Tuples and Sequences
	- Tuples are immutable sequences, written as values separated by commas.
	- They support indexing, slicing, nesting, and packing/unpacking.
	- A tuple with one item needs a trailing comma.

	**Example:**

	```python
	t = 12345, 54321, 'hello!'
	print(t[0])     # 12345
	print(t)        # (12345, 54321, 'hello!')

	u = t, (1, 2, 3, 4, 5)
	print(u)        # ((12345, 54321, 'hello!'), (1, 2, 3, 4, 5))

	empty = ()
	singleton = 'hello',
	print(len(empty))     # 0
	print(len(singleton)) # 1
	print(singleton)      # ('hello',)

	# Unpacking
	x, y, z = t
	print(x, y, z)  # 12345 54321 hello!
	```
---
## Sets
	- A set is an unordered collection with no duplicates.
	- Supports fast membership tests and math operations: union, intersection, difference, symmetric difference.
	- Use `{}` or `set()` to create sets.
	- Set comprehensions are supported.

	**Example:**

	```python
	basket = {'apple', 'orange', 'apple', 'pear'}
	print(basket)                # {'apple', 'orange', 'pear'}

	a = set('abracadabra')
	b = set('alacazam')

	print(a)        # {'a', 'r', 'b', 'c', 'd'}
	print(a - b)    # {'r', 'd', 'b'}
	print(a | b)    # {'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
	print(a & b)    # {'a', 'c'}
	print(a ^ b)    # {'r', 'd', 'b', 'm', 'z', 'l'}

	# Set comprehension
	s = {x for x in 'abracadabra' if x not in 'abc'}
	print(s)        # {'r', 'd'}
	```
---
## Dictionaries
	- Dictionaries are key-value mappings (`{key: value}`).
	- Keys must be immutable (e.g., strings, numbers, tuples).
	- Main operations: insert, access, delete, test membership.
	- Dict comprehensions are supported.

	**Example:**

	```python
	tel = {'jack': 4098, 'sape': 4139}
	tel['guido'] = 4127
	print(tel)            # {'jack': 4098, 'sape': 4139, 'guido': 4127}
	print(tel['jack'])    # 4098

	del tel['sape']
	print(tel)            # {'jack': 4098, 'guido': 4127}

	print(list(tel))      # ['jack', 'guido']
	print(sorted(tel))    # ['guido', 'jack']
	print('guido' in tel) # True

	# dict() constructor
	d = dict([('sape', 4139), ('guido', 4127)])
	print(d)  # {'sape': 4139, 'guido': 4127}

	# comprehension
	d2 = {x: x**2 for x in (2, 4, 6)}
	print(d2) # {2: 4, 4: 16, 6: 36}
	```
---
## Looping Techniques
	- `dict.items()` → iterate key + value
	- `enumerate()` → iterate index + value
	- `zip()` → iterate multiple sequences together
	- `reversed()` → iterate backward
	- `sorted()` → iterate in sorted order
	- Use `set() + sorted()` for unique, sorted values

	**Best practice:** avoid modifying lists while looping.

	**Example:**

	```python
	knights = {'gallahad': 'the pure', 'robin': 'the brave'}
	for k, v in knights.items():
		print(k, v)
	# gallahad the pure
	# robin the brave

	for i, v in enumerate(['tic', 'tac', 'toe']):
		print(i, v)
	# 0 tic
	# 1 tac
	# 2 toe

	for q, a in zip(['name','quest'], ['lancelot','holy grail']):
		print(f"What is your {q}? It is {a}.")
	# What is your name? It is lancelot.
	# What is your quest? It is holy grail.
	```
---
## More on Conditions
	- Conditions can use operators: `in`, `not in`, `is`, `is not`.
	- Comparisons can be chained: `a < b == c`.
	- Boolean operators `and`, `or`, `not` are short-circuit operators.
	- Assign result of condition to variable.
	- Use walrus operator `:=` for assignment inside expressions.

	**Example:**

	```python
	string1, string2, string3 = '', 'Trondheim', 'Hammer Dance'
	non_null = string1 or string2 or string3
	print(non_null)  # Trondheim

	a, b, c = 2, 3, 3
	print(a < b == c)  # True
	```
---
## Comparing Sequences and Other Types
	- Sequences are compared lexicographically (like dictionary order).
	- Comparison goes element by element until a difference is found.
	- If one sequence is a prefix of another, the shorter one is smaller.
	- Strings compare by Unicode code points.
	- Mixed numeric types compare by value (`1 == 1.0`).
	- Otherwise, comparing incompatible types raises `TypeError`.

	**Example:**

	```python
	print((1, 2, 3) < (1, 2, 4))         # True
	print([1, 2, 3] < [1, 2, 4])         # True
	print('ABC' < 'C' < 'Pascal' < 'Python')  # True
	print((1, 2, 3) == (1.0, 2.0, 3.0))  # True
	```
---
## Reference
	- [Python 3 Tutorial — The del statement](https://docs.python.org/3/tutorial/datastructures.html#the-del-statement)  
	- [Python 3 Tutorial — Tuples and Sequences](https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences)  
	- [Python 3 Tutorial — Sets](https://docs.python.org/3/tutorial/datastructures.html#sets)  
	- [Python 3 Tutorial — Dictionaries](https://docs.python.org/3/tutorial/datastructures.html#dictionaries)  
	- [Python 3 Tutorial — Looping Techniques](https://docs.python.org/3/tutorial/datastructures.html#looping-techniques)  
	- [Python 3 Tutorial — More on Conditions](https://docs.python.org/3/tutorial/datastructures.html#more-on-conditions)  
	- [Python 3 Tutorial — Comparing Sequences and Other Types](https://docs.python.org/3/tutorial/datastructures.html#comparing-sequences-and-other-types)

