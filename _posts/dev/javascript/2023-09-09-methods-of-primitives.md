---
title: "[JS] Methods of Primitives"
date: 2023-09-09
categories: [Dev, JavaScript]
tags: [JavaScript]
---

## Introduction

Javascript enables us to use **primitives** (string, numbers, etc.) as objects and use methods with it. Primitives can't use methods directly since they are not objects. Let's take a look at how this works.

## Solution

Here is an example.

```jsx
let num = 123;

console.log(num.toString()); // 123 (type string)
```

1. `num` is a primitive number.
2. `num` is implicitly converted to a **Number** object when we call `toString()` method on `num`.
   - This is known as **autoboxing** or **implicit type coercion**.
   - JS automatically wraps the primitive value in its corresponding **wrapper object** to access the method.
3. The method runs and returns a new string (shown by console).
4. The object is destroyed, leaving the primitive `num` alone.

So, if we look at the whole process, it will look something like this.

```jsx
let num = 123;
console.log(typeof num); // Output: "number"

let numObject = new Number(num);
console.log(typeof numObject); // Output: "object"

console.log(numObject.toString()); // Output: "123"
```

## Conclusion

JavaScript primitive types work with temporary objects to use methods. JavaScript engines are well tuned to optimize that internally, so they are not expensive to call.
