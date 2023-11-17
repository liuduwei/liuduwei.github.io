---
title: var, let - what's difference in the for loop
date: 2022-6-17 16:36:40
tags: Javascript
---
We've all written simple for loops to iterate over arrays and objects countless times. But have you ever stopped to consider how the scope of variables used inside loops works? I recently came across an interesting code snippet that highlighted an important distinction between var and let in this context.

```javascript
for (var i = 0; i < 3; i++) {
  const log = () => console.log(i);
  setTimeout(log, 100);
}
```
When running this, you might expect it to log the numbers 0, 1, 2 - one for each iteration of the loop. But it actually logs 3, 3, 3!

Why is that? It has to do with how var declarations are scoped. Variables defined with var have function scope, meaning they are accessible outside of any blocks like if statements or for loops.

In this example, i is declared with var at the start of the for loop. Each iteration increments it and passes the reference to i into the timeout callback
If we change var to let:

```javascript
for (let i = 0; i < 3; i++) {
  //...
}
```
Now it logs 0, 1, 2 as expected. let bindings are block scoped, so i is treated as a new variable each iteration rather than a single changing reference.

Moral of the story? Be mindful of scope differences when using loops - it can subtly alter how your code behaves over time. Stick with let if you want block scoping within loops.