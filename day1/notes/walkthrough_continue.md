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

- **num = 2** → even → prints `Even number: 2`, skips odd print  
- **num = 3** → odd → prints `Odd number: 3`  
- **num = 4** → even → prints `Even number: 4`  
- **num = 5** → odd → prints `Odd number: 5`  
- **num = 6** → even → prints `Even number: 6`  
- **num = 7** → odd → prints `Odd number: 7`  
- **num = 8** → even → prints `Even number: 8`  
- **num = 9** → odd → prints `Odd number: 9`  
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
