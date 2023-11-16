---
title: History of javascript module development
date: 2022-5-16 18:07:48
tags: Javascript
---

> Recently I came across an article call [The Evolution of JavaScript Modularity](https://github.com/myshov/history-of-javascript/tree/master/4_evolution_of_js_modularity) from a github Repo, This article is so well-written, thus this is kind of a summary of that article.

### The Name Collision

From the moment of its appearance JavaScript has used the global object window as a storage for all variables defined without the `var` keyword. In 1995-1999 it was very convenient, because JavaScript code tended to solve small tasks that hadn't required a lot of lines of code. But when the codebase of applications had became large this feature of the language began to lead to nasty errors because of the name collisions. Let’s look at this example:

```
	// file greeting.js
	var helloInLang = {
    	en: 'Hello world!',
    	es: '¡Hola mundo!',
    	ru: 'Привет мир!'
	};

	function writeHello(lang) {
    	document.write(helloInLang[lang]);
	}

	// file hello.js
	function writeHello() {
    	document.write('The script is broken');
	}
```

When we place the script `greeting.js` on the page and after it `hello.js` there will be conflict, that is instead of the greeting we will get the message "The script is broken" in this particular case.

It is obvious that in the large projects this can cause a lot of headaches. Moreover you cannot be sure that the third-party scripts on the page won't break anything in your app.

And there's an another tedious moment that you need manual control of the `script` tag in the HTML.

### Directly Defined Dependencies (1999)

let's look at the implementation of this pattern using Dojo Toolkit.

The gist of directly defined dependencies lied in the getting of the code of the modules (in terms of the Dojo - resources) via explicit invocation of the function dojo.require (which is also used to initialise the loaded module). That is in this approach the dependencies were defined directly in the code at those places, where they should to be used.

Let's revise our example using Dojo 1.6:

```javascript
// file greeting.js
dojo.provide("app.greeting");

app.greeting.helloInLang = {
  en: "Hello world!",
  es: "¡Hola mundo!",
  ru: "Привет мир!",
};

app.greeting.sayHello = function (lang) {
  return app.greeting.helloInLang[lang];
};

// file hello.js
dojo.provide("app.hello");

dojo.require("app.greeting");

app.hello = function (x) {
  document.write(app.greeting.sayHello("es"));
};
```

Here we see that modules are defined using the function dojo.provide, and the process of getting of the code of the module starts when you use dojo.require. It is a fairly simple approach that was used in the Dojo up to version 1.7; Google Closure Library uses it to this day.

### The Namespace Pattern (2002)

> For sloving the issue with name collisions, the namespace pattern was introduced. usually, It is a way to create an Object mounted in Window all method and properties we need reside in it.

Actually Dojo mentioned before in the previous chapter which already use this Parttern.

If we apply this idea to our example we get something like this:

```javascript
// file app.js
var app = {};

// file greeting.js
app.helloInLang = {
  en: "Hello world!",
  es: "¡Hola mundo!",
  ru: "Привет мир!",
};

// file hello.js
app.writeHello = function (lang) {
  document.write(app.helloInLang[lang]);
};
```

As we can see the logic and the data resides now in the properties of the object app. Thus we don't pollute the global scope but continue to have access to the various parts of the application from different files.

But there is a significant flaw that we can modify all the properties of the app object from the global scope.

### The Module Pattern (2003)

> It's main idea is encapsulating data and code with a closure and providing access to them through methods accessible from the outside.

Here is a basic example of this type of pattern:

```javascript
var greeting = (function () {
  var module = {};

  var helloInLang = {
    en: "Hello world!",
    es: "¡Hola mundo!",
    ru: "Привет мир!",
  };

  module.getHello = function (lang) {
    return helloInLang[lang];
  };

  module.writeHello = function (lang) {
    document.write(module.getHello(lang));
  };

  return module;
})();
```

Here we see the immediately invoked function express, and We can see that the module pattern is very similar to the previous one, but now the data and the methods are encapsulated in a closure.
Dive in deep see article [JavaScript Module Pattern: In-Depth](http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html)

### Template Defined Dependencies (2006)

> This pattern defines dependencies via inclusion into the target file the special labels.
> The similars:
> Comment Defined Dependencies (2006)
> Externally Defined Dependencies (2007)

The resolving this labels into actual code can be performed via templating, and special build tools, for example, borshik. In contrast to the previous discussed detached dependency definitions patterns, this pattern only works with pre-build step.

For example:

```javascript
// file app.tmp.js

/*borschik:include:../lib/main.js*/

/*borschik:include:../lib/helloInLang.js*/

/*borschik:include:../lib/writeHello.js*/

// file main.js
var app = {};

// file helloInLang.js
app.helloInLang = {
  en: "Hello world!",
  es: "¡Hola mundo!",
  ru: "Привет мир!",
};

// file writeHello.js
app.writeHello = function (lang) {
  document.write(app.helloInLang[lang]);
};
```

### CommonJs Modules (2009)

> CommonJS is the most common module format at the present moment. You can use it not only on the server-side in Node.JS but also on the client-side using Browserfiy or Webpack, which can transform set of CommonJS modules into one bundle.

As an example of the CommonJS module let's adapt our module by this way:

```javascript
// file greeting.js
var helloInLang = {
  en: "Hello world!",
  es: "¡Hola mundo!",
  ru: "Привет мир!",
};

var sayHello = function (lang) {
  return helloInLang[lang];
};

module.exports.sayHello = sayHello;

// file hello.js
var sayHello = require("./lib/greeting").sayHello;
var phrase = sayHello("en");
console.log(phrase);
```

### AMD (2009)

> Base the CommonJs, But loading of the modules should not synchronous, use the browser functionality for the parallel loading of the scripts

If we will rewrite our example using AMD format we will get something like this:

```javascript
// file lib/greeting.js
define(function () {
  var helloInLang = {
    en: "Hello world!",
    es: "¡Hola mundo!",
    ru: "Привет мир!",
  };

  return {
    sayHello: function (lang) {
      return helloInLang[lang];
    },
  };
});

// file hello.js
define(["./lib/greeting"], function (greeting) {
  var phrase = greeting.sayHello("en");
  document.write(phrase);
});
```

The file hello.js is the entry point of the program. In this file there is a function define that declares a module. The first argument of the function is an array of dependencies. The execution of the code of the module, which is defined as a function in the second argument of define, will be launched only after that fact when all dependencies of this module will be loaded. This deferred code execution of the module makes a possibility for the parallel loading of its dependencies.

### UMD (2011)

> There were two formats, CommonJs and AMD, could not get along with each other, so UMD format has been developed for solution of this problem.

As an example let's refactor our module greeting.js for the simultaneous support of different environments CommonJS and AMD:

```javascript
(function (define) {
  define(function () {
    var helloInLang = {
      en: "Hello world!",
      es: "¡Hola mundo!",
      ru: "Привет мир!",
    };

    return {
      sayHello: function (lang) {
        return helloInLang[lang];
      },
    };
  });
})(
  typeof module === "object" && module.exports && typeof define !== "function"
    ? function (factory) {
        module.exports = factory();
      }
    : define
);
```

In the heart of this implementation pattern lies the immediately invoked function expression. That function takes different arguments depending on the environment. The passed argument is the following function if the code is used as a CommonJS module:

```Javascript
function (factory) {
    module.exports = factory();
}
```

If the code is used as an AMD module, the argument of function is define. Due this substitution the code can be used in different environments.

### ES2015 Modules (2015)

By tradition, let's adapt our example to show the specification in action:

```javascript
// file lib/greeting.js
const helloInLang = {
  en: "Hello world!",
  es: "¡Hola mundo!",
  ru: "Привет мир!",
};

export const greeting = {
  sayHello: function (lang) {
    return helloInLang[lang];
  },
};

// file hello.js
import { greeting } from "./lib/greeting";
const phrase = greeting.sayHello("en");
document.write(phrase);
```
