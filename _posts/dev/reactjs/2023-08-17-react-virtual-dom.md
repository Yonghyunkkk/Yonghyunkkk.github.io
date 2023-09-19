---
title: "[ReactJS] What is Virtual DOM?"
date: 2023-08-17
categories: [Dev, ReactJS]
tags: [ReactJS]
---

## Introduction

We all know that React uses virtual DOM to optimize performance. However, do we really know what virtual DOM is? In this article, we are going to learn about what virtual DOM is and its advantages. Lets get started!!

## What is DOM?

![d](/assets/img/react/DOM.png)

Before we learn about what virutal DOM is, we should first understand what DOM is. DOM, which stands for **Domain Object Model**, represents xml or html documents as a **tree structure**.

For example, when we request a webpage to the server, we recieve a HTML document as a response. This HTML document is then converted to a tree structure to show the user the requested page in the browser. This tree structure is DOM.

DOM acts as an interface for the web document so that JavaScript and other scripting languages can modify, access, and interact with the document's content. For example, we use DOM APIs like `addEventListener()` to add events.

## Problem using DOM

The problem of DOM manipulation is that re-rendering is expensive. Every time you make a change to an element, the DOM will re-render that element and all of its children. This could become very costly if we are working on a big web application, which would slow down the performance.

## How does virtual DOM solve this?

![d](/assets/img/react/VirtualDom.png)

When we render an application user interface, React will create a virtual DOM for that user interface. This virtual DOM will be stored in memory as a JavaScript object. When we make modification to the user interface, a new virtual DOM will be created with the updated change.

> **Note:** Virtual DOM is just an object representing the UI, nothing gets painted.

After the new virtual DOM is created, React will use an algorithm called **reconciliation** to detect the changes made to the UI by comparing the new virtual DOM and the previous virtual DOM.

After finisihing this process, React will use this information to update and repaint the **actual DOM**. This improves the overall performance since it will only repaint the updated node in the actual DOM.

## Conclusion

In conclusion, virtual DOM is an optimization technique that can be used with libraries like ReactJS, which increases the overall performance of a web application.
