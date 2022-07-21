# Lecture Guide: Big O

If taught poorly, this lecture could be incredibly boring. If we spit a bunch of letter and numbers at students, they aren't going to see the value. Do not make the main focus listing all Big-O Notations. O(_n_<sup>2</sup>) is not fun to talk about, much less even say! Instead, spend 80% of lecture investing the students in why they should care about efficient algorithms! 

## Suggested Lecture Flow
1. Start lecture grounding the fellows in the Why 
2. Make sure everyone is on the same page with a few key terms: algorithm, time complexity, space complexity 
3. Invest the fellows with a coding demo
4. Overview Big-O Notation and the different classes of algorithms

### 1. The Why

This lesson is important because it introduces students to the concept of efficient algorithms and gives them a language and **terminology for how to communicate** this to their peers. We teach fellows that words are their world, and in tech, they need to understand this lingo in order to communicate their knowledge of writing *scalable* code. Companies don't want just any developers, they want developers who can write efficient code!

### 2. Important Terms and Concepts

**What is an algorithm?** Is it a list of steps or set of rules to be followed. 
**How do we measure the efficiency of an algorithm?** There are two main ways. Time complexity refers to how fast an algorithm is; the faster an application runs on your computer, the better! Space complexity refers to how much memory an algorithm takes up; the less memoery an application takes up on your computer, the better!

### 3. Coding Demo

The following activity will get the students invested in the importance of writing efficent code. You should **code this entire activity from scratch** for fellows to better understand. You should code using Snippets in Chrome developer tools. If fellows are confused, use `debugger` or `console.log` so the fellows can see the data. 

Given a problem: write a function that takes in an array of numbers and returns the difference between the max element and the min element in the array. 

There are many algorithms we can use solve this problem! (Optionally, you can have students come up with their own algorithms before revealing the two below):
1. Sort the array and return the difference between the last and first element: `array[array.length - 1] - array[0]`
2. Iterated through the array keeping track of the largest and smallest numbers seen. At the end, return the difference between the largest and smallest values.

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
  for(number of nums){ // Could be nice reviewing for...of loops as an alternative to for loops, but a regular for loop works too!
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
// Make fellows predict what the following invocation will evaluate to in the example above!

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
// Reassign integers to be an array of 100,000 random numbers
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
// Reassign integers to be an array of 1,000,000 random numbers!!
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
If you keep making the data set biggest, you'll get to the point where you computer stalls, as if it broke for a good 2-10 seconds. **This shock value is what we want the fellows to walk away with**. 

When they are first learning to code, they want to make code that works. One day, when they are working for Facebook, who has millions of users, they need to be thoughtful and try to write code that not only works, but is efficient in speed (run time complexity) and memory (space complexity)!

This is as heavy activity, so make space for fellows to decompress and ask questions before jumping into the last part of lecture.

### 4. Big O Notation 

Define **Big-O Notation**. It is a way to describe how an algorithm will scale as the data set gets bigger. 
    * We say that Algorithm2 is O(_n_) aka linear time, because as the size of the array grows, the number of operations the computer has to do will grow linearly. In other words, for each additional element in the array, the computer does one additional loop.
    * We say that Algorithm1 is O(_n_ * log _n_) time because the efficency of sorting is O(_n_ * log _n_) time.

Now would be a great time to pull up this [cheatsheet](https://www.bigocheatsheet.com/) so students can see the O(_n_) is a more efficient runtime than O(_n_ * log _n_). **As you explain the rest of the Big-O run times, be sure to always refer back to this chart for the fellows!**
* O(1) is constant run time. An example is indexing an array. It doesn't matter if `array` is 10 elements or 1,000,000 elements long. Checking `array[1]` is going to take the same amount of time.
* O(log _n_) is logarithmic, where each iteration takes half the amount of time as the last iteration, like with binary search.
* O(_n_) is linear, where each iteration takes the same amount of time as the last iteration.
* O(_n_ * log _n_) is log linear. Any sorting algorithm is log linear. 
* O(_n_<sup>2</sup>) is quadratic. An algorithm with a nested `for` loop is quadratic. 
* O(2<sup>_n_</sup>) or exponential time and O(_n_!) or factorial time are less common. 
