## for Statements 
```python
words = ["cat", "window", "defenestrate"]
for w in words:                         # loops over each item in the list
    print(w, len(w))                    # prints word and its length

# Result:
# cat 3
# window 6
# defenestrate 12
```
---
## range() Funtion 
```python
for i in range(5):                      # generates numbers 0–4
    print(i)

# Result:
# 0
# 1
# 2
# 3
# 4

print(list(range(5, 10)))               # start=5, stop=10
# [5, 6, 7, 8, 9]

print(list(range(0, 10, 3)))            # step = 3
# [0, 3, 6, 9]

print(list(range(-10, -100, -30)))      # negative step
# [-10, -40, -70]

```
---
### break and continue 

```python
# break example: stops loop when condition is met
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(f"{n} equals {x} * {n//x}")
            break                       # exit inner loop

# Result:
# 4 equals 2 * 2
# 6 equals 2 * 3
# 8 equals 2 * 4
# 9 equals 3 * 3
```
- [Read the step-by-step walkthrough](https://github.com/Krystalblast/associate-software-engineer-prep/blob/main/day1/notes/walkthrough_break.md)
```python
# continue example: skips current iteration
for num in range(2, 10):
    if num % 2 == 0:
        print(f"Even number: {num}")
        continue                       # go to next iteration
    print(f"Odd number: {num}")

# Result:
# Even number: 2
# Odd number: 3
# Even number: 4
# Odd number: 5
# Even number: 6
# Odd number: 7
# Even number: 8
# Odd number: 9

```
---
## else on Loops 
```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(n, "equals", x, "*", n//x)
            break                       # break = skip else
    else:
        print(n, "is a prime number")   # only runs if no break occurs

# Result:
# 2 is a prime number
# 3 is a prime number
# 4 equals 2 * 2
# 5 is a prime number
# 6 equals 2 * 3
# 7 is a prime number
# 8 equals 2 * 4
# 9 equals 3 * 3

```
---
## Reference
- [Python 3 Tutorial — 4.2 for Statements](https://docs.python.org/3/tutorial/controlflow.html#for-statements)  
- [Python 3 Tutorial — 4.3 The range() Function](https://docs.python.org/3/tutorial/controlflow.html#the-range-function)  
- [Python 3 Tutorial — 4.4 break and continue Statements](https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements)  
- [Python 3 Tutorial — 4.5 else Clauses on Loops](https://docs.python.org/3/tutorial/controlflow.html#else-clauses-on-loops)

