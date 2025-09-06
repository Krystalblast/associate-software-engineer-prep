```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']

# count()
>>> fruits.count('apple')
2
>>> fruits.count('tangerine')
0

# index()
>>> fruits.index('banana')
3
>>> fruits.index('banana', 4)   # หา 'banana' ตั้งแต่ตำแหน่ง 4 เป็นต้นไป
6

# reverse()
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']

# append()
>>> fruits.append('grape')
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']

# sort()
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']

# pop()
>>> fruits.pop()
'pear'
>>> fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange']

# insert()
>>> fruits.insert(0, 'mango')
>>> fruits
['mango', 'apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange']

# remove()
>>> fruits.remove('banana')
>>> fruits
['mango', 'apple', 'apple', 'banana', 'grape', 'kiwi', 'orange']

# extend()
>>> fruits.extend(['pineapple', 'melon'])
>>> fruits
['mango', 'apple', 'apple', 'banana', 'grape', 'kiwi', 'orange', 'pineapple', 'melon']

# copy()
>>> copy_fruits = fruits.copy()
>>> copy_fruits
['mango', 'apple', 'apple', 'banana', 'grape', 'kiwi', 'orange', 'pineapple', 'melon']

# clear()
>>> fruits.clear()
>>> fruits
[]
```
---
## Reference
[Python 3 Tutorial — 5.1.1 More on Lists](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)
