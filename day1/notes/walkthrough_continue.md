## Continue Example

This repo demonstrates how `continue` work in Python loops, along with step-by-step walkthroughs.

---

### Code
```python
for num in range(2, 10):
    if num % 2 == 0:
        print(f"Even number: {num}")
        continue
    print(f"Odd number: {num}")
```
---

### Walkthough

**Outer loop → `num` takes values from 2 through 9.**

**num = 2**
- 2 % 2 == 0 → condition true  
- Prints: **Even number: 2**  
- `continue` jumps to next loop → skips the odd-print line  

---

## num = 3
- 3 % 2 != 0 → condition false  
- Doesn’t continue → runs the last print  
- Prints: **Odd number: 3**  

---

## num = 4
- 4 % 2 == 0 → condition true  
- Prints: **Even number: 4**  
- `continue` skips the odd print  

---

## num = 5
- 5 % 2 != 0 → condition false  
- Prints: **Odd number: 5**  

---

## num = 6
- 6 % 2 == 0 → condition true  
- Prints: **Even number: 6**  
- Skips odd print  

---

## num = 7
- 7 % 2 != 0 → condition false  
- Prints: **Odd number: 7**  

---

## num = 8
- 8 % 2 == 0 → condition true  
- Prints: **Even number: 8**  

---

## num = 9
- 9 % 2 != 0 → condition false  
- Prints: **Odd number: 9**

----

## Output
```yaml
Even number: 2
Odd number: 3
Even number: 4
Odd number: 5
Even number: 6
Odd number: 7
Even number: 8
Odd number: 9
```
