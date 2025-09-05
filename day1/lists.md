# Lists in Python

- **Create a list** with square brackets:
  ```python
  fruits = ["apple", "banana", "cherry"]

- **Indexing and slicing**
  ```python
  fruits[0]     # "apple"
  fruits[-1]    # "cherry"
  fruits[1:]    # ["banana", "cherry"]

- **Concatenation**
  ```python
  [1, 2, 3] + [4, 5]   # [1, 2, 3, 4, 5]

- **Mutable (changeable)**
  ```python
  fruits[1] = "blueberry"
   #["apple", "blueberry", "cherry"]

- **Append items**
  ```python
  fruits.append("orange")
  #["apple", "blueberry", "cherry", "orange"]

- **Assignment doesn't copy**
  ```python
  a = fruits
  a.append("grape")
  # fruits also changes

- **Slice returns new list**
  ```python
  b = fruits[:]
  
- **Slice assignment**
  ```python
  letters = ["a", "b", "c", "d"]
  letters[1:3] = ["X", "Y"]
  # ["a", "X", "Y", "d"]

- **Length of list**
  ```python
  len(fruits)   # 5

- **Nested lists**
  ```python
  x = [["a", "b"], [1, 2]]
  x[0][1]   # "b"

---

## Reference
- [Python 3 Tutorial — 3.1.3 Lists](https://docs.python.org/3/tutorial/introduction.html#lists)
