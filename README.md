# Week 1 Functional Programming w/Javascript

## Weekend
#### Objectives:

Functional Programmming
* React is functional and NOT Object Oriented
	* a paradigm where functions and not objects are the first class citizens
* what will be covered:
	* Pure Functions
	* First Class Functions
	* Higher Order Functions
	* Immutablility
	* Closures
	* Currying Functions
	* Recursion
	* Composition Over Inheritance
	* JavaScript Methods used Commonly for FUnctional Programming
Technical Interview whiteboarding in lieu of projects for at least a portion of this section
* meaning:
	* submit a solution
	* meet all peer requirements within their feedback
	* evaluations for peers are complete and have constructive feedback included

#### Intro To Functional Programming
* Stateless: can no longer store info in objects!!
* about what objects *do* not what they *are*
* we won't store info in objects rather we'll pass between functions
* we wil not reassign variable values
	* only const, no use of let where we can michael phelps it
* functions are more abstract
* **functional programming uses a method called composition where OOP uses inheritance to give objects functionality** 
* both paradigns can be incorporated

#### Testing Functional Code
* we can still use Jest to run tests for functional code
* **How to write tests for functional code:**
	* write test for 'smallest unit of behavior' (simplest)
		* in functional programming you always return the same output
	* verify the test fails
	* get the test to pass
* lessons on using jest with babel and webpack are bottom of the page [here](https://www.learnhowtoprogram.com/react-part-time/functional-programming-with-javascript-1e75b6d0-055f-43e6-9f66-7a959ffc3f78/testing-functional-code)
#### Using Node in Command Line
* using a REPL (READ-EVAL-PRINT-LOOP)
* we've tested front end JS code using the browser
	* we can test back-end code 'server-side' via Node
	* invoking node and then a file name
		* orrrr using a require statement such as:
```javascript
require('./js-code.js')
```
* must use the relative path "./" for this to add any files (can do multiple)
#### Immutability
* an essential component of functional programming
* **cant change the value of any variable!!! not for objects, primitives or arrays!!!**
OOP approach:
```javascript
let x = 1
x = 2 + 1
```
Functional approach: 
```javascript
const x = 1
const newX = 2 + x
```

* use const instead of let
* immutability leads to more reliable variables within the code
#### Imperative Vs. Declarative Programming
* imperative code is telling the program exactly what we want to do and how to do it step by step
* declarative is preferred for functional programming
	* with declarative we declare what the end result should be and let our program decide the best way to get that result
* its the difference between a step by step guide for how to wash clothes and use a washing machine vs "Wash the clothes"
* when we are making tags like </input/> in our HTML that's delcarative
* .map() in JS is also declarative programming 
* declarative code is considered more reusable and readable and easier to collaborate on
#### Pure Functions
* when we write in a functional style, the functions we write must be pure
* **a pure function will always return the same output given a specific input**
* a pure function cannot return a random value
* **A pure function always returns an output
* **cannot have side effects outside the returned value. no greater alteration 
	* they return a single thing!!
* a function that changes something in the DOM has a sideeffect of altering the DOM (ei. outside the function)
* **cannot rely on external variables or states
	* like affecting a property of a class
	* which is an external state that it would be altering perhaps
* same goes for global variables
* **benefits**
	* easier to test
		* 1 input == 1 output
	* can look at in isolation! like a black box
		* no external info is needed to review or understand the code
	* easier to isolate and prevent bugs
		* owing to the first two reasons
#### First Class Citizens
* in JavaScript functions are first class citizens
* this is because it has the fullest of capabilities
	* learn how to program distills this to "can be used same as a variable"
* it can be passed into another function as an argument
* we can assign a function to a variable
	* like when we store an anonymous function in one here:
```javascript
const funkyVar = function(foo) {
	return foo;
}

>> funkyVar("Hello!");
<< "Hello!"
```

* A function can also return another function
	* this is called a **higher order function
	* this allows for a programming tool called a closure

#### Closures
* a closure is an innter function that has access to variables from an outer function
* closures are made everytime a function is created, at creation time of the function
* if we have:

```javascript
function welcome(salutation) {
  return function(yourName) {
    return `${salutation}! Nice to meet you, ${yourName}!`
  }
}

const heyThere = welcome("Hey there");
```
then you'd get:
```javascript
> heyThere()
"Hey there! Nice to meet you, undefined!"
```

```javascript
> heyThere("Quin")
"Hey there! Nice to meet you, Quin!"
```

* a callback function does not have access to variables in the scope of the outer function **unless** it is defined inside the inner function
* can also be used in enclosing private data as seen [here.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
#### Currying
* named afteer **Haskell** (*eyyyyy*) Curry
* **currying a function** is taking a single function with more than one argument and rewriting it as a series of functions with one argument eac
* **a unary function** is a function that takes one argument
* such as turning the above:
```javascript
function aThingIMaybeLike(howMuchILikeIt, thing, reason) {
  return `I ${howMuchILikeIt} ${thing} because ${reason}.`;
}
```
into a series of nested closures like so:
```javascript
function aThingIMaybeLike(howMuchILikeIt) {
  return function(thing) {
    return function(reason) {
      return `I ${howMuchILikeIt} ${thing} because ${reason}.`;
    }
  }
}
```
* allows for greater flexibility and reusablity of code
#### Map, Reduce, and Filter
* looking at why these funcs are used so much in functional programming paradigm
* difference between these two:
 ```javascript
const numArray = [1, 2, 3, 4, 5];
let doubledArray = [];
numArray.forEach(function(element) {
  doubledArray.push(element * 2);
});
doubledArray;
```
and 
```javascript
const numArray = [1, 2, 3, 4, 5];
const doubledArray = numArray.map (e => e * 2);
```
* here we use an implicit return
	* **arrow functions allow for an implicit return value
**use map to alter every element of an array
reduce:
* will reduce an array to a single element
	* like summing an array
	* or finding the longest/shortest string in an array
**filter:
* to filter an array based on pre-described conditions
* ex to filter for developers at a company from an array of objects as such:
```javascript
const employees = [
  {
    name: "Ada",
    role: "developer"
  },
  {
    name: "Tom",
    role: "HR"
  },
  {
    name: "Jasmine",
    role: "developer"
  },
  {
    name: "Hank",
    role: "administrative assistant"
  }
];
```
then
```javascript
const developers = employees.filter(e => e.role === "developer");

output will be:
[ { name: 'Ada', role: 'developer' },
  { name: 'Jasmine', role: 'developer' } ]
```
will output
#### Recursion
* a function that calls upon itself
* uses a base case and a recursive condition
* **should always include a termination case
	* like if a recursive function requires a number a termination case would check it is really a number and exit the function if it aint!
* functions will complete from inner most to outermost
* all functions called go into the JavaScript Stack!
	* follows a LIFO (last in first out model)
* Tail call optimization
	* the return value of a function is computed and it doesnt allocate the entire function to the stack
	* browsers DOES NOT use this
	* ES6 DOES
	* Node DOES too
* an alternative is a **trampoline function
	* wracks a recursive function in a loop and breaks it down so each function doesn't heap onto the stack
