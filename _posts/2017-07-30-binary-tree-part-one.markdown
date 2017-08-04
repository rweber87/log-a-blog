---
layout: post
title:  "Binary Tree: Breadth Vs. Depth Part 1"
date:   2017-07-30 15:30:04 -0400
categories: Binary Tree: Breadth Vs. Depth Part 1
---

The topic of breadth vs. depth specifically relates to how one can touch every point within a binary tree, also known as traversing the tree. In order to fully understand what that means it's important for us to grasp what exactly a binary tree is. According to [Wikipedia.org](https://en.wikipedia.org/wiki/Binary_tree) "a binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child." Below is a picture example of a standard binary tree.    

![binaryTree](https://rweber87.github.io/log-a-blog/assets/post9/binaryTree.png)

Starting from the top, the root node `2` has two childern - `7` as the left node and `5` as the right. `7` has two child nodes `2` as the left node and `6` as the right. I think you get the point from here.

This data structure is different from another type of binary tree known as a binary search tree (BST). The primary difference are the child nodes from the parent nodes. Unlike an unsorted binary tree, a binary search tree's root node's left child is less than the root node, while the right child is greater than the root node. Let's look at a quick example of a binary search tree to see the difference: 

![binaryTree](https://rweber87.github.io/log-a-blog/assets/post9/binarySearchTree.png)

Here we have a root node of `8` with two child nodes. The left child node `3` is in fact less than the parent node, while the right node `10` is greater than the root node. 

But how would you traverse either data structure without repeating a node within the tree? There are two common ways to walk the tree graph using either the breadth technique or the depth technique.

The breadth technique builds up a queue of nodes as we traverse the tree, and removes the element from the queue as we hit each node. Similar to the accounting technique known as [FIFO](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)) the first (or oldest) item to be added to the queue is the first item to be processed.

We'll first build out our node tree using objects with letters as values.

![binaryTree](https://rweber87.github.io/log-a-blog/assets/post9/nodeTree.png)

We've created a root node starting at `A` and have assigned child nodes up until the letter `F` that have ended with a result that looks like this:

![binaryTree](https://rweber87.github.io/log-a-blog/assets/post9/letterTree.png)

Here we've written a function that takes in the whole tree and pushes it into an empty array or our 'queue'. Next we created a while loop that says while there are any elements in the array (because 0 is a falsey value in javascript) then do this next step. The next step is where the traversing magic happens.

```javascript
function breadthFirstTraversal(rootNode) {
  var queue = [];
  queue.push(rootNode);
  while (queue.length) {
    var visitedNode = queue.shift();
    if (visitedNode.left) {
      queue.push(visitedNode.left);
    }
    if (visitedNode.right) {
      queue.push(visitedNode.right);
    }
    console.log('visited:', visitedNode.value);
  }
}
```

We start by shifting the only element in the array or the root node and making that our `visitedNode`. (Reminder: `shift()` removes the first element from an `array` and returns that element). If the `visitedNode` has a left child then `push()` that child into the queue. Do the same if the `visitedNode` has a right node. Because the queue now has two new nodes in it, we continue this process until we reach our base case or the last nodes within our tree. The output of that algorithm is this: 

![binaryTree](https://rweber87.github.io/log-a-blog/assets/post9/algorithmOutput.png)

This breadth technique earned its name from how it traverses the tree. You can see it started from the root node `A` and `console.log`'d the next layer of elements `B` and `C`. Finally it did the last layer of our binary tree and `console.log`'d `D`, `E`, and `F`. I.e. it focuses on going broadly through each layer before moving on to the following one.

Next blog post we'll focus on depth to see how that differs from this technique. 

Questions or comments? Feel free to shoot me an email (click the link below).

[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->