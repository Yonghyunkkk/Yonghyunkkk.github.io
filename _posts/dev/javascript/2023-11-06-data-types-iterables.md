---
title: "[JS] Data Types - Iterables"
date: 2023-11-06
categories: [Dev, JavaScript]
tags: [JavaScript]
---

## 1. String is Iterable

String can use `for..of` loops to iterate over its characters.

```jsx
for (let char of 'text'){
  console.log(char); // t, then 2, then x, then t
}
```

## 2. Iterables and Array-Likes

*Iterables* and *Array-Likes* are different from each other.

- ***Iterables*** are objects that implement the `Symbol.iterate` (`for..of` method) method.
- ***Array-Likes*** are objects that have `indexes` and `length`.

String would be both an *iterable* and *array-like*, because `for..of` and `length` works. However, an object would be an *array-like*, not *iterable*.

```jsx
let arrayLike = { // has indexes and length => array-like
  0: "Hello",
  1: "World",
  length: 2
};

// Error (no Symbol.iterator)
for (let item of arrayLike) {}
```

## 3. Array.from

Then, how can we make an *iterable* or *array-like* value to a **real** Array? We can use `Array.from` for this.

```jsx
let arrayLike = {
  0: "Hello",
  1: "World",
  length: 2
};

let arr = Array.from(arrayLike); // (*)
alert(arr.pop()); // World (method works)
```

Also, we can add a mapping function to it.

```jsx
// square each number
let arr = Array.from(range, num => num * num);

alert(arr); // 1,4,9,16,25
```


