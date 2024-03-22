---
title: What Did new Keyword, Object.create() Do In Javascript
date: 2022-08-22 14:34:19
tags: [Javascript, Object]
---

We can use both ```new``` and Object.create() implement inherantance in javascript:

```
// new
function People(name) {
  this.name = name;
}

People.prototype.sayName = function () {
  console.log(this.name);
};

var leo = new People("leo");

// object.create()
var People = {
  name: "liu",
  sayName() {
    console.log(this.name);
  },
};

var norris = Object.create(People);
norris.name = "norris";
norris.sayName();
```

we can implement our new and Object.create():

```
// my new
function myNew(constructor, ...params) {
  var o = {};
  Object.setPrototypeOf(o, constructor.prototype);
  var result = constructor.apply(o, params);
  return result instanceof o ? result : o;
}

//my Obejct.create
if (Object.create == null) {
  Object.create = function (parent) {
    function F() {}
    F.prototype = parent;
    return new F();
  };
}
```
