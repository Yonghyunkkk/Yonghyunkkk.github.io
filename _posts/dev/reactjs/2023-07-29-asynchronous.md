---
title: "[JS] Asyncrhonous, Promises, and Async/Await"
date: 2023-07-29
categories: [Dev, ReactJS]
tags: [ReactJS]
---

## Asynchronous vs Synchronous

Synchronous and asynchronous code are two ways of executing code in a program. **Synchronous code executes one after the other**, blocking execution until a task is completed, while **asynchronous code allows the program to continue executing while waiting for a task to complete**. Asynchronous code is particularly useful when dealing with tasks that require waiting for external resources, such as fetching data from a server, since it allows the program to execute other code while waiting for the data to be fetched.

## CallBack Functions

In JavaScript, asynchronous code is often implemented using callbacks, promises, or async/await syntax. A callback function is **any function that is passed as an argument to another function**, so that it can be executed in that other function. Its main purpose is to execute code in response to an event, such as the completion of an asynchronous operation. Callbacks are commonly used to handle the results of asynchronous operations, but they can lead to a concept known as "callback hell" when too many nested callbacks are used, making the code difficult to understand and manage.

## Promises

Promises are **objects that represent the eventual completion or failure of an asynchronous operation**. They are immutable and execute the callback function only once. Promises solve the issue of callback hell by using then and catch to chain the different promises returned. This allows for a more structured and readable code.

## Async/Await

Async/await is a newer syntax introduced in ES2017 that simplifies the process of writing asynchronous code. It helps developers write more readable code and solves the disadvantages of using callback functions and promises. The async keyword is used in front of a function, which means that the **function will always return a promise**. If the returned object is not a promise, the function wraps the object with a promise and returns it. The **await keyword can only be used inside an async function**, and its role is to wait until a promise is finished before executing the next line of code. While it waits until the promise finishes, the CPU works on different parts of the program, which prevents the CPU from wasting resources.

## Conclusion

Overall, asynchronous code is an important part of modern JavaScript programming, and using various techniques such as callbacks, promises, and async/await can help simplify the process of working with asynchronous operations and make your code more readable and maintainable.
