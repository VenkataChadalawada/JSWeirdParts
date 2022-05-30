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





