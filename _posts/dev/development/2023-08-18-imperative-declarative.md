---
title: "[Dev] Imperative VS Declarative Code"
date: 2023-08-18
categories: [Dev, Development]
tags: [Development]
---

## Introduction

It is easy to see the word imperative and declarative when developing code. Most of us know that React has a declarative syntax. What does declarative mean anyway? In this article we will take a loot at what imperative and declarative code is, and their differences.

## Imperative Code

Imperative code tells computer how to do things. It focuses on explicitly specifying the step-by-step instructions for achieving a desired outcome. For example, in this code we explicitly that we want to create a new array with each number multiplied by 2.

```jsx
const numbers = [1, 2, 3, 4, 5];
const doubledNumbers = [];

for (let i = 0; i < numbers.length; i++) {
  doubledNumbers.push(numbers[i] * 2);
}

console.log(doubledNumbers);
```

### Key Characteristics

1. Specifies how to achieve a desired outcome step-by-step.
2. Emphasizes explicit instructions and control flow.
3. Directly manipulates state and data.
4. Relies on loops, conditionals, and mutable variables.

## Declarative Code

Declarative code focuses on what you want from the computer. You define the desired outcome or result, and the underlying system or framework takes care of the implementation details. For example, in this code we define what should be rendered based on the data (users array) without specifying how it should be rendered. React takes care of updating and rendering the user list automatically when the users array changes.

```jsx
import React from "react";

const App = () => {
  const users = ["Alice", "Bob", "Charlie"];

  return (
    <div>
      <h1>User List</h1>
      <ul>
        {users.map((user, index) => (
          <li key={index}>{user}</li>
        ))}
      </ul>
    </div>
  );
};

export default App;
```

### Key Characteristics

1. Describes what should be done rather than how to do it.
2. Emphasizes expressing the desired outcome or result.
3. Abstracts away implementation details.
4. Relies on existing abstractions or frameworks to handle the execution.

## Conclusion

I hope that this clarifies the difference between imperative and declarative programming. Also, many programming languages and frameworks provide support for combining declarative and imperative programming styles. This flexibility allows developers to leverage the benefits of both paradigms as per their specific needs and requirements.
