# Python Loop Control Examples
ตัวอย่างการใช้ `break`, `continue`, และ `pass` ใน Python พร้อม walkthrough

---

## Break Example

### Code
```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(f"{n} equals {x} * {n//x}")
            break
```

### Walkthrough
- `n = 2` → inner loop empty → nothing happens
- `n = 3` → not divisible by 2 → nothing happens  
- `n = 4` → divisible by 2 → prints `4 equals 2 * 2` → break
- `n = 5` → not divisible by 2, 3, 4 → nothing happens
- `n = 6` → divisible by 2 → prints `6 equals 2 * 3` → break
- `n = 7` → not divisible by 2, 3, 4, 5, 6 → nothing happens
- `n = 8` → divisible by 2 → prints `8 equals 2 * 4` → break
- `n = 9` → divisible by 3 → prints `9 equals 3 * 3` → break

### Output
```
4 equals 2 * 2
6 equals 2 * 3
8 equals 2 * 4
9 equals 3 * 3
```

---

## Continue Example

### Code
```python
for num in range(2, 10):
    if num % 2 == 0:
        print(f"Even number: {num}")
        continue
    print(f"Odd number: {num}")
```

### Walkthrough
- `num = 2` → `2 % 2 == 0` → condition true → prints `Even number: 2` → continue skips odd print
- `num = 3` → `3 % 2 != 0` → condition false → prints `Odd number: 3`
- `num = 4` → `4 % 2 == 0` → condition true → prints `Even number: 4` → continue skips odd print
- `num = 5` → `5 % 2 != 0` → condition false → prints `Odd number: 5`
- `num = 6` → `6 % 2 == 0` → condition true → prints `Even number: 6` → continue skips odd print
- `num = 7` → `7 % 2 != 0` → condition false → prints `Odd number: 7`
- `num = 8` → `8 % 2 == 0` → condition true → prints `Even number: 8` → continue skips odd print
- `num = 9` → `9 % 2 != 0` → condition false → prints `Odd number: 9`

### Output
```
Even number: 2
Odd number: 3
Even number: 4
Odd number: 5
Even number: 6
Odd number: 7
Even number: 8
Odd number: 9
```

---

## Pass Example

### Code
```python
for n in range(2, 5):
    if n == 3:
        pass  # placeholder - does nothing
    print(n)
```

### Walkthrough
- `n = 2` → not equal to 3 → prints `2`
- `n = 3` → equals 3 → `pass` does nothing → prints `3`
- `n = 4` → not equal to 3 → prints `4`

### Output
```
2
3
4
```

---

## Summary

- **`break`**: Exits the current loop entirely
- **`continue`**: Skips the rest of the current iteration and moves to the next
- **`pass`**: Does nothing - useful as a placeholder when syntax requires a statement
