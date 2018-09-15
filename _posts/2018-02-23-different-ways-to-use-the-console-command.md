---
layout: post
title: Different ways to use the 'console' command
categories: javascript console
image: https://images.unsplash.com/photo-1529392960549-df4af50eac23?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=cbb5faad99367a05fc9ce16f668f8865&auto=format&fit=crop&w=1350&q=80
---

If you have ever open the developer tools and used the console, most likely you have used many times the following snippet to debug your JS code.

```javascript
console.log("Hello world");
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
```

![null](/img/uploads/console-group.png)

## console.table

This method allows you to present data in a tabular way. This might come specially handy when you want to compare different sets of data with the same structure, kinda like loading table rows from a data base.

```javascript
let sizes = [
	{ name: "Enrique", height: "190cm" },
	{ name: "Eddie", height: "30cm (big for a cat" },
	{ name: "My building", height: "1000cm" }
];

console.table(sizes);
```

![null](/img/uploads/console-table.png)

## console.error

This one is very similar to console.log, with the exception that is styles it differently, making it pop more, when an error or a unwanted situation occurs.

![](/img/uploads/console-error.png)

## console.assert

This one is similar to a console.error together with a conditional line. It might save you a line of code, if you want to write your output in a more compact way.

```javascript
function isEven(n) {
	let isEven = n % 2 == 0;
	if (!isEven) console.error("Number is not even");
	return isEven;
}

// ...is the same as...

function isEven(n) {
	let isEven = n % 2 == 0;
	console.assert(isEven, "Number is not even");
	return isEven;
}
```

With this commands you might make your output in the debugging console a little more enjoyable to read, and maybe more helpful to finish your tasks faster.
