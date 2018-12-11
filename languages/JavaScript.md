# JavaScript Notes

## JavaScript

Prototypes are a fundamental feature of Javascript. Given this topic's importance to the language, they are a very hot interview/phone screen topic. Having a strong grasp on Javascript Prototypes will give you a major leg-up in the application process.

[JavaScript Notes](https://medium.freecodecamp.org/the-definitive-javascript-handbook-for-a-developer-interview-44ffc6aeb54e)

## Types && Coercion

There are 7 built-in types: null, undefined, boolean, string, number, object, and symbol.

All of the aforementioned types, aside from object, are primitives.

```
typeof 0              // number
typeof true           // boolean
typeof 'Hello'        // string
typeof Math           // object
typeof null           // object  !!
typeof Symbol('Hi')   // symbol (New ES6)
```

### Null vs Undefined

Undefined is the absence of a definition. It is used as the default value for uninitialized variables, function arguments that were not provided and missing properties of objects. Functions return undefined when nothing has been explicitly returned.

Null is the absence of a value. It is an assignment value that can be assigned to a variable as a representation of ‘no-value’.

### Falsey Values

```
Falsy values: "", 0, null, undefined, NaN, false.

Anything not explicitly on the falsy list is truthy — boolean coerced to true.
```

### String & Number coercion

The first thing you need to be aware of is the + operator. This is a tricky operator because it works for both number addition and string concatenation.

But, the star symbol, / , and -operators are exclusive for numeric operations. When these operators are used with a string, it forces the string to be coerced to a number.


```
1 + "2" = "12"
"" + 1 + 0 = "10"
"" - 1 + 0 = -1
"-9\n" + 5 = "-9\n5"
"-9\n" - 5 = -14
"2" * "3" = 6
4 + 5 + "px" = "9px"
"$" + 4 + 5 = "$45"
"4" - 2 = 2
"4px" - 2 = NaN
null + 1 = 1
undefined + 1 = NaN
```

### == vs. ===

It is widely spread that == checks for equality and === checks for equality and type. Well, that is a misconception.

In fact, == checks for equality with coercion and === checks for equality without coercion — strict equality.

```
2 == '2'            // True
2 === '2'           // False
undefined == null   // True
undefined === null  // False
```

Some tricky comparisons to look out for:

```
false == ""  // true
false == []  // true
false == {}  // false
"" == 0      // true
"" == []     // true
"" == {}     // false
0 == []      // true
0 == {}      // false
0 == null    // false
```
### Value vs Reference

Simple values (also known as primitives) are always assigned by value-copy: null, undefined , boolean, number, string and ES6 symbol.

```
var a = 2;        // 'a' hold a copy of the value 2.
var b = a;        // 'b' is always a copy of the value in 'a'
b++;
console.log(a);   // 2
console.log(b);   // 3
var c = [1,2,3];
var d = c;        // 'd' is a reference to the shared value
d.push( 4 );      // Mutates the referenced value (object)
console.log(c);   // [1,2,3,4]
console.log(d);   // [1,2,3,4]
/* Compound values are equal by reference */
var e = [1,2,3,4];
console.log(c === d);  // true
console.log(c === e);  // false
```

### Scope

Scope refers to the execution context. It defines the accessibility of variables and functions in the code.

Global Scope is the outermost scope. Variables declared outside a function are in the global scope and can be accessed in any other scope. In a browser, the window object is the global scope.

Local Scope is a scope nested inside another function scope. Variables declared in a local scope are accessible within this scope as well as in any inner scopes.

```
function outer() {
  let a = 1;
  function inner() {
    let b = 2;
    function innermost() {
      let c = 3;
      console.log(a, b, c);   // 1 2 3
    }
    innermost();
    console.log(a, b);        // 1 2 — 'c' is not defined
  }
  inner();
  console.log(a);             // 1 — 'b' and 'c' are not defined
}
outer();
```

You may think of Scopes as a series of doors decreasing in size (from biggest to smallest). A short person that fits through the smallest door — innermost scope — also fits through any bigger doors — outer scopes.

### Hoisting

The behavior of “moving” var and function declarations to the top of their respective scopes during the compilation phase is called hoisting.

Function declarations are completely hoisted. This means that a declared function can be called before it is defined.

```
console.log(toSquare(3));  // 9

function toSquare(n){
  return n*n;
}
```

let and const are not hoisted. var is hoisted

```
{  /* Original code */
  console.log(i);  // undefined
  var i = 10
  console.log(i);  // 10
}

{  /* Compilation phase */
  var i;
  console.log(i);  // undefined
  i = 10
  console.log(i);  // 10
}
// ES6 let & const
{
  console.log(i);  // ReferenceError: i is not defined
  const i = 10
  console.log(i);  // 10
}
{
  console.log(i);  // ReferenceError: i is not defined
  let i = 10
  console.log(i);  // 10
}
```

### Function Expression vs Function Declaration

#### Function Expression

A Function Expression is created when the execution reaches it and is usable from then on — it is not hoisted.

```
var sum = function(a, b) {
  return a + b;
}
```

#### Function Declaration
A Function Declaration can be called both before and after it was defined — it is hoisted.

```
function sum(a, b) {
  return a + b;
}
```

### Variables: var, let and const

Before ES6, it was only possible to declare a variable using var. Variables and functions declared inside another function cannot be accessed by any of the enclosing scopes — they are function-scoped.

Variables declared inside a block-scope, such as if statements and for loops, can be accessed from outside of the opening and closing curly braces of the block.

Note: An undeclared variable — assignment without var, let or const — creates a var variable in global scope.

```
function greeting() {
  console.log(s) // undefined
  if(true) {
    var s = 'Hi';
    undeclaredVar = 'I am automatically created in global scope';
  }
  console.log(s) // 'Hi'
}
console.log(s);  // Error — ReferenceError: s is not defined
greeting();
console.log(undeclaredVar) // 'I am automatically created in global scope'
```

ES6 let and const are new. They are not hoisted and block-scoped alternatives for variable declaration. This means that a pair of curly braces define a scope in which variables declared with either let or const are confined in.

```
let g1 = 'global 1'
let g2 = 'global 2'
{   /* Creating a new block scope */
  g1 = 'new global 1'
  let g2 = 'local global 2'
  console.log(g1)   // 'new global 1'
  console.log(g2)   // 'local global 2'
  console.log(g3)   // ReferenceError: g3 is not defined
  let g3 = 'I am not hoisted';
}
console.log(g1)    // 'new global 1'
console.log(g2)    // 'global 2'
```

### Closures

A closure is the combination of a function and the lexical environment from which it was declared. Closure allows a function to access variables from an enclosing scope — environment — even after it leaves the scope in which it was declared.

```
function sayHi(name){
  var message = `Hi ${name}!`;
  function greeting() {
    console.log(message)
  }
  return greeting
}
var sayHiToJon = sayHi('Jon');
console.log(sayHiToJon)     // ƒ() { console.log(message) }
console.log(sayHiToJon())   // 'Hi Jon!'
```

Refers to variables in outer scope.

One of the main benefits of closures is that it allows data encapsulation. This refers to the idea that some data should not be directly exposed. The following example illustrates that.

### Immediate Invoked Function Expression (IIFE)

An IIFE is a function expression that is called immediately after you define it. It is usually used when you want to create a new variable scope.

On IIFE you are calling the function exactly when you are defining it.

```
var result = [];
for (var i=0; i < 5; i++) {
  result.push( function() { return i } );
}
console.log( result[1]() ); // 5
console.log( result[3]() ); // 5
result = [];
for (var i=0; i < 5; i++) {
  (function () {
    var j = i; // copy current value of i
    result.push( function() { return j } );
  })();
}
console.log( result[1]() ); // 1
console.log( result[3]() ); // 3
```

### Context

Context is often confused as the same thing as Scope.

To clear things up, lets keep the following in mind:

Context is most often determined by how a function is invoked. It always refers to the value of this in a particular part of your code.

Scope refers to the visibility of variables.

### Function calls: call, apply and bind

All of these three methods are used to attach this into function and the difference is in the function invocation.

.call() invokes the function immediately and requires you to pass in arguments as a list (one by one).

.apply() invokes the function immediately and allows you to pass in arguments as an array.

.call() and .apply() are mostly equivalent and are used to borrow a method from an object. Choosing which one to use depends on which one is easier to pass the arguments in. Just decide whether it’s easier to pass in an array or a comma separated list of arguments.

.bind() returns a new function, with a certain context and parameters. It is usually used when you want a function to be called later with a certain context.

That is possible thanks to its ability to maintain a given context for calling the original function. This is useful for asynchronous callbacks and events.

.bind() works like the call function. It requires you to pass in the arguments one by one separated by a comma.

### 'this' keyword

Understanding the keyword this in JavaScript, and what it is referring to, can be quite complicated at times.

The value of this is usually determined by a functions execution context. Execution context simply means how a function is called.

The keyword this acts as a placeholder, and will refer to whichever object called that method when the method is actually used.

.bind() works a little bit differently. It creates a new function that will call the original one with the object that was bound to it.

### Strict Mode

JavaScript is executed in strict mode by using the “use strict” directive. Strict mode tightens the rules for parsing and error handling on your code.

Some of its benefits are:

* Makes debugging easier — Code errors that would otherwise have been ignored will now generate errors, such as assigning to non-writable global or property.
* Prevents accidental global variables — Assigning a value to an undeclared variable will now throw an error.
* Prevents invalid use of delete — Attempts to delete variables, functions and undeletable properties will now throw an error.
* Prevents duplicate property names or parameter values — Duplicated named property in an object or argument in a function will now throw an error. (This is no longer the case in ES6)
* Makes eval() safer — Variables and functions declared inside an eval() statement are not created in the surrounding scope.
* “Secures” JavaScript eliminating this coercion — Referencing a this value of null or undefined is not coerced to the global object. This means that in browsers it’s no longer possible to reference the window object using this inside a function.

### Prototype and Inheritance

Prototype is one of the most confusing concepts in JavaScript and one of the reason for that is because there are two different contexts in which the word prototype is used.

#### Prototype relationship
Each object has a prototype object, from which it inherits all of its prototype’s properties.
__proto__ is a non-standard mechanism (available in ES6) for retrieving the prototype of an object. It points to the object’s “parent” — the object’s prototype.

All normal objects also inherit a .constructor property that points to the constructor of the object. Whenever an object is created from a constructor function, the __proto__ property links that object to the .prototype property of the constructor function used to create it.

Object.getPrototypeOf()is the standard ES5 function for retrieving the prototype of an object.

#### Prototype property
Every function has a .prototype property.
It references to an object used to attach properties that will be inherited by objects further down the prototype chain. This object contains, by default, a .constructor property that points to the original constructor function.
Every object created with a constructor function inherits a constructor property that points back to that function.

```
function Dog(breed, name){
  this.breed = breed,
  this.name = name
}
Dog.prototype.describe = function() {
  console.log(`${this.name} is a ${this.breed}`)
}
const rusty = new Dog('Beagle', 'Rusty');

/* .prototype property points to an object which has constructor and attached
properties to be inherited by objects created by this constructor. */
console.log(Dog.prototype)  // { describe: ƒ , constructor: ƒ }

/* Object created from Dog constructor function */
console.log(rusty)   //  { breed: "Beagle", name: "Rusty" }
/* Object inherited properties from constructor function's prototype */
console.log(rusty.describe())   // "Rusty is a Beagle"
/* .__proto__ property points to the .prototype property of the constructor function */
console.log(rusty.__proto__)    // { describe: ƒ , constructor: ƒ }
/* .constructor property points to the constructor of the object */
console.log(rusty.constructor)  // ƒ Dog(breed, name) { ... }
#### Prototype Chain

The prototype chain is a series of links between objects that reference one another.

When looking for a property in an object, JavaScript engine will first try to access that property on the object itself.

If it is not found, the JavaScript engine will look for that property on the object it inherited its properties from — the object’s prototype.

The engine will traverse up the chain looking for that property and return the first one it finds.

The last object in the chain is the built-in Object.prototype, which has null as its prototype. Once the engine reaches this object, it returns undefined.

#### Own vs Inherited Properties

Objects have own properties and inherited properties.

Own properties are properties that were defined on the object.

Inherited properties were inherited through prototype chain.

```
function Car() { }
Car.prototype.wheels = 4;
Car.prototype.airbags = 1;

var myCar = new Car();
myCar.color = 'black';

/*  Check for Property including Prototype Chain:  */
console.log('airbags' in myCar)  // true
console.log(myCar.wheels)        // 4
console.log(myCar.year)          // undefined

/*  Check for Own Property:  */
console.log(myCar.hasOwnProperty('airbags'))  // false — Inherited
console.log(myCar.hasOwnProperty('color'))    // true
```

Object.create(obj) — Creates a new object with the specified prototype object and properties.

```
var dog = { legs: 4 };
var myDog = Object.create(dog);

console.log(myDog.hasOwnProperty('legs'))  // false
console.log(myDog.legs)                    // 4
console.log(myDog.__proto__ === dog)       // true
```

#### Inheritance by Reference

An inherited property is a copy by reference of the prototype object’s property from which it inherited that property.

If an object’s property is mutated on the prototype, objects which inherited that property will share the same mutation. But if the property is replaced, the change will not be shared.

```
var objProt = { text: 'original' };
var objAttachedToProt = Object.create(objProt);
console.log(objAttachedToProt.text)   // original

objProt.text = 'prototype property changed';
console.log(objAttachedToProt.text)   // prototype property changed

objProt = { text: 'replacing property' };
console.log(objAttachedToProt.text)   // prototype property changed
```

#### Classical Inheritance vs. Prototypal Inheritance

In classical inheritance, objects inherit from classes — like a blueprint or a description of the object to be created — and create sub-class relationships. These objects are created via constructor functions using the new keyword.

The downside of classical inheritance is that it causes:
inflexible hierarchy
tight coupling problems
fragile base class problems
duplication problems
And the so famous gorilla/banana problem — “What you wanted was a banana, what you got was a gorilla holding the banana, and the entire jungle.”

In prototypal inheritance, objects inherit directly from other objects. Objects are typically created via Object.create(), object literals or factory functions.

### Event Loop Lecture Notes

JavaScript is a single threaded programming language. It can only run one thing at a time.

The call stack is a data structure that records where in the program we are.

The heap is where memory allocation happens.

The call stack is where the stack frames live.

Stack overflow is where there are too many stacks in the call stack, and it has reached past the stack bound.

Blocking is when the execution of additional JavaScript in the Node.js process must wait until a non-JavaScript operation completes. This happens because the event loop is unable to continue running JavaScript while a blocking operation is occurring.

All of the I/O methods in the Node.js standard library provide asynchronous versions, which are non-blocking, and accept callback functions. Some methods also have blocking counterparts, which have names that end with Sync.

The event loop's job is to loop at the call stack and loop at the task queue.

If the stack is empty, it takes the first thing on the queue and pushes it onto the stack, effectively running it.

Any runtime commands will be run immediately, and any call back commands will be thrown into the task queue temporarily. When all of the runtime commands have completed running, only then will the callback commands be pushed onto the call stack to be executed.

Even though logically, it may seem like a command with a setTimeout timer of 0 milliseconds should run in constant time, the event loop actually pushes the event to the beginning of the task queue to only run after all of the real time events have concluded.

However, if you clone the V8 code base, and search all files using grep for setTimeout, DOM, or HTTP Request, those searches return empty.

We have our Web APIs, web services that hold the DOM, time out, AJAX, etc.

#### What is Event Delegation?

If you add an event listener to a DOM element, all nested children DOM elements also gain that same event listener through inheritance.

#### What is Event Bubbling?

The opposite of Event Delegation, also known as propagation. If a child DOM element's events will also bubble up and fire on all it's parents.

#### What is the difference between target and currentTarget?

The latter is the element with the listener attached, the former is the element that actually triggered it.

#### What is an IIFE?

An IIFE is an immediately invoked function expression.

```
// the following example would error out
function foo(){

}();

//this however is more acceptable
var foo = function(){
  // this is an expression
  //resolves to a value, even if just 'undefined'
};


//if you want to run it in one line, put parentheses around an expression like so:

(function foo(){})();
```

An expression is any valid unit of code that resolves to a value.

The use case of an IIFE would be to control variable scope.

The variables used in an IIFE are not available outside of the function expression itself.

#### Null/Undeclared/Undefined

Undeclared: You forgot to declare it somewhere before you referenced it.

Undefined: It has been declared, but not assigned a value.
```
var foo;

console.log(foo);
```

Null is a value. Its value is null. It has a "nothing" value.

It's value is not zero, not an empty string, object, or array. It is inherently falsy.

#### How do you check for these states?

Undeclared usually lets you know it is undeclared, except when assigning a value.

Checking for undefined also kind of sucks, you can use typeof, but it will return undefined as a string ("undefined").

=== is preferred to check if something is undefined.

typeof null will return an object, which is a bug

=== can also be used to check if something is null.

#### Asynchronous JavaScript

JavaScript is a single-threaded programming language. This means that the JavaScript engine can only process a piece of code at a time.

One of its main consequences is that when JavaScript encounters a piece of code that takes a long time to process, it will block all code after that from running.

JavaScript uses a data structure that stores information about active functions named Call Stack.

A Call Stack is like a pile of books. Every book that goes into that pile sits on top of the previous book.

The last book to go into the pile will be the first one removed from it, and the first book added to the pile will be the last one removed.

The solution to executing heavy pieces of code without blocking anything is asynchronous callback functions. These functions are executed later — asynchronously.

The asynchronous process begins with an asynchronous callback functions placed into a Heap or region of memory. You can think of the Heap as an Event Manager.

The Call Stack asks the Event Manager to execute a specific function only when a certain event happens. Once that event happens, the Event Manager moves the function to the Callback Queue. Note: When the Event Manager handles a function, the code after that is not blocked and JavaScript continues its execution.

The Event Loop handles the execution of multiple pieces of your code over time. The Event Loop monitors the Call Stack and the Callback Queue.

The Call Stack is constantly checked whether it is empty or not. When it is empty, the Callback Queue is checked if there is a function waiting to be invoked. When there is a function waiting, the first function in the queue is pushed into the Call Stack, which will run it. This checking process is called a ‘tick’ in the Event Loop.

```
const first = function () {
  console.log('First message')
}
const second = function () {
  console.log('Second message')
}
const third = function() {
  console.log('Third message')
}

first();
setTimeout(second, 0);
third();

// Output:
  // First message
  // Third message
  // Second message
```

Note: The second() function is not executed after 0ms. The time you pass in to setTimeout function does not relate to the delay of its execution. The Event Manager will wait the given time before moving that function into the Callback Queue. Its execution will only take place on a future ‘tick’ in the Event Loop.

#### Event Bubbling/Capturing

Bubbling

The bubbling principle is simple.

When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.

Stopping bubbling

A bubbling event goes from the target element straight up. Normally it goes upwards till <html>, and then to document object, and some events even reach window, calling all handlers on the path.

But any handler may decide that the event has been fully processed and stop the bubbling.

The method for it is event.stopPropagation().

Capturing

There’s another phase of event processing called “capturing”. It is rarely used in real code, but sometimes can be useful.

The standard DOM Events describes 3 phases of event propagation:

Capturing phase – the event goes down to the element.
Target phase – the event reached the target element.
Bubbling phase – the event bubbles up from the element.

#### Event Delegation

Capturing and bubbling allow us to implement one of most powerful event handling patterns called event delegation.

The idea is that if we have a lot of elements handled in a similar way, then instead of assigning a handler to each of them – we put a single handler on their common ancestor.

In the handler we get event.target, see where the event actually happened and handle it.


#### ES6 Changes

Block Scope

ES5 only had “function-level scope” (i.e. you wrap code in functions to create scope) and caused a lot of issues. ES6 provides “block”-level scoping(i.e curly-braces to scope) when we use “let” or “const” instead of “var”.

Prevent Duplicate Variable Declaration

ES6 doesn’t allow duplicate declaration of variables when we declare them using “let” or “const” in the same scope. This is very helpful in avoiding duplicate function expressions coming from different libraries (like the “add” function expression below).

babel — A Tool to convert ES6 to ES5

Babel is the most popular tool used to convert ES6 to ES5

Makes It Trivial To Use Functions In Loops

In ES5, if you had a function inside a loop (like for(var i = 0; i < 3; i++) {…}), and if that function tried to access the looping variable “i”, we’d be in trouble because of hoisting. In ES6, if you use “let”, you can use functions without any issue.

Strict Mode

Strict Mode(“use strict”) helps identify common issues (or “bad” parts) and also helps with “securing” JavaScript. In ES5, the Strict Mode is optional but in ES6, it’s needed for many ES6 features. So most people and tools like babel automatically add “use strict” at the top of the file putting the whole JS code in strict mode and forcing us to write better JavaScript.

### WebPage LifeCycle

#### DOMContentLoaded, load, beforeunload, unload

The lifecycle of an HTML page has three important events:

* DOMContentLoaded – the browser fully loaded HTML, and the DOM tree is built, but external resources like pictures <img> and stylesheets may be not yet loaded.
* load – the browser loaded all resources (images, styles etc).
* beforeunload/unload – when the user is leaving the page.

#### DOMContentLoaded

DOMContentLoaded event happens on the document object.

To listen for this event we have to use "addEventListener":

```
document.addEventListener("DOMContentLoaded", ready);
```

At the first sight DOMContentLoaded event is very simple. The DOM tree is ready – here’s the event. But there are few peculiarities.

#### DOMContentLoaded and scripts

When the browser initially loads HTML and comes across a <script>...</script> in the text, it can’t continue building DOM. It must execute the script right now. So DOMContentLoaded may only happen after all such scripts are executed.

External scripts (with src) also put DOM building to pause while the script is loading and executing. So DOMContentLoaded waits for external scripts as well.

The only exception are external scripts with async and defer attributes. They tell the browser to continue processing without waiting for the scripts. This lets the user see the page before scripts finish loading, which is good for performance.

#### DOMContentLoaded and styles

External style sheets don’t affect DOM, and so DOMContentLoaded does not wait for them.

But there’s a pitfall: if we have a script after the style, then that script must wait for the stylesheet to execute:

```
<link type="text/css" rel="stylesheet" href="style.css">
<script>
  // the script doesn't not execute until the stylesheet is loaded
  alert(getComputedStyle(document.body).marginTop);
</script>
```

The reason is that the script may want to get coordinates and other style-dependent properties of elements, like in the example above. Naturally, it has to wait for styles to load.

As DOMContentLoaded waits for scripts, it now waits for styles before them as well.

#### Built-in browser autofill

Firefox, Chrome and Opera autofill forms on DOMContentLoaded.

For instance, if the page has a form with login and password, and the browser remembered the values, then on DOMContentLoaded it may try to autofill them (if approved by the user).

So if DOMContentLoaded is postponed by long-loading scripts, then autofill also awaits. You probably saw that on some sites (if you use browser autofill) – the login/password fields don’t get autofilled immediately, but there’s a delay till the page fully loads. That’s actually the delay until the DOMContentLoaded event.

One of minor benefits in using async and defer for external scripts – they don’t block DOMContentLoaded and don’t delay browser autofill

#### readyState
What happens if we set the DOMContentLoaded handler after the document is loaded?

Naturally, it never runs.

There are cases when we are not sure whether the document is ready or not, for instance an external script with async attribute loads and runs asynchronously. Depending on the network, it may load and execute before the document is complete or after that, we can’t be sure. So we should be able to know the current state of the document.

The document.readyState property gives us information about it. There are 3 possible values:

* "loading" – the document is loading.
* "interactive" – the document was fully read.
* "complete" – the document was fully read and all resources (like images) are loaded too.

So we can check document.readyState and setup a handler or execute the code immediately if it’s ready.

Like this:

```
function work() { /*...*/ }

if (document.readyState == 'loading') {
  document.addEventListener('DOMContentLoaded', work);
} else {
  work();
}
```

#### Lifecycle events summary

Page lifecycle events:

* DOMContentLoaded event triggers on document when DOM is ready. We can apply JavaScript to elements at this stage.
* All inline scripts and scripts with defer are already executed.
* Async scripts may execute both before and after the event, depends on when they load.
* Images and other resources may also still continue loading.
load event on window triggers when the page and all resources are loaded. We rarely use it, because there’s usually no need to wait for so long.
* beforeunload event on window triggers when the user wants to leave the page. If it returns a string, the browser shows a question whether the user really wants to leave or not.
unload event on window triggers when the user is finally leaving, in the handler we can only do simple things that do not involve delays or asking a user. Because of that limitation, it’s rarely used.
* document.readyState is the current state of the document, changes can be tracked in the readystatechange event:
* loading – the document is loading.
* interactive – the document is parsed, happens at about the same time as DOMContentLoaded, but before it.
* complete – the document and resources are loaded, happens at about the same time as window.onload, but before it.

#### DOM Events

DOM events are set to notify whenever any such event takes place.

Events can be anything from basic user interactions (such as clicks, or keydowns) to automated notifications of things happening in the rendering model.

#### Most Common Events

| Event Name  | Fired When |
| ------------- | ------------- |
| Cached  | The resources listed in the manifest have been downloaded, and the application is now cached.  |
| Error  | A resource failed to load.  |
| Abort  | The loading of a resource has been aborted.  |
| Load  | A resource and its dependent resources have finished loading.  |
| beforeunload  | The window, the document and its resources are about to be unloaded.  |
| unload  | The document or a dependent resource is being unloaded.  |

#### Network Events

| Event Name  | Fired When  |
| ------------- | ------------- |
| online  | The browser has gained access to the network.  |
| offline  | The browser has lost access to the network.  |

#### Focus Events

| Event Name  | Fired When  |
| ------------- | ------------- |
| focus  | An element has received focus (does not bubble).  |
| blur  | An element has lost focus (does not bubble).  |


#### Promises

* A “producing code” that does something and takes time. For instance, the code loads a remote script. That’s a “singer”.
* A “consuming code” that wants the result of the “producing code” once it’s ready. Many functions may need that result. These are the “fans”.
* A promise is a special JavaScript object that links the “producing code” and the “consuming code” together. In terms of our analogy: this is the “subscription list”. The “producing code” takes whatever time it needs to produce the promised result, and the “promise” makes that result available to all of the subscribed code when it’s ready.


The constructor syntax for a promise object is:

```
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
```

The function passed to new Promise is called the executor. When the promise is created, this executor function runs automatically. It contains the producing code, that should eventually produce a result. In terms of the analogy above: the executor is the “singer”.


The resulting promise object has internal properties:

* state — initially “pending”, then changes to either “fulfilled” or “rejected”,
* result — an arbitrary value of your choosing, initially undefined.
When the executor finishes the job, it should call one of the functions that it gets as arguments:

* resolve(value) — to indicate that the job finished successfully:
  * sets state to "fulfilled",
  * sets result to value.
* reject(error) — to indicate that an error occurred:
  * sets state to "rejected",
  * sets result to error.

Here is an example of a Promise constructor and a simple executor function with its “producing code” (the setTimeout):

```
let promise = new Promise(function(resolve, reject) {
  // the function is executed automatically when the promise is constructed

  // after 1 second signal that the job is done with the result "done!"
  setTimeout(() => resolve("done!"), 1000);
});
```
