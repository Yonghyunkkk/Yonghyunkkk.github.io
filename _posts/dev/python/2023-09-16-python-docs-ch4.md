---
title: "[Python] Ch4. More Control Flow Tools"
date: 2023-09-16
categories: [Dev, Python]
tags: [Python]
---

## 4.1 `for` statements

Modifying the collection while iterating over the same collection is **tricky to get right**.

**Instead:**

1. Create a copy.
2. Create a new collection.

```python
users = {'Bob': 'active', 'John': 'inactive'}

# Create a copy
for user, status in users.copy().items():
    if status == "inactive":
        del users[user]

# Create a new collections
new_users = {}
for user, status in users.items():
    if status == "active":
        new_users[user] = status
```

## 4.2 `range()`

```python
list(range(0, 10, 3)) # [0, 3, 6, 9]

list(range(-10, -100, -40)) # [-10, -50, -90]
```

## 4.3 `break`, `continue`, and `else` on loops

1. `break` statement breaks out from the **innermost** `for` or `while` loop.
2. `for` and `while` loops can add `else` clause.
   - `for`: `else` clause runs after final iteration is finished.
   - `while`: `else` clause runs after condition becomes false.
   - If loop is terminated by a `break`, the `else` clause does not executes for both `for` and `while`.

```python
for i in range(2, 5):
    for j in range(2, i):
        if i % j == 0:
            print(f'{i} is not a prime number')
            break
    else:
        print(f'{i} is a prime number')

2 is a prime number
3 is a prime number
4 is not a prime number
```

## 4.4 `pass` Statements

`pass` statements does **nothing**.

They are used for **placeholder statements**.

```python
while True:
    pass
```

## 4.5 `match` Statements

`match` statement takes a value and compares its value to successive patterns.

```python
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"
```

We can use the `|` operator instead.

```python
case 401 | 403 | 404:
return "Not Allowed"
```

## 4.6 functions

- The actual parameters (arguments) to a function call are introduced in the local symbol table of the called function when it is called.
- Arguments are passed using call by value, where the value is always an object reference, not the value of the object.
- When a function calls another function or calls itself recursively, a new local symbol table is created for that call.

## 4.6.1 Default Argument Values

Using **default values** for arguments enabled a function to be called with fewer arguments.

```python
def say_hello(prompt, retries=4, reminder="Please say hello"):
    #some code in this function

```

For example, you can call this function in 3 different ways:

- `say_hello('Hi!')`: Only provide the **mandatory** argument.
- `say_hello('Hi!', 3)`: Provide one of the optional argument.
- `say_hello('Hi!', 3, 'Hello')`: Provide both of the optional argument.

```python
def add_number(num, L=None):
    if L is None:
        L = []
    L.append(num)
    return L
```

> **Note:** Mutable objects should use `None` for default values.

## 4.6.2 Keyword Arguments

Functions can be called using `kwarg=value`.

```python
def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
    print("-- This parrot wouldn't", action, end=' ')
    print("if you put", voltage, "volts through it.")
    print("-- Lovely plumage, the", type)
    print("-- It's", state, "!")

parrot(1000)                                          # 1 positional argument
parrot(voltage=1000)                                  # 1 keyword argument
parrot(voltage=1000000, action='VOOOOOM')             # 2 keyword arguments
parrot(action='VOOOOOM', voltage=1000000)             # 2 keyword arguments
parrot('a million', 'bereft of life', 'jump')         # 3 positional arguments
parrot('a thousand', state='pushing up the daisies')  # 1 positional, 1 keyword

parrot()                     # required argument missing
parrot(voltage=5.0, 'dead')  # non-keyword argument after a keyword argument
parrot(110, voltage=220)     # duplicate value for the same argument
parrot(actor='John Cleese')  # unknown keyword argument
```

> **Note:** Keyword arguments must follow positional arguments.

Final formal parameter in the form `**arg_name` receives a **dictionary**.

```python
def cheeseshop(kind, *arguments, **keywords):
    print("-- Do you have any", kind, "?")
    print("-- I'm sorry, we're all out of", kind)
    for arg in arguments:
        print(arg)
    print("-" * 40)
    for kw in keywords:
        print(kw, ":", keywords[kw])

cheeseshop("Limburger", "It's very runny, sir.",
           "It's really very, VERY runny, sir.",
           shopkeeper="Michael Palin",
           client="John Cleese",
           sketch="Cheese Shop Sketch")

-- Do you have any Limburger ?
-- I'm sorry, we're all out of Limburger
It's very runny, sir.
It's really very, VERY runny, sir.
----------------------------------------
shopkeeper : Michael Palin
client : John Cleese
sketch : Cheese Shop Sketch
```

## 4.6.4 Special Parameters

1. Use **positional-only** when you don't want users to know the name of parameters.
2. Use **keyword-only** when names have meaning.
3. Use **positional-only** for **api**.

```python
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
```

## 4.6.5 Arbitrary Argument Lists

Use `*args` for arbitrary number of arguments.

```python
def concat(*args, sep="/"):
    return sep.join(args)

concat('orange', 'apple') # orange.apple
```

## 4.6.6 Unpacking Argument Lists

Arguments that are in an array or tuple can be unpacked for a function call.

```python
args = [3,6]
list(range(*args)) # [3, 4, 5]
```

This can work with dictionaries also.

```python
def parrot(voltage, state="a stiff", action="voom"):
    print(voltage, stage, action)

d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
parrot(**d) #four million bleedin VOOM
```

## 4.6.7 Lambda Expressions

Lambda function is a small, anonymous function that is defined without a name.

```python
lambda arguments: expression

data = [(2, "Apple"), (1, "Banana"), (3, "Orange")]
sorted_data = sorted(data, key=lambda x: x[1])
print(sorted_data)
# Output: [(2, "Apple"), (1, "Banana"), (3, "Orange")]
```

## 4.6.8 Documentation Strings

Also known as **docstrings**, are used to provide information about modules, classes, functions, and methods.

```python
def multiply(x, y):
    """Multiplies two numbers and returns the result."""
    return x * y

print(multiply.__doc__)
# Multiplies two numbers and returns the result.
```

## 4.6.9 Function Annotations

Optional metadata information about the types used by user-defined functions.

- Use a colon for parameter name.
- Use -> for return type.

```python
def add(x: int, y: int) -> int:
    return x + y
```
