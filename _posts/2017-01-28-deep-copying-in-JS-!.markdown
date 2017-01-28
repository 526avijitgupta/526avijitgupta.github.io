---
title: "Deep copying in JS !"
layout: post
date: 2017-01-27 01:13
image: '/assets/images/'
description:
tag:
blog: true
jemoji:
author: Avijit Gupta
---

#### The Problem

By default, when copying by `=`, javascript keeps the reference to the same object (called a **shallow copy**). This can lead to you pulling your hair for a long time!

```
var a = [1,2,3];
var b = a;
a[0] = 5;
console.log(b[0]); // 5
```

#### The Story

While working with a piece of javascript code yesterday, me and Utkarsh were faced with the same issue. While we modified the copy of the array, the original one also got modified which lead to unexpected results. We needed to create a **deep copy** of the original array.

1. Using `Object.create` (incorrectly):

```
var obj_1 = {name: 'a'};
var obj_2 = Object.create(obj_1);
obj_2.name = 'c';
console.log(obj_1.name); // 'c'
```


2. Using `Object.create`:

Turns out, only the *copies* made out of `Object.create` are independantly not referenced to each other:

```
var obj_1 = {name: 'a'};
var obj_2 = Object.create(obj_1);
var obj_3 = Object.create(obj_1);

// Now, obj_2 and obj_3 do not point to the same value.

obj_2.name = 'c';
console.log(obj_3.name); // 'a'
```


3. Using `Object.create` with Arrays:


```
var a = [1,2,3];
var b = Object.create(a);
console.log(b); // Object { }
```
When we applied `Object.create` on arrays, the result wasn't actually an real array!


4. Using `Object.create` with `Array.from`:

```
var a = [1,2,3];
var b = Array.from(Object.create(a));
var c = Array.from(Object.create(a));
b[0] = 8;
console.log(c[0]); // 1
```

We were momentarily satisfied with the result, until we found out that our Array wasn't simply composed of numbers or strings, it contained complex objects as it's elements. This method didn't seem to work in that case:

```
var a = [{name: 1},{name: 2},{name: 3}];
var b = Array.from(Object.create(a));
var c = Array.from(Object.create(a));
b[0].name = 8;
console.log(c[0].name); // 8
```

We gave a few more tries to convert the pseduo array into a real array, but it turned out to be futile due in our case!


#### The Final Soution

Credits: [StackOverflow]()
A recursive function that copied an element's value while handling the cases for the value being an object or an array. 
```
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

The problem took longer to solve than we expected, but it turned out to be a great learning experience for the both of us!
