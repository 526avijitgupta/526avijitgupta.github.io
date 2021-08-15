---
title: "Deep copying in JS!"
type: post
date: 2017-01-27
tags: ["mwos", "js"]
---

### The Problem

Now-a-days, I'm working on the [ringleader](http://github.com/mozmark/ringleader/) project. And just yesterday, me and one of my team mates [Utkarsh](http://github.com/iamutkarshtiwari/) observed that there were a couple of errors being generated in our javascript code. Some investigation revealed the source of errors to be a copy of an array which contained the same reference as the original array. Thus, a change in the copy was leading to a change in the original array as well. So, we needed to create a **deep copy** of the original array to overcome this problem.

By default, when copying by `=`, javascript keeps the reference to the same object (called a **shallow copy**).

```js
var a = [1,2,3];
var b = a;
a[0] = 5;
console.log(b[0]); // 5
```

### What All we Tried

Our initial thought was to use [Object.create](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/create).

* Using `Object.create`:

Object.create seemed to solve the problem when we first looked at it.

```js
var obj = {name: 'a'};
var obj_copy = Object.create(obj);
obj_copy.name = 'c';
console.log(obj.name); // 'a'
```

But it was later that we realized that since we had object(s) inside an array, `Object.create` didn't work correctly:

```js
var arr = [{name: 'a'}];
var arr_copy = Object.create(arr);
arr_copy[0].name = 'c';
console.log(arr[0].name); // 'c'
```

Turns out, even the *copies* made out of `Object.create` are not independantly referenced in this case:

```js
var arr = [{name: 'a'}];
var arr_copy_1 = Object.create(arr);
var arr_copy_2 = Object.create(arr);

// Now, arr_copy_1 and arr_copy_2 still point to the same reference.

arr_copy_1[0].name = 'c';
console.log(arr_copy_2[0].name); // 'c'
```

* Using `Object.create` with arrays:

On applying `Object.create` to an array, the result wasn't actually a real array (it was a [pseduo array](http://stackoverflow.com/questions/9016051/javascript-arrays-created-with-object-create-not-real-arrays))!

```js
var a = [1,2,3];
var b = Object.create(a);
console.log(b); // Object { }
```

* Using `Object.create` with `Array.from`:

To convert the previously obtained pseduo array into a real array, we tried using [Array.from](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from):

```js
var a = [1,2,3];
var b = Array.from(Object.create(a));
var c = Array.from(Object.create(a));
b[0] = 8;
console.log(c[0]); // 1
```

At this point we believed that we have the correct solution, until we found out the array which we were trying to deep copy wasn't simply composed of numbers or strings, it was deeply nested with objects, arrays and functions.

```js
var a = [{name: 1},{name: 2},{name: 3}];
var b = Array.from(Object.create(a));
var c = Array.from(Object.create(a));
b[0].name = 8;
console.log(c[0].name); // 8
```

We gave a few more tries to convert the pseduo array into a real array, but each time the reference of it's consisting arrays or objects was still maintained in the copies.


* Using `JSON.stringify` and `JSON.parse`:

Continuing further, we tried using another method altogether. But this again did not work since our array contained objects which had `function`s inside them. On [JSON.stringify](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) ing an object, all it's non-serializable properties are lost:

```js
var a = {name: 'a', exec: function() {return true;}};
var b = JSON.parse(JSON.stringify(a));
console.log(b); // {name: 'a'}
```

### The Solution

Finally, on a bit of Googling we found this wonderful utility function which does exactly what we need. It's a recursive function that copies an element's value while handling the cases for the value being an object or an array:

```js
function copy(o) {
   var output, v, key;
   output = Array.isArray(o) ? [] : {};
   for (key in o) {
       v = o[key];
       output[key] = (typeof v === "object") ? copy(v) : v;
   }
   return output;
}
```

So now, the following works:

```js
var a = [{name: 1},{name: 2},{name: 3}];
var b = copy(a);
var c = copy(a);
b[0].name = 8;
console.log(c[0].name); // 1
```

The problem resulted to be tougher than we expected, but it certainly turned out to be a great learning experience for the both of us!
