---
title: "Type Checking Against Custom Type on Typescript"
date: 2021-08-29T22:14:38+07:00
description: Typescript allows us to create our own function, that it will understand, and will narrow the type. A type guard is some expression that performs a runtime check that guarantees the type in some scope
tags: [typescript, tips]
featured_image: https://www.azavea.com/wp-content/uploads/2020/10/2020-10-08_run-time-typescript.jpg
categories: Programming
comment: false
---

> **NOTE!**: There are many solutions to this problem. but this is my approach to solve the problem i'm facing

# The Problem
```typescript
type StringType = {
  baz: string;
}

type ObjectType = {
  foo: string;
  bar: number;
}

type MyType = ObjectType | StringType

const MyFunction = (x: MyType): string => {
  x.foo; // typescript error
  x.bar; // typescript error
  x.baz; // typescript error
  
  return ""
}
```

# My Solution
```typescript
type TypeIdentifier = "STRINGTYPE" | "OBJECTTYPE";

type StringType = {
  typeIdentifier: TypeIdentifier
  baz: string;
}

type ObjectType = {
  typeIdentifier: TypeIdentifier
  foo: string;
  bar: number;
}

type MyType = ObjectType | StringType;

const MyFunction = (x: MyType): string | null => {
  switch(x.typeIdentifier) {
    case "STRINGTYPE":
      const y = x as StringType;
      return y.baz;
    case "OBJECTTYPE":
      const y = x as ObjectType;
      return y.foo;
    default:
      return null;
  }
}
```

what about type guard with `is`?

yes type guard is cool, but I read [this article](https://medium.com/ovrsea/checking-the-type-of-an-object-in-typescript-the-type-guards-24d98d9119b0#5da7) about type checking with `is`
and on the bottom of the article said
**Warning: a type guard can introduce errors**

therefore I prefer this method because it is more explicit
