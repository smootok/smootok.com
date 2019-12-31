---
title: Problem Solving Patterns in Programming
description: Master common problem solving patterns.
date: 2019-11-11T22:02:31.777Z
---

## Objective

Master common problem solving patterns.

## Some Patterns

* Frequency Counters
* Multiple Pointers
* Sliding Window
* Divide and Conquer
* Dynamic Programming
* Greedy Algorithms
* Backtraking
* **Many more!**

We will cover in this article the first 3 patterns, they don't have official names. I found them on a udemy course by Colt Steel. each pattern can solve multiple problems, but they don't cover all possible scenarios, so you should think of other solutions if you can't apply them.

### Frequency Counters Pattern

The first pattern we will cover is Frequency Counters. This pattern uses objects or sets to collect values/frequencies of values. This can often avoid the need for nested loops or O(n<sup>2</sup>) operations with arrays / strings.

**Let's explore an example**

> Write a function called same, which accepts two arrays. The function should return true if every value in the array has it's corresponding value squared in the second array. The frequency of values must be the same.

```js
same([1,2,3], [4,1,9]) // true
same([1,2,3], [1,9]) // false
same([1,2,1], [4,4,1]) // false (must be same frequency)
```

**Naive Solution**

```js
function same(arr1, arr2){
  if(arr1.length !== arr2.length){
    return false
  }
  for(let i = 0; i < arr1.length; i++){
    let correctIndex = arr2.indexOf(arr1[i] ** 2)
      if(correctIndex === -1) {
        return false;
      }
    arr2.splice(correctIndex,1)
  }
  return true
}
```

The idea is that we have two arrays, the first thing we do is checking if the two arrays have different length then we return `false`, there is no way for it to be true, that's because the frequency of values should be the same, else we loop over the first array we can loop over the second one it doesn't matter because they have the same length, and we search using `indexOf` the index of each `arr1` value squared in `arr2`. if the index equal -1 then we return `false`, else we remove the element using `splice`. The Time complexity of this solution is **O(n<sup>2</sup>)** because we loop over the first array and we use `indexOf` inside the loop.

**Frequency Counters Solution**

```js
function same(arr1, arr2) {
  if (arr1.length !== arr2.length) {
    return false
  }
  const obj1 = {}
  const obj2 = {}

  for (let i = 0; i < arr1.length; i++) {
    obj1[arr1[i]] = obj1[arr1[i]] ? obj1[arr1[i]] + 1 : 1
    obj2[arr2[i]] = obj2[arr2[i]] ? obj2[arr2[i]] + 1 : 1
  }

  for (key in obj1) {
    if (obj1[key] !== obj2[key ** 2]) {
      return false
    }
  }
  return true
}
```

Instead of looping over the first array and checking for each value using `indexOf`, we loop one time and we store the frequency of each array in an object, then we compare them in the second loop but this time it's not nested so the time complexity is **O(n)**, much better than the naive solution.

### Multiple Pointers Pattern

The next problem solving pattern is multiple pointers. The idea is that we create pointers or values that correspond to an index or position and move towards the beginning, end or middle based on a certain condition.
Very efficient for solving problems with minimal space complexity as well.

**Example**

> Write a function called sumZero which accepts a sorted array of integers. The function should find the first pair where the sum is 0. Return an array that includes both values that sum to zero or undefined if a pair does not exist.

```js
sumZero([-3,-2,-1,0,1,2,3]) // [-3,3] 
sumZero([-2,0,1,3]) // undefined
sumZero([1,2,3]) // undefined
```

**Naive Solution**

```js
function sumZero(arr){
  for(let i = 0; i < arr.length; i++){
    for(let j = i+1; j < arr.length; j++){
      if(arr[i] + arr[j] === 0){
        return [arr[i], arr[j]]
      }
    }
  }
}
```

This solution is simple, we use two nested loop that calculate the sum of each element in the first loop with the rest of the array using the second loop, until we found 0. The Time complexity of this solution is **O(n<sup>2</sup>)**.

**Multiple Pointers Solution**

```js
function sumZero(arr) {
  let left = 0
  let right = arr.length - 1
  while (left < right) {
    const sum = arr[left] + arr[right]
    if (sum === 0) {
      return [arr[left],arr[right]]
    } else if (sum > 0) {
      right--
    } else {
      left++
    }
  }
}
```

The idea here is that we use two pointers one in the left of the array and the second one in the right, and we start looping by seeing what is the sum of the two elements, if the sum is positive we move the right pointer down, if it is negative we add one to the left pointer until we found the sum equal to 0, else the function will return undefined when the left pointer become equal to the right pointer. The Time complexity of this solution is **O(n)**.

### Sliding Window

The last pattern in this article is Sliding Window. This pattern involves creating a window which can either be an array or number from one position to another. Depending on a certain condition, the window either increases or closes (and a new window is created). Very useful for keeping track of a subset of data in an array/string etc.

**Example**

Write a function called maxSubarraySum which accepts an array of integers and a number called n. The function should calculate the maximum sum of n consecutive elements in the array.

```js
maxSubarraySum([1,2,5,2,8,1,5],2) // 10
maxSubarraySum([1,2,5,2,8,1,5],4) // 17
maxSubarraySum([4,2,1,6],1) // 6
maxSubarraySum([4,2,1,6,2],4) // 13
maxSubarraySum([],4) // null
```

**Naive Solution**

```js
function maxSubarraySum(arr, n) {
  if ( n > arr.length){
    return null
  }
  var max = -Infinity
  for (let i = 0; i <= arr.length - n ; i ++){
    temp = 0
    for (let j = 0; j < n; j++){
      temp += arr[i + j]
    }
    if (temp > max) {
      max = temp
    }
  }
  return max
}
```

The first thing we do is checking if `n` is greater than the length of the array, if true we return `null` because we can't sum them, example `n = 3` we can't sum 3 elements if we only have 2 elements in the array.
Otherwise we make `max` and we started it at `-Infinity` because it will work also when we have negative numbers in the array. After that we create a loop that goes from 0 to the length of the array - num, because
we will reach the end of the array using the nested loop, and we make comparison if the temp max greater than the current max, the temp max become the current max else we keep the old value of the current max. The Time complexity of this solution is **O(n<sup>2</sup>)**.

**Sliding Window Solution**

```js
function maxSubarraySum(arr, n) {
  if (arr.length < n) {
    return null
  }

  let tempSum = 0
  let maxSum = 0

  for (let i = 0; i < n; i++) {
    maxSum += arr[i]
    tempSum += arr[i]
  }

  for (let i = n; i < arr.length; i++) {
    tempSum = tempSum - arr[i - n] + arr[i]
    maxSum = tempSum > maxSum ? tempSum : maxSum
  }

  return maxSum
}
```

The idea here is that at the very beginning we sum together the first `n` elements in the array. we keep track of the sub sum in `maxSum` and we store the next potential sub sum in `tempSum`, and we compare it with `maxSum`, if `tempSum` is greater than `maxSum`, we update `maxSum` with `tempSum`, but this time we get the value of `tempSum` without using nested loop, but by substracting the first element in each sub and adding the last element in each sub. The Time complexity of this solution is **O(n)**.
