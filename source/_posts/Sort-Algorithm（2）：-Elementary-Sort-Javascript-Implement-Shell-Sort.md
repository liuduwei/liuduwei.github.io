---
title: Sort Algorithm（2）： Elementary Sort Javascript Implement - Shell Sort
date: 2024-03-23 20:30:41
tags: [Javascript, Algorithm, Sort]
---

Shell Sort is a very efficient sorting algorithm; its time complexity can almost reach O(n) in real-world production.

The code Shell Sort moves elements in the same way as Selection Sort, but it seeks local sorting and then achieves global sorting.

Let's see How it works:

```
var { less } = require("./Shuffle");

function shellSort(a) {
  var length = a.length;
  var h = 1;
  while (h < Math.floor(length / 3)) h = 3 * h + 1; //3x + 1 increament

  while (h >= 1) {
    for (let i = h; i < length; i++) {
      // h-insertion_sort
      for (let j = i; j >= h && less(a[j], a[j - h]); j -= h) {
        let temp = a[j - h];
        a[j - h] = a[j];
        a[j] = temp;
      }
    }
    h = Math.floor(h / 3); // next increament
  }
}

module.exports = shellSort;
```

Why is Shell Sort so effective compared to Selection Sort? It 
moves elements in multiple positions, the number of increments every time, but Selection Sort moves elements in only one position.

Shell Sort is more simple than Quick Sort, so the application is widespread in small embedded devices.
