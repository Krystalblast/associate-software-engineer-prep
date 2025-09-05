# match Statement in Python (Python 3.10+) ⭐ Difficult

The `match` statement is Python’s **structural pattern matching** (introduced in Python 3.10).

- Similar to `switch` in other languages, but **more powerful**.  
- Compares a value against multiple **patterns**.  
- The first matching `case` block is executed.  
- `_` (underscore) acts as a **wildcard** (matches anything).  
- Can also **extract parts of data** into variables (like unpacking).  

---

## Example 1: Basic match
```python
def http_error(status):
    match status:
        case 400:
            return "Bad request"         # matches 400
        case 404:
            return "Not found"           # matches 404
        case 418:
            return "I'm a teapot"        # matches 418
        case _:                          # wildcard (default)
            return "Something's wrong"

print(http_error(404))
# Result: Not found
```
--- 

## Example 2: Matching a tuple
```python
point = (0, 5)
match point:
    case (0, 0):
        print("Origin")                  # matches (0,0)
    case (0, y):
        print(f"Y={y}")                  # captures second value into variable y
    case (x, 0):
        print(f"X={x}")
    case (x, y):
        print(f"Point at X={x}, Y={y}")  # fallback: binds both values

# Result:
# Y=5

```
--- 
### Explanation:

- `case (0, y)` matches any tuple where the first element is `0`.

- The second element is captured into variable `y` → here `y=5`.

- That’s why it prints `Y=5`.
