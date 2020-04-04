
							ES5(ECMA Script 5)

TODO : Improve the structuring

							   ES 5 PART I
1) Null vs Undefined
    null is an assigned value. It means nothing.
    undefined means a variable has been declared but not defined yet.
    null is a primitive value in Javascript although typeof(null) returns object but it is a known bug of the language. 
    undefined is of type undefined.
    null !== undefined but null == undefined.

A Statement does logical thing  
If else or condition statement or loop  
A statement is chained with ; while expression with , (comma)  
A statement is such that it can be placed where a value is required
```
myVar
x+3
Bar(2,3)
statement 
>console.log("a", "b");
b
```

Object literal vs block   

`{ foo: bar(3, 5) }`  
The above line is both statement and expression   
```
function test(printTwo) { printing: { console.log("One"); if (!printTwo) break printing; console.log("Two"); } console.log("Three"); }

function () {   }   function expression 
function foo() {  } named function expression 
```

Control flow statements  
	That change the flow of program on certain conditions or  Control Flow is a fundamental concept in 
	programming that allows you to dictate how your code runs under different conditions or until a
	certain condition is met.
	```
	
	if else  
	
	switch  
	
	for  
	
	for in  
	
	nested if else   
	
	while, do while, break, &&, || 
	
	for in   (for parsing objects ) 
	
	```
	
-Code could be self explanatory. 

There are 2 types of comment  
```
a) Documentation comments 
b) Clarification comments 
```
-Don't comment obvious things.   

-Comment if you have wasted a lot of time to create a better solution and realize why the other solutions 
 won't work and it is most appropriate way to solve the particular problem otherwise other developer checking 
 the code will also try to improve that particular code without thinking of the loophole.  

Strict mode makes several changes to normal JavaScript semantics:   

a) Eliminates some JavaScript silent errors by changing them to throw errors.  

b) Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode 
   code can sometimes be made to run faster than identical code that's not strict mode.  

c) Prohibits some syntax likely to be changed in future versions of ECMAScript.  

'use strict'  in script  
'use strict'  in function  
 Modules are auto strict   

-If a global variable is updated accidentally in some file it will throw error  

-strict mode makes assignments which would otherwise silently fail to throw an exception. For example, 
NaN is a non-writable global variable. In normal code assigning to NaN does nothing; the developer
receives no failure feedback. In strict mode assigning to NaN throws an exception. 

JavaScript’s types:-
  The ECMAScript language types are:- 
	``` 
	
	Undefined,  
	Null,  
	Boolean,  
	String,  
	Number,  
	Object  
	
	```
	
Static versus dynamic
	```
	Static   - >  compile time
	Dynamic  - >   runtime 
	```

JavaScript is dynamically typed, types of variables are generally not known at compile time

Statically type-checked languages perform this kind of check at compile time, dynamically type-checked languages at runtime
JavaScript performs a very limited kind of dynamic type checking,

> var foo = null; > foo.prop TypeError: Cannot read property 'prop' of null Mostly, however, things silently fail or work. 


coersion
 JavaScript, the main way of dealing with a value whose type doesn’t fit is to coerce it to the correct type. Coercion means implicit type conversion. Most operands coerce: > '3' * '4' 12 JavaScript has internal functions for performing this kind of conversion explicitly [1]. Some of them can be accessed in the language, via the functions Boolean, Number, String, Object. > Number(true) 1 > Number('123') 123 > String(true) 'true'
typeof([1,2,3])  is object as its an ordered list of values mapped to index for JS

Object is reference type all other types mentioned above are primitives including a new element named symbol 

// Outputs: "Objects coerce to true." if ({}) { console.log("Objects coerce to true."); }

var functionTrue = Boolean(true); var functionFalse = Boolean(false); 

But the Boolean function can also be used as a constructor with the new keyword:

var constructorTrue = new Boolean(true); var constructorFalse = new Boolean(false); 

The tricky thing here is that when Booleanis used as a constructor, it doesn't return a primitive. Instead it returns an object.

// Outputs: true console.log(primitiveTrue); // Outputs: true console.log(functionTrue); // Outputs: Boolean {} console.log(constructorTrue);

// Two approaches to coercing 0 into false var byFunction = Boolean(0); var byNotNot = !!0;

// Outputs: "My false Boolean object is truthy!" if (constructorFalse) { console.log("My false Boolean object is truthy!"); } else { console.log("My false Boolean object is falsy!"); }

Use valueOf() for correct truthy false value in case of Boolean Object 

Null

Null means an empty or non-existent value. Null is assigned, and explicitly means nothing.null is also an object 
console.log(typeof test1);
// object

USE === instead of ==  triple === checks both data type and value comparison 

In JavaScript there are only six falsy values.

false

0 (zero)

“” (empty string)

null

undefined

NaN (Not A Number)

Comparing false, 0, and "" with loose equality (==) will result in equality:

false == 0
// true0 == ""
// true"" == false
// true

null and undefined are only equal to themselves:

null == null
undefined == undefined
null == undefined// true

NaN isn’t equivalent to anything (not even itself!):

NaN == null
NaN == undefined
NaN == NaN
// false

3 === '3'
// false (Number compared to String)3 == '3'
// true

Logical operators 
&& logical AND 
||    logical OR
!     logical NOT

Short circuit evaluation 

function potentiallyBuggyCodeAvailable(){

code;

debugger;

}


When the debugger is invoked, execution is paused at the debugger statement. It is like a breakpoint in the script source.
Use debugging tools in web browser developers tools 

Parameters are used to define a function. They are also called formal parameters and formal arguments. In the following example, param1 and param2 are parameters:

function foo(param1, param2) {...} 

Arguments are used to invoke a function. They are also called actual parameters and actual arguments. In the following example, 3 and 7 are arguments:

foo(3, 7);

Defining Functions

All functions are objects, instances of Function:

function id(x) { return x; } console.log(id instanceof Function); // true 

Therefore, functions get their methods from Function.prototype.

Function Expressions

A function expression produces a value—a function object. For example:

var add = function (x, y) { return x + y }; console.log(add(2, 3)); // 5

The value produced by a function expression can be assigned to a variable (as shown in the example), passed as an argument to another function, and more. Because normal function expressions don’t have a name, they are also called anonymous function expressions.

Named function expressions

You can give a function expression a name. Named function expressions allow a function expression to refer to itself, which is useful for self-recursion:

var fac = function me(n) { if (n > 0) { return n * me(n-1); } else { return 1; } }; console.log(fac(3)); // 6 

NOTE

The name of a named function expression is only accessible inside the function expression:


Function Declarations/statement 
The following is a function declaration:
function add(x, y) { return x + y; }

The Function Constructor

The constructor Function() evaluates JavaScript code stored in strings. For example, the following code is equivalent to the previous example:

var add = new Function('x', 'y', 'return x + y');


foo(); // TypeError
 bar(); // ReferenceError
 var foo = function bar() { 	// ... };

This snippet is more accurately interpreted (with hoisting) as:

var foo; foo(); // TypeError bar(); // ReferenceError foo = function() { 	var bar = ...self... 	// ... }

First JS code compiles and then function declarations and variable declarations are hoisted i.e., the declaration part is seen on the top of the scope and assignment remains at same place except function expressions.

for undefined value type error comes this the case when we try to print variable that is declared but the not initialized while in case of function expression referenced error comes 


Functions First

Both function declarations and variable declarations are hoisted. But a subtle detail (that can show up in code with multiple "duplicate" declarations) is that functions are hoisted first, and then variables.

Consider:

foo(); // 1 var foo; function foo() { 	console.log( 1 ); } foo = function() { 	console.log( 2 ); };

1 is printed instead of 2! This snippet is interpreted by the Engineas:

function foo() { 	console.log( 1 ); } foo(); // 1 foo = function() { 	console.log( 2 ); };

While multiple/duplicate vardeclarations are effectively ignored, subsequent function declarations dooverride previous ones.


foo(); // 3 function foo() { 	console.log( 1 ); } var foo = function() { 	console.log( 2 ); }; function foo() { 	console.log( 3 ); }

We can be tempted to look at var a = 2; as one statement, but the JavaScript Engine does not see it that way. It sees var a and a = 2as two separate statements, the first one a compiler-phase task, and the second one an execution-phase task.

What this leads to is that all declarations in a scope, regardless of where they appear, are processed first before the code itself is executed. You can visualize this as declarations (variables and functions) being "moved" to the top of their respective scopes, which we call "hoisting".


this keyword in JavaScript 
In functions: this is an extra, often implicit, parameter.

Outside functions (in the top-level scope): thisrefers to the global object in browsers and to a module’s exports in Node.js.

In a string passed to eval(): eval() either picks up the current value of this or sets it to the global object, depending on whether it is called directly or indirectly.


First-Class Functions vs Higher-Order Functions

What’s the difference?

First class functions are treated like objects. Higher order functions either accept a function as an argument, return a function, or both.



 real functions, the value of this depends on the mode one is in:

Sloppy mode: this refers to the global object(window in browsers). function sloppyFunc() { console.log(this === window); // true } sloppyFunc(); 

Strict mode: this has the value undefined. function strictFunc() { 'use strict'; console.log(this === undefined); // true } strictFunc();

Functions become constructors if you invoke them via the new operator. That operator creates a new object and passes it to the constructor via this: var savedThis; function Constr() { savedThis = this; } var inst = new Constr(); console.log(savedThis === inst); // true

this in methods

In methods, things are similar to more traditional object-oriented languages: this refers to the receiver, the object on which the method has been invoked. var obj = { method: function () { console.log(this === obj); // true } } obj.method();

this in the top-level scope

In browsers, the top-level scope is the global scope and this refers to the global object (like windowdoes): <script> console.log(this === window); // true </script> In Node.js, you normally execute code in modules. Therefore, the top-level scope is a special module scope: // `global` (not `window`) refers to global object: console.log(Math === global.Math); // true // `this` doesn’t refer to the global object: console.log(this !== global); // true // `this` refers to a module’s exports: console.log(this === module.exports); // true

eval() can be called either directly (via a real function call) or indirectly (via some other means). The details are explained here.

If eval() is called indirectly, this refers to the global object:

> (0,eval)('this === window') true

JS don't have block scope it's either local scope or global scope and if we don't define variable using var or let keyword it get s declared in global scope. 

For browser or for web developer per se the global scope is windows object and( global object for nodejs). 

setTimeout Variables are Executed in the Global Scope, this keyword used in setTimeout refers to the global object not to var object it is declared in

Scope and closures
JavaScript falls under the general category of "dynamic" or "interpreted" languages, it is in fact a compiled language. It is notcompiled well in advance, as are many traditionally-compiled languages, nor are the results of compilation portable among various distributed systems.


Let's meet the cast of characters that interact to process the program var a = 2;, so we understand their conversations that we'll listen in on shortly:

Engine: responsible for start-to-finish compilation and execution of our JavaScript program.

Compiler: one of Engine's friends; handles all the dirty work of parsing and code-generation (see previous section).

Scope: another friend of Engine; collects and maintains a look-up list of all the declared identifiers (variables), and enforces a strict set of rules as to how these are accessible to currently executing code.

var a = 2;.

The first thing Compiler will do with this program is perform lexing to break it down into tokens, which it will then parse into a tree. 

To summarize: two distinct actions are taken for a variable assignment: First, Compiler declares a variable (if not previously declared in the current scope), and second, when executing, Engine looks up the variable in Scopeand assigns to it, if found

LHS and RHS lookup 
When I say:

console.log( a );

The reference to a is an RHS reference, because nothing is being assigned to a here. Instead, we're looking-up to retrieve the value of a, so that the value can be passed to console.log(..).

By contrast:

a = 2;

The reference to a here is an LHS reference, because we don't actually care what the current value is, we simply want to find the variable as a target for the = 2 assignment operation.



Engine scope and compiler
function foo(a) { 	console.log( a ); // 2 } foo( 2 );

Let's imagine the above exchange (which processes this code snippet) as a conversation. The conversation would go a little something like this:

Engine: Hey Scope, I have an RHS reference for foo. Ever heard of it?

Scope: Why yes, I have. Compiler declared it just a second ago. He's a function. Here you go.

Engine: Great, thanks! OK, I'm executing foo.

Engine: Hey, Scope, I've got an LHS reference for a, ever heard of it?

Scope: Why yes, I have. Compiler declared it as a formal parameter to foo just recently. Here you go.

Engine: Helpful as always, Scope. Thanks again. Now, time to assign 2 to a.

Engine: Hey, Scope, sorry to bother you again. I need an RHS look-up for console. Ever heard of it?

Scope: No problem, Engine, this is what I do all day. Yes, I've got console. He's built-in. Here ya go.

Engine: Perfect. Looking up log(..). OK, great, it's a function.

Engine: Yo, Scope. Can you help me out with an RHS reference to a. I think I remember it, but just want to double-check.

Scope: You're right, Engine. Same guy, hasn't changed. Here ya go.

Engine: Cool. Passing the value of a, which is 2, into log(..).


If an RHS look-up fails to ever find a variable, anywhere in the nested Scopes, this results in a ReferenceError being thrown by the Engine. It's important to note that the error is of the type ReferenceError.

By contrast, if the Engine is performing an LHS look-up and arrives at the top floor (global Scope) without finding it, and if the program is not running in "Strict Mode" [^note-strictmode], then the global Scopewill create a new variable of that name in the global scope, and hand it back to Engine.

"No, there wasn't one before, but I was helpful and created one for you."

"Strict Mode" [^note-strictmode], which was added in ES5, has a number of different behaviors from normal/relaxed/lazy mode. One such behavior is that it disallows the automatic/implicit global variable creation. In that case, there would be no global Scope'd variable to hand back from an LHS look-up, and Engine would throw a ReferenceError similarly to the RHS case.

Now, if a variable is found for an RHS look-up, but you try to do something with its value that is impossible, such as trying to execute-as-function a non-function value, or reference a property on a null or undefined value, then Engine throws a different kind of error, called a TypeError.

ReferenceError is Scoperesolution-failure related, whereas TypeError implies that Scoperesolution was successful, but that there was an illegal/impossible action attempted against the result

Lexical scope is used in JS
eval is used to cheat the lexical scope that states that first innermost scope will check and so on lastly the global scope 
And shadowing can also be done that is naming the same variable in different scopes 
function foo(str, a) { 	eval( str ); // cheating! 	console.log( a, b ); } var b = 2; foo( "var b = 3;", 1 ); // 1 3

function foo(str) { "use strict"; eval( str ); console.log( a ); // ReferenceError: a is not defined } foo( "var a = 2"

with (keyword ) is other way of cheating lexical scope 
function foo(obj) { 	with (obj) { 		a = 2; 	} } var o1 = { 	a: 3 }; var o2 = { 	b: 3 }; foo( o1 ); console.log( o1.a ); // 2 foo( o2 ); console.log( o2.a ); // undefined console.log( a ); // 2 -- Oops, 
Lexical scope means that scope is defined by author-time decisions of where functions are declared


JS compiler does
1) Lexing
2) parsing ( taking token and creating AST Abstract Syntax Tree) 
3) Code-Generation: the process of taking an AST and turning it into executable code. 


function sayHello() { console.log("hello");};var func = sayHello;

You are assigning the variable func a reference to the function sayHello, nota copy. Here, func is simply an alias to sayHello. Anything you do on the alias you will actually be doing on the original function. For example:

func.answer = 42;console.log(sayHello.answer); // prints 42

Scopes have a lifetime

When you call a function, you create a scope during the execution of that function. Then that scope goes away.

When you call the function a second time, you create a new different scope during the second execution. Then this second scope goes away as well.

function printA() { console.log(answer); var answer = 1;};printA(); // this creates a scope which gets discarded right afterprintA(); // this creates a new different scope which also gets discarded right after;

Closures span multiple scopes

When you define a function, a closure gets created

Unlike scopes, closures are created when you define a function, not when you execute it. Closures also don’t go away after you execute that function.

You can access the data in a closure long after a function is defined and after it gets executed as well.

A closures encompasses everything the defined function can access. This means the defined function’s scope, and all the nested scopes between the global scope and the defined function scope plus the global scope itself.

var G = 'G';// Define a function and create a closurefunction functionA() { var A = 'A' // Define a function and create a closure function functionB() { var B = 'B' console.log(A, B, G); } functionB(); // prints A, B, G // functionB closure does not get discarded A = 42; functionB(); // prints 42, B, G}functionA();

But the relation between scopes and closures is not always simple like this. Things become different when the defining and invoking of functions happen in different scopes. Let me explain that with an example:

var v = 1;var f1 = function () { console.log(v);}var f2 = function() { var v = 2; f1(); // Will this print 1 or 2?};f2();






							ES5 Part II



But the relation between scopes and closures is not always simple like this. Things become different when the defining and invoking of functions happen in different scopes. Let me explain that with an example:

var v = 1;var f1 = function () { console.log(v);}var f2 = function() { var v = 2; f1(); // Will this print 1 or 2?};f2();

What do you think the above example will print? The code is simple, f1()prints the value of v, which is 1 on the global scope, but we execute f1()inside of f2(), which has a different vthat’s equal to 2. Then we execute f2().

Will this code print 1 or 2?

If you’re tempted to say 2, you’ll be surprised. This code will actually print 1. The reason is, scopes and closures are different. The console.log line will use the closure of f1(), which is created when we define f1(), which means the closure of f1() gives us access to only the scope of f1() plus the global scope. The scope where we execute f1() does not affect that closure. In fact, the closure of f1() will not give us access to the scope of f2() at all. If you remove the global v variable and execute this code, you’ll get a reference error:

var f1 = function () { console.log(v);}var f2 = function() { var v = 2; f1(); // ReferenceError: v is not defined};f2();

Since closures give us references to variables in scopes, the access that they give us means both read and write, not just read.

// ReferenceError: funcName is not defined funcName(); // TypeError: undefined is not a function varName(); var varName = function funcName() { console.log("Definition not hoisted!"); }; 

As you can see, the function's name doesn't get hoisted if it is part of a function expression.

A Tricky problem in JS 
// interviewer: what will the following code output?const arr = [10, 12, 15, 21];for (var i = 0; i < arr.length; i++) { setTimeout(function() { console.log('Index: ' + i + ', element: ' + arr[i]); }, 3000);}

This question deals with the topics: closures, setTimeout, and scoping. The correct answer to this is question is:

Index: 4, element: undefined(printed 4 times).

setTimeout(function() {//code}, 1000) 
setInterval
clearInterval(timeoutId) ;


JavaScript is designed on a simple object-based paradigm. An object is a collection of properties, and a property is an association between a name (or key) and a value. A property's value can be a function, in which case the property is known as a method

Unassigned properties of an object are undefined (and not null).
However, any property name that is not a valid JavaScript identifier (for example, a property name that has a space or a hyphen, or that starts with a number) can only be accessed using the square bracket notation. 

JavaScript object property names (keys) can only be strings or Symbols You can also access properties by using a string value that is stored in a variable:

var propertyName = 'make';
myCar[propertyName] = 'Ford';

Starting with ECMAScript 5, there are three native ways to list/traverse object properties:
for...in loop
Object.keys(o) 
Object.getOwnPropertyNames(o)

To create new variable 
1) use object initializers
		{s:2,p:3} 
2) Using constructor
			function Car(make, model, year) {
				this.make = make;
				this.model = model; 
				this.year = year; 
			}
var mycar = new Car('Eagle', 'Talon TSi', 1993);

JavaScript is a prototype-based language, meaning object properties and methods can be shared through generalized objects that have the ability to be cloned and extended. This is known as prototypical inheritance and differs from class inheritance. 

let x = new Object().

The double square brackets that enclose [[Prototype]] signify that it is an internal property, and cannot be accessed directly in code.

To find the [[Prototype]] of this newly created object, we will use the getPrototypeOf() method.

Object.getPrototypeOf(x);
JavaScript has a [[Prototype]] as it creates a way for any two or more objects to be linked.

When you attempt to access a property or method of an object, JavaScript will first search on the object itself, and if it is not found, it will search the object's [[Prototype]]. If after consulting both the object and its [[Prototype]] still no match is found, JavaScript will check the prototype of the linked object, and continue searching until the end of the prototype chain is reached.

When you attempt to access a property or method of an object, JavaScript will first search on the object itself, and if it is not found, it will search the object's [[Prototype]]. If after consulting both the object and its [[Prototype]] still no match is found, JavaScript will check the prototype of the linked object, and continue searching until the end of the prototype chain is reached.


Introduction

JavaScript is a prototype-based language, meaning object properties and methods can be shared through generalized objects that have the ability to be cloned and extended. This is known as prototypical inheritance and differs from class inheritance. Among popular object-oriented programming languages, JavaScript is relatively unique, as other prominent languages such as PHP, Python, and Java are class-based languages, which instead define classes as blueprints for objects.

In this tutorial, we will learn what object prototypes are and how to use the constructor function to extend prototypes into new objects. We will also learn about inheritance and the prototype chain.

JavaScript Prototypes

In Understanding Objects in JavaScript, we went over the object data type, how to create an object, and how to access and modify object properties. Now we will learn how prototypes can be used to extend objects.

Every object in JavaScript has an internal property called [[Prototype]]. We can demonstrate this by creating a new, empty object.

let x = {}; 

This is the way we would normally create an object, but note that another way to accomplish this is with the object constructor: let x = new Object().

The double square brackets that enclose [[Prototype]] signify that it is an internal property, and cannot be accessed directly in code.

To find the [[Prototype]] of this newly created object, we will use the getPrototypeOf() method.

Object.getPrototypeOf(x); 

The output will consist of several built-in properties and methods.

Output

{constructor: ƒ, _defineGetter: ƒ, __defineSetter_: ƒ, …} 

Another way to find the [[Prototype]]is through the _proto_ property. _proto_ is a property that exposes the internal [[Prototype]] of an object.

It is important to note that ._proto_is a legacy feature and should not be used in production code, and it is not present in every modern browser. However, we can use it throughout this article for demonstrative purposes.

x._proto_; 

The output will be the same as if you had used getPrototypeOf().

Output

{constructor: ƒ, _defineGetter: ƒ, __defineSetter_: ƒ, …} 

It is important that every object in JavaScript has a [[Prototype]] as it creates a way for any two or more objects to be linked.

Objects that you create have a [[Prototype]], as do built-in objects, such as Date and Array. A reference can be made to this internal property from one object to another via the prototypeproperty, as we will see later in this tutorial.

Prototype Inheritance

When you attempt to access a property or method of an object, JavaScript will first search on the object itself, and if it is not found, it will search the object's [[Prototype]]. If after consulting both the object and its [[Prototype]] still no match is found, JavaScript will check the prototype of the linked object, and continue searching until the end of the prototype chain is reached.

At the end of the prototype chain is Object.prototype. All objects inherit the properties and methods of Object. Any attempt to search beyond the end of the chain results in null.

In our example, x is an empty object that inherits from Object. x can use any property or method that Object has, such as toString().

x.toString(); 

Output

[object Object] 

This prototype chain is only one link long. x -> Object. We know this, because if we try to chain two [[Prototype]]properties together, it will be null.

x._proto.proto_; 

Output

null 

Let's look at another type of object. If you have experience Working with Arrays in JavaScript, you know they have many built-in methods, such as pop() and push(). The reason you have access to these methods when you create a new array is because any array you create has access to the properties and methods on the Array.prototype.

We can test this by creating a new array.

let y = []; 

Keep in mind that we could also write it as an array constructor, let y = new Array().

If we take a look at the [[Prototype]] of the new y array, we will see that it has more properties and methods than the xobject. It has inherited everything from Array.prototype.

y._proto_; [constructor: ƒ, concat: ƒ, pop: ƒ, push: ƒ, …]
This is the reason we can push and pop from the array 

y._proto_ === Array.prototype; // true y._proto.proto_ === Object.prototype; // true 

We can also use the isPrototypeOf()method to accomplish this.

Array.prototype.isPrototypeOf(y); // true Object.prototype.isPrototypeOf(Array); // true

We can use the instanceof operator to test whether the prototype property of a constructor appears anywhere within an object's prototype chain.

y instanceof Array; // true

To summarize, all JavaScript objects have a hidden, internal [[Prototype]]property (which may be exposed through _proto_ in some browsers). Objects can be extended and will inherit the properties and methods on [[Prototype]] of their constructor.

These prototypes can be chained, and each additional object will inherit everything throughout the chain. The chain ends with the Object.prototype.

We have seen some built-in JavaScript constructors, such as new Array() and new Date(), but we can also create our own custom templates from which to build new objects.

// Add greet method to the Hero prototype Hero.prototype.greet = function () { return `${this.name} says hello.`; }

function Point(x, y) { this.x = x; this.y = y; } Point.prototype = { dist: function () { return Math.sqrt((this.x*this.x)+(this.y*this.y)); }, toString: function () { return "("+this.x+", "+this.y+")"; } } We assign an object to Point.prototype, via an object initializer with two properties dist and toString. Now there is a clear separation of responsibility: The constructor is responsible for setting up instance-specific data, the prototype contains shared data (i.e., the methods). Note that prototypes are highly optimized in JavaScript engines, so there is usually no performance penalty for putting methods there. Methods are called just like before, you don’t notice whether they are stored in the instance or in the prototype

To fix extend(), we must ensure that only own properties of source are considered. function extend(target, source) { for (var propName in source) { // Is propName an own property of source? if (source.hasOwnProperty(propName)) { // (1) target[propName] = source[propName]; } } return target; } There is one more problem: The above code fails if source has an own property whose name is “hasOwnProperty” [3]:

var proto = { bla: true }; var obj = Object.create(proto); obj.foo = 123; obj.bar = "abc"; obj has both inherited and own properties: > obj.bla true > obj.foo 123

var obj = Object.create(proto, { foo: { value: 123 }, bar: { value: "abc" } });

Object.keys()
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.keys(object1));
// expected output: Array ["a", "b", "c"]

 language = {
  set current(name) {
    this.log.push(name);
  },
  log: []
}

language.current = 'EN';
language.current = 'FA';

console.log(language.log);
// expected output: Array ["EN", "FA"]

var obj = {
  log: ['a', 'b', 'c'],
  get latest() {
    if (this.log.length == 0) {
      return undefined;
    }
    return this.log[this.log.length - 1];
  }
}

console.log(obj.latest);
// expected output: "c"


if (somethingBadHappened) { throw new Error('Something bad happened'); }

Any value can be thrown:

function throwIt(exception) { try { throw exception; } catch (e) { console.log('Caught: '+e); } }

Array 
Array in JS are non homogeneous and non contiguous and the memory allocation is not together 
var array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]

const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15

var words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);
console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]

var array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});

// expected output: "a"
// expected output: "b"
// expected output: "c"

var array1 = ['a', 'b', 'c'];

Mutating
array.push() and array.ushift().
array.pop() removes an item at the end of the array
array.shift() removes an item at the beginningof the array.

let mutatingRemove = ['a', 'b', 'c', 'd', 'e']; mutatingRemove.splice(0,2 ); // ['c', 'd', 'e'] 
array.splice() 


Non-Mutating 
 array.concat()
... Spread operator 
// use const const arr1 = ['a', 'b', 'c', 'd', 'e']; const arr2 = arr1.filter(a => a !== 'e'); // ['a', 'b', 'c', 'd'] // OR const arr2 = arr1.filter(a => { return a !== 'e'; }); // ['a', 'b', 'c', 'd'] 


array.slice() takes two parameters.

The first parameter is the index where the copy should begin.

The second parameter is the index where the copy should end. This end index is non-inclusive.
array.map

To create a regular expression 
1)var re = /ab+c/;  //using enclosing slashes 
2) var re = new RegExp('ab+c'); //using RegExp constructor 

match a single 'a' followed by zero or more 'b's followed by 'c', you'd use the pattern /ab*c


Date Object
let now = new Date(); // will display method call time date and time

var today = new Date();
var birthday = new Date('December 17, 1995 03:24:00');
var birthday = new Date('1995-12-17T03:24:00');
var birthday = new Date(1995, 11, 17);
var birthday = new Date(1995, 11, 17, 3, 24, 0);

var date1 = new Date('December 17, 1995 03:24:00');
// Sun Dec 17 1995 03:24:00 GMT...

var date2 = new Date('1995-12-17T03:24:00');
// Sun Dec 17 1995 03:24:00 GMT...

console.log(date1 === date2);
// expected output: false;

console.log(date1 - date2);
// expected output 0

JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate. It is based on a subset of the JavaScript Programming Language, Standard ECMA-262 3rd Edition - December 1999. JSON is a text format that is completely language independent but uses conventions that are familiar to programmers of the C-family of languages, including C, C++, C#, Java, JavaScript, Perl, Python, and many others. These properties make JSON an ideal data-interchange language.

JSON is built on two structures:

A collection of name/value pairs. In various languages, this is realized as an object, record, struct, dictionary, hash table, keyed list, or associative array.
An ordered list of values. In most languages, this is realized as an array, vector, list, or sequence.


Working with JSON

parse

stringify

difference between objects and JSON


-Sharing global variables between unrelated code is a big no-no in development.

Modules are reusablw chunk of code in ES5 that we can reuse in any project and in the same project the dependency of one module should be
very less on other modules.

we can use closure based way of creating and using functions to avoid global namespacing pollution using 

var myGradesCalculate = (function () {
    
  // Keep this variable private inside this closure scope
  var myGrades = [93, 95, 88, 0, 55, 91];
  
  var average = function() {
    var total = myGrades.reduce(function(accumulator, item) {
      return accumulator + item;
      }, 0);
      
    return'Your average grade is ' + total / myGrades.length + '.';
  };

  var failing = function() {
    var failingGrades = myGrades.filter(function(item) {
        return item < 70;
      });

    return 'You failed ' + failingGrades.length + ' times.';
  };

  // Explicitly reveal public pointers to the private functions 
  // that we want to reveal publicly

  return {
    average: average,
    failing: failing
  }
})();

myGradesCalculate.failing(); // 'You failed 2 times.' 
myGradesCalculate.average(); // 'Your average grade is 70.33333333333333.'

or ew can also use commonJS that works like NodeJs modeule approach.

commonJS code
function myModule() {
  this.hello = function() {
    return 'hello!';
  }

  this.goodbye = function() {
    return 'goodbye!';
  }
}

module.exports = myModule;

There are two obvious benefits to this approach over the module patterns we discussed before:

1. Avoiding global namespace pollution
2. Making our dependencies explicit

AMD
CommonJS is all well and good, but what if we want to load modules asynchronously? The answer is called Asynchronous Module Definition, or AMD for short.

Loading modules using AMD looks something like this:

define(['myModule', 'myOtherModule'], function(myModule, myOtherModule) {
  console.log(myModule.hello());
});

Creating and using code using ES6 Modules

// lib/counter.js

var counter = 1;

function increment() {
  counter++;
}

function decrement() {
  counter--;
}

module.exports = {
  counter: counter,
  increment: increment,
  decrement: decrement
};


// src/main.js

var counter = require('../../lib/counter');

counter.increment();
console.log(counter.counter); // 1


Module bundling

What is module bundling?
On a high level, module bundling is simply the process of stitching together a group of modules (and their dependencies) into a single file (or group of files) in the correct order.

As with all aspects of web development, the devil is in the details. :)

Why bundle modules at all?
When you divide your program into modules, you typically organize those modules into different files and folders. Chances are, you’ll also have a group of modules for the libraries you’re using, like Underscore or React.

As a result, each of those files has to be included in your main HTML file in a <script> tag, which is then loaded by the browser when a user visits your home page. Having separate &lt;script> tags for each file means that the browser has to load each file individually: one… by… one.

…Which is bad news for page load time.

To get around this problem, we bundle, or “concatenate” all our files into one big file (or a couple files as the case may be) in order to reduce the number of requests. When you hear developers talking about the “build step” or “build process,” this is what they’re talking about.


Task runners like Gulp and Grunt make concatenation and minification straightforward for developers, ensuring that human-readable code stays exposed for developers while machine-optimized code gets bundled for browsers.

What are the different ways to bundle modules?
Concatenating and minifying your files works great when you’re using one of the standard module patterns (discussed in the previous post) to define your modules. All you’re really doing is mashing together a bunch of plain vanilla JavaScript code.

However, if you’re adhering to non-native module systems that browsers can’t interpret like CommonJS or AMD (or even native ES6 module formats), you’ll need to use a specialized tool to convert your modules into properly-ordered browser-friendly code. That’s where Browserify, RequireJS, Webpack, and other “module bundlers” or “module loaders” come into play.

In addition to bundling and/or loading your modules, module bundlers offer a ton of additional features like auto-recompiling code when you make a change or producing source maps for debugging.

Here are a couple of the options for building/converting ES6 modules to work in the browser, with #1 being the most common approach today:

Use a transpiler (e.g. Babel or Traceur) to transpile your ES6 code to ES5 code in either CommonJS, AMD, or UMD format. Then pipe the transpiled code through a module bundler like Browserify or Webpack to create one or more bundled files.

Deep Copy and shallow copy
1) when we initialize one object variable with another we just pass the reference.
2) every object in JS has Object class in it's prototype chain.
3) On using a for in loop to individually copy all the elements 
	objCopy object has a new Object.prototype method different from the mainObj object prototype method, which is not what we want. We 		want an exact copy of the original object.


https://scotch.io/bar-talk/copying-objects-in-javascript


instanceof, typeof, new


Pure, total and partial functions

Pure Functions
They also makes maintaining and refactoring code much easier. You can change a pure function and not have to worry about unintended side effects messing up the entire application and ending up in debugging hell.

When used correctly the use of pure functions produces better quality code. It’s a cleaner way of working with lots of benefits.


			
