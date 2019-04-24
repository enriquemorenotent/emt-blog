---
layout: post
title: Different ways to use the 'console' command
published-on: "2019-04-16"
categories: javascript console
---

If you have ever open the developer tools and used the console, most likely you have used many times the following snippet to debug your JS code.

```javascript
console.log("Hello world");
// Hello world
```

The log function is the most common tool, in order to output information of our running code, but just recently I learned a few other ones that might as well be useful for debugging from this article. I am going to list them here as well, in case it could help someone.

## console.group

With this method you are capable of defining semantic groups to encapsulate the data you are printing. This will sure be handy when you have a lot of lines to read, and you want to have a better overview of the whole output.

```javascript
function name(obj) {
  console.group("Profile");
  console.log("name: ", obj.name);
  console.log("age: ", obj.age);
  console.log("details: ", obj.details);
  console.groupEnd();
}

name({ name: "Enrique", age: 36, details: "Needs to get fit" });
name({ name: "Linda", age: "I shouldn't tell...", details: "Very pretty" });
// *-- Profile ---
// | name: Enrique
// | age: 36
// | details: Needs to get fit
//
// *-- Profile ---
// | name: Linda
// | age: I shouldn't tell
// | details: Very pretty
```

## console.table

This method allows you to present data in a tabular way. This might come specially handy when you want to compare different sets of data with the same structure, kinda like loading table rows from a data base.

```javascript
let sizes = [
  { name: "Enrique", height: "190cm" },
  { name: "Eddie", height: "30cm (big for a cat)" },
  { name: "My building", height: "1000cm" }
];

console.table(sizes);
// ----------------------------------------------------
// | (index) | name          | height                 |
// ----------------------------------------------------
// | 0       | "Enrique"     | "190cm"                |
// ----------------------------------------------------
// | 1       | "Eddie"       | "30cm (big for a cat)" |
// ----------------------------------------------------
// | 2       | "My building" | "1000cm"               |
// ----------------------------------------------------
```

## console.error

In this case the message will be formatted as an error, making it pop more, helping to differentiate errors from other types of messages.

```javascript
console.error("Something bad happened!");
// ❌ Something bad happened!
```

## console.warn

This one is very similar to console.error, but the formatting is different. It is mainly used to show warning that are non-fatal for the execution of the application, but should be taken into account.

```javascript
console.warn("Something bad happened!");
// ⚠️ Something bad happened!
```

## console.assert

This one will trigger an error, if the first parameter of the funtion has a falsy value.

```javascript
function isEven(n) {
  let isEven = n % 2 == 0;
  console.assert(isEven, "Number is not even");
}

isEven(2);
// Nothing will be shown
isEven(3);
// "Number is not even" will be shown
```

With this commands you might make your output in the debugging console a little more enjoyable to read, and maybe more helpful to finish your tasks faster.

## console.time

There is an interesting API that can be used to meassure timing between operations.

```javascript
console.time();
// code snippet 1
console.timeLog(); // default: [time] ms
// code snippet 2
console.timeEnd(); // default: [time] ms
```

## console.count

This is an interesting one if you want to test, for instance, how many times a function is executed. This could be used for many things, like counting renders for a React component :)

```javascript
console.count("foo"); // foo: 1
console.count("bar"); // bar: 1
console.count("foo"); // foo: 2
console.count("foo"); // foo: 3
console.count("bar"); // bar: 2
console.countReset("foo");
console.count("foo"); // foo: 1
```
