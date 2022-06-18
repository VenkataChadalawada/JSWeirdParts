## Big O - Arrays

``` javascript

const arr1 = ['a', 'b', 'c'];
const arr2 = ['d', 'e', 'f'];

//push - O(1)
arr1.push('z');
console.log(arr1); // [ 'a', 'b', 'c', 'z' ]

// pop - O(1)
arr1.pop();
console.log(arr1); // [ 'a', 'b', 'c' ]

// unshift - O(n)
arr1.unshift('x'); 
console.log(arr1); // [ 'x', 'a', 'b', 'c' ]

// shift - O(n)
arr1.shift(); 
console.log(arr1); //[ 'a', 'b', 'c' ]

// concat - O(n)
const arr3 = arr1.concat(arr2);
console.log(arr3); // [ 'a', 'b', 'c', 'd', 'e', 'f' ]

// slice - returns a shallow copy of an array into a new array from 
const arr4 = arr3.slice(2);
console.log(arr4); // [ 'c', 'd', 'e', 'f' ]
const arr5 = arr3.slice(0,1);
console.log(arr5); // [ 'a' ]
const arr6 = arr3.slice(1,5);
console.log(arr6); // [ 'b', 'c', 'd', 'e' ]

// splice
arr3.splice(1,0,'K'); // inserts at 1st index position
console.log(arr3); // ['a', 'K','b','c', 'd', 'e','f']

arr3.splice(4,2,'L'); // inserts at 4th index replacing 2 elements from there
console.log(arr3); // [ 'a', 'K', 'b', 'c', 'L', 'f' ]



```
