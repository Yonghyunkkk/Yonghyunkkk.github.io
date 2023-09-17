---
title: "[ReactJS] Set Up Proxy Server in React"
date: 2023-08-10
categories: [Dev, ReactJS]
tags: [ReactJS]
---

## Problem

My frontend was running over HTTPS and my backend was running over HTTP. I could not change my backend to run over HTTPS, since my backend was running in my company's kubernetes container, which only supported HTTP. I tried changing the insecure content on chrome browser from block to allowed, but this did not solve the problem. After taking some time doing some research, I found out that I need to set up a **proxy server in React**.

## What is a proxy server?

A proxy server is basically a system or application that acts as an intermediary between a client and server when making requests. The proxy server will handle requests from the client and send those requests to the server. Then, it will send the response received from the server back to the client.

## Why is a proxy server used?

1. Protect clients from bad server responses.
2. Cache requests and responses to improve performance.
3. Protect client's data and request that should be made anonymously.
4. Specify requests that are allowed and not.

## Use Cases in React

1. Cross-origin limitations that block HTTPS API requests from HTTPS sites (mixed content error).
2. Fetching data from browsers that does not support CORS.
3. Fetching media resources from server.

## Solution

To solve the mixed content issue, I configured the proxy manually in React.

First, you have to install http-proxy-middleware using npm or yarn.

> **Note:** `react-scripts` should be higher than `@2.0.0`

```bash
npm i http-proxy-middleware
```

Second, create the file `setupProxy.js` in `src/setupProxy.js`. You should change the target to your backend server url. Also, it is a good practice to add /api to your endpoints, so that you can easily detect the api endpoints when reading your code.

> **Note:** You must create the file in this directory.
>
> **Note:** You do not need to import this file anywhere.

```jsx
const { createProxyMiddleware } = require("http-proxy-middleware");

module.exports = function (app) {
  app.use(
    "/api",
    createProxyMiddleware({
      target: "http://localhost:5000",
      changeOrigin: true,
    })
  );
};
```

Set your api request endpoints in this way.

```jsx
const { isLoading, error, data, refetch } = useQuery(["data"], () =>
  axios
    .get("/api/data")
    .then((response) => response.data)
    .catch((error) => {
      console.log(error);
      return [];
    })
);
```

Lastly, you should also set the endpoints in your backend including `/api`, if you haven't done so. It needs to match the request endpoints declared in your frontend.

```python
@app.get("/api/data")
def read_data():
    return {'data' : 1}
```

## Conclusion

By using proxy servers, you are able to achieve better security and performance. Now that you know the use cases of the proxy server in React, I encourage you to use it whenever you find errors related to the use cases mentioned in this article.
