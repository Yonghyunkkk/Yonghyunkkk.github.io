---
title: "[Python] Ch7. Input and Output"
date: 2023-09-19
categories: [Dev, Python]
tags: [Python]
---

## 7.1 Formatted String Literals

- Formatted string literals `f`:

```python
name = 'John'
print(f'Hello my name is {name}.')
# Hello my name is John.

print(f'The value of pi is approximately {math.pi:.3f}.')
# The value of pi is approximately 3.142.
```

- Convert values before formatting:
  - `!a` for **ascii()**
  - `!s` for **str()**
  - `!r` for **repr()**

```python
print(f'My hovercraft is full of {animals!r}.')
# My hovercraft is full of 'eels'.
```

- Expand an expression using `=`:

```python
name = 'John'
area = 'HK'
print(f'He is {name=} {area=}')
# He is name='John' area='HK'
```

## 7.2 String format() Method

- `str.format()`:

```python
name = 'John'
area = 'HK'
print('Hello my name is {0} and I am currently in {1}'.format(name, area))
# Hello my name is John and I am currently in HK.

print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred', other='Georg'))
# The story of Bill, Manfred, and Georg.

table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))
# Jack: 4098; Sjoerd: 4127; Dcab: 8637678
```

## 7.3 Old String Formatting

- Use modulo `%`:

```python
name = 'John'
print('Hello my name is %s' % name)
# Hello my name is John.
```

## 7.4 Reading and Writing Files

- `open(filename, mode, encoding=None)` returns a **file obejct**:

  - 1st arg: filename
  - 2nd arg: mode to be used
    1. `r` for read
    2. `w` for write
    3. `+r` both read and write
  - 3rd arg: Default is `encoding=utf-8`

- `with` keyword:
  - Automatcially **closes** the file after its suite finishes, even though exception is raised.
  - **Shorter** than using `try-finally` blocks.
  - If not using `with`, use `f.close()` to close file and free up system resources.

## 7.5 Methods of File Objects

```text
A trusting little leaf of green,
A bold audacious frost;
A rendezvous, a kiss or two,
And youth for ever lost.
```

1. `f.read(size)`:

   - Reads data and return it as string or bytes object.
   - `size` is an optional argument.

   ```python
   f = open('A Fallen Leaf.txt', 'r')

   print(f.read())

   f.close()

   # A trusting little leaf of green,
   # A bold audacious frost;
   # A rendezvous, a kiss or two,
   # And youth for ever lost.
   ```

2. `f.readline()`:

   - Reads a single line from the file.

   ```python
   f = open('A Fallen Leaf.txt', 'r')

   print(f.readline())

   f.close()

   # A trusting little leaf of green,
   ```

3. Use a `for` loop:

   - Memory efficient, fast, and more simple code.

   ```python
   f = open('A Fallen Leaf.txt', 'r')

   for line in f:
       print(line, end='')

   f.close()

   # A trusting little leaf of green,
   # A bold audacious frost;
   # A rendezvous, a kiss or two,
   # And youth for ever lost.
   ```

4. `f.readlines()`:

   - Stores all the lines to a list.

   ```python
   f = open('A Fallen Leaf.txt', 'r')

   print(f.readlines())

   f.close()

   # ['A trusting little leaf of green,\n', 'A bold audacious frost;\n', 'A rendezvous, a kiss or two,\n', 'And youth for ever lost.']
   ```

5. `f.writes(string)`:

   - Writes _string_ to file and returns the number of characters written.
   - Need to convert to **str** or **bytes object**.

   ```python
   f = open('A Fallen Leaf.txt', 'r+')

   print(f.write('Trees are good.')) # 15

   f.close()
   ```

## 7.6 JSON

We can use `json` to _serialize_ and _deserialize_ data.

- **Serialize:**
  - Take Python data hierarchies and convert them to JSON string representation.
- **Deserialize:**
  - Reconstruct data from JSON string representation.

```python
import json
x = [1, 'simple', 'list']
json.dumps(x)
# '[1, "simple", "list"]'
```
