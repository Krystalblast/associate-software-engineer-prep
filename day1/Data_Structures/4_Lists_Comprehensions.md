# List Comprehensions
  A compact way to build lists.

```python
# squares of 0–9
>>> [x**2 for x in range(10)]
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# combine elements of two lists (if not equal)
>>> [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]

# double values
>>> vec = [-4, -2, 0, 2, 4]
>>> [x*2 for x in vec]
[-8, -4, 0, 4, 8]

# filter out negatives
>>> [x for x in vec if x >= 0]
[0, 2, 4]

# apply a function
>>> [abs(x) for x in vec]
[4, 2, 0, 2, 4]

# strip whitespace
>>> freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']
>>> [w.strip() for w in freshfruit]
['banana', 'loganberry', 'passion fruit']

# tuples (must be parenthesized)
>>> [(x, x**2) for x in range(6)]
[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]

# flatten a nested list
>>> vec2d = [[1,2,3], [4,5,6], [7,8,9]]
>>> [num for row in vec2d for num in row]
[1, 2, 3, 4, 5, 6, 7, 8, 9]

# use functions
>>> from math import pi
>>> [str(round(pi, i)) for i in range(1, 6)]
['3.1', '3.14', '3.142', '3.1416', '3.14159']

```
---
## Reference
[Python 3 Tutorial — List Comprehensions](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions)
