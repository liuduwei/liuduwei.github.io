---
title: Sort Algorithm（1）： Elementary Sort Javascript Implement - Selection， Insertion， Bubble Sort
date: 2023-01-23 16:37:13
tags: [Javascript, Algorithm, Sort]
---

Elementary Sort, The slowest and simplest Sort algorithm, time complexity is O(n^2)

## Bubble Sort
As Its name, the bigger element will be like a heavy item, Sinking to the bottom of the water, and the small one will swim up to the surface

Here's the algorithm animation: [Bubble Sort](https://www.cs.usfca.edu/~galles/visualization/ComparisonSort.html)

javascript code:

```
function bubbleSort(a) {
  for (let i = a.length - 1; i >= 0; i--) {
    for (let j = 0; j < i; j++) {
      if (a[j] < a[j + 1]) {
        exchange(a, j, j + 1);
      }
    }
  }
}

function exchange(a, i, j) {
  var temp = a[i];
  a[i] = a[j];
  a[j] = temp;
}

module.exports = bubbleSort;
```

## Insertion Sort
loop through elements, every time counter new element Insert it into already ordered element in front of it.

javascript code:

```
function insertionSort(a, low = 0, high = a.length - 1) {
  for (let i = low; i <= high; i++) {
    for (let j = i; j > low && less(a[j], a[j - 1]); j--) {
      exchange(a, j, j - 1)
    }
  }
}

function exchange(){...see before}

function less(a, b) {
  return a < b ? true : false;
}
```

## Selection Sort

Loop through elements, choose the smallest one, and put it into the front of elements every round.

javascript code:

```
function selectionSort(a) {
  var length = a.length;
  for (let i = 0; i < length; i++) {
    let min = i;
    // find min
    for (let j = i; j < length; j++) {
      if (less(a[j], a[min])) {
        min = j;
      }
    }

    // exchange
    if (a[min] != a[i]) {
      let temp = a[i];
      a[i] = a[min];
      a[min] = temp;
    }
  }
}

module.exports = selectionSort;
```

## Conclusion

There may be other optimizations for these three algorithms, but  I just want to talk about the basic version in this post, other optimizations can be discussed in new posts.

Next, I want to talk about Shell Sort, I treat it as Advanced Selection Sort, It's really amazing in real-world production, tiny easy code but effective
