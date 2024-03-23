---
title: Implement Your Own Call, Bind, Apply
date: 2022-10-23 13:39:53
tags:[Javascript]
---

```call```,```bind```,```apply``` these three functions are very useful in everyday development, What exactly did they do? Let's break it down.

## call
use case:
```
var person = {
  name: "leo",
  sayName(greetings) {
    console.log(greetings, this.name);
  },
};

var anotherPerson = {
  name: "norris",
};

person.sayName.call(anotherPerson, "hi");
```

What ```function.call(object,...params)``` do:

1. point this to the object passed in by first parameter
2. invoke function in context of object

Here is our versoin of ```call```:

```
function myCall(object, ...params) {
  var o = object || window;
  var fn = Symbol("fn");
  o[fn] = this;
  o[fn](...params);
  delete o[fn];
}

Function.prototype.myCall = myCall;

var person = {
  name: "leo",
  sayName(greetings) {
    console.log(greetings, this.name);
  },
};

var anotherPerson = {
  name: "norris",
};

person.sayName.myCall(anotherPerson, "hi");
```

## Apply
It's almost exactly the same as the call, The only difference is in the second argument of the function.

> Note: This function is almost identical to apply(), except that the function arguments are passed to call() individually as a list, while for apply() they are combined in one object, typically an array — for example, func.call(this, "eat", "bananas") vs. func.apply(this, ["eat", "bananas"]).

Here is our version of Apply:

```
function myApply(object, args) {
  var o = object || window;
  var fn = Symbol("fn");
  o[fn] = this;
  if (Array.isArray(args)) {
    o[fn](...args);
  } else {
    o[fn]();
  }
  delete o[fn];
}

Function.prototype.myApply = myApply;

var person = {
  name: "leo",
  sayName(greetings) {
    console.log(greetings, this.name);
  },
};

var anotherPerson = {
  name: "norris",
};

person.sayName.myApply(anotherPerson, ["hi"]);
```

## bind
```Function.bind(object, ...args)``` do:
1. return a function that, when executed, executes the target function, with the target's this always pointing to the target object.\

code:

```
function myBind(object, ...args1) {
  var fn = this;
  return function f(...args2) {
    var args = args1.concat(args2);
    fn.call(object, ...args);
  };
}

Function.prototype.myBind = myBind;

var person = {
  name: "leo",
  sayName(greetings) {
    console.log(greetings, this.name);
  },
};

var anotherPerson = {
  name: "norris",
};

var f = person.sayName.myBind(anotherPerson, "hi");
f();
```