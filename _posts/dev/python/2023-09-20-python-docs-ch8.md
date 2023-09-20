---
title: "[Python] Ch8. Errors and Exceptions"
date: 2023-09-20
categories: [Dev, Python]
tags: [Python]
---

## 8.1 Syntax Errors

- Also known as **parsing errors**:

```python
while True print('Hello world')
    File "<stdin>", line 1
    while True print('Hello world')
                ^
    SyntaxError: invalid syntax
```

## 8.2 Exceptions

```python
10 * (1/0) # ZeroDivisionError

4 + name * 3 # NameError

'2' + 2 # TypeError
```

## 8.3 Handling Exceptions

- Use `try / except`.

```python
while True:
    try:
        x = int(input("Please enter a number: "))
        print('This is the statement after input.')
        y = 1 / x
        print(y)
        break
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")
    except ZeroDivisionError:
        print("The number should be greater than 0. Try again...")

'''
Please enter a number: 0
This is the statement after input.
The number should be greater than 0. Try again...
Please enter a number: f
Oops!  That was no valid number.  Try again...
Please enter a number: 1
This is the statement after input.
1.05
'''
```

- You can use a `tuple` to group multiple exceptions together:

```python
except (RuntimeError, TypeError, NameError):
    pass
```

- The `else` clause can be used to add code if *try clause* does not raise an exception:

```python
while True:
    try:
        x = int(input("Please enter a number: "))
        print('This is the statement after input.')
        y = 1 / x
        print(y)
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")
    except ZeroDivisionError:
        print("The number should be greater than 0. Try again...")
    else:
        print('Success!!')
        break

'''
Please enter a number: 1
This is the statement after input.
1.0
Success!!
'''
```

- Exception handlers also handle exceptions that occur inside functions:

```python
def this_fails():
    x = 1/0

try:
    this_fails()
except ZeroDivisionError as err:
    print('Handling run-time error:', err)

# Output: Handling run-time error: division by zero
```

## 8.4 Raising Exceptions

- Use `raise` to **force** a specified exception:

```python
raise NameError('HiThere')
'''
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere
'''
```

## 8.5 Clean-up Actions

- Use `finally`:

```python
def bool_return():
    try:
        return True
    finally:
        return False

bool_return()
# False
```

## 8.6 Predefined Clean-up Actions

- `with` ensures that a file is closed even if a problem is encountered:

```python
with open("my.txt") as f:
    for line in f:
        print(line, end="")
```
