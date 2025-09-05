# Numbers in Python

- **Operators**
  ```python
  print(2 + 3)     # 5   addition
  print(5 - 2)     # 3   subtraction
  print(4 * 3)     # 12  multiplication
  print(8 / 2)     # 4.0 division (always float)
  print(7 // 2)    # 3   floor division
  print(7 % 2)     # 1   modulus (remainder)
  print(2 ** 3)    # 8   exponentiation (power)
  print((2 + 3) * 4)  # 20 parentheses for grouping

- **Variables**
  ```python
  width = 20
  height = 5 * 9
  print(width * height)   # 900

  # Using undefined variable
  # print(n)              # NameError: name 'n' is not defined

- **Mixed Types**
  ```python
  print(4 * 3.75 - 1)   # 14.0  int + float → converted to float

- **Special Variable _ in Interactive Mode**
  ```python
  # In interactive mode, last result is stored in _
  >>> 5 * 2
  10
  >>> _ + 3
  13    # 10 + 3

---
## Reference
- [Python 3 Tutorial — 3.1.1 Numbers](https://docs.python.org/3/tutorial/introduction.html#numbers)
