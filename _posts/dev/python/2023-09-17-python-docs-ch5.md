---
title: "[Python] Ch5. Data Structures"
date: 2023-09-17
categories: [Dev, Python]
tags: [Python]
---

## 5.1 List Methods

`list.append(x)`

- Add an item at the end of a list. Same as `a[len(a):] = [x]`

`list.extend(iterable)`

- Add a list to the end of a list. Same as `a[len(a):] = iterable`

`list.insert(i,x)`

- First arg is the index and the second arg is an item.
- `a.insert(len(a),x)` is equivalent to `a.append(x)`.

`list.remove(x)`

- Removes the first item from the list.

`list.pop(i)`

- Remove item at the given index `i`.
- If no index is specified, it removes the last element.

`list.clear()`

- Remove all items from the list. Same as `del a[:]`.

`list.index(x, start, end)`

- Returns the zero-based index for the first item that matches the value `x`.
- Start and end limits the search to a particular subsequence.

`list.count(x)`

- Returns the number of times `x` appears in the list.

`list.sort(x, key=None, reverse = True)`

- Sort items in place.

`list.reverse()`

- Reverse the order of elements in the list.

`list.copy()`

- Create a shallow copy of a list. Same as `a[:]`.

```python
fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
fruits.count('apple')
2
fruits.count('tangerine')
0
fruits.index('banana')
3
fruits.index('banana', 4)  # Find next banana starting at position 4
6
fruits.reverse()
fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
fruits.append('grape')
fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']
fruits.sort()
fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']
fruits.pop()
'pear'
```

> **Note:** `insert`, `remove`, and `sort` does not have a return value.

### How to create a multidimensional list?

You should **always** use <span style="font-weight: bold; color: orange;">list comprehension</span> when creating ***multidimensional list***. 

For example, if you try to make a ***multidimensional list*** like this:

```python
array = [[None] * 2] * 3

print(array) # [[None, None], [None, None], [None, None]]
```

However, when you change the value, it appears like this:

```python
array[0][0] = 5

print(array) # [[5, None], [5, None], [5, None]]
```

The reason is because replicating a list using `*` does not create ***copies***. It only creates <span style="font-weight: bold; color: orange;">references</span> to the exiting object. The `* 3` creates <span style="font-weight: bold; color: orange;">3 references</span> to the same list of length two. 

Hence, **always** use <span style="font-weight: bold; color: orange;">list comprehension</span> when creating ***multidimensional arrays***.

## 5.2 Use Lists as Stack (LIFO)

```python
stack = [1,2]
stack.append(3) # [1,2,3]

stack.pop() # [1,2]
```

## 5.3 Use Lists as Queue (FIFO)

```python
from collections import deque

queue = deque([1,2])
queue.popleft() # [2]

queue.append(3) # [2,3]
```

## 5.4 List Comprehensions

```python
a = []
for x in range(10):
    a.append(x ** 2)

# This is equivalent to...
a = list(map(lambda x : x ** 2, range(10)))

# Or...
a = [ x ** 2 for x in range(10) ]

combs = []
for x in [1,2,3]:
    for y in [3,1,4]:
        if x != y:
            combs.append((x,y))

# This is equivalent to...
combs = [ (x,y) for x in [1,2,3] for y in [3,1,4] if x != y ]
```

## 5.5 Nested List Comprehensions

```python
matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
]

a = [[row[i] for row in matrix] for i in range(4)]

# This is equivalent to...

a = []
for i in range(4):
    for row in matrix:
        a.append([row[i] for row in matrix])

# Or...

a = list(zip(*matrix))
```

## 5.6 del Statement

`del` can use the index to delete an element from a list. It can also use slicing technique.

```python
a = [1, 2, 3, 4, 5, 6]
del a [0] # [2, 3, 4, 5, 6]

b = [1, 2, 3, 4]
del b[1:3] # [1, 4]

del b [:] # []
```

## 5.7 Tuples and Sequences

Sequence Types - List, Tuple, Range, String (**Ordered Collections**)

Tuple consists of number of values separated by commas. *Tuples* and *Lists* are used for different purpose. Tuples are **immutable** and the elements are **heterogeneous**. The elements are access through **unpacking** or **indexing**. It would be <span style="font-weight: bold; color: orange;">beneficial</span> to use tuples for data that should <span style="font-weight: bold; color: orange;">not be changed</span>! On the other hand, lists are **mutable** and the elements are **homogeneous**. 

```python
t = 1, 'hi', 2 # This is tuple packing.
t[0] # 1

print(t) # (1, 'hi', 2)

a, b, c = t # This is tuple unpacking.

u = t, (1, 2, 3)

print(u) # ((1, 'hi', 2), (1, 2, 3))

# Tuples are immutable!
t[0] = 3 # TypeError

v = ([1, 2, 3], [4, 5, 6])
v[0][0] = 10

print(v) # ([10, 2, 3], [4, 5, 6])
```

Tuple with 0 or 1 item.

```python
empty = ()
singleton = 'Hello', # Have to add a comma

len(empty) # 0

len(singleton) # 1

print(singleton) # ('Hello', )
```

> **Note:** When unpacking sequences, the number of variables on the left side should match the length of sequences!
{: .prompt-info}

## 5.8 Sets

**Unordered** collections with **no duplicate** elements. Also supports union, intersection, difference, and symmetric difference.

> **Note:** To create an empty set, use `set()` not `{}`.
{: .prompt-info}

```python
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
print(basket)                      # show that duplicates have been removed
{'orange', 'banana', 'pear', 'apple'}
'orange' in basket                 # fast membership testing
True
'crabgrass' in basket
False

# Demonstrate set operations on unique letters from two words

a = set('abracadabra')
b = set('alacazam')
a                                  # unique letters in a
{'a', 'r', 'b', 'c', 'd'}
a - b                              # letters in a but not in b
{'r', 'd', 'b'}
a | b                              # letters in a or b or both
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
a & b                              # letters in both a and b
{'a', 'c'}
a ^ b                              # letters in a or b but not both
{'r', 'd', 'b', 'm', 'z', 'l'}
```

Set comprehension is also supported.

```python
a = {x for x in 'abracadabra' if x not in 'abc'}
print(a) # {'r', 'd'}
```

## 5.9 Dictionaries

Dictionaries are a set of **key: value pairs**.

- Keys should be always **immutable**.
  - strings, numbers, tuples
  - Tuples should only contain string, number, and tuples

```python
tel = {'jack': 4098, 'sape': 4139}
tel['guido'] = 4127

print(tel) # {'jack': 4098, 'sape': 4139, 'guido': 4127}

print(tel['jack']) # 4098

del tel['sape']
tel['irv'] = 4127

print(tel) # {'jack': 4098, 'guido': 4127, 'irv': 4127}

list(tel) # ['jack', 'guido', 'irv'] List all the keys

sorted(tel) # ['guido', 'irv', 'jack'] List all the keys in sorted order

'guido' in tel
True

'jack' not in tel
False
```

`dict()` constructor builds a dictionary directly from sequence of key-value pairs:

```python
dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
# {'sape': 4139, 'guido': 4127, 'jack': 4098}
```

Dict comprehension is also supported:

```python
{x: x**2 for x in (2, 4, 6)}
# {2: 4, 4: 16, 6: 36}
```

We can use keyword arguments to create a dict when the key is a **string**.

```python
dict(sape=4139, guido=4127, jack=4098)
# {'sape': 4139, 'guido': 4127, 'jack': 4098}
```

## 5.10 Looping Techniques

1. Loop through dict using `items()`:

   ```python
   data = {'Sally': 10, 'Sue', 24}

   for name, age in data.items():
       print(name, age)

   # Sally 10
   # Sue 24
   ```

2. Loop through using `zip()`:

   ```python
   names = ['Sally', 'Sue']
   ages = [10, 24]
   for name, age in zip(names, ages):
       print(f'My name is {name} and age is {age}')

   # My name is Sally and age is 10
   # My name is Sue and age is 24
   ```

3. Loop over a sequence in reverse using `reversed()`:

   ```python
   for n in reversed(range(1,10,2)):
       print(n) # 9, 7, 5, 3, 1

   ```

4. Loop over a sequence using `sorted()`:

   ```python
   a = [2, 1, 3]
   for num in sorted(a): # Creates a new sorted list
       print(num) # 1, 2, 3
   ```

5. Use `set()` to delete duplicates:

   ```python
       basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
       for f in sorted(set(basket)):
           print(f) # apple, banana, orange, pear
   ```

6. Create a new list instead when you are changing a list inside a loop.

## 5.11 More on Conditions

1. Difference between `==`, `!=`, and `is`, `is not`:

   - `==` and `!=` compare the values of objects.
   - `is` and `is not` compare the identities (same memory location).

2. Comparison chaining:

   - `a < b == c` is same as `(a < b) == c`.
   - `A and not B or C` is same as `(A and (not B)) or C`.

3. `and` and `or` are short-circuit operators:

   - `a and b and c` if a is true and b is false, it won't evaluate c.

4. Assigning result of a comparison:

   ```python
   string1, string2, string3 = '', 'Trondheim', 'Hammer Dance'
   non_null = string1 or string2 or string3
   non_null
   'Trondheim'
   ```

## 5.12 Comparing Sequences

Comparison uses lexicographical ordering:

```python
(1, 2, 3)              < (1, 2, 4)
[1, 2, 3]              < [1, 2, 4]
'ABC' < 'C' < 'Pascal' < 'Python'
(1, 2, 3, 4)           < (1, 2, 4)
(1, 2)                 < (1, 2, -1)
(1, 2, 3)             == (1.0, 2.0, 3.0)
(1, 2, ('aa', 'ab'))   < (1, 2, ('abc', 'a'), 4)
```
