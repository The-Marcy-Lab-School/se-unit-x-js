# Lecture: Big O

## The Why

### What should the focus of lecture be?

### Suggested Coding Demo

The following activity will get the students invested in the importance of writing efficent code. You should **code this entire activity from scratch** for fellows to better understand. You should code using Snippets in Chrome developer tools. If fellows are confused, use `debugger` or `console.log` so the fellows can see the data. 

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

So which is algorithm is better? Now's a great chance to explain to fellows that in coding, what is "better" is subjective! **Coding is all about tradeoffs**. Students might have noticed that Algorithm1 is shorter! Shorter code is better, right? Sometimes...

But Algorithm2 is more **time efficient**. That doesn't mean it's always faster. But it will get faster as the data set scales and gets bigger.
```js
integers = [4, 2, 8, 3, 9, 2, 1];

console.time("Algorithm 1");
maxMinDiff1(integers);
console.timeEnd("Algorithm 1");
// Algorithm 1: 0.077880859375 ms

console.time("Algorithm 2");
maxMinDiff2(integers);
console.timeEnd("Algorithm 2");
// Algorithm 2: 0.121826171875 ms

//Algorithm 2 is actually slower here when the data size is 7 numbers!
```
```js
integers = [];
for(let i = 0; i < 100000; i++){
  integers.push(Math.random() * 100)
}

console.time("Algorithm 1");
maxMinDiff1(integers);
console.timeEnd("Algorithm 1");
// Algorithm 1: 64.5986328125 ms

console.time("Algorithm 2");
maxMinDiff2(integers);
console.timeEnd("Algorithm 2");
// Algorithm 2: 3.208984375 ms

// Algorithm 2 is way faster here when the data size is 100,000 numbers!
```
```js
integers = [];
for(let i = 0; i < 1000000; i++){
  integers.push(Math.random() * 100)
}

console.time("Algorithm 1");
maxMinDiff1(integers);
console.timeEnd("Algorithm 1");
// Algorithm 1: 457.02783203125 ms

console.time("Algorithm 2");
maxMinDiff2(integers);
console.timeEnd("Algorithm 2");
// Algorithm 2: 15.061279296875 ms

// When we add another 0, the data set is 1,000,000! There's a huge difference. Keep adding one more 0 to the data size and show the students what happens!
```
If you keep making the data set biggest, you'll get to the point where you computer stalls, as if it broke for a good 2-10 seconds. **This shock value is what we want the fellows to walk away with**

## So What?
When they are first learning to code, they want to make code that works. One day, when they are working for Facebook, who has millions of users, they need to be thoughtful and try to write code that not only works, but is efficient in speed (run time complexity) and memory (space complexity)!

