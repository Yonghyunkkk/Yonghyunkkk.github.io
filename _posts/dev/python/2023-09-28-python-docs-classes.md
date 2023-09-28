---
title: "[Python] Ch9. Classes"
date: 2023-09-28
categories: [Dev, Python]
tags: [Python]
---

## 9.1 Python Namespaces

***Namespacing*** is mapping from names to objects. Most ***namespaces*** are implemented as ***dictionaries*** in Python. 

Here are some examples of namespaces in Python:
- Set of built-in names(functions such as `abs()`, built-in exception names)
- Global names in a module.
- Local names in a function invocation.
- Set of attributes inside an object.

> There is no relation between names in different namespaces.
>
> Two different modules can define a function `calculate`.
{: .prompt-tip}

Attributes may be *read-only* or *writable*. For example, you can remove an attribute from an object by `del modname.the_answer`.

Here are some information about namespaces created at different moments:

- The namespace with built-in names is created when the Python interpreter starts and never goes away.
- The global namespace for a module is created when the module's definition is read and typically lasts until   the interpreter exits.
- Top-level statements in the interpreter belong to a module called "main" and have their own global namespace.
- Functions have a local namespace created when they are called and deleted when they return or encounter an unhandled exception.
- Recursive invocations of a function each have their own local namespace.

## 9.2 Python Scopes

***Scope*** is a region of a Python program where a namespace is *directly accessible*. Usually, there are 3 or 4 nested scopes where namespaces are *directly accessible*.

1. The ***innermost scope*** contains **local names**.
2. Any ***enclosing functions*** contains **non-local** and **non-global** names.
3. ***Next-to-last scope*** contains current module's **global names**.
4. ***Outermost scope*** contains **built-in names**.

To *rebind* variables that are outside the ***innermost scope***, we can use the `nonlocal` statement. If we do not delcare this statement, we can **only read** the variable, unable to change the value of the variable.

Here is an example of scopes and namespaces using `global` and `nonlocal`:

```python
def scope_test():
    def do_local():
        spam = "local spam"

    def do_nonlocal():
        nonlocal spam
        spam = "nonlocal spam"

    def do_global():
        global spam
        spam = "global spam"

    spam = "test spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)

scope_test()
print("In global scope:", spam)
```

The result is:

```text
After local assignment: test spam
After nonlocal assignment: nonlocal spam
After global assignment: nonlocal spam
In global scope: global spam
```

## 9.3 Class Objects

Class objects support two operations: ***attribute reference*** and ***instantiation***.

- Attribute Reference: `obj.name`

    ```python
    class MyClass:
    """A simple example class"""
    i = 12345

    def f(self):
        return 'hello world'
    ```

    > `MyClass.i` and `MyClass.f` are attribute references here.

- Instantiation: `x = myClass()`

    ```python
    class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart

    x = Complex(3.0, -4.5)
    print(x.r, x.i) # 3.0, -4.5
    ```

    > We can also use *arguments* when declaring class objects.
    {: .prompt-tip}

## 9.4 Instance Objects

Instance objects have two kind of valid attributes: **data attributes** and **methods**.

- Data attributes correspond to ***instance variables***.
- ***Method*** is a function belonging to an object.

## 9.5 Class and Instance Variables

- ***Instance variables*** are for data **unique** to each instance. 
- ***Class variables*** are for attributes and methods **shared** by all instances of the same class.

    ```python
    class Dog:

    kind = 'canine'         # class variable shared by all instances

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance

    >>> d = Dog('Fido')
    >>> e = Dog('Buddy')
    >>> d.kind                  # shared by all dogs
    'canine'
    >>> e.kind                  # shared by all dogs
    'canine'
    >>> d.name                  # unique to d
    'Fido'
    >>> e.name                  # unique to e
    'Buddy'
    ```

- ***Class variables*** should not declare **mutable** objects.

    ```python
    class Dog:

    tricks = []             # mistaken use of a class variable

    def __init__(self, name):
        self.name = name

    def add_trick(self, trick):
        self.tricks.append(trick)

    >>> d = Dog('Fido')
    >>> e = Dog('Buddy')
    >>> d.add_trick('roll over')
    >>> e.add_trick('play dead')
    >>> d.tricks                # unexpectedly shared by all dogs
    ['roll over', 'play dead']
    ```

> Use instance variables instead for **mutable** objects.
{: .prompt-info}

```python
class Dog:

    def __init__(self, name):
        self.name = name
        self.tricks = []    # creates a new empty list for each dog

    def add_trick(self, trick):
        self.tricks.append(trick)
```

## 9.6 Random Remarks

1. Function outside of a class can be defined:

    ```python
    def fs(self, x, y):
        return min(x, x+y)

    class C:
        f = f1 # define outside function
    ```

2. Methods can call other methods using `self`:

    ```python
    class Bag:
    def __init__(self):
        self.data = []

    def add(self, x):
        self.data.append(x)

    def addtwice(self, x):
        self.add(x)
        self.add(x)
    ```

## 9.7 Inheritance

- Python offers inheritance in clasess also:
    - You must define the `BaseClassName` in your subclass.

    ```python
    class ParentClass:
        def __init__(self, attribute):
            self.attribute = attribute

    class ChildClass(ParentClass):
        def __init__(self, attribute, child_attribute):
            super().__init__(attribute)  # Call the parent class constructor
            self.child_attribute = child_attribute
    ```

- To check whether a class is a subclass or not use:
    1. `isinstance(obj, int)`
        - returns `True` if obj is a subclass of int.

    2. `issubclass()`
        - Checks class inheritance.

- Python also supports ***multiple inheritance***.

```python
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    <statement-N>
```

## 9.8 Private Variables

- Use `_` underscore for naming private variables and methods:

    ```python
    class MyClass:
        def __init__(self):
            self._private_variable = 10  # Declare a private variable with a single underscore prefix

        def _private_method(self):
            # Private method implementation
            pass

        def public_method(self):
            # Access the private variable and private method within the class
            print(self._private_variable)
            self._private_method()
    ```

## 9.9 Odds and Ends

Use `dataclasses` or `pydantic` to declare data types:

```python
from dataclasses import dataclass

@dataclass
class Employee:
    name: str
    dept: str
    salary: int
```