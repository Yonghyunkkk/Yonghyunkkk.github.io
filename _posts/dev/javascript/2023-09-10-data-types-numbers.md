---
title: "[JS] Data Types - Numbers"
date: 2023-09-10
categories: [Dev, JavaScript]
tags: [JavaScript]
---

## Contents

- [1. Ways to Write Numbers](#1-ways-to-write-numbers)
- [2. toString(base)](#2-tostringbase)
- [3. Rounding](#3-rounding)
- [4. Imprecise Calculations](#4-imprecise-calculations)
- [5. parseInt and parseFloat](#5-parseint-and-parsefloat)
- [6. Other Math Functions](#6-other-math-functions)

## 1. Ways to Write Numbers

- Different ways to write 1 billion.

```jsx
let billion = 1000000000;
let billion = 1_000_000_000;
let billion = 1e9;
```

- Different ways to write 0.001.

```jsx
let num = 0.001;
let num = 1e-3;
```

## 2. toString(base)

- Returns a **string** representation of a number
- **Two dots** to call a method.

  - If we want to call a method directly on a number, use **two dots**.

  ```text
  123..toString()
  ```

  - JavaScript syntax implies the decimal part after the first dot.

  - We can also use

  ```text
  (123).toString()
  ```

## 3. Rounding

- `Math.floor`

  - Rounds down: `3.1` becomes `3`, and `-1.1` becomes `-2`.

- `Math.ceil`

  - Rounds up: `3.1` becomes `4`, and `-1.1` becomes `-1`.

- `Math.round`

  - Rounds to the nearest integer: `3.1` becomes `3`, and `3.5` becomes `4`.

- `Math.trunc`

  - Removes anything after the decimal point: `3.1` becomes `3`.

- Round to `n-th digit`

  1. Multiply-and-divide

     ```jsx
     let num = 1.23456;

     console.log(Math.round(num * 100) / 100); // 1.23
     ```

  2. `toFixed(n)`: round numbers to `n`digits after point and returns a **string**

     ```jsx
     let num = 12.36;

     console.log(num.toFixed(1)); // "12.4"

     let num2 = 12.34;

     console.log(num.toFixed(5)); // "12.34000" zeroes added to match exactly 5
     ```

## 4. Imprecise Calculations

```jsx
console.log(0.1 + 0.2 == 0.3); // false

console.log(0.1 + 0.2); // 0.30000000000000004
```

This example returns **false** because there is no way to **store exactly** 0.1 or 0.2. The most **reliable** way to solve this problem is to use the method `toFixed(n)`. Remember that `toFixed(n)` returns a string. We can use the **unary plus** to coerce it into a number.

```jsx
let sum = 0.1 + 0.2;

console.log(+sum.toFixed(2)); // 0.3
```

## 5. parseInt and parseFloat

Numeric conversion using `+` and `Number` is **strict**. It only accepts a values that is exactly a number. For example, this won't work since it has a string in it.

```jsx
console.log(+"100px"); // NaN
```

To solve this kind of error, we can use `parseInt` and `parseFloat`. They **read** a number from a string until they can't.

- `parseInt`: returns an **integer**
  - Second Parameter: specifies the **base** of numeral system.
- `parseFloat`: returns a **float**

```jsx
alert(parseInt("100px")); // 100
alert(parseFloat("12.5em")); // 12.5

alert(parseInt("12.3")); // 12, only the integer part is returned
alert(parseFloat("12.3.4")); // 12.3, the second point stops the reading
```

## 6. Other Math Functions

- `Math.random()`

  - Returns a random number from 0 to 1 (not including 1).

  ```jsx
  alert(Math.random()); // 0.1234567894322
  alert(Math.random()); // 0.5435252343232
  ```

- `Math.max() & Math.min()`

  - Returns the max and min number.

  ```jsx
  alert(Math.max(3, 5, -10, 0, 1)); // 5
  alert(Math.min(1, 2)); // 1
  ```

- `Math.pow(n, power)`
  - Returns `n` raised to the given power.
  ```jsx
  alert(Math.pow(2, 10)); // 2 in power 10 = 1024
  ```
