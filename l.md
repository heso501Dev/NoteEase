
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

## `splice()` Method

The `splice()` method in JavaScript is used to modify an array by adding, removing, or replacing elements. It changes the original array.


#### Syntax:
```js
array.splice(start, deleteCount, item1, item2, ...)
```

```js
// Example 1: Removing elements
let arr1 = [1, 2, 3, 4, 5];
arr1.splice(2, 2);  // Removes 2 elements starting from index 2
console.log(arr1);  // Output: [1, 2, 5]

// Example 2: Adding elements
let arr2 = [1, 2, 5];
arr2.splice(2, 0, 3, 4);  // Adds 3 and 4 at index 2 without removing any elements
console.log(arr2);  // Output: [1, 2, 3, 4, 5]

// Example 3: Replacing elements
let arr3 = [1, 2, 3, 4, 5];
arr3.splice(2, 1, 6, 7);  // Removes 1 element at index 2 and adds 6 and 7
console.log(arr3);  // Output: [1, 2, 6, 7, 4, 5]
```

start: The index at which to start changing the array.
deleteCount: The number of elements to remove starting from the start index.
item1, item2, ...: The items to add to the array, starting from the start index.

<h1> Web API storage </h1>

The Web Storage API provides ways for websites to store data in a user's browser
| Storage Type        | Data Persistence           | Data Size            | Example Use Case             |
|---------------------|----------------------------|----------------------|-----------------------------|
| **Local Storage**    | Permanent (until deleted)   | 5MB to 10MB per domain | User preferences, settings   |
| **Session Storage**  | Temporary (session-based)   | 5MB to 10MB per domain | Storing session data         |
| **IndexedDB**        | Permanent                   | Can store much larger data | Large data like images, objects |

## Local Storage

`localStorage` is an object in JavaScript that provides a way to store data persistently in the web browser. It is part of the Web Storage API and allows you to save data as key-value pairs, which remain stored even after the user closes the browser or navigates away from the page. localStorage data is stored per domain and is accessible only within the same origin.

```js
// Store a key-value pair in localStorage (setItem)
localStorage.setItem('username', 'JohnDoe');  // Stores 'JohnDoe' under the key 'username'

// Retrieve the value of a key from localStorage (getItem)
let username = localStorage.getItem('username');  // Retrieves the value of 'username' (i.e., 'JohnDoe')
console.log(username);  // Output: 'JohnDoe'

// Remove a key-value pair from localStorage (removeItem)
localStorage.removeItem('username');  // Removes the key 'username' and its associated value

// Clear all items from localStorage (clear)
localStorage.clear();  // Removes all stored data from localStorage

// Get the name of a key at a specific index (key)
let keyAtIndex0 = localStorage.key(0);  // Returns the key at index 0 in the storage
console.log(keyAtIndex0);  // Output: The first key name stored in localStorage

// Get the number of items stored in localStorage (length)
let numberOfItems = localStorage.length;  // Returns the total number of items stored
console.log(numberOfItems);  // Output: The number of items in localStorage
```


## Session Storage

`sessionStorage` is similar to localStorage but with a key difference: data stored in sessionStorage is only available for the duration of the page session. Once the browser tab or window is closed, the data is cleared.

```js

// Store a key-value pair in sessionStorage (setItem)
sessionStorage.setItem('username', 'JaneDoe');  // Stores 'JaneDoe' under the key 'username'

// Retrieve the value of a key from sessionStorage (getItem)
let username = sessionStorage.getItem('username');  // Retrieves the value of 'username' (i.e., 'JaneDoe')
console.log(username);  // Output: 'JaneDoe'

// Remove a key-value pair from sessionStorage (removeItem)
sessionStorage.removeItem('username');  // Removes the key 'username' and its associated value

// Clear all items from sessionStorage (clear)
sessionStorage.clear();  // Removes all stored data from sessionStorage

// Get the name of a key at a specific index (key)
let keyAtIndex0 = sessionStorage.key(0);  // Returns the key at index 0 in the storage
console.log(keyAtIndex0);  // Output: The first key name stored in sessionStorage

// Get the total number of items stored in sessionStorage (length)
let numberOfItems = sessionStorage.length;  // Returns the total number of items stored
console.log(numberOfItems);  // Output: The number of items in sessionStorage
```

## Key Differences Between `localStorage` and `sessionStorage`:


| **Feature**          | **localStorage**                                             | **sessionStorage**                                           |
|----------------------|-------------------------------------------------------------|------------------------------------------------------------|
| **Persistence**      | Data persists even after the browser or tab is closed.      | Data is cleared once the browser tab or window is closed.   |
| **Scope**            | Data is shared across browser tabs of the same origin.      | Data is specific to a particular browser tab or window only. |

**Note** Both Stores data as key-value pairs `(both key and value are strings)`

<h1> JSON </h1>


JSON (JavaScript Object Notation) can represent an array of objects. A JSON array is a list of items enclosed in square brackets [], and each item in the array can be an object.

```js

[
  {
    "name": "Alice",
    "age": 25,
    "city": "New York"
  },
  {
    "name": "Bob",
    "age": 30,
    "city": "Los Angeles"
  },
  {
    "name": "Charlie",
    "age": 35,
    "city": "Chicago"
  }
]
```

## methods

```js
let userData = '{"name": "Bob", "age": 30}';

// Using JSON.parse() to convert JSON string to a JavaScript object
let user = JSON.parse(userData);
console.log(user.name);  // Output: Bob

// Using JSON.stringify() to convert the object back to JSON string
let jsonString = JSON.stringify(user);
console.log(jsonString);  // Output: '{"name":"Bob","age":30}'
```
