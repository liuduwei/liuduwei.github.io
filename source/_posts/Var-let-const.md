---
layout: var,
title: The Var, let, Const - What's the Difference?
date: 2022-4-16 16:35:29
tags: Javascript
---

| Aspect      | var                                                                                 | let                                                                                                                                             | const                                                                                                                                           |
| ----------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Scope       | Function scope; variable is accessible inside function even if declared after usage | Block scope; variable is only accessible inside nearest enclosing {...}                                                                         | Block scope; variable is only accessible inside nearest enclosing {...}                                                                         |
| Re-declared | Can re-declare var anywhere in the function                                         | Cannot re-declare let in the same block                                                                                                         | Cannot re-declare const anywhere                                                                                                                |
| Updated     | Can update/reassign the value                                                       | Can update/reassign the value                                                                                                                   | Cannot update/reassign the value, must be initialized and value cannot change                                                                   |
| Hoisted     | Function scoped variables are hoisted to the top of the function                    | hoisted to the top of its block or scope, but it is not initialized. Accessing the variable before its declaration results in a ReferenceError. | hoisted to the top of its block or scope, but it is not initialized. Accessing the variable before its declaration results in a ReferenceError. |
