---
title: "[JS] Data Types - Strings"
date: 2023-09-13
categories: [Dev, JavaScript]
tags: [JavaScript]
---

## Contents

- [1. Backticks](#1-backticks)
- [2. String Length](#2-string-length)
- [3. Accessing Characters](#3-accessing-characters)
- [4. String are Immutable](#4-strings-are-immutable)
- [5. Lower and Upper Case](#5-lower-and-upper-case)
- [6. Substring](#6-substring)
- [7. Comparing Strings](#7-comparing-strings)

## 1. Backticks

- Inside backticks, strings could be represented with **newline**.

```jsx
let str1 = "Hello\nWorld"; // two lines using a "newline symbol"

// two lines using a normal newline and backticks
let str2 = `Hello
World`;

alert(str1 == str2); // true
```

## 2. String Length

- `length` **property** has the string length

```jsx
alert(`My\n`.length); // 3
```

> **Note:** `length` is a property
>
> Calling `str.length()` does **not work**.
>
> `str.length` is a **numeric property** not a function.

## 3. Accessing Characters

We can use square brackets `[pos]` or `str.at(pos)` to access characters.

- Square brackets does not support **negative index**. (will return undefined)
- `str.at(pos)` supports **negative index**.

```jsx
let str = `Hello`;

alert(str[-2]); // undefined
alert(str.at(-2)); // l
```

## 4. Strings are Immutable

Strings **can't** be changed in JavaScript.

```jsx
let str = "Hi";

str[0] = "h"; // error
alert(str[0]); // doesn't work
```

We would have to use **concatenation** instead and assign it to a new variable.

```jsx
let str = "Hi";

str = "h" + str[1]; // replace the string

alert(str); // hi
```

## 5. Lower and Upper Case

`toLowerCase()` and `toUpperCase()` can be used to change the string.

```jsx
alert("Interface".toUpperCase()); // INTERFACE
alert("Interface".toLowerCase()); // interface

// Only Single Character is Lower Cased
alert("Interface"[0].toLowerCase()); // 'i'
```

## 6. Substring

1. `str.slice(start [, end])`

   Returns the string from **start** to **end** (does not include end).

   For example:

   ```jsx
   let str = "stringify";
   alert(str.slice(0, 5)); // 'strin'
   alert(str.slice(0, 1)); // 's'
   ```

   Slice goes to **end**, if there is **no second argument**:

   ```jsx
   let str = "stringify";
   alert(str.slice(2)); // 'ringify', from the 2nd position till the end
   ```

   Negative values are also possible:

   ```jsx
   let str = "stringify";
   alert(str.slice(-4, -1)); // 'gif'
   ```

2. `str.substring(start [, end])`

   Same as `slice`, but allows `start` to be greater than `end`. This simply swaps the `start` and `end` value.

   ```jsx
   let str = "stringify";

   // these are same for substring
   alert(str.substring(2, 6)); // "ring"
   alert(str.substring(6, 2)); // "ring"

   // ...but not for slice:
   alert(str.slice(2, 6)); // "ring" (the same)
   alert(str.slice(6, 2)); // "" (an empty string)
   ```

3. `str.substr(start [, length])`

   Returns the part of the string from `start`, with `length`.

   ```jsx
   let str = "stringify";
   alert(str.substr(2, 4)); // ring
   ```

   When the first argument is **negative**, it counts from the end:

   ```jsx
   let str = "stringify";
   alert(str.substr(-4, 2)); // 'gi'
   ```

> Which one is most practical?
>
> It is **best** to use `slice`, since it allows **negative arguments** and **shorter** to write.
>
> `substr` has a minor drawback: non-browser environments may fail to support it.

## 7. Comparing Strings

Strings are compared charcter-by-character in **alphabetical** order.

1. Lowercase letter is **always** greater than uppercase:

   ```jsx
   alert("a" > "Z"); // true
   ```

2. Letters with diacritical marks are "out of order":

   ```jsx
   alert("Österreich" > "Zealand"); // true
   ```

3. `str.codePointAt(pos)` returns number representing the character:

   ```jsx
   alert("Z".codePointAt(0)); // 90
   ```

4. `str.fromCodePoint(code)` returns character from number:

   ```jsx
   alert(String.fromCodePoint(90)); // Z
   ```

5. `str1.localeCompare(str2)` returns an integer `str1` is >, =, < than `str2` according to **language rules**.

   ```jsx
   alert("Österreich".localeCompare("Zealand")); // -1
   ```
