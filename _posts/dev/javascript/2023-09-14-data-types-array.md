---
title: "[JS] Data Types - Arrays"
date: 2023-09-20
categories: [Dev, JavaScript]
tags: [JavaScript]
---

## 1. Declaring an Array

Array is an object.

```jsx
let arr = new Array();
let arr = [];
```

## 2. Adding an Element

```jsx
let fruits = ['orange', 'grape'];
fruits[2] = 'lemon';
console.log(fruits) // ['orange', 'grape', 'lemon'];

console.log(fruits.length) // 3
```

## 3. Storing Different Types

```jsx
let arr = [ 'Apple', {quantity: 3}, function() { alert('Hi'); } ];
console.log(arr[1].quantity); // 3
console.log(arr[2]()); // 'Hi'
```

> Trailing Comma
>
> Arrays can end with a comma:
> ```jsx
  let fruits = [
  "Apple",
  "Orange",
  "Plum",
];
```
> Makes it easier to remove or add elements.
{: .prompt-info}

## 4. Get Elements

JavaScript can't use a negative index for ***square brackets***.

- Calculate the last index instead:

```jsx
let fruits = ['Apple', 'Orange']
console.log(fruits[fruits.length - 1]) // 'Orange'
```

- Or use `.at()`:

```jsx
let fruits = ['Apple', 'Orange']
console.log(fruits.at(-1)) // 'Orange'
```

## 5. Use Array as Queue

```jsx
let fruits = ['apple', 'orange']

fruits.push('pear') // add pear to the end

fruits.shift() // removes apple

console.log(fruits) // orange, pear
```

## 6. Use Array as Stack

```jsx
let fruits = ['apple', 'orange']

fruits.push('pear') // add pear to the end

fruits.pop() // removes pear

console.log(fruits) // apple, orange
```

## 7. Unshift

- Adds an element to the beginning of an array:

```jsx
let fruits = ['apple', 'orange']

fruits.unshift('pear')

console.log(fruits) // pear, apple, orange
```

## 8. Internals

Arrays are special structures to work with ***ordered data***.

> - Don't add ***non-numeric properties*** like arr.test = 5.
>
> - Don't make ***holes*** like arr[0] = 0 and arr[10000] = 0.
>
> - Don't fill the array in ***reverse-order*** like arr[999], arr[998].
{: .prompt-danger}

## 9. Loops

- Use `for`:

```jsx
let arr = ["Apple", "Orange", "Pear"];

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

- Use `for...of`:

```jsx
let arr = ["Apple", "Orange", "Pear"];

for (let fruit of fruits) {
    console.log(fruit);
}
```

- **Don't** use `for...in`:
    - This also works for arrays, but it iterates over ***all properties***, not only the numeric ones.
    - It is more suitable for ***generic objects***.
    - 10 - 100 times slower.

## 10. Length

The `length` property does not count the number of values in the array. It actually returns the ***greatest numeric index plus one*** of the array.

```jsx
let fruits = [];
fruits[123] = 'apple';
console.log(fruits.length) // 124
```

- It also can be used to clear an array:

```jsx
let arr = [1, 2, 3, 4, 5];

arr.length = 3;
console.log(arr); // [1, 2, 3]

arr.length = 5; // return the length back (won't work)
console.log( arr[4] ) // undefined: the values aren't returned
```

## 11. Use [] instead of `new Array`

When `new Array` is called with a single argument as a ***number***, it declares an array with the single argument as the ***length***.

```jsx
let arr = new Array(2);

console.log(arr[0]); // undefined: no elements

console.log(arr.length); // 2
```

## 12. Multidimensional Array

```jsx
let arr = [
    [1, 2, 3],
    [4, 5, 6],
]

console.log( arr[1][1] ) // 5
```

## 13. toString

- `toString` returns a ***comma-separated list*** of items:

```jsx
let arr = [1, 2, 3];

console.log(String(arr) === '1,2,3'); // true
```

- We can use `square brackets` also:

```jsx
alert( [] + 1 ); // "1"
alert( [1] + 1 ); // "11"
alert( [1,2] + 1 ); // "1,21"
```

## 14. Don't Compare Arrays with ==

Let's recap the rules for `==`:

> Two objects are equal `==` only when the ***reference*** the same object.
>
> If one argument is an object and the other primitive, the object gets ***converted*** to a primitive.
{: .prompt-info}

- For example:

```jsx
alert( [] == [] ); // false
alert( [0] == [0] ); // false
```

> They are different since they reference different objects.

- True due to type conversion:

```jsx
// after [] was converted to ''
alert( 0 == '' ); // true, as '' becomes converted to number 0

alert('0' == '' ); // false, no type conversion, different strings
```

> Use `===` instead.

