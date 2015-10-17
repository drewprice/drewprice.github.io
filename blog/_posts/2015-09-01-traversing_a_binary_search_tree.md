---
layout: post
title:  "Traversing a binary search tree, with hobbits"
date:   2015-09-01 09:00:00
categories: ruby rails
tags: ruby rails
image: /assets/article_images/2014-11-30-mediator_features/nil
---
*[Exercism.io](http://exercism.io/) is a place to solve programming challenges in a social context. I was introduced to binary search trees through Exercism, and then promptly stumped by the problem of traversing them. Eventually, I gave in and used a method I had found but didn't understand to solve the problem. This is an attempt to understand.*
### tl;dr
The following method will perform an in-order traversal of a binary search tree. Recursion makes it look scary, maybe, but it's not too bad.

```ruby
def traverse(node)
  traverse(node.left) if node.left

  print node.value

  traverse(node.right) if node.right
end
```

## Binary Search Trees
### What is a binary tree?
A binary tree is a way of structuring or storing data, as nodes, where each node is the parent of two child nodes: one node on the left and one node on the right.

This definition makes the whole thing sound a bit ridiculous though.

Instead, imagine a tree.

<a href="http://adventuretime.wikia.com/wiki/To_Cut_a_Woman's_Hair">
![tree witch](/blog/assets/article_images/2015-09-01-traversing_a_binary_search_tree/tree_witch.png 'tree witch')
</a>

Great Job. So if we flip that upside down, we're pretty much there:

```
          o
         / \
        o   o
       /   / \
      o   o   o
```

Each `o` is a node, or a leaf, on the tree. Each leaf can have up to two branches. Through this system, each leaf in the tree is related to every other leaf on the tree.

### What is a binary search tree?
A binary search tree is just a particular type of binary tree. While any old binary tree will store information, a binary search tree adds some important order to this information.

Let's say the leaf at the very top of our tree is `4`. The branch to the right will only ever contain a leaf that is **greater than** `4`, while the branch to the left will only contain a leaf that is **less than** `4`. The same rule is then applied to each leaf individually, and as leaves are added to the tree they start by measuring up to the original leaf, `4`, in this case, and then working their way into the appropriate position.

```
          4
         / \
        3   6
       /   / \
      1   5   7
       \
        2
```
If that still seems a bit weird, [check this out](https://www.youtube.com/watch?v=D5SrAga1pno), and it'll make more sense. There are a lot of really neat perks to storing data this way, which you can learn more about in that link.

## Building a tree
The following code creates a class that is capable of building a binary search tree:

```ruby
class Node
  attr_accessor :value, :left, :right

  def initialize(value)
    @value = value
  end

  def insert(n)
    n < value ? assign_left(n) : assign_right(n)
  end

  private

  def assign_left(n)
    left ? left.insert(n) : self.left = Node.new(n)
  end

  def assign_right(n)
    right ? right.insert(n) : self.right = Node.new(n)
  end
end
```

So given the following:

```ruby
tree = Node.new(4)
tree.insert(3)
tree.insert(6)
tree.insert(1)
tree.insert(5)
tree.insert(2)
tree.insert(7)
```
We begin with `4` as our root node. When `3` is inserted, we compare it to the value of our root node. Because `3` is smaller than `4`, we then check to see if `4` already has a `left` branch. If it does, we then start the process over with the node on the end of that branch, but if it does not have a node we create one and store it there. The process continues like this until we have built a tree that is identical to the one portrayed above.

## Traversing the tree
The idea of iterating, in order, through every element of this tree sort of freaks me out. It's easy enough to do visually, but how do you teach a computer to do this?

Every attempt I made quickly became a huge swarm of nested iterations, lines and lines of code that made my soul ache and my program blow up. But it's just a gross problem, the solution has gotta be super gross—right?

No. Says [the internet](http://stackoverflow.com/questions/4542354/c-print-out-a-binary-search-tree?answertab=votes#tab-top).

```ruby
def traverse(node)
  traverse(node.left) if node.left

  print node.value

  traverse(node.right) if node.right
end
```

That's it. I don't get. Or I didn't. I think I do now, but rather than explaining it in language I really don't understand myself, I'd like to tell the story of a hobbit.

### The Hobbit, or There and Back Again
In a hole in the ground there lived a hobbit. Not a nasty, dirty, dark hole, filled with neckbeards and a cheeto smell, nor yet a dry, bare, computer bunker with nothing in it but scientists and intimidating words: it was a hobbit-hole, and that means comfort.

Our hobbit, Nodo Binaggins, is of the very nosy sort—always snooping about in that which isn't his. His hole in the ground is connected to two other holes. The one on the left is smaller, and the one on the right is larger.

One afternoon, knowing his neighbors have gone out for a smoke, Nodo plucks up the courage to map out he and his neighbors' homes. He wants to lay them all out, in order, from smallest to largest.

His plan is to draw the smallest hole, then come back and draw his own hole before heading to the larger hole and drawing that.

Nodo carefully opens the door leading to the smaller hole. But, here, our hobbit is surprised. Two more doors lead out of this hole, so he quickly chooses the left most door again *(it may be worth mentioning that this story is best imagined from a top-down perspective)*. This hole, he finds, is even smaller than the one he has just come from. There are no more doors, so he draws this hole on the left-most side of his page: it is the smallest hole

Moving quickly, he steps back into the other room, and closes the door. Stopping to think, Nodo assumes that this hole must be just like his own: it has a smaller hole to the left, and a larger hole to the right.

Very good then, he draws this hole as the second smallest, and proceeds into the remaining surprise door. Just as he suspected, this seems to be the third largest hole.

Stepping back out, he closes the door, walks back into his own apartment and closes his neighbor's door.

Nodo then draws his own hole as the fourth largest, knowing that the neighbor on his right has a bigger hole than his. Just to be sure, Nodo opens that door and is, again, surprised to see another door. This time, there is just one, and it's to the right.

Acting on his previous notion, Nodo draws the current hole before opening the other door: it's likely that the other is bigger, and he wants to keep his holes in order.

After drawing the fifth largest hole, Nodo opens up the door to find his suspicion is once again true: this room is bigger than the last. There are no doors leading away from it, so Nodo draws it and returns back into his neighbor's, closes the door, then back into his own home and finally closes that door too.

He has sucessfully mapped the sizes of the surrounding apartments, in order, and made it back to his own apartment without leaving any clue that he had ever been snooping through his poor neighbors' homes.

### So... what the hell?
Nodo, has just pulled off a recursive, in-order traversal of a binary search tree.

In code:

```ruby
def snoop(hole)
  snoop(hole.left) if hole.left

  print hole

  snoop(hole.right) if hole.right
end

```

That's pretty much the same thing as this:

```ruby
def traverse(node)
  traverse(node.left) if node.left

  print node.value

  traverse(node.right) if node.right
end
```
1. Start at the root
2. If there is something on the left, check that out (meaning, repeat step 2 with that node); if not,
3. print the value of the place you are in, then
4. go check out the thing on the right, if there is anything.
5. You've left a trail of 'open doors', these will guide you back to where you started.


## Takeaway
Scary, weird things don't have to be so scary or weird. It took me a few months to understand this answer that the internet generously bestowed upon me, but I really think that's because I let myself be intimidated at the sight of recursion rather than taking time to think through the story of the code.

It's easy to think that computers, with their big fancy algorithms and funky alien syntax, are incomprehensible and magic—but it's also wrong.

Computers only know how to do what people teach them to do, and people cannot do things that are incomprehensible and magic. Excluding wizards. People, if we over simplify it, can really only tell stories. Even if those stories are muddled up with jargon like *recursion* and syntax that makes it look like an octopus is typing, it's still just a story. A weird one to tell. But it is a story.
