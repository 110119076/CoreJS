**1. Closures**
  
**Question**

What will this print?

function outer() {

  let count = 0;

  return function inner() {
  
    count++;
    
    console.log(count);
    
  };
  
}

const fn = outer();

fn();

fn();

fn();

**Output**

1

2

3

**Explanation**

inner() remembers count even after outer() is finished.

🌍 Real-world:

Used in React hooks (useState)

Used in private variables

**2. var vs let in Loop (Classic Trap)**

**Question**

for (var i = 0; i < 3; i++) {

  setTimeout(() => console.log(i), 100);
  
}

**Output**

3

3

3

**Fix**

for (let i = 0; i < 3; i++) {

  setTimeout(() => console.log(i), 100);
  
}

**Correct Output**

0

1

2

**Explanation**

var → function scoped

let → block scoped

🌍 Real-world

Timers + loops = very common bug in production

**3. Event Loop (Must Know)**

**Question**

console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

Promise.resolve().then(() => console.log("Promise"));

console.log("End");

**Output**

Start

End

Promise

Timeout

**Explanation**

Order:

Sync → Start, End

Microtask → Promise

Macrotask → setTimeout

**4. this Keyword (Interview Favorite)**

**Question**

const obj = {

  name: "John",
  
  greet: function () {
  
    console.log(this.name);
    
  }
  
};

const fn = obj.greet;

fn();

**Output**

undefined

**Explanation**

this depends on how function is called, not where it's written.

**Fix**

const fn = obj.greet.bind(obj);

fn();

🌍 Real-world

React callbacks

Event handlers

**5. Hoisting**

**Question**

console.log(a);

var a = 10;

**Output**

undefined

**Another**

console.log(a);

let a = 10;

**Output**

ReferenceError

**Explanation**

var → hoisted + initialized as undefined

let → hoisted but in TDZ (Temporal Dead Zone)

**6. == vs ===**

**Question**

console.log(0 == false);

console.log(0 === false);

**Output**

true

false

**Explanation**

== → type coercion

=== → strict check

**7. Prototype & Inheritance**

**Question**

function Person(name) {

  this.name = name;
  
}

Person.prototype.sayHi = function () {

  console.log("Hi " + this.name);
  
};

const p1 = new Person("John");

p1.sayHi();

**Output**

Hi John

**Explanation**

JS uses prototype-based inheritance

🌍 Real-world

Class in JS is just syntactic sugar over prototype

**8. Debounce Implementation (VERY IMPORTANT)**

**Question**

Write debounce function

**Solution**

function debounce(fn, delay) {

  let timer;

  return function (...args) {
  
    clearTimeout(timer);
    
    timer = setTimeout(() => fn.apply(this, args), delay);
    
  };
  
}

**Intuition**

Only last call executes

🌍 Real-world

Search bar API calls

Resize events

**9. Deep vs Shallow Copy**

**Question**

const obj1 = { a: 1, b: { c: 2 } };

const obj2 = { ...obj1 };

obj2.b.c = 100;

console.log(obj1.b.c);

**Output**

100

**Explanation**

Spread = shallow copy

Nested objects still share reference

**Deep Copy**

const deep = JSON.parse(JSON.stringify(obj1));

**10. Currying**

**Question**

function add(a) {

  return function (b) {
  
    return a + b;
    
  };
  
}

add(2)(3);

**Output**

5

**Explanation**

Breaking function into smaller functions

🌍 Real-world

Functional programming

Reusable logic
