---
layout: post
title:  "String Equation Algorithm"
date:   2017-08-03 15:30:04 -0400
categories: String Equation Algorithm
---

I received a code challenge recently to write a function that takes in a string as an argument of a mathematical equation and return the solution of the equation. Each character within the equation is separated by a space. I didn't do well during the actual interview IMO because I broke a fundamental rule of code challenges...before you write any code come up with a game plan first! The main reason behind this approach is so you don't go down a path that makes it difficult to dig a way out of it that ends up being the wrong approach.

My goal of this blog is to solve the equation while pointing out where I went wrong so others can avoid the same mistakes I made. 

To make solving this equation even easier the person administering the interview told me the equation would only use the multiplication and addition operators. The first steps I took was writing out an example input to visually have something to go by. 

`'3 * 4 + 5 + 2 * 3'`

Recalling the [order of operations](https://en.wikipedia.org/wiki/Order_of_operations) I recited the rhyme they taught back in grade school: "Please Excuse My Dear Aunt Sally" --> mathematically translates to "Parantheses Exponent Multiplication Division Addition Subtraction". Being told our input will only have multiplication and addition our only concern should be handling any multiplication first followed by addition. 

This seems easy enough, however I immediately forgot this with my initial approach. I started by taking our input and splitting it by the spaces (which is correct), then thought to iterate through the string one character at a time (wrong).

```javascript
function stringToEquation(formula){
  var arr = formula.split(" ");
end
```

The problem with iterating over this new array one character at a time is it creates duplicative work. Our approach should be finding the multiplication operators and solving those first. Looking at the problem I wanted to solve this in one step as opposed to a few small steps to get to our solution. Luckily the administrator gave me a hint at the end recommending I create a new array with the multiplication portion solved first:

```javascript
function stringToEquation(formula){
  var arr = formula.split(" ");
  var solution = 0;
  
  while(arr.indexOf("*") > -1 ){
    var multNums = [Number(arr[arr.indexOf("*") - 1]) * Number(arr[arr.indexOf("*") + 1])];
    arr = arr.slice(0, arr.indexOf("*") - 1).concat(multNums, arr.slice(arr.indexOf("*") + 2));
  };
end
```

While we have multiplication operators in our array `while(arr.indexOf("*") > -1 )` we're taking the element before and the element after and multiplying those values converted to numbers together `var multNums = [Number(arr[arr.indexOf("*") - 1]) * Number(arr[arr.indexOf("*") + 1])];`. Next we're saving over our exisiting split `arr` by concatenating the beginning of the array up to the first element we multiplied, the multiplied numbers, and the remainder of the array from the second element we multiplied `arr = arr.slice(0, arr.indexOf("*") - 1).concat(multNums, arr.slice(arr.indexOf("*") + 2));`. 

Our `arr` before running this section of code and afterwards looks something like this:

![arr](https://rweber87.github.io/log-a-blog/assets/post11/arr.png)

Great! This handles all of the multiplication operators in our array. This next part is relatively simple given we only have addition left to handle. The last step left is to iterate over everything in our new `arr` and add the remaining values to get our solution.

```javascript
function stringToEquation(formula){
  var arr = formula.split(" ");
  var solution = 0;
  
  while(arr.indexOf("*") > -1 ){
    var multNums = [Number(arr[arr.indexOf("*") - 1]) * Number(arr[arr.indexOf("*") + 1])];
    arr = arr.slice(0, arr.indexOf("*") - 1).concat(multNums, arr.slice(arr.indexOf("*") + 2));
  };
  
  arr.forEach(function(el){
    if(el != "+"){
      solution += Number(el)
    };
  });

  return solution;
  
}
```

In our `forEach()` we're only selecting the values that are not our operators and adding them to our defined `var solution` variable at the beginning of our function. 

Once we've solved this problem it becomes really easy to modify our algorithm to handle other operators. Here we've simply added another `while` loop to handle the division operator. You get the point from here. 


```javascript
function stringToEquation(formula){
  var arr = formula.split(" ");
  var solution = 0;
  
  while(arr.indexOf("*") > -1 ){
    var multNums = [Number(arr[arr.indexOf("*") - 1]) * Number(arr[arr.indexOf("*") + 1])];
    arr = arr.slice(0, arr.indexOf("*") - 1).concat(multNums, arr.slice(arr.indexOf("*") + 2));
  };

  while(arr.indexOf("/") > -1 ){
    var divNums = [Number(arr[arr.indexOf("/") - 1]) / Number(arr[arr.indexOf("/") + 1])];
    arr = arr.slice(0, arr.indexOf("/") - 1).concat(divNums, arr.slice(arr.indexOf("/") + 2));
  };

  
  arr.forEach(function(el){
    if(el != "+"){
      solution += Number(el)
    };
  });

  return solution;
  
}

```

The key takeaways I learned from this experience are:

1. Make sure you understand the challenge by going through an example before writing any code (i.e. Take an example from beginning to the end solution)

2. Ensure you follow the specs given so you don't solve for the wrong solution (i.e. Remembering to multiply _before_ you add)

3. Sometimes taking more steps than you think are necessary is in fact the right approach (i.e. Creating a new array with multiplied values then adding the remaining values together)

Questions or comments? Feel free to shoot me an email (click the link below).

[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->