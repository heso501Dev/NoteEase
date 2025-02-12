
<h1> Hoisting </h1>
  
`hoisting` refers to the behavior of moving declarations (but not initializations) to the top of their scope during the compilation phase, before the code execution. This applies to both variables and functions.
  

## Hoisting with Variables
  
- **var**:
	- Variables declared using var are hoisted to the top of their scope and initialized with `undefined`.
  ```js
  	console.log(x); // undefined (hoisted to top, but not assigned yet)
	var x = 10;
	console.log(x); // 10 (after assignment)
  ```

- **`let` and `const`**:
	- Variables declared with `let` and `const` are also hoisted, but they are in a "temporal dead zone" from the start of the block until the declaration is encountered. Accessing them before initialization results in a `ReferenceError`.
 
		```js
 		 console.log(x); // ReferenceError: Cannot access 'x' before initialization
 		 let x = 10;
		```
  
## Hoisting with Functions
  
- **Function Declarations**:
	- Entire function declarations are hoisted to the top, so you can call the function before it's declared in the code.
 
  ```js
		myFunction(); // "Hello"
		function myFunction() {
    		console.log("Hello");
		}
	```

- **Function Expressions**:
	- If a function is assigned to a variable (e.g., through a function expression), the hoisting behavior follows the same rules as variable hoisting. Only the declaration of the variable is hoisted, not the assignment of the function.
  
  ```js
  		myFunction(); // TypeError: myFunction is not a function
			var myFunction = function() {
 			console.log("Hello");
		};
	```
    
<h1> Functional Programming </h1>

In **Functional Programming** (FP), functions are considered **first-class citizens** (or first-class objects). This means that functions in such languages can:

1. **Be assigned to variables**
2. **Be passed as arguments to other functions**
3. **Be returned from other functions**
4. **Be stored in data structures** like arrays or objects

```js
// 1. Assigning Functions to Variables
const greet = function(name) {
  return `Hello, ${name}!`;
};
console.log(greet("Alice"));  // Output: Hello, Alice!

// 2. Passing Functions as Arguments
function sayHello(name, callback) {
  console.log("Hi, " + name);
  callback();
}
sayHello("Alice", function() {
  console.log("This is a callback function.");
});

// 3. Returning Functions from Other Functions
function multiplyBy(factor) {
  return function(num) {
    return num * factor;
  };
}
const double = multiplyBy(2);
console.log(double(5));  // Output: 10

// 4. Storing Functions in Data Structures
const operations = [
  function(a, b) { return a + b; }, // Addition
  function(a, b) { return a - b; }  // Subtraction
];
console.log(operations[0](3, 2));  // Output: 5 (Addition)
console.log(operations[1](3, 2));  // Output: 1 (Subtraction)
```

<h1> Object </h1>

An object is a collection of key-value pairs, where each key (also called a "property") is a string, and the value can be any valid JavaScript data type, including another object or a function.

```js
// 1. Creating an Object (using Object Literal Syntax)
const person = {
  name: "Alice",
  age: 30,
  greet: function() {
    console.log("Hello, " + this.name);
  }
};

// 2. Accessing Object Properties
console.log(person.name);  // Output: Alice
console.log(person["age"]); // Output: 30

// 3. Modifying and Adding Properties
person.age = 31;  // Modifying an existing property
person.job = "Engineer";  // Adding a new property
console.log(person);  // Output: { name: 'Alice', age: 31, greet: [Function: greet], job: 'Engineer' }

// 4. Methods in Objects
person.greet();  // Output: Hello, Alice

// 5. 'this' in Objects
const personWithThis = {
  name: "Bob",
  greet: function() {
    console.log("Hello, " + this.name);  // 'this' refers to the 'personWithThis' object
  }
};
personWithThis.greet();  // Output: Hello, Bob

// 6. Object Destructuring
const { name, age, job } = person;
console.log(name);  // Output: Alice
console.log(age);   // Output: 31
console.log(job);   // Output: Engineer

// 7. Nested Objects
const personWithAddress = {
  name: "Alice",
  address: {
    street: "123 Main St",
    city: "Wonderland"
  }
};
console.log(personWithAddress.address.city);  // Output: Wonderland

// 8. Object Methods: Object.keys(), Object.values(), Object.entries()
console.log(Object.keys(person));   // Output: ['name', 'age', 'greet', 'job']
console.log(Object.values(person)); // Output: ['Alice', 31, [Function: greet], 'Engineer']
console.log(Object.entries(person)); // Output: [['name', 'Alice'], ['age', 31], ['greet', [Function: greet]], ['job', 'Engineer']]

// 9. Deleting Object Properties
delete person.job;  // Removes the 'job' property
console.log(person);  // Output: { name: 'Alice', age: 31, greet: [Function: greet] }

// 10. Object Constructor Function
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const person1 = new Person("Charlie", 25);
const person2 = new Person("Diana", 28);

console.log(person1.name);  // Output: Charlie
console.log(person2.age);   // Output: 28

// 11. Object Spread Syntax (Copying and Merging Objects)
const personCopy = { ...person1, job: "Teacher" };
console.log(personCopy);  // Output: { name: 'Charlie', age: 25, job: 'Teacher' }
```


<h1> Window </h1>

In the browser, the window object represents the global environment and is the object that provides access to things like:

- Browser properties (like window.location, window.document, window.console, etc.)
- Global functions (like alert(), setTimeout(), setInterval())
- Global variables (like window.innerWidth, window.navigator)

##  Everything is Inside the window Object
- **Global Variables**: Any variable declared in the global scope becomes a property of the window object.


```js
	let message = "Hello, World!";
	console.log(window.message);  // Output: "Hello, World!"
```


- **Global Functions**: Any function declared globally is also attached to the window object.
```js
function greet() {
  console.log("Hello!");
}
console.log(window.greet);  // Output: [Function: greet]
```

- **Browser APIs**: Many browser-specific objects and methods are part of the window object, like document, navigator, and location.

```js
	console.log(window.document);   // The Document object, represents the webpage.
	console.log(window.navigator);  // Information about the browser and system.
	console.log(window.location);   // Information about the current URL.
```

## Examples of window Properties

```js
	console.log(window.document.title);  // Output: Title of the current webpage
	window.console.log("This is a message");  // Output: This is a message
	window.alert("Hello, World!");  // Displays an alert popup
    
	window.setTimeout(() => {
 		 console.log("This message is delayed");
	}, 2000);  // Logs after 2 seconds

	console.log(window.location.href);  // Output: current URL
	window.location.href = "https://example.com";  // Redirects the browser

```

## this in the Browser Context
In the browser, when you're in the global scope (or in a regular function that's not in strict mode), the keyword this refers to the window object. `this` refers to the `window object` by default in the browser environment (unless you're in strict mode or within an object method).

```js
	console.log(this === window);  // Output: true
```

## window vs globalThis
In the global scope, window is the global object in browsers. However, JavaScript now also has globalThis, which provides a universal reference to the global object, regardless of the environment (browser, Node.js, etc.).

In browsers: window and globalThis refer to the same object.
In Node.js: globalThis is used to refer to the global object, while window is not available.


```js
	console.log(globalThis === window);  // Output: true in browsers, false in Node.js
```



## Function

Functions are objects that do things (run code). You can treat them like objects, adding extra properties to them if you want.Functions are objects that do things (run code). You can treat them like objects, adding extra properties to them if you want.

- **Functions can store information**:

	- Just like objects, you can add extra stuff (properties) to a function.
    ```js
    function greet() {
    console.log("Hello!");
   }

	greet.message = "This is a function";  // Adding a property to the function
	console.log(greet.message);  // Output: This is a function
	```
    
- **You can treat functions like objects**:
	- You can store a function in a variable and use it later.
```js
	const sayHello = function() {
  	console.log("Hello!");
	};

	sayHello();  // Output: Hello!
```

- **Functions are special objects**:

	- When you check the type of a function, JavaScript says it’s a "function", but behind the scenes, it’s really an object.
   	
    ```js
    console.log(typeof func);  // Output: "function"
	console.log(greet instanceof func);  // Output: true
	```
    
 
<h1> Array </h1>

In JavaScript, arrays are objects that are created with a special structure and behavior. They are part of the window object (in browsers) and come with built-in properties and methods designed for working with lists of data.



```js
let arr = [1, 2, 3, 4, 5];

// .reverse()
let reversedArr = arr.reverse();
console.log("Reversed:", reversedArr);  // Output: [5, 4, 3, 2, 1]

// .fill()
arr = [1, 2, 3, 4, 5];
arr.fill(0);  
console.log("Filled:", arr);  // Output: [0, 0, 0, 0, 0]

// .map()
let mappedArr = arr.map(x => x + 1);
console.log("Mapped:", mappedArr);  // Output: [1, 1, 1, 1, 1]

// .shift()
arr.shift();
console.log("Shifted:", arr);  // Output: [0, 0, 0, 0]

// .split() (string method)
let str = "apple,banana,cherry";
let splitArr = str.split(",");
console.log("Split:", splitArr);  // Output: ["apple", "banana", "cherry"]

// .toString()
let arrToStr = arr.toString();
console.log("ToString:", arrToStr);  // Output: "0,0,0,0"

// .join()
let joinedStr = arr.join("-");
console.log("Joined:", joinedStr);  // Output: "0-0-0-0"
```
