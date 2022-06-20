## Big O - Arrays

``` javascript

const arr1 = ['a', 'b', 'c'];
const arr2 = ['d', 'e', 'f'];
// Accessing - O(1)
// Searching - O(n)

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

// slice - O(n) returns a shallow copy of an array into a new array from 
const arr4 = arr3.slice(2);
console.log(arr4); // [ 'c', 'd', 'e', 'f' ]
const arr5 = arr3.slice(0,1);
console.log(arr5); // [ 'a' ]
const arr6 = arr3.slice(1,5);
console.log(arr6); // [ 'b', 'c', 'd', 'e' ]
// Note: A shallow copy of an object is a copy whose properties share the same references
// Note: A deep copy of an object is a copy whose properties do not share the same reference - let ingredients_list_deepcopy = JSON.parse(JSON.stringify(ingredients_list));

// splice - O(n)
arr3.splice(1,0,'K'); // inserts at 1st index position
console.log(arr3); // ['a', 'K','b','c', 'd', 'e','f']

arr3.splice(4,2,'L'); // inserts at 4th index replacing 2 elements from there
console.log(arr3); // [ 'a', 'K', 'b', 'c', 'L', 'f' ]
console.log(arr6);

// sort - O(n*logn)

// foreach/filter/map/reduce

// join
const elements = ['Fire', 'Air', 'Water'];
console.log(elements.join());
// expected output: "Fire,Air,Water"
console.log(elements.join(''));
// expected output: "FireAirWater"
console.log(elements.join('-'));
// expected output: "Fire-Air-Water"

//index of
const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];
console.log(beasts.indexOf('bison'));
// expected output: 1
// start from index 2
console.log(beasts.indexOf('bison', 2));
// expected output: 4
console.log(beasts.indexOf('giraffe'));
// expected output: -1

//incldes
const array1 = [1, 2, 3];
console.log(array1.includes(2));
// expected output: true
const pets = ['cat', 'dog', 'bat'];
console.log(pets.includes('cat'));
// expected output: true
console.log(pets.includes('at'));
// expected output: false

//toString
const array2 = [1, 2, 'a', '1a'];
console.log(array2.toString());
// expected output: "1,2,a,1a"

//isArray
Array.isArray([1, 2, 3]);  // true
Array.isArray({foo: 123}); // false

//of - Array.of() method creates a new Array instance from a variable number of arguments
Array.of(1, 2, 3); // [1, 2, 3]
Array(1, 2, 3);    // [1, 2, 3]



```
