# JS cheat sheet

Simple Javascript cheat sheet. 

# Table of content

- [JS cheat sheet](#js-cheat-sheet)
- [Table of content](#table-of-content)
- [References](#references)
- [JS basic](#js-basic)
    - [Types and operators](#types-and-operators)
        - [Objects type](#objects-type)
        - [Primitive types](#primitive-types)
        - [Operator precedence and associativity](#operator-precedence-and-associativity)
        - [JS coercion](#js-coercion)
    - [JS execution context](#js-execution-context)
        - [Global objects](#global-objects)
        - [Creation and hoisting](#creation-and-hoisting)
        - [Execution stack](#execution-stack)
        - [The scope chain](#the-scope-chain)
        - [let, var scope](#let-var-scope)
        - [Events queue](#events-queue)
    - [Objects and functions](#objects-and-functions)
        - [Functions are objects](#functions-are-objects)
        - [Functions statements / expressions](#functions-statements--expressions)
        - [By value / by reference](#by-value--by-reference)
        - [Objects and 'this' keyword](#objects-and-this-keyword)
        - [Immediately invoked function expression](#immediately-invoked-function-expression)
        - [Closure !!!](#closure)
        - [call(), apply(), bind()](#call-apply-bind)
    - [Building objects](#building-objects)
        - [Functions constructor](#functions-constructor)
        - [Prototype](#prototype)
- [Node JS](#node-js)

# References
[JavaScript - The Right Way](http://jstherightway.org/)

# JS basic

## Types and operators
[JavaScript data types and data structures | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

### Objects type
- Object

### Primitive types
There are six primitive type in JavaScript
- Undefined
- Null
- Boolean (true/false)
- Number (floating point number)
- String
- Symbol (new in ECMAScript 6)

### Operator precedence and associativity
[Operator precedence  | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

### JS coercion

```javascript
var a = 3 + '4'
console.log(a) // 34
```

## JS execution context

### Global objects

```javascript
console.log(this)
// Window file:///home/pankracy/Desktop/test_js/index.html
console.log(window)
// Window file:///home/pankracy/Desktop/test_js/index.html
window === this
// true
```

### Creation and hoisting

- Creation phase sets up memory space for variables and functions (hoisting).
- All variable are set to undefined in creation phase.

```javascript
b();
console.log(a);

var a = 'Hello World!';

function b() {
    console.log('Called b!');
}
```
```
"Called b!"
undefined
```

### Execution stack

When new function is invocated, create new execution context.

```javascript
function b() {
    var myVar;
    console.log(myVar);
}

function a() {
    var myVar = 2;
    console.log(myVar);
    b();
}

var myVar = 1;
console.log(myVar);
a();
console.log(myVar);
```

```
1
2
undefined
1
```

### The scope chain

Reference to lexical environments.

- reference to **global** execution context
```javascript
function b() {
    console.log(myVar);
}

function a() {
    var myVar = 2;
    b();
}

var myVar = 1;
a();
```

```
1
```

- reference to **a function** execution context
```javascript
function a() {
    var myVar = 2
    
    function b() {
        console.log(myVar);
    }
    
	b();
}

var myVar = 1;
a();
```

```
2
```
- reference to **global** (can't find myVar in **a function** execution context and look for it in **global** execution context)

```javascript
function a() {
    //var myVar = 2
    
    function b() {
        console.log(myVar);
    }
    
	b();
}

var myVar = 1;
a();
```

```
1
```

### let, var scope
[let - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)

```javascript
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
```

### Events queue

JavaScript engine is single threaded, but in browser are other part e.g. events queue. Js look on events queue when execution stack is empty.

```javascript
// long running function
function waitFourSeconds() {
    var ms = 4000 + new Date().getTime();
    while (new Date() < ms){}
    console.log('finished function');
}

function clickHandler() {
    console.log('click event!');   
}

// listen for the click event
document.addEventListener('click', clickHandler);


waitFourSeconds();
console.log('finished execution');
```

## Objects and functions

### Functions are objects
First class function, function can be anonymous. Function have two base property name and code which is invocable ().

```javascript
function sayHi() {
    console.log('Hi !')
}

sayHi.language = 'english'
console.log(sayHi)  // function sayHi() { ... }
console.log(sayHi.language) // "english"
```

```javascript
var a = function(){}
console.log(a.__proto__)  //function () {}
console.log(a.__proto__.__proto__)  // [object Object] { ... }
console.log([].__proto__.__proto__)  // [object Object] { ... }
```
Everything is objects or primitive

### Functions statements / expressions
Function statements don't value.
Function expression ends up creating value.

**Function expression isn't hoisting!**


```javascript
sayHi();  // "error"

var sayHi = function() {
    console.log('hi');   
}
```

### By value / by reference

```javascript
// by value
var a = 3;
var b;

b = a;
a = 2;

console.log(a); // 2
console.log(b); // 3

// by reference (all objects (including functions))
var c = { greeting: 'hi' };
var d;

d = c;
c.greeting = 'hello'; // mutate

console.log(c); // [object Object] {greeting: "hello"}
console.log(d); // [object Object] {greeting: "hello"}

// by reference (even as parameters)
function changeGreeting(obj) {
    obj.greeting = 'Hola'; // mutate   
}

changeGreeting(d);
console.log(c); // [object Object] {greeting: "hello"}
console.log(d); // [object Object] {greeting: "hello"}

// equals operator sets up new memory space (new address)
c = { greeting: 'howdy' };
console.log(c); // [object Object] {greeting: "howdy"}
console.log(d); // [object Object] {greeting: "hello"}

```
**Objects are sets by reference!!!**

### Objects and 'this' keyword

```javascript
function a() {
    console.log(this);
    this.newvariable = 'hello';
}

var b = function() {
    console.log(this);   
}

a();

console.log(newvariable); // not good!

b();

var c = {
    name: 'The c object',
    log: function() {
        var self = this;
        
        self.name = 'Updated c object';
        console.log(self);
        
        var setname = function(newname) {
            self.name = newname;   
        }
        setname('Updated again! The c object');
        console.log(self);
    }
}

c.log();
```

### Immediately invoked function expression
Execution code in the fly
```javascript
var test = 'Ooops 2 xD !';

(function() {
    var test = 'Opps !'
    console.log('Hi !')  // "Hi !"
}()); // IIFE

console.log(test) // "Ooops 2 xD !"
```

### Closure !!!

```javascript
function greet(whattosay) {

   return function(name) {
       console.log(whattosay + ' ' + name);
   }

}

var sayHi = greet('Hi');
sayHi('Tony'); // "Hi Tony"

```

```javascript
function buildFunctions() {
 
    var arr = [];
    
    for (var i = 0; i < 3; i++) {
        
        arr.push(
            function() {
                console.log(i);   
            }
        )    
    }
    return arr;
}

var fs = buildFunctions();

fs[0]();  // "1"
fs[1]();  // "1"
fs[2]();  // "1"

function buildFunctions2() {
 
    var arr = [];
    
    for (var i = 0; i < 3; i++) {
        arr.push(
            (function(j) {
                return function() {
                    console.log(j);   
                }
            }(i))
        )
    }
    return arr;
}

var fs2 = buildFunctions2();

fs2[0]();  // "0"
fs2[1]();  // "1"
fs2[2]();  // "2"
```

### call(), apply(), bind()
What 'this' keyword point :)

## Building objects

### Functions constructor

Function constructor: function unset to create new object with using new operator to make it.

```javascript
function Test() {
  console.log(this)  
  this.Test = 'a'
  console.log('invoked')  
}

var a = new Test()
console.log(a)

// [object Object] { ... }
// "invoked"
// [object Object] {Test: "a"}
```

### Prototype 

```javascript
function Test() {
  console.log(this);
  this.test = 'a';
  console.log('invoked');
}

test.prototype.getHi = function(){
  return 'Hi'
}

var a_test = new Test();
console.log(a_test.getHi());

```

# Node JS
