---
title: reduceObject
tags: object,transform,intermediate
---

Filters an array of objects based on a condition while also filtering out unspecified keys.

- Use `Object.entries()` to get an array of key-value tuples
- Use `Array.prototype.reduce()` on the result, and apply the arguments of the returned function, so it’s easier to generate a new object, or any other type you need.

```js
const reduceObject = object => (...args) => Object.entries(object).reduce(...args);
```

```js
const data = {
  john: { age: 12 },
  mike: { age: 42 },
};

const getIsAdult = ({ age }) => age >= 18;

const appendIsAdultReducer = ((accumulator, [key, value]) => ({
  ...accumulator,
  [key]: { ...value, isAdult: getIsAdult(value) },
}));

reduceObject(data)(appendIsAdultReducer, {});
// {
//   "john": { "age": 12, "isAdult": false },
//   "mike": { "age": 42, "isAdult": true },
// }
```
