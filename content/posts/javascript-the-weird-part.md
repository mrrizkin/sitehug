---
title: "JavaScript: the weird part"
date: 2021-08-28T19:48:07+07:00
description: "Javascript. Love it or hate it it seems to have become the defacto virtual machine of the internet that Java was supposed to be. And it is odd. Like properly odd. This is a short collection of some weird things that I have noticed about it."
tags: [fun, javascript]
featured_image: "https://charlieharvey.org.uk/graphics/js-weird-parts.png"
categories: Programming
comment : false
---

I keep a little list of these by my desk for my own sick amusement (which is something that my pal oxguin reckons is not a fact to be shared out loud). If you like this little lot, then you would probably enjoy some of the prior art at wtfjs.

# Comparison craziness
Let’s start by making x an array with 0 in it.
``` javascript
var x = [0] // [0]
```
It should equal itself, which is good.
``` javascript
x == x // true
```
But it also equals not itself, which is not so good.
``` javascript
x == !x // true
```
What about comparing a 3 element array and a string?
``` javascript
Array(3) == ",," // true
```
Ri-iight.

# Type twattery
The type of not a number is, well, a number. Sensible.
``` javascript
typeof NaN // "number"
```
Well at least that means it ought to be equal to itself, right?
``` javascript
NaN == NaN // false
```
So much for NaN. I wonder what the type of null is …
``` javascript
typeof null // "object"
```
… but of course it is not actually an instanceof Object
``` javascript
null instanceof Object // false
```
So, what is a string then?
``` javascript
"string" instanceof String // false
```
Uh-huh.

# Bounds buffoonery
How about a really big number first of all. Wait. What?
``` javascript
9999999999999999 // 10000000000000000
```
Hopefully small numbers make more sense.
``` javascript
0.1 + 0.2 == 0.3 // false
```
I guess not. I bet that max is still bigger than min though.
``` javascript
Math.max() > Math.min() // false
```
``` javascript
Math.max() < Math.min()  // true
```
Maybe not.

# Array assinity
Calling + on an empty array and an empty array gives the empty string. Who knew?
``` javascript
[] + [] // ""
```
How about an empty array and an empty object?
``` javascript
[] + {} // "[object Object]"
```
An empty object and an empty array gives, ummm, 0.
``` javascript
{} + [] // 0
```
Whereas an empty object and an empty object is not a number. Which is true, I suppose.
``` javascript
{} + {} // NaN
```

# Boolean balderdash
I’ve heard of that boolean arithmetic. Let’s give it a try.
``` javascript
true + true === 2 // true
```
``` javascript
true - true === 0 // true
```
Ah. It looks like true is equal to one. I’ll just check.
``` javascript
true === 1 // false
```
Doh!

# And one for luck
See if you can work out what this will evaluate to
``` javascript
(! + [] + [] + ![]).length // 9
```
Wow! Thanks for reading this far. Got any favourite weird parts of Javascript? Share them in the comments.

Incidentally, these were all evaluated on spidermonkey 24.2.0. Maybe they won’t work in node/whatever other js engine you are using…
