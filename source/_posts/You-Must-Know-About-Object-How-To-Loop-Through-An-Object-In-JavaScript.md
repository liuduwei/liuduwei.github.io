---
title: You Must Know About Object - How To Loop Through An Object In JavaScript
date: 2022-08-19 20:58:56
tags: [Javascript, Object]
---

Loop through an Object is much harder than doing the same thing in an Array because you can't use those convenient syntaxes like for-of, forEach (by the way, you should never use for-in) when dealing with an Object, so today let's look at how many methods are there to loop through an Object

## Create an object to test
```
function Ob() {
  this.name = "liu";
  this.age = 22;
}
var ob = new Ob();

Object.defineProperty(ob, "gender", {
  value: "male",
  enumerable: false,
});

var mySb = Symbol("special");

ob[mySb] = "sp";

var mySbEnumerableFalse = Symbol("emfalse");
Object.defineProperty(ob, mySbEnumerableFalse, {
  value: "emfalse:value",
  enumerable: false,
});

Ob.prototype.father = "leo";
```
console log this in Node:
```
console.log(ob);

output:
Ob { name: 'liu', age: 22, [Symbol(special)]: 'sp' }
```
notice,console.log(Object) will only output own enumerable properties.

## Object.keys(Object)(Object.Values(); Object.entries())
those methods above will return an array including the parameter Object's keys or values or [key, value] pairs, here's the code:
```
console.log(Object.values(object)); // ignore enumerable: false 
console.log(Object.keys(object)); // ignore enumerable: false 
console.log(Object.entries(object)); // ignore same
```

output here:
```
[ 'liu', 22 ] // Object.values(object)
[ 'name', 'age' ] // Object.keys(object)
[ [ 'name', 'liu' ], [ 'age', 22 ] ] // Object.entries(object)
```
so these three methods only count their own enumerable none symbol properties in

## Object.getOwnPropertyNames（getOwnPropertySymbols(ob)）
directly look at the code:
```
console.log(Object.getOwnPropertyNames(ob)); // enumerable: false would still in output array [names....], but no symbol keys
console.log(Object.getOwnPropertySymbols(ob)); // enumerable: false would still in output array [names....], only symbol keys
```
output:
```
[ 'name', 'age', 'gender' ]
[ Symbol(special), Symbol(emfalse) ]
```
The two are complementary, and will output all own properties but not include ancestors', no matter how the enumerable.

## Reflect.ownKeys()
it's do the same thing as ```Object.getOwnPropertyNames()``` and ```Object.getOwnPropertySymbols(ob)```
code here:
```
console.log(Reflect.ownKeys(ob));

output:
[ 'name', 'age', 'gender', Symbol(special), Symbol(emfalse) ]
```

## summary
which methods to use it's a subjective topic, it's up to your real code context, and I like the use ```Reflect.ownKeys()``` , but it's only available in es6, so i will contact ```Object.getOwnPropertyNames()``` and ```Object.getOwnPropertySymbols(ob)```
	
	
## Reference List
[JS遍历对象的七种方法](https://juejin.cn/post/7129374520015585317)

