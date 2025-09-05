# Strings in Python

- **Basic strings**
  ```python
  s1 = 'Hello'    # single quote
  s2 = "World"    # double quote
  print(s1, s2)   # Hello World

- **Including quotes**
  ```python
  s1 = 'He said: "Hi"'
  s2 = "It's a nice day"
  s3 = 'It\'s also correct'   # escaping with \
  
- **print() function**
  ```python
  print("Line 1\nLine 2")
  # Line 1
  # Line 2

  print(r"C:\new_folder")   # raw string
  # C:\new_folder
  
- **Multiline strings**
  ```python
  text = """This is
  a multiline
  string."""
  print(text)
  # This is
  # a multiline
  # string

  text2 = """This is \
  still one line"""
  print(text2)
  # This is still one line

- **String operations**
  ```python
  "Hello " + "World"   # 'Hello World'
  "Ha" * 3             # 'HaHaHa'

  # Adjacent string literals auto-concatenate
  "Hello" "World"      # 'HelloWorld'

- **Indexing and slicing**
  ```python
  word = "123"
  word[0]     # '1'
  word[1]     # '2'
  word[2]     # '3'
  word[3]     # Error: string index out of range
  word[-1]    # '3'

  word[0:2]   # '12'  (exclude word[2])
  word[:2]    # '12'  (exclude word[2])
  word[1:]    # '23'  (include word[1])
  word[1:55]  # '23' (safe even if out of range)

- **Strings are immutable**
  ```python
  word = "hello"
  # word[0] = "H"   # ❌ Error: strings can't be changed

- **Length of a string**
  ```python
  len("Hello")   # 5

----

## Reference
- [Python 3 Tutorial — 3.1.2 Text (Strings)](https://docs.python.org/3/tutorial/introduction.html#text)



