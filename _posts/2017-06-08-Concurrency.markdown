---
layout: post
title:  "Concurrency"
date:   2017-06-08 15:30:04 -0400
categories: Concurrency
---

**Concurrency vs. Parallelism:**

Per wikipedia's definition "...concurrency is the decomposability property of a program, algorithm, or problem  into order-independent or partially-ordered components or units. This means that even if the concurrent units of the program, algorithm, or problem are executed out-of-order or in partial order, the final outcome will remain the same." Asynchronous is one behavior of concurrency.

How does this relate to code that we've written? This allows for a better user experience while giving the illusion of multiple processes being run at the same time. Javascript is a synchronous language that we use in an asynchronous way. Javascript is still a single threaded language - only one function can be running at once, but we use the browser and the server to give the illusion of performing multiple tasks at one given time, like fetching data from an API while rendering something to the DOM.

On the other hand, parallelism is the ability to carry out multuple tasks or calculuations **simultaneously**. Larger problems can be solved more quickly by breaking them down into smaller ones executed at the same time. 

Our brains are hardwired to keep track of things similar to single-threaded languages or in a sequencial manor. We perform one task at a time before moving on to the subsequent one and most things have a standard order of operations. From a computational perspective, this limits the amount of processing that could be done at one time if you have multiple CPU's to delegate multiple tasks. 

**Analogy**

A great analogy to illustrate the difference between concurrenct behavior and parallel behavior involves a rollercoaster. If you get to a rollercoaster that has 30 seats available and they only let one person ride a time is an example of concurrent or asynchronous behavior. You're not able to delegate multiple tasks that can be performed simultaneously. Conversely, parallelism is when you allow 30 people to ride the rollercoaster all at the same time. The biggest advantage this gives us is processing speed through CPU power.

**Javascript Generators**

This bit of research brought me to discover a javascript concept known as generators. Generators have the built in functionality to pause the function and wait for some other operation to complete. It's essentially a function that can be exited to perform another task and later re-entered.  *This sounds awfully siumilar to concurrent behavior.* Let's look at some code:

**Examples**

Below we'll declare a function called `incrementer()` that increments the index by one using a while loop.

```javascript
  function incrementer() {
    var index = 0
    while (index < 3) {
      index++
      console.log(index)
    }   
  }
```

When we call this function the expected behavior is the numbers `0, 1, 2` are printed to the console before the program is exited. What if we wanted to hook into that loop and perform some other task before moving to the next number? That's where javascript generators comes into play.

Let's re-write that same function using our generator notation.

```javascript
  function* incrementer() {
      var index = 0;
        while (index < 3)
        yield index++;
  }

  var inc = incrementer();
```

Above we've delcared the same function with a few new notational differences, and saved it as a variable called `inc`. We've added a star after declaring the function and inserted the term `yield` before incrementing our index. This yield is where the magic happens. The expression is run as normal until the `yield` has been hit in the sequence. To envoke this function we'll need another new syntactical concept called `next()`. 

```javascript
console.log(inc.next().value)
```

Per normal synchronous javascript behavior we would expect this to again print out all the numbers before stopping. We've now wired the function up to stop once the `yield` has been hit allowing us to hook into this method. Everytime this function is envoked it will execute once giving us the capacity to perform other tasks before completing the while condition.

Questions or comments? Feel free to shoot me an email (click the link below).

[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->