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
1) creation Phase : It sets up memory space for variables and functions
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



