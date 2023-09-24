---
title: "[Python] Solve Import X could not be resolved in VSCode"
date: 2023-09-24
categories: [Dev, Python]
tags: [Python]
---

## Problem

Recently, I have been developing a fastapi project in a virtual environment. 

However, when I tried to import modules, I got this error.

> Import "X" could not be resolved by Pylance (reportMissingImports)
{: .prompt-warning}

I found out that this problem was related to a missing ***additional path*** where `pip` had installed the modules that I wanted to import.

## Solution

1. First, we need to find the location of the imported module:

    ```text
    $ python
    >>> import modulename
    >>> print(modulename.__file__)
    ```

2. Open settings in VSCode.

3. Search ***pylance***.

4. Find the ***Extra Paths*** config item.

5. Select ***add item*** to add a path to the parent folder of the module. 
    - It won't do any *recursive tree searching*.

![d](/assets/img/python/extra-path.png)