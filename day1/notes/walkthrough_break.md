# Walkthrough of Break Example

This file explains step-by-step why the program prints the results it does.

---

### n = 2
Inner loop: `x` would range from 2 to 1 → empty, so nothing happens.

### n = 3
Inner loop: `x = 2`  
3 % 2 != 0 → so no print.

### n = 4
Inner loop: `x = 2, 3`  
- For x = 2: 4 % 2 == 0 → prints: `4 equals 2 * 2`  
- `break` stops further checks (so it doesn’t check x = 3)

### n = 6
Inner loop: `x = 2, 3, 4, 5`  
- For x = 2: 6 % 2 == 0 → prints: `6 equals 2 * 3`  
- `break` stops immediately (so it never checks x = 3, 4, 5)

### n = 8
Inner loop: `x = 2, 3, 4, 5, 6, 7`  
- For x = 2: 8 % 2 == 0 → prints: `8 equals 2 * 4`  
- `break` stops right away

### n = 9
Inner loop: `x = 2, 3, 4, 5, 6, 7, 8`  
- For x = 2: not divisible  
- For x = 3: 9 % 3 == 0 → prints: `9 equals 3 * 3`  
- `break` stops here

---


