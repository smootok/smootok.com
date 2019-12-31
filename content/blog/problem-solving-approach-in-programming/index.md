---
title: Problem Solving Approach in Programming
description: Define what an algorithm is, and Device a plan to solve algorithms.
date: 2019-11-06T12:16:00.214Z
---

## Objectives

* Define what an algorithm is
* Device a plan to solve algorithms

## What is an algorithm?

An algorithm is a **process** or **set of steps** to accomplish a certain task.

When we say **algorithm**, we could be talking about a set of mathematicals steps we need to do to solve a problem, we could be talking about facebook algorithms that suggest certain ads to you, or google algorithms when you search something.
So that could be something simple, or difficult it doesen't matter.

## Why we need to know this?

Almost everything that you do in programming involves some kind of algorithm!
It's the **foundation** for being a successful problem solving and developer.

## How do you improve?

A lot of people think that people are inherently good or bad about algorithms, Some people are just naturally better at solving problems, but this doesen't mean that it is hopeless for people who has struggles. 

Using theses steps you will improve your problem solving skills:

1. Understand the problem
2. Explore concrete examples
3. Break it down
4. Solve / Simplify
5. Look back and Refactor

### Step 1: Understand the problem

So imagine you sitting in a room, and there is an interviewer in front of you, that ask you a question, and you didn't know how to solve it, So the first thing I will do is understanding the problem, there are some questions you can ask that help you to clarify things.

1. Can I restate the problem in my own words?
2. What are the inputs that go in the problem?
3. What are the outputs that should come from the solution to the problem?
4. Can the outputs be determined from the inputs? In other words, do I have enough informations to solve the problem? 
5. How should I label the important pieces of data that are part of the problem?

Let's explore how can we apply theses questions in a simple example.

> Write a function which takes two numbers and returns their sum.

➡️1. **Can I restate the problem in my own words?**

Implement addition.

➡️2. **What are the inputs that go in the problem?**

We need two numbers, but we should think about the type of numbers, how large these numbers can be, are we only working with two inputs, what happens if someone leave an input off.

➡️3. **What are the outputs that should come from the solution to the problem?**

The type that function should return (integer, float, string?).

➡️4. **Can the outputs be determined from the inputs? In other words, do I have enough informations to solve the problem?**

Yes, if the user enter two parameters, else if he enter only one parameter, should we handle this? should we add 0 or return undefined? it's depends.

➡️5. **How should I label the important pieces of data that are part of the problem?**

In this example it's simpler, the important informations are the inputs (num1, num2).

### Step 2: Explore concrete examples

Comming up with examples can help you understand the problem better. They also provide sanity checks that eventual function works how it should.

1. Start with simple examples
2. Progress to more complex examples
3. Explore examples with empty inputs / invalid inputs

Let's apply these steps in concrete example.

> Write a function that takes in string and returns counts of each character  in the string.

➡️1. **Start with simple examples**

```js
  chartCount('aaaa')
  chartCount('hello')
```
Should I return object like that:
`{a: 4}`, 
`{h: 1, e: 1, l: 2, o: 1}`
or should I return object with all letters 
`{a: 4, b: 0, c: 0, d: }...`.

➡️2. **Progress to more complex examples**

```js
  chartCount('My phone number is 180295')
  chartCount('Hello hi')
```

Should I count numbers, spaces, Should capital letters be counted the same as smaller ones? or should we store them differently ?

➡️3. **Explore examples with empty inputs and invalid inputs**

```js
  chartCount()
  chartCount("")
  chartCount({})
  chartCount("$#1")
```

Should we return an empty object in this case or null or undefined?

### Step 3: Break it down

Explicitly write out the steps you need to take, this forces you to think about the code  you'll write before you write it, and help you catch any lingering conceptual issues or misunderstandings before you dive in and have to worry about details like language  syntax...

Let's explore the same example as before

> Write a function which takes in a string and returns counts of each character in the string.

```js
  function chartCount(str) {
    // make object to return at the end
    // loop over the string
    // look at each character if exist already in our object
    // if the character is a letter and is a key in the object, add one to count
    // if the character is a letter and not in the object, add it to the object and set value to 1
    // if character is something else (space, period, etc.) don't do anything
    // return object at the end
  }
```

This is a simple problem we can solve it without doing theses steps, but for complicated problems it realy can be a life saver.

### Step 4: Solve or Simplify

Solve the problem if you can, else try to ignore the hard part.

**How to Simplify the problem?**

1. Find the core difficulty in what you're trying to do
2. Temporary ignore that difficulty
3. Write a simplified solution
4. Then incorporate that difficulty back in

So one more time, Let's return to this example.

> Write a function which takes in a string and returns counts of each character in the string.

```js
  function chartCount(str) {
    // make object to return at the end
    const obj = {}

    // loop over the string
    for (let letter of str) {
      // look at each character if exist already in our object
      if (letter in count) {
        // if the character is a letter and is a key in the object, add one to count
        obj[letter]++
      }
      else {
        // if the character is a letter and not in the object, add it to the object and set value to 1
        obj[letter] = 1
      }
    }
    // return object at the end
    return obj
  }
```

This is a simplified solution, it works for simple input, but I ignored the case when the user enter space or number temporary, because I found that it is the most hard part.

After focusing only in the hard part, I finished finding three different solutions like using regex `/[a-z]/`, creating a new array containing all valid characters and checking if the letter exist in the array, or using `charCodeAt`.

### Step 5: Look back and Refactor

Congrats on solving it, but you're not done!
It's important to ask some questions if you want improve your solution.

* Can you check the result?
* Can you derive the result differently?
* Can you understand it at glance?
* Can you use the result or method for some other problem?
* Can you improve the performance of your solution?
* Can you think of other ways to refactor?
* How have other people solve this problem?

Let's explore the new solutions after refactoring the old one.

```js
  function chartCount(str) {
    const obj = {}

    for (let letter of str) {
      letter = letter.toLowerCase()
      const code = letter.charCodeAt(0)
      if ((code > 96 && code < 123)) // lower alpha (a-z)
      obj[letter] = ++obj[letter] || 1
    }
    return obj
  }
```

We end up finding a good solution to our problem, you can apply this approach to any programming problem you encountered.
