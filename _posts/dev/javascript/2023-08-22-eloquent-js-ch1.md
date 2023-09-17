---
title: "[Eloquent JS] Ch1. Values, Types, & Operators"
date: 2023-08-22
categories: [Dev, JavaScript]
tags: [JavaScript]
---

## 1. Unary Operators

- Operators that take only one value (typeof, !).
- Minus operator can be **both** binary and unary.

```jsx
console.log(typeof 4.5);
// -> number

console.log(-(10 - 2));
// -> -8
```

## 2. Comparison

- Strings are ordered **alphabetically**.
- Uppercase letters are always **"less"** than lowercase letters `'Z' < 'a'`.
- **Nan** is the only value is JS that is not equal to itself.

```jsx
console.log("Aardvark" < "Zoroaster");
// → true

console.log(NaN == NaN);
// → false
```

## 3. Empty Values

- `null` and `undefined` are themselves values, but carry no information.
- Treat them mostly interchangeable.

```jsx
console.log(null == undefined);
```

## 4. Automatic Type Conversion

- JS automatically **converts** the value to the type it needs, when an operator is applied to the **"wrong"** type of value **(type coercion)**.
- When a value does not map to a number in an obvious way, it converts to **NaN**.

```jsx
console.log(8 * null);
// → 0
console.log("5" - 1);
// → 4
console.log("5" + 1);
// → 51
console.log("five" * 2);
// → NaN
console.log(false == 0);
// → true
console.log("" == 0);
// → true
```

- `null` and `undefined` only produces **true**, when both sides are `null` or `undefined`
- We can use this behavior to check whether a value has a real value or not.

```jsx
console.log(null == undefined);
// → true
console.log(null == 0);
// → false
```

- If you do not want type conversions, you can use the **strict equality operator:** `===` and `!==`.
- Checks whether the values are **precisely equal** to one another.
- Use **strict equality operator** for most of the time.

```jsx
console.log("" === false);
// → false
```

## 5. Short Circuiting of Logical Operators

- `||` and `&&` can be used to handle values of different types.
- `||` will return the value to its **left** when it can be converted to **true**, otherwise **false**.
- Useful to check whether a value is empty, by placing the **replacement value** on the **right**.

```jsx
console.log(null || "user");
// → user
console.log("Agnes" || "user");
// → Agnes
```

- `&&` will return the value to its **right** when it can be converted to **true**, otherwise **false**.

```jsx
console.log(null && "user");
// → null
console.log("Agnes" && "user");
// → user
```

- Part on their **right** will only be evaluated **when necessary** (short-circuit evaluation).
- `true || x` will only check the left part since it is true
- `false && x` will only check the right part since it is false
