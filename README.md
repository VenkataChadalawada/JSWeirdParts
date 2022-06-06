# JSWeirdParts

#### Syntax Parsers, 
A program that reads your code and determines what it does and if its grammar is valid

#### Execution contexts, 
A wrapper to help manage the code that is running

#### Lexical Environments
where something sits physically in the code you write

#### Name/Value Pairs
A name which maps to a value eg: address = '101 main st', An object is a collection of name value pairs

#### Global Environment & Global Object
Global Object in the beginning is window and this for the global level is window.

#### Hoisting
Execution context is created in two phases 
1) creation Phase : It sets up memory space for variables(set up and undefined) and functions
2) execution phase : start executing the code


```
b();
console.log(a);
var a = 'hello world';
function b() {
   console.log('called b!');
}

```
Output:-
```
  called b!
  undefined
``` 

you didnt get error saying "a is not defined", instead you got it "undefined". so dont get into this trap.

#### lexical scoping
A nested or inner function have access to the same stuff that its parent or grand parent functions no matter how many levels up.

```
function fruitcollection(){
const fruits = ['apples', 'oranges', 'bananas'];
  function cryForHelp() {
      function inner() {
         for(let fruit of fruits) {
            console.log("pls help us"+ fruit + "\n");
         }
      }
      inner();
  }
  cryForHelp();
}
// run
fruitcollection();

O/P:-
-----
pls help us apples
pls help us oranges
pls help us bananas
```

#### Function Expression
```
const a = function(x,y){
   return x+y;
   }
```

#### Higher Order Function
functions that accepts functions as arguments and returns functions

#### Methods
we can add functions as properties on objects, we call them methods!
```
const math = {
   blah : 'hi',
   add(x,y){
   return x+y;
   },
   multiply(x,y){
   return x*y;
   }
}
math.add(2,3)

O/p:-
-----
5
```
#### THIS in methods
The value of `this` changes depends on invocation context of the function it is used in
```
const person = {
   first: 'Robert',
   last: 'Davis',
   fullName(){
      return `${this.first} ${this.last}`;
   }
}
person.fullName();
person.last = 'Stephenson';
person.fullName();

O/P:-
----
Robert Davis
Robert Stephenson
```
if we say
```
const RamName = person.fullName;
RamName(); // it will be blank because the context of `this` is window here.
O/p:-
------
<blank>

```
NOTE: remember if we use  ARROW function => as an object method and refer this it will be outer scope window . but if we use functions that actually runs on window and wanted scoping the same arrow function brings the context this to be object instead of window.
eg:--
``` javascript
const person = {
   first: 'Robert',
   last: 'Davis',
   fullName1 : function(){ // regular function
      return `Hello ${this.first} ${this.last}`; // Hello Robert Davis
   },
   fullName2 : () => { // arrow function
      return `Hello ${this.first} ${this.last}`; // Hello undefined undefined
   },
   shoutName1 : function(){
      setTimeout(() => { // arrow func
         console.log(this.fullName1()); // Robert Davis
      }, 3000);
   },
   shoutName2 : function(){
      setTimeout(function(){ // regular function
         console.log(this.fullName1()); // Error: this.fullName1 is not a function
      }, 3000);
   }
}

person.fullName1();
person.fullName2();
person.shoutName1();
person.shoutName2();
```

### Array Methods

- Push : add to end
- Pop : remove from end
- Unshift : add to start
- shift : remove from start
- concat : merge arrays
- includes : look for a value
- indexOf : finding the value index 
- join : creates a string from array
- reverse : reverse an array
- slice : copies a portion of an array
- splice : removes or replaces portion of an array
- sort : sorts an array

### DOM : Properties & Methods 
Methods:-
--------
- classList()
- getAttribute()
- setAttribute()
- appendChild()
- append()
- prepend()
- removeChild()
- remove()
- createElement()

Properties:-
--------
- innerText
- textContent
- innerHTML
- value
- parentElement
- children
- nextSibling
- previousSibling
- style

### Event Bubling
It is a process that starts with the element that triggered the event and then bubbles up to the containing elements in the hierarchy.

``` html
...
<body>
   <p onClick="alert('paragraph clicked')">
      I am a paragraph
   <button onClick="alert('button clicked')"> click me </button>
   </p>
</body>
...
```

Now when you click on button you would see two alerts, first button clicked and second paragraph clicked. event bubbles up from origin to all the way highest level. sometimes we want that effect. Several other times you dont. if we dont want that behaviour we could add `event.stopPropagation()` in the listener where bubbling starts in this case its button.

### Event Delegation

Event Delegation is basically a pattern to handle events efficiently. Instead of adding an event listener to each and every similar element, we can add an event listener to a parent element and call an event on a particular target using the . target property of the event object.

``` html
...
<ul id="tweets" onClick="ul been clicked">
   <li> hi </li>
   <li> hello </li>
</ul>
...

```

if we clicked on `li` , even if our listener on `ul` we would get listened in `ul` but `event.target` would be  `li` 
eg:
``` javascript
if event.target.nodeName === LI {
  event.target.remove();
}
```

### how call stack works

when a script calls function, the interpreter adds it to the call stack and then starts carrying out the function.
Any functions that are called by this function gets further adds up in the call stack and runs when their calls are reached
when the current fucntion is reached , the interpreter takes it off the stack and resumes execution where it left off in the last code.

``` javascript
const multiply = (x,y) => x * y;
const square = (x) => multiply (x, x);
const isRightTriangle = (a,b,c) => {
   square(a) + square(b) === square(c)
}
isRightTriangle(3,4,5);
```

### JS is single threaded
one thing at a time, does that mean do we need to wait for longer actions, The answer is NO, there are ways around

### Callbacks - how do they work?
callback function is a function you specify to an existing function/method, to be invoked when an action is completed, requires additional processing, etc.
Example
``` javascript

console.log(" first-- ");
setTimeout(() => {
   // call back function
   console.log('after three secs');
}, 3000);
console.log('second');

```

 Browser does the work 
 
### how does Browsers work?
Browsers come with webAPIs that are able to handle certain tasks in the background (like making requests or setTimeouts)
JS call stack recognizes these webAPI functions and passes them off to the browser to take care of.
Once the browser finishes those tasks, It puts them in callback Queue and JS eventloop will keep checking if there is anything in that queue if they  return to the queue by browser then they are pushed onto the stack as callbacks by event loop, then JS will execute them.

### Event loop
The event loop is a constantly running process that monitors both the callback queue and the call stack. If the call stack is not empty, the event loop waits until it is empty and places the next function from the callback queue to the call stack.


### call back hell
In this, each callback takes arguments that have been obtained as a result of previous callbacks. This kind of callback structure leads to lesser code readability and maintainability. We can avoid the callback hell with the help of Promises. Promises in javascript are a way to handle asynchronous operations in Node.

### Promises
A promise is an object representing the eventual completion or failure of an asynchronous operation
``` javascript
const examplePromise = (url) => {
   return new Promise((resolve, reject) => {
         const delay = Math.floor(Math.random()*4500);
         setTimeout(() => {
            if(delay >4000) {
               reject('connection time out');
            } else { 
               resolve('success');
            }
         }, delay);
   });
}

```
With promises you could use them two ways

``` javascript
examplePromise('abc.com').then(() => {
   examplePromise('def.com').then(() => {
      examplePromise('ghi.com').then(() => {
         console.log('ghi success');
      }).catch((e) => {
          console.log('ghi fail');
      });
   }).catch((e) => {
        console.log('def fail');
      });
}).catch((e) => {
     console.log('abc fail');
});
```

or you could chain them


``` javascript
examplePromise('abc.com').then(() => {
  console.log('abc success');
  return examplePromise('def.com');
  }).then(() => {
      console.log('def success');
      return examplePromise('ghi.com');
  }).then(() => {
      console.log('ghi success');
  }).catch((e) => {
      console.log(' any failed');
  });
```

#### Example full promise

#### Async Await - syntactic sugar for Promises

```javascript
const sing = async () => {
throw new Error('problem'); 
return `LALALALA`
}

sing.then(() => {
console.log('Promise resolved');
})
.catch(err => {
console.log('eeror'+err);
});
```

``` javascript
const login(usr, pass) => {
if(!usr || !pass) throw 'Missing Credentials'
if(pass === '1234') return 'Welcome'
throw 'Invalid pass';
}

login('ajhd').then(msg => {
console.log('error');
}).catch(err =>{
console.log('error');
});
```

### with Await
``` javascript
async function rainbow() {
await func1();
await func2(abc);
return 'all done';
};

async function printRainbow() {
await rainbow();
console.log('end of rainbow');
}

printRainbow() ;
```

#### how to handle errors in async await

- 1 use good old fashion try and catch

``` javascript
const fakeRequest = (url) => {
return new Promise((resolve, reject) => {
const delay = Math.floor(Math.random()*4500)+500;
setTimeout(() =>
 {
if(delay >4000){
reject('connection Timeout')
} else {
resolve(`here is your fake data from ${url}`)
}
}, delay);
})
}
}

async function makeTwoRequests(){
try{
let data1 = await fakeRequest('/page1');
console.log(data1);
} catch(e) {
  console.log('error'+e);
}
}


```

### OOP 

#### Prototypes
JS objects inherits features from one another

* note: remember arrays are objects in javascript

> Array.prototype

>String.prototype

we can add our own
``` javascript
String.prototype.grumps = () =. alert('go away');
const cat = 'Blue';
cat.grumpus();


String.prototype.yell = 
function(){
console.log(this);
return `${this.toUpperCase()}`;
};

// you can over ride too
Array.prototype.pop = function(){
return 'sorry no pop for you';
};


const dog = 'tim';
dog.__proto__

__proto__ is the reference to prototype
remember you should not need to do anything on this.

```

#### factory functions

``` javascript
function hex(r, g, b){
  return '#'+((1<<24) + (r<<16) + (g<<8) +b).toString(16).slice(1);
}
hex(255, 100, 25);

// -----
function makeColor(r,g,b) {
const color = {};
color.r = r;
color.g = g;
color.b = b;
color.rgb = function() {
const {r,g,b} = this;
return `rgb(${r}, ${g},  ${b})`;
};
color.hex = function (){
  return '#'+((1<<24) + (r<<16) + (g<<8) +b).toString(16).slice(1);
}

return color;
}

const firstColor = makeColor(35, 255, 150);
firstColor.hex()
 
```

####  constructor function
people use this pattern instead of factory function

instead of using their own copy we will use one function 

#### new keyword
/* 1) creates a blank, plain javascript object;
2) Links (sets the constructor of) this object to another object;
3) Passes the newly created object from Step1 as the this context;
4) returns this if the function doesnt return its own object.

*/
function Color(r,g,b) {
this.r = r;
this.g = g;
this.b =b;
console.log(this);
}

Color(30,40, 50);
// if we call Color directly `this` refers to `window`

new Color(30, 40, 50);

```
// to add a method
``` javascript

function Color(r,g,b) {
this.r = r;
this.g = g;
this.b =b;
}

Color.prototype.rgb = function(){
const {r,g,b} = this;
return `rgb(${r}, ${g}, ${b})`;
};

Color.prototype.hex = function (){
  return '#'+((1<<24) + (r<<16) + (g<<8) +b).toString(16).slice(1);
}
// usage 
const a = new Color(30, 40, 50);
a.rgb();

```

note: dont use arrow functions remember they behave differently and change this scope

### Classes
syntactic sugar for prototypes like above - advantage we dont have to break up things and gives more structure

class Color {
constructor(r, g, b) {
// executes immediately as soon as it calles for one time
 this.r = r;
this.b = b;
this.g = g;
this.name = name;
}
// methods
greet() { 
// it shows up in this class  __proto__ like prototype as above
return `hellow from ${this.name}`;
}

rgb(){
const {r,g,b} = this;
return `rgb(${r}, ${g}, ${b})`;
}

hex(){
return '#'+((1<<24) + (r<<16) + (g<<8) +b).toString(16).slice(1);
}
}

// usage
const c1 = new Color(255, 67, 89, 'tomato');
c1.greet();

```
we can call a method in constructor to be called immediately

```
constructor(r, g, b) {
// executes immediately as soon as it calles for one time
 this.r = r;
this.b = b;
this.g = g;
this.name = name;
this.calculateColorIndex();
}

```
#### Extends & Super

``` javascript
class Cat{
constructor(name, age){
this.name = name;
this.age = age;
}
eat(){
return `${this.name} is eating!`;
}
meow(){
return 'Meoww';
}

}

class Dog{
constructor(name, age){
this.name = name;
this.age = age;
}
eat(){
return `${this.name} is eating!`;
}
bark(){
return 'Boww
}
}
```

we can save this repeating func

``` javascript
class Pet{
constructor(name, age){
this.name = name;
this.age = age;
}
eat(){
return `${this.name} is eating!`;
}
}

class Cat extends Pet{
// say you wanna add additional values during intializing cat
constructor(name, age, livesLeft=9){
super(name, age); // reuse from super class
this.livesLeft = livesLeft;
}
meow(){
return 'Meoww';
}
}

class Dog extends Pet{
bark(){
return 'Boww
}
// method overriding
eat() {
 return `${this.name} scarfs his food`;
}
}
```
```
const dog1 = new dog('jaki', 13);
dog1.eat()
const cat1 = new Cat('monty', 9)
```
