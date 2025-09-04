# Numbers in Python

- **Interactive mode**  
  - Prompt uses `>>>` for input, `...` for continuation.  

- **Comments**  
  - Start with `#`.  

- **Operators**  
  - `+`, `-`, `*`, `/` → basic arithmetic  
  - `()` → parentheses for grouping  
  - `/` → always returns a float  
  - `//` → floor division (discards fractional part)  
  - `%` → modulus (remainder of division)  
  - `**` → exponentiation (power)  

- **Variables**  
  - `=` assigns a value to a variable.  
  - If a variable is not defined, using it will raise an error.  

- **Special variable `_`**  
  - In interactive mode, the result of the last expression is automatically stored in `_`.  
  - Useful when using Python as a calculator to continue calculations easily.
  - 
# Strings in Python

- Strings are of type `str`. They can be enclosed in single quotes (`'...'`) or double quotes (`"..."`).  
- To include quotes inside a string, either:
  - Escape them with `\`, or  
  - Use the other type of quotation marks.  

- `print()` function:  
  - Prints readable output.  
  - Supports escaped and special characters.  

- Common escape sequences:  
  - `\n` → newline  
  - `r"..."` → raw string (ignores escape sequences)  

- Multiline strings:  
  - Use triple quotes `"""..."""` or `'''...'''`.  
  - By default, each new line in code = `\n` inside the string.  
  - To avoid inserting a new line, add `\` at the end of the line.  

- String operations:  
  - Concatenate with `+`  
  - Repeat with `*`  
  - Adjacent string literals (e.g. `"Hello" "World"`) are automatically concatenated — but this doesn’t work with variables or expressions, where you must use `+`.  

- Indexing and slicing:  
  - Strings are indexed, starting from **0**.  
  - Negative indices count from the end, starting at **-1**.  
    - Example:  
      ```python
      word = "123"
      word[0]   # '1'
      word[-1]  # '3'
      ```
  - Slicing uses `[:]`:  
    - `word[0:2]` → characters from index 0 up to (but not including) 2  
    - Omitting the first index defaults to 0: `word[:2] = '12'` 
    - Omitting the second index defaults to the end: `word[1:] = '3'`  
    - Always includes the start index, excludes the end index.  s[:i] + s[i:] is always equal to s
    - Slices never cause errors if out of range: `word[1:55]` → `'3'`  

- Strings are **immutable** — they cannot be changed after creation.  

- `len()` returns the length of a string.  
