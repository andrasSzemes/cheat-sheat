<style>
.block {
    background-color: #f5f5f5;
    padding: 6px 10px;
    border-radius: 5px;
    box-shadow: 0 0 5px 0px grey;margin:15px 0px;
    padding-bottom: 1px;
    font-size:13px;
    transition: all 1s ease;
    overflow: hidden;
}
code {
    font-size: 12px;
}
.block2 {
    background-color: #fffae7;
    padding: 6px 10px;
    border-radius: 5px;
    box-shadow: 0 0 5px 0px grey;margin:15px 0px;
    padding-bottom: 1px;
    font-size:13px;
    color: #7c1212;
    font-weight: 600
}

.detail .long {
    display: none;
  }

  .detail:hover .short {
    display: none;
  }
  .detail:hover .long {
    display: inline;
  }

  .detail .short {
    background-color: #FFF6E9;
  }
</style>

<div class="block">

# Bit of history
JavaScript is a high-level, dynamic, and interpreted programming language.

It was built in only 10 days in 1995 by a single person, Brendan Eich, who was tasked with building a simple scripting language to be used in version 2 of the Netscape browser. It was initially called LiveScript, but since the Java language was so popular at the time, the name was changed to JavaScript - although Java and JavaScript are in no way related.

For the first few years, after it was built, JavaScript was a simple scripting language to add mouseover effects and other interactivity to static pages. Those effects were being added to webpages using the `<script>` HTML element.

Inside each of the script elements, there could be some JavaScript code. Due to the rule that HTML, CSS, and JavaScript must be backward compatible, even the most advanced code written in JavaScript today ends up being written between those script tags.

In 1996 Netscape made a deal with the organization known as ECMA (European Computer Manufacturers Association) to draft the specification of the JavaScript language, and in 1997 the first edition of the ECMAScript specification was published.

JavaScript as a language is not a completely separate, stand-alone entity. It only exists as an implementation. This implementation is known as a JavaScript engine. Even at the beginning different browsers interpreted the code slightly differently and developers had to take into consideration that. For solving this issue jQuery was a solution.

Traditionally, the only environment in which it was possible to run a JavaScript engine, was the browser. More specifically, a JavaScript engine was just another building block of the browser. It was there to help a browser accomplish its users' goal of utilizing the internet for work, research, and play.

Additionally, the JavaScript engine itself comes with different ways to interact with various other parts of the browser. These are known as Browser APIs.

Thus, the code that you write in the JavaScript programming language allows you to:
1. Interact with the JavaScript engine inside of the browser
2. Interact with other browser functionality that exists outside of the JavaScript engine, but is still inside the browser.

The webpage development then was revolutionised with the appearance of frameworks like React.

Although traditionally it was possible to interact with the JavaScript engine only inside of the browser, this all changed in 2009, when Node.js was built by Ryan Dahl.

He came up with a way to use a JavaScript engine as a stand-alone entity. Suddenly, it was possible to use JavaScript outside of the browser, as a separate program on the command line, or as a server-side environment. Therefore JavaScript’s capabilities greatly depend on the environment it’s running in. For instance, Node.js supports functions that allow JavaScript to read/write arbitrary files, perform network requests, etc.

Also as it begin to be popular, now it can be used to translate to other languages also. Like using ReactNative, which converts from JS to Kotlin and Swift. Moreover there are other languages which are converted back to JS as that's the language of the running enginge, like TypeScript (which added strong typing and more to JS).

Today, JavaScript is ubiquitous and is running in browsers, on servers, actually, on any device that can run a JavaScript engine.
</div>


<div class="block">

# Facts
When it comes to developing a webpage, you don't really have another choise than JS to use (allows direct interaction with webpages dynamically ont the client). So using it in the backend is quite handy to simplyfy development.

Basically we would kill half of the previous webpages still running on the internet if we would cut out this language. (Have to keep up backward compatibility)

JavaScript is a high level language, which means it needs to be interpreted (converted to binary code that the CPU is able to work with)

Can be used for: power websites, communicate with databases/apis, mobile apps (ReactNative), program devices (IoT)
</div>


# JS features

```javascript
// comment for facilitate communication with your furture self, team members

/*
  multi-line
  comment
*/
```
<div class="detail">
<div class="short">

```js
; // delimiter, ASI
```
</div>
<div class="long">

```javascript
; // delimiter
// the engine has a feature known as Automatic Semi-colon Insertion for missing ones

// EXAMPLE FOR ASI ERROR
let a = 5
let b = 10

let sum = a + b // TypeError: b is not a function
(function() {
    console.log('Hello');
})()
```
</div>
</div>



<div class="detail">
<div class="short">

```js
console.log("Hello, World");
```

</div>
<div class="long">

```javascript
console.log("Hello, World");
console.log("Hello," + " World");
console.log("Hello,", "World"); // space added between


// STYLE CONSOLE LOG
console.log("%cHello, World", "color: blue; font-size: 40px"); // %c is a must here

console.log("%cHello%c, %cWorld%c!", 
  "color: blue", 
  "", // No style for the comma
  "color: red",
  "text-decoration: underline"
);
```
</div>
</div>











```javascript
var apple; // fine, value: undefined
apple = "pomme"
```

```javascript
// 7 primitive datatypes

// String
"a", 'b', `template ${1 + 2}
literal`

// Number
42, 42.424242

// BigInt
BigInt(123456789012345678901234567890);
123456789012345678901234567890n;

// Boolean
true, false

null        // intentional absence of value
undefined   // not yet assigned a value, ({}).alma == undefined


// Symbol
Symbol('sym1')


typeof("abc")
typeof(123)
typeof(1 < 2)
typeof([])        // object
typeof(() => {})  // function
```

```javascript
// falsy values
false, 0, -0, 0n, "", null, undefined, NaN, document.all

// truthy values
true, {}, [], 42, "0", "false", new Date(), -42, 12n, 3.14, -3.14, Infinity, -Infinity
```

<div class="detail">
<div class="short">

```js
const sym = Symbol("description");
```
</div>
<div class="long">

```javascript
// Symbols can be used as keys for object properties, ensuring that the properties do not collide with other properties, even if they have the same name.
const sym = Symbol("description");

const obj = {
  [sym]: "value"
};
console.log(obj[sym]); // Outputs: value

const symbols = Object.getOwnPropertySymbols(obj);



// Creating a global symbol
const globalSym1 = Symbol.for("globalKey");
const globalSym2 = Symbol.for("globalKey");

console.log(globalSym1 === globalSym2); // Outputs: true

// Retrieving the key for a global symbol
const key = Symbol.keyFor(globalSym1);
console.log(key); // Outputs: globalKey
```
</div>
</div>



### Operators
```javascript
3 + 4 // +, -, /, *, **, >, <, %
"a" + "b" // concatenation operator instead of addition operator
1 + "2" // "12" as coercion happens

true && true
true || false
! false

100 == "100"  // true, Loose Equality Operator
100 === "100" // false, Strict Equality Operator or Identity Operator
!=
!==

=
+= // -=
```

###  Flow control statements
```js
// conditional statements
if (contition) {}
else if (condition2) {}
else {}
```

```js
// switch statement
switch (value) {
    case 1:
        // ...
        break
    case 2:
        // ...
        break
    default:
        // ...
}
```



<div class="detail">
<div class="short">

```js
// loops

for (let i=1; i<10; ++i) {
    console.log(i)
}

for (let color of ['red', 'orange', 'yellow']) {}
for (const prop in obj) {}

while (condition) {
    
}
```
</div>
<div class="long">


```javascript
// loops

for (let i=1; i<10; ++i) {
    console.log(i)
}

const exampleObj = {a: 1, b: 2}

for (let color of ['red', 'orange', 'yellow']) {}

for (const key of Object.keys(exampleObj)) {}

for (const value of Object.values(exampleObj)) {}

for (const [key,value] of Object.entries(exampleObj)) {}


// SOME SPICE
const hierarchyObj = Object.create(exampleObj)
hierarchyObj.c = 3

// iterates over object AND it's prototype too
for (const prop in hierarchyObj) {console.log(prop)}                // a, b, c
for (const prop of Object.keys(hierarchyObj)) {console.log(prop)}   // c


while (condition) {
    
}
```
</div>
</div>

```javascript
try {
    throw new Error("abc")
} catch (error) {
    // ...
}
```



### Some string features
```javascript
// string
"abc".length

"abc"[0]
"abc".charAt(0) // "a"

"abcc".indexOf("c")        // 2
"abcc".lastIndexOf() ("c") // 3

"ab" + "c"       // "abc"
"ab".concat("c") // "abc"

"ho-ho-ho".split("-"); // ['ho', 'ho', 'ho']

"abc".toUpperCase() // "ABC"
"ABC".toLowerCase() // "abc"
```

### Functions
First class function/ first-class citizens:
  a function can be: passed to another function, saved in a variable, be returned from a function
  in other words, a function is just a value

Hoisting is a behavior in JavaScript where (variable) and function declarations are moved to the top of their containing scope during the compilation phase before the code is executed. This means that (variables) and functions can be used before they are declared in the code.

```javascript
// Function Declaration : hoisted, must have a name
//   The function can be called before it is defined due to hoisting.
add(1,2)

function add(a, b) {
  return a + b
}



// Function Expression : NOT hoisted
//   Anonymous Function Expression
const substract = function(a, b) {
  return a - b
}
substract(7,2)

//   Named Function Expression
//     The name can be used within the function for recursion or debugging
const factorial = function fact(n) { // 
  if (n <= 1) return 1;
  return n * fact(n - 1);
};
factorial(5)



// Arrow Function
const multiply = (a, b) => a + b;
const multiply2 = (a, b) => {
  return a + b
}





// passing as parameter
function doSomething(num1, num2, fn) {
  fn(num1, num2)
}
doSomething(1,2,add)        // works
doSomething(1,2,substract)  // works
doSomething(1,2,multiply)   // works


// higher-order function
//   A higher-order function is a function that either takes one or more functions as arguments or returns a function as its result.
```


<div class="detail">
<div class="short">

Traditional functions have their own this context, arrow functions do not.
</div>
<div class="long">

<div class="block">

Traditional functions have their own this context, which can be explicitly set using methods like .call(), .apply(), or .bind(). When you use .call() on a traditional function, the this context within that function is set to the value you pass as the first argument to .call().

Arrow functions do not have their own this context. Instead, they lexically inherit this from the surrounding scope at the time they are defined.

```js
const myObject = {
  value: 42,
  
  // Traditional function expression
  traditionalFunction: function() {
    console.log('Traditional function:', this.value);
  },
  
  // Arrow function expression
  arrowFunction: () => {
    console.log('Arrow function:', this.value);
  },
  
  // Function expression assigned to a property
  functionExpression: function() {
    console.log('Function expression:', this.value);
  }
};

// Calling methods
myObject.traditionalFunction();  // "Traditional function: 42"
myObject.arrowFunction();        // "Arrow function: undefined"
myObject.functionExpression();  // "Function expression: 42"

// Using .call() to change `this` context
const otherContext = { value: 99 };

myObject.traditionalFunction.call(otherContext); // "Traditional function: 99"
myObject.arrowFunction.call(otherContext);      // "Arrow function: undefined"
myObject.functionExpression.call(otherContext); // "Function expression: 99"
```

To see an example where an arrow function's this context is not undefined, you need to define the arrow function within a context where this is not the global scope or undefined.

```js
class MyClass {
  constructor(value) {
    this.value = value;
  }
  
  // Traditional method
  traditionalMethod() {
    console.log('Traditional method:', this.value);
  }
  
  // Arrow function as a property
  arrowFunction = () => {
    console.log('Arrow function:', this.value);
  }
}

const instance = new MyClass(42);

// Calling methods
instance.traditionalMethod();  // Output: "Traditional method: 42"
instance.arrowFunction();      // Output: "Arrow function: 42"

// Using `.call()` to change `this` context
const otherContext = { value: 99 };

instance.traditionalMethod.call(otherContext); // Output: "Traditional method: 99"
instance.arrowFunction.call(otherContext);     // Output: "Arrow function: 42"
```
</div>
</div>
</div>



<div class="detail">
<div class="short">

Arrow functions do not have their own arguments object. Instead, they inherit arguments from the surrounding context.
</div>
<div class="long">

<div class="block">

Arrow functions do not have their own arguments object. Instead, they inherit arguments from the surrounding context. This can be useful when you need to access the arguments object of an outer function.

```js
function outerFunction() {
  console.log(arguments); // Logs the arguments of outerFunction
  
  const innerFunction = () => {
    console.log(arguments); // Inherits arguments from outerFunction
  };
  
  innerFunction(1, 2, 3); // Logs the same arguments as outerFunction
}

outerFunction('a', 'b'); // Logs ['a', 'b'] twice
```
</div>
</div>
</div>

```js
function noDefaultParams(number) {
    console.log('Result:', number * number)
}

noDefaultParams(); // Result: NaN
// JavaScript, due to its dynamic nature, doesn't throw an error,
//   but it does return a non-sensical output.

function withDefaultParams(number = 10) {
    console.log('Result:', number * number)
}

function greet(name, age = 25) {
  console.log(`Hello, my name is ${name} and I am ${age} years old.`);
}

greet('Alice', 30); // Output: Hello, my name is Alice and I am 30 years old.
greet('Bob');       // Output: Hello, my name is Bob and I am 25 years old.
greet();            // Output: Hello, my name is undefined and I am 25 years old.
```







```js
// TODO: constructor function, prototype
```


<div class="detail">
<div class="short">

```js
Math.ceil()
Math.floor()
Math.round()
Math.pow(2,3)
Math.sqrt(16)
Math.abs(-10)
Math.min(9,8,7) // returns 7
Math.max(9,8,7) // returns 9
Math.random()
```
</div>
<div class="long">


```javascript
Math.PI, Math.E, Math.LN2

Math.ceil() // rounds up to the closest integer 

Math.floor() // rounds down to the closest integer 

Math.round() // rounds up to the closest integer if the decimal is .5 or above; otherwise, rounds down to the closest integer 

Math.trunc() // trims the decimal, leaving only the integer


Math.pow(2,3) // calculates the number 2 to the power of 3, the result is 8 

Math.sqrt(16) // calculates the square root of 16, the result is 4 

Math.cbrt(8) // finds the cube root of 8, the result is 2 

Math.abs(-10) // returns the absolute value, the result is 10 

// Logarithmic methods:
Math.log(), Math.log2(), Math.log10() 

// Return the minimum and maximum values of all the inputs:
Math.min(9,8,7) // returns 7
Math.max(9,8,7) // returns 9

// Trigonometric methods:
Math.sin(), Math.cos(), Math.tan(), etc.


Math.random() // decimal number between 0 and 0.99
```
</div>
</div>





### Array

```javascript
// build
[] // array literal syntax
const arr = ['a', 'b', 'c']
arr.push('d')
arr.pop() // remove last item
// TODO general method examples

// access content
arr[0] // 'a'
```





### Object

```javascript
const obj = { // object literal notation
  key: "value"
}

obj.key2 = 2 // dot notation

obj["key  3"] = 4       // brackets notation
obj["1212"] = 4         // obj.1212 = 4 does not work
obj[obj.key] = "value'" // can evaluate expressions

console.log(obj["key"])

obj.func = () => {}
obj.func2 = function() {}
```







### Variables
```javascript
// scope
// var:         global or function scope
// const, let:  global or block scope


// ES5
// number is accessible here with undefined value
var number = 1 // global scope
var number = 2 // redeclaration is OK

function func() {
  // only accessible in the function where it is declared
  var localScopedVariable = 2
}

// ES6 introduced block scope
// only accessible in the block it is declared in
// block scope is used when we use let and const keywords for declaration

// color is NOT accessibel before declaration
let color = "red";
let color = "";     // can not be redeclared, const is the same
if (color == "red") {
  let color = "blue";
}
```





### OOP
```javascript
const obj = {
  value: 1,
  increment: function() {
    this.value++;
  }
}


const obj = {
  value: 1,
  increment: () => { // does not work
    this.value++;
  }
}



class Something {
  constructor(param1, param2) {
    super()
    this.param1 = param1;
    this.param2 = param2;
  }

  method() {
    // ...
  }
}

const something = new Something("that", 123)
```

Every class is a child class of the Object class.
When using a default or empty constructor method, JavaScript implicitly calls the Object superclass to create the instance.

```javascript
class Animal { /* ...class code here... */ }

var myDog = Object.create(Animal)




class Animal { /* ...class code here... */ }
class Bird extends Animal { /* ...class code here... */ }
class Eagle extends Bird { /* ...class code here... */ }

const animal1 = new Animal();
animal1.getPrototype();       // {constructor: f, ..., getPrototype: f}
// same returned value as for Animal.prototype

const bird1 = new Bird();
bird1.getPrototype();         // Animal {constructor: f, ..., getPrototype: f}
// same returned value as for Bird.prototype.__ptoto__
```


JavaScript has a number of built-in object types, such as:

 Math, Date, Object, Function, Boolean, Symbol, Array, Map, Set, Promise, JSON, etc.

These objects are sometimes referred to as "native objects".

Even tough we can create an Array, Function, RegExp using their constructor, it's best practice to create them using thair literal.


```javascript
var bird = {
  hasWings: true
}

// prototype
var penguin1 = Object.create(bird) // class syntax is prefered instead of this
console.log(penguin1)           // {}
console.log(penguin1.hasWings)  // true

bird.hasWings = false
console.log(penguin1.hasWings)  // false
```

Using the class syntax, all the methods will live in the prototype object, and only the new object's data will exist on the object instance itself. (even there's a middle class in the hierarchy with some properties, that data will live in the created object. It can be seen when console logging it)

If a method is not existing on the actual object, it will look up in the hierarchy for the first occurence of it.

```javascript
class Animal {
    constructor(color = 'yellow', energy = 100) {
        this.color = color;
        this.energy = energy;
    }
}
class Cat extends Animal {
    constructor(sound = 'purr', canJumpHigh = true, canClimbTrees = true, color, energy) {
        super(color, energy);
        this.sound = sound;
        this.canClimbTrees = canClimbTrees;
        this.canJumpHigh = canJumpHigh;
    }
}
class Tiger extends Cat {
    constructor(tigerSound = "Roar!", sound,canJumpHigh,canClimbTrees, color,energy) {
        super(sound,canJumpHigh,canClimbTrees, color,energy);
        this.tigerSound = tigerSound;
    }
}
```

```javascript
// de-structure, the original object/array stays intact

let {PI} = Math;
console.log(PI);

const colors = ['red', 'blue', 'green'];
const [first, second, third] = colors;

// spread operator
const params = ['a', 1, true];
function test(str, num, bool) {
  console.log(str, num, bool)
}
test(...params)

  // concatenate arrays
  const firstHalf = [1,2,3,4,5]
  const secondHalf = [6,7,8,9]
  const newArray = [...firstHalf, ...secondHalf]

  // join objects
  const obj1 = {a: 1}
  const obj2 = {b: 2}
  const newObj = {...obj1, ...obj2}

  // split string
  [..."Hello"]

  // copy obj, array
  const copyArr = [...newArray]
  const copyObj = {...newObj}

// rest operator
const [first, second, third, ...rest] = [1,2,3,4,5,6,7]

function prod(rate, ...nums) { return nums.map(num => num * rate) }
prod(2,1,2,3,4,5).forEach(num => console.log(num))
```

JavaScript is somewhat limited in the types of data structures available compared to other programming languages, such as, Java or Python.
Objects, arrays, maps and sets are available.

With maps any value can be used as a key. With objects, keys can only be strings or symbols.
```javascript
const uniqueNums = new Set([1,2,3,1,2,3,4,1,2,3])


const map = new Map();
map.set('name', 'Alice');
map.set('age', 30);
map.set('city', 'New York');
map.get('name') // 'Alice'

map.forEach((value, key) => {
  console.log(`${key}: ${value}`);
});

for (const [key, value] of map) { // no real need for .entries()
  console.log(`${key}: ${value}`);
}

for (const [key, value] of map.entries()) {
  console.log(`${key}: ${value}`);
}
```


```js
// foreach
['a', 'b', 'c'].forEach(value => console.log(value))
['a', 'b', 'c'].forEach((value, index) => console.log(`${index}. ${value}`))

// filter
['a', 'b', 'c'].filter(value => value != 'b')

// map
['a', 'b', 'c'].map(value => `${value} ${value}`)
```


Without modules, all functions and variables which are globally declared are available, but name collision is a problem if you use libraries.

CommonJS solves this issue in NodeJS, but not in browsers. Require, Module.exports
To make the import work, a static server is needed.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<script type="module">
    import {someFunction} from './index.js'

    someFunction()
</script>
<body>
    
</body>
</html>
```
```javascript
export function someFunction() {
  console.log("Something!")
}

export default greeting;
```

JSON is just a string
it's popularity comes from
- lightweight syntax very similar to "a stringified JavaScript object"
- easier to handle in JavaScript code, since, JSON, after all, is just JavaScript

all JSON code is JavaScript, but not all JavaScript code is JSON

```javascript
const jsonStr = '{"a": "b"}'
const plainObj = JSON.parse(jsonStr)
plainObj.c = "d"
JSON.stringify(plainObj)
```

In JSON no functions or JS comments allowed.



Topics still:
- promises and async/await
- modules
- closures
- Prototypal Inheritance
- Web APIs
  - fetch
  - localStorage
- Development Tools
  - Webpack
  - Babel 