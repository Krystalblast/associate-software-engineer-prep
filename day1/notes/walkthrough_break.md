
## Break Example

This repo demonstrates how `break` work in Python loops, along with step-by-step walkthroughs.

---

### Code
```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(f"{n} equals {x} * {n//x}")
            break
```
----

# Walkthroughs

- **n = 2** → inner loop empty → nothing happens  
- **n = 3** → check x=2 → not divisible → nothing happens  
- **n = 4** → x=2 → divisible → prints `4 equals 2 * 2`, then `break` stops  
- **n = 6** → x=2 → divisible → prints `6 equals 2 * 3`, then stops  
- **n = 8** → x=2 → divisible → prints `8 equals 2 * 4`, then stops  
- **n = 9** → x=2 (fail), x=3 (works) → prints `9 equals 3 * 3`, then stops

---

**Output**

Even number: 2
Odd number: 3
Even number: 4
Odd number: 5
Even number: 6
Odd number: 7
Even number: 8
Odd number: 9


