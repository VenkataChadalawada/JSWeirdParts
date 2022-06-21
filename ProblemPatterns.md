## Frequency Counter

``` javascript
function validAnagram(str1, str2){
  // add whatever parameters you deem necessary - good luck!
  const letters1 = str1.split('');
  const letters2 = str2.split('');

  let hash1 = {}, hash2 = {};

  letters1.map((letter) => {
    hash1[letter] ? hash1[letter] = hash1[letter]+1 : hash1[letter] = 1;
  });

  letters2.map((letter) => {
    hash2[letter] ? hash2[letter] = hash2[letter]+1 : hash2[letter] = 1;
  });

  let res;
  for(let key in hash1){
    if(hash2[key] && hash1[key] === hash2[key]){
      res = true;
    } else {
      return false;
    }
  }

  return res;
}
```

## MutiPointer

// sumZero
``` javascript
function sumZero(arr){
  // if unsorted - sort it - O(NlogN)
  let start = 0;
  let end = arr.length-1;
 
  while(start < end){
    console.log(arr[start]);
    console.log(arr[end]);
    let sum = arr[start]+arr[end];
    if(sum === 0 ){
      break;
    } else if(sum > 0) {
      end--;
    } else {
      start++;
    }
  }
  return [arr[start], arr[end]]
}

sumZero([-4, -3, -2, -1, 0, 3, 1, 5, 10]);

```

// countUniqueValues
function countUniquevalues(arr){
  let i = 0, j = 1;
  while(j < arr.length){ // 1<10
    console.log('-', i);
    if(arr[j] !== arr[i]){
      i++;
      arr[i] = arr[j];
    } else {
      j++;
    }
  }
  console.log(arr);
  return i+1;
}

console.log(countUniquevalues([1,1,1,2,3,3,4,4,5,6]));

## sliding window

``` javascript
function maxSubArraySum(arr, num) {
  let maxSum = 0;
  let tempSum = 0;
  if(arr.length<num) return null;
  for(let i=0;i<num;i++){
    maxSum+=arr[i];
  }
  tempSum = maxSum;
  for(let i=num;i<arr.length;i++){
    tempSum = tempSum - arr[i-num]+ arr[i]
    maxSum = Math.max(maxSum, tempSum);
  }
  return maxSum;

}
console.log(maxSubArraySum([2,6,9,2,1,8,5,6,3],3));
```

