


**HTML Questions:**

**What are semantic HTML elements and why are they important?**

Answer: Semantic HTML elements clearly describe their meaning in a human- and machine-readable way. Examples include ```<article>, <section>, <header>, <footer>, <nav>```, etc. They are important because they improve accessibility, SEO, and code readability, making it easier for search engines and assistive technologies to understand the structure and content of the web pages.

**How do you create a responsive layout in HTML and CSS?**

Responsive layouts can be created using CSS media queries, flexible grid layouts (like CSS Grid and Flexbox), and relative units like percentages, em, rem, and viewport units (vw, vh). Media queries allow different styles to be applied at different screen sizes.

```css
Copy code
/* Example of a media query */
@media (max-width: 600px) {
	.container {
		flex-direction: column;
	}
}
```

**Explain the difference between inline, block, and inline-block elements in HTML.**

- Inline elements do not start on a new line and only take up as much width as necessary. Examples include ```<span>, <a>, <img>```.
- Block elements start on a new line and take up the full width available. Examples include ```<div>, <p>, <h1>```.
- Inline-block elements are similar to inline elements but allow setting width and height. They do not start on a new line. Examples include ```<button>, <input>``` when styled with display: inline-block.


**What are the HTML5 new form elements and attributes?**

	HTML5 introduced several new form elements and attributes:

Answer: HTML5 introduced several new form elements and attributes to enhance form functionality:
- Elements: ```<datalist>, <output>, <progress>, <meter>, <time>```.
- Attributes: required, placeholder, pattern, min, max, step, autofocus, autocomplete, novalidate.

**How can you optimize an HTML page for better performance?**

Optimization can be achieved by:

- Minimizing and compressing HTML, CSS, and JavaScript files.

- Using efficient image formats and compression techniques.

- Leveraging browser caching.

- Deferring or asynchronously loading JavaScript.

- Using a Content Delivery Network (CDN) for static assets.

- Reducing the number of HTTP requests by combining files.  

**JavaScript Questions:**

**What is the difference between var, let, and const?**

-  `var`: Function-scoped or globally scoped if declared outside a function. Can be re-declared and updated. Hoisted to the top of their scope.

-  `let`: Block-scoped. Cannot be re-declared in the same scope but can be updated. Not hoisted to the top.

-  `const`: Block-scoped. Cannot be re-declared or updated. The value it holds cannot be reassigned (though properties of objects can be changed).

**Explain closures in JavaScript.**

A closure is a function that retains access to its own scope, the scope of the outer function, and the global scope. This allows a function to access variables from its outer scope even after the outer function has finished executing.

```javascript

function  outer() {
let  counter = 0;
	function  inner() {
		counter++;
		console.log(counter);
	}

	return  inner;
}

const  increment = outer();

increment(); // 1

increment(); // 2

```
**What are promises and how do they work?**

Promises are objects that represent the eventual completion (or failure) of an asynchronous operation and its resulting value. They have states: pending, fulfilled, or rejected. Promises provide `.then()` and `.catch()` methods to handle success and error cases.

```javascript
const  promise = new  Promise((resolve, reject) => {

setTimeout(() => {
	resolve("Success!");
	}, 1000);
});

promise.then(result  => {
	console.log(result); // "Success!"
}).catch(error  => {
	console.error(error);
});
```

**Explain the concept of "this" in JavaScript.**

- In a method, `this` refers to the object the method belongs to.

- In a function, `this` refers to the global object (or `undefined` in strict mode).

- In an event handler, `this` refers to the element that received the event.

- Arrow functions do not have their own `this`; they inherit `this` from the surrounding lexical context.

```javascript
const  obj = {
value:  42,

method() {
	console.log(this.value);
}
};

obj.method(); // 42
```

**What are higher-order functions in JavaScript?**

Higher-order functions are functions that can take other functions as arguments or return them as results. They enable functional programming techniques such as `map`, `filter`, and `reduce`.

  

```javascript
function  higherOrderFunction(fn) {
	return  function(x) {
		return  fn(x);
	};
}

const  double = higherOrderFunction(x  =>  x * 2);
console.log(double(5)); // 10
```

  

**TypeScript Questions:**

**What are the main differences between TypeScript and JavaScript?**

- TypeScript is a superset of JavaScript adding static typing for type checking.

- Includes interfaces, generics, and access modifiers (`public`, `private`, `protected`).

- Supports modern JavaScript features, transpiling them to older versions if needed.

- Provides enhanced tooling and autocompletion due to type annotations.

**Explain the concept of interfaces in TypeScript.**

Interfaces define the structure of an object, specifying types for properties and methods. They enforce type checking to ensure objects adhere to specific structures.

```typescript
interface  Person {
	name: string;
	age: number;
	greet(): void;
}

const  person: Person = {
	name:  "John",
	age:  30,
	greet() {
		console.log("Hello!");
	}
};
```

**What are generics in TypeScript and how do they work?**

Generics allow creating reusable components that can work with various data types. They enable functions, classes, and interfaces to operate on types specified as parameters.

```typescript
function  identity
	(arg: T): T {
	return  arg;
}

let  numberIdentity = identity(42);

let  stringIdentity = identity("Hello");
```

**How does TypeScript handle modules and namespaces?**

**Modules**: Uses ES6 module system where each file is a module with its own scope. Imports and exports are handled using `import` and `export` keywords.

**Namespaces**: Used to group related code under a single namespace to avoid global scope pollution. Created using the `namespace` keyword.

```typescript
export  function  add(a: number, b: number): number {
	return  a + b;
}
// main.ts

import { add } from  './math';

console.log(add(2, 3)); // 5

namespace  MathUtils {
	export  function  add(a: number, b: number): number {
		return  a + b;
	}
}

console.log(MathUtils.add(2, 3)); // 5
```

**What are decorators in TypeScript?**

Decorators are special declarations that modify the behavior of classes, methods, accessors, properties, or parameters. They are used for meta-programming and are an experimental feature in TypeScript.
```typescript
function  log(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
const  originalMethod = descriptor.value;
descriptor.value = function (...args: any[]) {
	console.log(`Calling ${propertyKey} with arguments: ${args}`);
	return  originalMethod.apply(this, args);
	};
}

class  Example {
@log
	sayHello(name: string) {
		console.log(`Hello, ${name}!`);
	}
}

const  example = new  Example();
example.sayHello("Alice"); // Logs: Calling sayHello with arguments: Alice
// Hello, Alice!
```
