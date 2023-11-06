---
title: "[JS] Data Types - Map and Set"
date: 2023-11-06
categories: [Dev, JavaScript]
tags: [JavaScript]
---

## 1. Map

**Map** is a collection of keyed data items, just like an `Object`.

The difference between `Map` and `Object` is that `Map` allows keys of any type.

## 2. Map Methods

Here are the methods that can be used with `Map`.

- `new Map()` - creates a new map.
- `map.set(key, val)` - stores value by key
- `map.get(key)` - returns the value by key, `undefined` if `key` doesn't exist.
- `map.has(key)` - returns `true` if key exits, otherwise `false`.
- `map.delete(key)` - removes the element (key/value pair) by key.
- `map.clear()` - removes everything from the map.
- `map.size` - return the current element count.

For example,

```jsx
map.set('1', 'str1');   // a string key
map.set(1, 'num1');     // a numeric key
map.set(true, 'bool1'); // a boolean key

// remember the regular Object? it would convert keys to string
// Map keeps the type, so these two are different:
alert( map.get(1)   ); // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3
```

One thing here is to notice that unlike `Objects`, `Map` does not convert the **key** to strings!!

> `map[key]` isn't the right way to use a `Map`
>
> Although `map[key]` also works, this is treating a `map` as an `object`, applying all corresponding limitations on an `object` (only string/symbol keys and so on).
>
> Hence, we should use `map` methods: `set`, `get`, and so on...
{: .prompt-tip}

One **important** property of `Map` is that it can use an `object` as keys.

```jsx
let john = { name: "John" };

// for every user, let's store their visits count
let visitsCountMap = new Map();

// john is the key for the map
visitsCountMap.set(john, 123);

alert( visitsCountMap.get(john) ); // 123
```

> How `Map` compares keys
>
> `Map` uses roughly the same as strict equaility `===`, but the difference is that `NaN` is considered equal to `NaN`.
>
> Hence, `NaN` can be used as a key.
{: .prompt-tip}

> Chaining
>
> Every `map.set` call returns the map itself, so we can **chain** the calls.
{: .prompt-tip}

## 3. Map Iteration

There are 3 methods:

- `map.keys()` - returns an iterable for keys.
- `map.values()` - returns an iterable for values.
- `map.entries()` - returns an iterable for entries `[key, val]`, used by default in `for..of`.

For example:

```jsx
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion',    50]
]);

// iterate over keys (vegetables)
for (let vegetable of recipeMap.keys()) {
  alert(vegetable); // cucumber, tomatoes, onion
}

// iterate over values (amounts)
for (let amount of recipeMap.values()) {
  alert(amount); // 500, 350, 50
}

// iterate over [key, value] entries
for (let entry of recipeMap) { // the same as of recipeMap.entries()
  alert(entry); // cucumber,500 (and so on)
}
```

> `Map` preserves order
>
> Unlike a regular `Object` where the order is not preserved, `Map` preserves the order of values inserted.
{: .prompt-tip}

Also, `Map` has a `forEach` method:

```jsx
// runs the function for each (key, value) pair
recipeMap.forEach( (value, key, map) => {
  alert(`${key}: ${value}`); // cucumber: 500 etc
});
```

## 4. Map from Object

```jsx
let obj = {
  name: "John",
  age: 30
};

let map = new Map(Object.entries(obj));

alert( map.get('name') ); // John
```

`Object.entries` returns the array of key/value pairs: `[ ["name","John"], ["age", 30] ]`.

## 5. Object from Map

```jsx
let map = new Map();
map.set('banana', 1);
map.set('orange', 2);
map.set('meat', 4);

let obj = Object.fromEntries(map.entries()); // make a plain object (*)

// done!
// obj = { banana: 1, orange: 2, meat: 4 }

alert(obj.orange); // 2
```

## 6. Set

A `Set` is a collection of values where each value **only occurs once**.

It is much better for uniqueness checks.

## 7. Set Methods

- `new Set([iterable])` - creates a set, if `iterable` is provided, copies values from it into set.
- `set.add(val)` - add a value and returns the set itself.
- `set.delete(val)` - removes value, return `true` if `value` existed, otherwise `false`.
- `set.has(val)` - returns `true` if value exists, otherwise `false`.
- `set.clear()` - removes everything from the set.
- `set.size` - total number of elements.

## 8. Iteration over Set

We can use `for..of` or `forEach`.

```jsx
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// the same with forEach:
set.forEach((value, valueAgain, set) => {
  alert(value);
});
```

> `forEach` has 3 arguments. This is for compatibility with `Map`. This may help replace `Map` with `Set` in the future.
{: .prompt-tip}

Same methods `Map` has for iterators are also supported:

- `set.keys()` - returns an iterable object for values.
- `set.values()` - same as `set.keys()`.
- `set.entries()` - returns an iterable object for entries `[val, val]`.
