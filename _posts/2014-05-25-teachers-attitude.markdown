---
layout: post
title:  "Developing a teachers attitude."
date:   2014-05-25
---

This past [8LU][Univ] was my first Friday as an resident at 8th Light. The festivities on Friday put me in a good mood. Furthermore I was able to help one of our novice apprentices with a problem they were facing in their code! Unfortunately, I wasn't quite satisfied with the knowledge I shared, despite finding a solution to the problem at hand.

To elaborate, they were working on an Tic Tac Toe problem in Ruby. She was attempting to recursively call a function thats utility was to check the validity of a move and place a piece on the board. If the move was not valid the function would simply be called again. Fair enough, this sounds like a good enough solution to the problem. I've tried to recreate the problem in pseudocode to elaborate the issue.

{% highlight python %}
def move(position, mark):
  redunant(position)
  game[position] = mark

def redundant(position):
  if not valid:
    out()
    move(*args)
  else:
    move(*args)

def out():
  print "not valid"

def valid(position):
  return this or that
{% endhighlight %}

The apprentice was able to tell me her goal; to recursively call the function to request a new position if the input was not valid. I immediately decided to try and track down her base case and recursive case. Upon realizing that there was no recursive call in the body I asked where she attempting to make her recursive call, it turned out to be in a separate function that I believe was redundant. As a result I suggested that we eliminate this function and simply relocate the conditional in the `move` function, then recursively call the function if an invalid position was given. We arrived at a solution similar to the pseudocode below:

{% highlight python %}
def move(position, mark)
  if not valid(position):
    out()
    move(position, mark) #recursive call
  else #base case
    game[position]

def out():
  print "not valid"

def valid(position):
  return this or that
{% endhighlight %}

Nothing was lost by refactoring the redundant function, and to be honest, the `out` function could be refactored into the move function as well in my opinion. However, I do not think I made a good enough case or gave sufficient enough advice for her to understand exactly why her attempt was unsuccessful and why the revised solution worked.

This interaction made me realize another goal that I'd like to achieve at 8th Light. To be able to express myself vocally (as opposed to written advice, in which I do not struggle as much) in the domain of my career. I realize that this skill will not only help people requesting help from me, but will also enhance my own ability to express issues that I am experiencing myself.

[Univ]: http://university.8thlight.com/
