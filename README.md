# es6-features

List and summary of es6 Features
-
####Arrows

* Uses `=>` instead of `function` 
* The `this` feature can be refered to the correct function rather than the function that `this` is called in

####Classes

* Use the `class` keyword to declare a class
* Classes cant be hoisted
* Classes can be named or unnamed


```js
// unnamed

var Rectangle = class {

  constructor(height, width) {

    this.height = height;

    this.width = width;

  }

};


// named

var Rectangle = class Rectangle {

  constructor(height, width) {

    this.height = height;

    this.width = width;

  }
};
```

####Enhanced Object Literals

* Is an object that contains zero or more pairs of property names which have values associated to it
* It includes everything within `{}`
* Properties can be called the usual way

~~~~js
var sales = 'Toyota';

function carTypes(name) {
  if (name === 'Honda') {
    return name;
  } else {
    return "Sorry, we don't sell " + name + ".";
  }
}

var car = { myCar: 'Saturn', getCar: carTypes('Honda'), special: sales };

console.log(car.myCar);   // Saturn
console.log(car.getCar);  // Honda
console.log(car.special); // Toyota
~~~~

####Template Strings

* ```(back-ticks)`
* Include `${(expression)}`
* The expressions in the place holders and the text between them get passed to a function

####Destructing

* Makes it possible to extract data from arrays and objects into distinct variables

~~~~js
const scores = [10, 20, 30, 40, 50];
var a, b, rest;
[a, b] = scores;
console.log(a); // 10
console.log(b); // 20

[a, b, ...rest] = scores;
console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30, 40, 50]

({a, b} = {a: 10, b: 20});
console.log(a); // 10
console.log(b); // 20
~~~~

* It reverses the syntax. The variable is declared on the left hand side and the value is on the right

~~~~js
var x = [1, 2, 3, 4, 5];
var [y, z] = x;
console.log(y); // 1
console.log(z); // 2
~~~~

####Default Parameters

* Sets the values in a function to default if not stated
* But otherwise returns the value that the user has inputted as the missing value

~~~~js
function multiply(a, b = 1) {
  return a * b;
}

multiply(5, 2); // 10
multiply(5, 1); // 5
multiply(5);    // 5
~~~~

####Rest Parameters

* If an array ends with `...` then it indicates the user wants to include the 'rest' of the parameters in that array
* The 'rest' of the values in the array are then printed when they are called

~~~~js
// Before rest parameters, the following could be found:
function f(a, b) {
  var args = Array.prototype.slice.call(arguments, f.length);

  // …
}

// to be equivalent of

function f(a, b, ...args) {
  
}
~~~~

####Spread Operator

* This includes an array within another array
* This is done by calling the first array within the second array

~~~~js
var parts = ['shoulders', 'knees']; 
var lyrics = ['head', ...parts, 'and', 'toes']; 
// ["head", "shoulders", "knees", "and", "toes"]
~~~~

####Let Statment 

* Allows the user to use a variable for that particular function/ block statement that they are currently working in.
* The `var` keyword is a global variable, where `let` is defined locally or within a function
* It can therefore be used multiple times not overwritting the previous value if the variable is in a different function

~~~~js
function varTest() {
  var x = 1;
  if (true) {
    var x = 2;  // same variable!
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function letTest() {
  let x = 1;
  if (true) {
    let x = 2;  // different variable
    console.log(x);  // 2
  }
  console.log(x);  // 1
}
~~~~

####Const Statement

* A constant value is created and can not be changed or altered in any way once it is assigned
* It can be declared either globally or locally to a function
* It must be assigned a value in the same statement as it is declared

~~~~js
// NOTE: Constants can be declared with uppercase or lowercase, but a common
// convention is to use all-uppercase letters.

// define MY_FAV as a constant and give it the value 7
const MY_FAV = 7;

// this will throw an error
MY_FAV = 20;

// will print 7
console.log('my favorite number is: ' + MY_FAV);

// trying to redeclare a constant throws an error
const MY_FAV = 20;

// the name MY_FAV is reserved for constant above, so this will also fail
var MY_FAV = 20;

// this throws an error also
let MY_FAV = 20;

// it's important to note the nature of block scoping
if (MY_FAV === 7) { 
    // this is fine and creates a block scoped MY_FAV variable 
    // (works equally well with let to declare a block scoped non const variable)
    let MY_FAV = 20;

    // MY_FAV is now 20
    console.log('my favorite number is ' + MY_FAV);

    // this gets hoisted into the global context and throws an error
    var MY_FAV = 20;
}
~~~~

####for…of Statement

* This function creates a loop iterating over objects (including Array, Map, Set, String, TypedArry)
* Similar to a `in` in objects but can include a previously mentioned object

~~~~js
let iterable = [10, 20, 30];

for (let value of iterable) {
  value += 1;
  console.log(value);
}
// 11
// 21
// 31
~~~~

~~~~js
let iterable = 'boo';

for (let value of iterable) {
  console.log(value);
}
// "b"
// "o"
// "o"
~~~~

####Generators

* Allows a function to be called within another function but only when the user wants that function to be called
* The `*` syntax is used to indicate a generator function
* The `next()` method returns the values when they are printed out

~~~~js
function* anotherGenerator(i) {
  yield i + 1;
  yield i + 2;
  yield i + 3;
}

function* generator(i) {
  yield i;
  yield* anotherGenerator(i);
  yield i + 10;
}

var gen = generator(10);

console.log(gen.next().value); // 10
console.log(gen.next().value); // 11
console.log(gen.next().value); // 12
console.log(gen.next().value); // 13
console.log(gen.next().value); // 20
~~~~ 

####Unicode

* Differentiates the difference between the different languages that are available to use within programming
* A small mistake can mean using a different langague so a set of numbers and defined characters are used to distinguish the different languages

####Modules

* When a file can be imported to a different file
* When functions, objects or pimitives from a file can be exported to a different location

~~~~js
import * as myModule from 'my-module';
~~~~

~~~~js
export { myFunction }; // exports a function declared earlier
export const foo = Math.sqrt(2); // exports a constant
~~~~

####Module Loaders

* The user can construct new code to be loaded and load code in isolatedor constrained contexts
* Different type of module loaders support:
	+ Dynamic Loading
	+ State isolation
	+ Global namespace isolation
	+ Compilation hooks
	+ Nested virtualisation

~~~~js
// Dynamic loading – ‘System’ is default loader
System.import('lib/math').then(function(m) {
  alert("2π = " + m.sum(m.pi, m.pi));
});

// Create execution sandboxes – new Loaders
var loader = new Loader({
  global: fixup(window) // replace ‘console.log’
});
loader.eval("console.log('hello world!');");

// Directly manipulate module cache
System.get('jquery');
System.set('jquery', Module({$: $})); // WARNING: not yet finalized
~~~~

####Map + Set + Weakmap + Weakset

* Map
 + any value(both objects and primitive values) may be used as either key or value
 + returns an array of [key, value] for each iteration
 + a maps insertion order is random
* Set
 + lets the user store unique values of any type of object. This may be a primitive value or an object reference
 + are collection of values
* Weakmap
 + is a collection of key and value pairs in which the keys are weakly referenceed. 
 + The keys must be objects only
 + Primitive data types are not allowed
* Weakset
 + lets the user store weakly held objects in a collection
 + they are a collection of objects
 + it is unique
 + they are not arbitrary values unlike sets

####Symboles

* Every symbol value returned from `Symbol()` is unique
* The data that is passed through the Symbol feature is only used as an identifier for object properties and nothing else

####Subclassable Built-ins

* `Array`, `Date` and `DOM Elements` can be subclassed
* Object contrstruction for a function named `Ctor` now uses two-phases:
 + Call `Ctor[@@create]` to allocate the object, installing any special behaviour
 + Invoke constructor on new instances to initiase
* The known `@@create` symbol is available via `Symbol.create`

~~~~js
// Pseudo-code of Array
class Array {
    constructor(...args) { /* ... */ }
    static [Symbol.create]() {
        // Install special [[DefineOwnProperty]]
        // to magically update 'length'
    }
}

// User code of Array subclass
class MyArray extends Array {
    constructor(...args) { super(...args); }
}

// Two-phase 'new':
// 1) Call @@create to allocate object
// 2) Invoke constructor on new instance
var arr = new MyArray();
arr[1] = 12;
arr.length == 2
~~~~

####Promises

* A promise represents a value which may be available now, in the future, or never
* A promise allows the user to associate handlers with an asynchronous actions eventual success value or failure reason
* It then allows the asynchronous method to return values that are associated with synchronous methods
* A promise can have one of three states:
 + pending: initial state, not fulfilled or rejected
 + fulfilled: meaning that the operation completed successfully
 + rejected: meaning that the operation failed

####Math + Number + String + Array + Object APIs

* New library that are included within ES6 including core Math, Array conversion helpers, String helpers and Object.assign

####Binary and Octal Literals

* Binary
 + The user uses an upper or lowercase b after a 0 to indicate they want to use binary syntax
 
~~~~js
var FLT_SIGNBIT  = 0b10000000000000000000000000000000; // 2147483648
var FLT_EXPONENT = 0b01111111100000000000000000000000; // 2139095040
var FLT_MANTISSA = 0B00000000011111111111111111111111; // 8388607
~~~~

* Octal
 + The user uses an upper or lowercase o after a 0 to indicate they want to use the octal syntax

~~~~js
var n = 0O755; // 493
var m = 0o644; // 420
~~~~

```
something here
```


####Tail Calls

* 'Remebers' what has previously been on the call stack and only repeats the process once if it is re-occuring

-
### References

1. [https://github.com/lukehoban/es6features](https://github.com/lukehoban/es6features)
2. [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)
3. [http://benignbemine.github.io/2015/07/19/es6-tail-calls/](http://benignbemine.github.io/2015/07/19/es6-tail-calls/)
4. [https://developer.mozilla.org/en-US/docs/Glossary/Unicode](https://developer.mozilla.org/en-US/docs/Glossary/Unicode)