# Using Lists as Stacks (LIFO)

```python
>>> stack = [3, 4, 5]
>>> stack.append(6)    # push
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]

>>> stack.pop()        # pop
7
>>> stack
[3, 4, 5, 6]

>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]

```
👉 append = push, pop = remove last
---
## Reference
[Python 3 Tutorial — Using Lists as Stacks](https://docs.python.org/3/tutorial/datastructures.html#using-lists-as-stacks)
