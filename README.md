## **Execution Context / Global Execution Context:**

&nbsp;

### **Everything in JS happens inside an Execution Context**

&nbsp;

1. Memory part (variable envrionment) => all the variables and functions are stored as **key:value** pairs inside memory component also called as **local memory**
2. Code execution part (thread of execution) => JS executes one line at a time from top to bottom & it executes in an order, thus called synchronous

&nbsp;

Note: JS is a **synchronous single threaded** language

&nbsp;

In the creation/initial stage of execution context, i.e, in memory component, all the variables are defined with a special value called **undefined** and all the functions (**not arrow functions**) store the entire function code in it. The **undefined** value will be replaced during the code execution phase.

&nbsp;

### **Note:**

**function foo() {}** : This will store the entire function in memory during creation phase

The following 2 functions are considered as variable and will be defined **undefined in the memory** during the creation phase

**var foo = () => {}**

**var foo = function () {}**

&nbsp;

Whenever a function is invoked, a brand **new Execution Context** is created inside the code component. Again it will have memory & code components

&nbsp;

Once the function is executed, that newly created Execution Context will be **deleted**.

&nbsp;

Once the program is executed, the whole **Global Execution Context** will be **deleted**.

&nbsp;

## **How does JS engine manages all this?**

How does creation, deletion and execution of Execution Context is managed?

## **Call Stack**

&nbsp;

Call Stack maintains the **order of execution of Execution Contexts**

&nbsp;

It's a stack with its first element as Global Execution Context (**GEC**)

Other execution contexts will be pushed & popped in different stages.

In the end, when the whole program is executed GEC will also be popped out of the stack

&nbsp;

## **Hoisting in JS:**

In the creation/initial stage of execution context, i.e, in memory component, all the variables are defined with a special value called **undefined** and all the functions (**not arrow functions**) store the entire function code in it. The **undefined** value will be replaced during the code execution phase.

&nbsp;

Thus even if the variables are called before defining, JS will not throw any error but returns **undefined** for the variables and executes the function.

Eg:

console.log(a);

var a = 10;

Console O/P: undefined

&nbsp;

If the variable itself is not defined anywhere in the program but called, then it will return **error as not defined**

&nbsp;

Any variable which is not inside a function is stored in **global space**

&nbsp;

Whenever a Global Execution Context (GEC) is created, a **Global Object** (also known as **window**) is also created

Whenever an Execution Context is created, **this** is created

&nbsp;

### **Note**: at global level, **this === window**

&nbsp;

### JS is a **loosely/weakly typed language**

That means, if I define "a" => var a;

Later I could define it as a number / string / bool / any data type

Eg:

var a;

a=10

a="Hi"

a=True

&nbsp;

## **What is a Scope?**

Where you **can access the specific variable or a function** in a code is called scope

&nbsp;

Scope is directly dependent on the **lexical environment**

&nbsp;

Lexical means hierarchy / in order / in sequence

&nbsp;

### **Lexical environment** is created whenever an execution context is created.

**Note**: A lexical environment is the **local memory** along with the **lexical environment of its parent**

Eg:

function a () {

function b () {}

}

&nbsp;

**function b is lexically inside function a**

**function a is lexically inside global scope**

Now let's say x is the parameter for function a and y is the parameter for function b

Local memory of Execution Context of function b will only have y in its memory

But lexical environment will have **local memory y** along with **lexical environment of its parent** function a which is **x**

Note: lexical environment of Global Execution Context is **null**

&nbsp;

This chain of lexical environments & parent references is called as **Scope Chain**

&nbsp;

### **let & const declarations are hoisted**

&nbsp;

## **Temporal Dead Zone**:

The time period from hoisting to until its assigned or initialized with some value

Eg:

console.log(a);

console.log(b);

var a = 10;

let b = 1;

&nbsp;

Console O/P:

undefined

Reference error: Cannot access b before initialization

&nbsp;

During the creation phase, both a & b are allocated memory and are initialized with the special value **undefined** but a is allocated inside Global Scope while b in a different scope (Script). Which means that, while executing console.log(b) b cannot be accessed as its not defined anywhere in global scope thus we get the reference error.

&nbsp;

Note: You **can't access the variables** when they are in **temporal dead zone**

&nbsp;

That means, **window.a** returns **10**, but **window.b** returns **undefined** as its not defined in a global scope

&nbsp;

You **can avoid temporal dead zone by initializing the variables in the top** of your code

&nbsp;

### **let & const are Block Scoped**

&nbsp;

## **What is a block in JS?**

Anything that is defined inside the curly braces in JS is called a block

### A block is also known as **Compound Statement**

Block is used to **group multiple statements** in JS

Eg:

{

var a = 10;

console.log(a);

}

&nbsp;

### **What all variables and functions we can access inside the block are known as Block Scope**

Consider the following example:

{

var a = 10;

let b = 20;

const c = 30;

}

&nbsp;

What will happen during the hoisting (i.e. before code execution starts)?

a:undefined in **Global Scope**

b:undefined & c:undefined in **Block Scope**

&nbsp;

That's why let & const **cannot be accessed outside the Block**

While var can be accessed anywhere

&nbsp;

## **Shadowing in JS:**

var is shadowed and modified inside the block

let & const are just shadowed inside the block but not modified

&nbsp;

Reason: It's because **var is defined in Global Scope** & if inside the block, it's assigned a value, it gets modified

Whereas let & const are defined in **Script Scope** & if they are inside the block it will be defined in **Block scope**, so it will not modify

Eg:

var a = 100;

let b = 200;

const c = 300;

{

var a = 10;

let b = 20;

const c = 30;

console.log("insideBlock", a, b, c);

}

console.log("outsideBlock", a, b, c);

&nbsp;

**Console O/P**:

insideBlock,10,20,30

outsideBlock,10,200,300

&nbsp;

### **Note: Block scope also follows lexical scope**

&nbsp;

## **Illegal Shadowing:**

let a = 10;

{

var a = 10;

}

**Syntax Error** "a" is already declared

&nbsp;

## **Closures:**

Function along with its lexical environment forms Closures

Function + Lexical Environment = Closures

&nbsp;

### Uses of Closures:

- Module Design Pattern
- Currying
- Functions like **once**
- Memoize
- maintaining state in async
- setTimeouts
- Iterators
- and many more…

&nbsp;

## **Dive Deep into Functions**

### **Function Statement vs Function Expression**:

Eg:

&nbsp;

a();

b();

// Function Statement

function a() {

console.log("a called");

}

&nbsp;

//Function Expression

var b = function () {

console.log("b called");

}

&nbsp;

**Console O/P:**

a called

Uncaught Type Error: b is not a function

&nbsp;

### **Note:**

Function Statement & Function Expression **differs in Hoisting**

### **Function Statement is also known as Function Declaration**

&nbsp;

## **Anonymous Functions:**

Function without a name

This will result to a Syntax Error

Eg:

function () {

&nbsp;

}

&nbsp;

**Note**: They are used in a place where functions are used as values

Just how we defined function b above

&nbsp;

## **Named Function Expression:**

Function Expression with Named Anonymous function is called as Named Function Expression

&nbsp;

Eg:

var b = function xyz() {

console.log("b called");

}

b():

xyz();

&nbsp;

**Console O/P:**

b called

Uncaught Reference Error: xyz is not defined

&nbsp;

## **Parameters vs Arguments:**

While creating function => parameters

While using the function => arguments

&nbsp;

## **First Class Functions:**

The ability to use functions as values is called as first class functions

Passing functions as arguments of another function

Eg:

var b = function (param) {

console.log(param)

}

function xyz() {

}

&nbsp;

b(xyz);

&nbsp;

**Console O/P:**

f xyz() {

&nbsp;

}

&nbsp;

## **Callback Functions**:

The function which you pass into another function is called as Callback function

&nbsp;

Remember JS is a **synchronous single threaded** language?

This callback functions helps to access to the asynchronous world

How?

Eg: setTimeout(function () { }, 5000) => That function is a call back function

&nbsp;

Eg:

setTimeout( function () {

console.log("timer ended");

}, 5000);

&nbsp;

function x(y) {

console.log("x");

y();

}

&nbsp;

x (function y () {

console.log("y");

})

&nbsp;

**Console O/P**:

x

y

timer ended (after 5000 ms) => Asynchronous operation

&nbsp;

Here, after x & y are consoled the Call Stack becomes empty, but after 5000 ms again it will be filled magically with the setTimeout (async) callback function

&nbsp;

## **What is Main Thread?**

Call Stack is also known as Main Thread

JS has only one call stack i.e., only one main thread

&nbsp;

Thus if any function takes long time, it will block the main thread until it is executed. In that case async functions / callback functions are the saviours

&nbsp;

### **Note**: Always use async operations for things which take time

&nbsp;

## **Event Listeners:**

onClick, onChange, etc => event Listeners

### **Closures with event listeners**

Eg:

function attachEventListeners() {

let counter = 0;

document.getElementById("clickMe").addEventListener(

"click", function xyz () {

console.log("Button is clicked", ++counter);

}

);

}

attachEventListeners();

&nbsp;

Console O/P:

Button is clicked 1 (if we click)

Button is clicked 2 (if we click again)

…

&nbsp;

**Note**: Scope of callback function (xyz here) is **Closure** & it's scope is **Global** Scope

&nbsp;

## **Garbage Collection & Remove event listeners:**

Why do we remove event listeners?

Event listeners are heavy, they take memory

Even when the **Call Stack is empty**, but still they will **not free up the memory**

Eg: consider the counter variable in the above example.

Even if the call stack is empty it can never forget / free the counter value as we may not know when someone can click that button & when clicked we have to return the total number of clicks happened up until then.

&nbsp;

That's why remove the event listeners if we no longer use and need them.

All the variables (like counter in the above example) held by the event listeners closure will be **garbage collected** once the event listeners are removed
