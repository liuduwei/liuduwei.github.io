---
title: Understand Javascript Prototype chain - Prototypal Inheritance
date: 2022-09-29 11:39:29
tags: [Javascript, Object, Prototype]
---

## prelude
Ever since I was introduced to the programming language javascript, Its prototype chain has always bothered me,
I read a lot of blog, posts about this topic, most of them say the same thing, Put a picture like this in the article,

![prototype chain](../images/JavascriptObjectHierarchy.jpg)

and told readers to remember :

```
1. People.prototype.constructor == Person 
2. PeopleLeo.__proto__ == Person.prototype 
```

it's not wrong, but it's just too hard to keep in mind for me, I memorize then forgot again and again, and every time I try to recall it, I was thinking what fuck is the ```prototype``` or ```__proto__```, they look like the same thing, who figure out these two names, why javascript use this mechanism to simulate class inheritance.

And now I know how this came to be, It dawned on me, after I read this [Javascript – How Prototypal Inheritance really works](https://blog.vjeux.com/2011/javascript/how-prototypal-inheritance-really-works.html)
I highly recommend you read this post.

## Prototypal inheritance
for me, the most important thing I learned from [Javascript – How Prototypal Inheritance really works](https://blog.vjeux.com/2011/javascript/how-prototypal-inheritance-really-works.html),
javascript's Inheritance is just prototypal Inheritance, It has nothing to do with class Inheritance, the ```new``` key word in javascript it's because:

> [Brendan Eich](https://brendaneich.com/) wanted Javascript to look like traditional Object Oriented programming languages such as Java and C++. In those, we use the new operator to make a new instance of a class. So he wrote a new operator for Javascript. (quote from https://blog.vjeux.com/2011/javascript/how-prototypal-inheritance-really-works.html)

if you came from other traditional Object Oriented programming languages that use class inheritance, when you try to understand the javascript prototypal inheritance, you will suck.

so embrace the prototypal inheritance, feel its beauty, and think it without class inheritance, all things come to be ease.

## some code example
After I realized what I learned from [Javascript – How Prototypal Inheritance really works](https://blog.vjeux.com/2011/javascript/how-prototypal-inheritance-really-works.html),  I was suddenly reminded of an online class I've taken before, it's [deep-javascript](https://frontendmasters.com/courses/deep-javascript-v3/) taught by Kyle Simpson, author of [You don't know Js](https://github.com/getify/You-Dont-Know-JS)

it also mentions the concept of prototypal inheritance, called OLOO: Objects Linked to Other Objects.

Here's some code I noted, see how prototypal inheritance works:
```
function Workshop(teacher) {
  this.teacher = teacher;
}

Workshop.prototype.ask = function (question) {
  console.log(this.teacher + question);
};
var deepJs = new Workshop("liu"); // not true prototypal inheritance, it's a simulation of class inheritance

function AnotherWorkShop(teacher) {
  Workshop.call(this, teacher);
}
// true prototypal inheritance
AnotherWorkShop.prototype = Object.create(Workshop.prototype);
AnotherWorkShop.prototype.speakUp = function (msg) {
  this.ask(msg.toUpperCase());
};

var reactJs = new AnotherWorkShop("leo");
reactJs.speakUp("hi");
```
and clean version
```
var Workshop = {
  setTeacher(teacher) {
    this.teacher = teacher;
  },

  ask(msg) {
    console.log(this.teacher, msg);
  },
};

var AnotherWorkShop = Object.assign(Object.create(Workshop), {
  speakUp(msg) {
    this.ask(msg);
  },
});

var recentJs = Object.create(AnotherWorkShop);
recentJs.setTeacher("leo");
recentJs.speakUp("delegation inheritance");
```
use es6 class syntax suger: 
```
class Workshop {
  constructor(teacher) {
    this.teacher = teacher;
  }

  ask(msg) {
    console.log(this.teacher, msg);
  }
}

class AnotherWorkShop extends Workshop {
  speakUp(msg) {
    this.ask(msg);
  }
}

var jsRecentParts = new AnotherWorkShop("kyle");

jsRecentParts.speakUp("hi");
```

## conclude
let's see this picture again,

![prototype chain](../images/JavascriptObjectHierarchy.jpg) 
 
Is everything clear and unambiguous?

## Reference
[Javascript Object Layout](http://www.mollypages.org/tutorials/js.mp)
[Javascript继承机制的设计思想](https://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)
[deep-javascript](https://frontendmasters.com/teachers/kyle-simpson/)
[Prototypal Inheritance in JavaScript](https://crockford.com/javascript/prototypal.html)