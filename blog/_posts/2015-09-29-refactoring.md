---
layout: post
title:  "You can't refactor what doesn't exist; or, Astrology is just the worst"
date:   2015-09-29 9:00:00
categories:
tags: code, refactoring
image: /blog/assets/article_images/2015-09-29-refactoring/galaxy.jpg
---
*I mean only mild disrespect for astrology in this post. Just kidding. Astrology really just provides a nice framework for the ideas I want to explore. I'm sure there are nuances that I don't understand.*

### tl;dr
Don't worry too much about the mess problem solving necessitates. Trying to clean up a mess that isn't complete will probably lead to bigger, more abstract mess. Make your code work, then make it something that someone else will be happy to work with.

## Messes are sort of ok. Sort of.
I have this problem: I like things to be neat. I especially like things I am working on to be neat.

For a while, I cut cheese for a living.

![](https://media.giphy.com/media/VNzCSWznRUP7i/giphy.gif 'bird fart')

I would thoroughly clean my table, line it with a fine cut of butcher paper, bring out a nicely polished cheese wire, slap a wheel down and get to work. I'd repeat this process for each wheel I cut.

The problem is that this quickly becomes a bit inefficient: cutting cheese is messy, and I was trying to make the whole process tidy. I was constantly cleaning up the very mess I needed to make.

Consider a coworker's approach: he would come in and just go nuts, cutting tons of cheese and making a huge mess.

We both produced a good end product—but he produced a whole lot more.

![](https://media.giphy.com/media/QeaI6Qj46pPuo/giphy.gif 'Magic')

The point is, writing code, especially when you are trying to solve a particular problem, is messy. And that's ok. It's important to allow yourself the space to create a working draft that accomplishes your goal. If you don't you'll wind up side-tracked from the task-at-hand. In other words, you set out to solve problem `x`, but along the way you decide you want to make your sketch of `x` a little prettier. You've now shifted your focus away from `x` and onto some meta information *about* `x`—but you're still not totally sure what the hell `x` should be.

## Bad abstraction isn't ok
Astrology is probably cool in a human, story-telling sort of way. However, it's super bad at what it claims to be, if we take that it claims to be a way of predicting or explaining behavior and events based on observations of sky.

The observations have been super important, and incredibly detailed, but the abstraction built from those observations is a bit silly. The position of a star that is so far away that it might not actually even be there anymore and you simply just don't know it yet, probably didn't effect your ride on the subway this morning. Nor did it determine certain life-long traits for you that make you more compatible with some people and less compatible with others.

![](https://media.giphy.com/media/WLfh70QlAAzrYQrVJe/giphy.gif)

The same thing happens when I start refactoring an incomplete idea in code. I start making certain assumptions about the code that are not based on the reality of its application. This is bad. This leads to code that is illogical and wanders in an almost aimless way, unless the aim was to simply write really tiny methods... but then, what do you call all these tiny methods? I have no idea, because I have no idea what it's supposed to do. It's a mess. Not a useful mess, just a regular mess.

## So. How to?
Yeah. Totally.

#### 1. Make it work
Write code, solve problems, go nuts. Don't clean up unless it totally makes sense. *"What about DRY and all the fun stuff that someone wrote in a book?"* Don't worry too much about it. Not yet. Things that are written in books are put there because they apply to making code easy for other people to read/understand/work with. You aren't there yet. That's meta stuff, you are still just in the stuff.

#### 2. Make it right
Now that your code does what you want it to do, get up, take a little walk, come back and read through it. Follow your methods and see how easily the code tells the story of what is actually happening. Think about all of those things written in books, and apply them where it makes sense. Enforce a stylesheet.

#### 3. Make it right, again. For next time.
Think about the possibility that someone who you may never meet may someday have to deal with the code you are writing. Be really nice to that person. That person, very likely, will often be future-you. Don't make too many assumptions about that person, just make your code flexible. Like a peacock with the face of a monkey. Get it? Frozen? Yeah? Whatever.
