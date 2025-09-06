# Using Lists as Queues (FIFO)
 Lists are inefficient for queues; use `collections.deque`.
```python
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])

>>> queue.append("Terry")    # Terry arrives
>>> queue.append("Graham")   # Graham arrives
>>> queue.popleft()          # First in, first out
'Eric'
>>> queue.popleft()
'John'

>>> queue
deque(['Michael', 'Terry', 'Graham'])

```
---
## Reference
[Python 3 Tutorial — Using Lists as Queues](https://docs.python.org/3/tutorial/datastructures.html#using-lists-as-queues)
