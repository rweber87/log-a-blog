---
layout: post
title:  "Binary Tree: Breadth Vs. Depth Part 2"
date:   2017-08-03 15:30:04 -0400
categories: Binary Tree: Breadth Vs. Depth Part 2
---

We've got a good grasp on binary trees and how to traverse them using the breadth strategy. Let's look at another way one can traverse a binary tree utilizing the depth method.

Just as the name suggests, we'll be going to the deepest part of the binary tree every time. Utilizing the example from the last blog post we have a root node starting with `A` that has two child nodes: left child node being `B` and the right child node being `C` etc. 

![binaryTree](https://rweber87.github.io/log-a-blog/assets/post9/letterTree.png)

In the breadth example we visited each layer of the binary tree and touched each node before moving to the subsequent level to do the same thing. Our depth function will be visiting the deepest node until each one has been visited.

While traversing the binary tree with breadth we're creating a queue of each node and running through them one by one (also known as [FIFO](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics))). In this example, we're creating a stack then winding it down. This is also known as [LIFO](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) where the last item added to the array is the first item to be executed.

```javascript
function depthFirstTraversal(rootNode) {
  var stack = [];
  stack.push(rootNode);
  while (stack.length) {
    var visitedNode = stack.pop();
    if (visitedNode.right) {
      stack.push(visitedNode.right);
    }
    if (visitedNode.left) {
      stack.push(visitedNode.left);
    }
    console.log('visited:', visitedNode.value);
  }
}
```

Using our same binary tree example from before our expected output utilizing depth is in this order - `A`, `B`, `D`, `E`, `C`, and finally `F`. Walking through the algorith above we first add the entire node to our stack. 

```javascript
{ value: 'A',
  left: { value: 'B', left: { value: 'D' }, right: { value: 'E' } },
  right: { value: 'C', left: { value: 'F' } } }
```

We visit `A`'s right node (`C`) and add it to our stack followed by `A`'s left node (`B`). The next iteration we do the same process by `pop()`ing the last element from the stack (`B` node) and repeat the same process until our result is as expected. 

![depthTraversalResult](https://rweber87.github.io/log-a-blog/assets/post10/depthTraversalResult.png)

These methods are really great practice when navigating interviews in an engineering capacity! 

Questions or comments? Feel free to shoot me an email (click the link below).

[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->