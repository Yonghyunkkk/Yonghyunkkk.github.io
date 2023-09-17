---
title: "[JS] Difference Between Axios and Fetch"
date: 2023-03-24
categories: [Dev, JavaScript]
tags: [JavaScript]
---

Whenever I made API calls in my project, I used Axios since it was more popular. I did not have a deep understanding of the difference between `Axios` and `fetch()`. To have a better understanding, I decided to write a post on the difference between these two.

## 1. Automatic JSON Data Transformation

**Axios**

- Automatically converts data to `JSON`
- Uses `data` property for request body
- Automatically transforms data from server

**Fetch**

- Transforms data using `JSON.stringify`
- Uses `body` as data property
- Uses `response.json` to parse response data as JSON

## 2. Backward Compatibility

**Axios**

- Wide browser support
  - IE11 (Would not matter since IE service ended)

**Fetch**

- Chrome, FireFox, Edge, Safari

## 3. Response Timeout

**Axios**

- Can use optional `timeoeut` property in config object
  - Set number of ms before request is aborted

**Fetch**

- Can use `AbortController`, but much complex

## 4. HTTP Interceptors

**Axios**

- Ability to intercept HTTP requests
  - Can declare both request/response interceptors

**Fetch**

- Does not provide mechanism to intercept HTTP requests
  - But, can come up with workaround

## 5. Simultaneous Requests

**Axios**

- Use `axios.all()`
  - Pass an array of requests
- Use `axios.spread()`
  - Assign properties of response array to separate variables

**Fetch**

- Use `Promise.all()`
  - Pass all fetch requests as an array
- Handle response using `async` function

## Conclusion

As discussed in the post, it seems that `Axios` is more convenient to use compared to `fetch()` method.
