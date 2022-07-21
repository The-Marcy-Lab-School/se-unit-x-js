# Lecture: Efficiency and Big O

## The Why

### What should the focus of lecture be?

### Suggested Coding Demo

The following activity will get the students invested in the importance of writing efficent code. You should **code this entire activity from scratch** for fellows to better understand. You should code using Snippets in Chrome developer tools. If fellows are confused, use `debugger` or `console.log` so the fellows to see the data. 

Given a problem: write a function takes in an array and returns the difference between the max number and the min number in the array. 

There are many algorithms we can use solve this problem! (Optionally, you can have students come up with their own algorithms before revealing the two below):
1. Sort the array and return the difference between the last and first element: `array[array.length - 1] - array[0]`
2. Iterated through the array keeping track of the largest and smallest numbers seens. At the end, return the difference between the largest and smallest values.

Which algorithm is better? and why?

```js
// Algorithm 1
function maxMinDiff1(nums){
  // Remember that .sort() will sort in place
  nums.sort((a, b) => a - b); // Remember to pass in a callback or else it will sort alphanumerically instead of numerically
  return nums[nums.length - 1] - nums[0];
}
```

```js
// Algorithm 2
function maxMinDiff2(nums){
  let largest = nums[0];
  let smallest = nums[0];
  for(number of nums){ 
    if(number > largest){
      largest = number
    } else if (number < smallest){
      smallest = number
    }
  }
  return largest - smallest
}
```

Can we prove both algorithms are correct solutions? **We should! We should always show the students**
```js
let integers = [4, 2, 8, 3, 9, 2, 1];
// Make fellows predict what the following invocation will evaluate to given the example above!

console.log(maxMinDiff1(integers)) 
console.log(maxMinDiff2(integers)) // Both evaluate to 8 because 9 - 1 is 8
```


