---
layout: post
title: "Permutations and Combinations"
date: 2014-07-06
---

The past Thursday one of our student apprentices was looking for a cleaner solution to generating all possible sets of a master mind game. Immediately combinations and permutations came to mind. Python provided functions to generate these sets and I quickly decided that we should search ruby docs to see if that was the case for Ruby. Of course, ruby provides four functions that operate on arrays; `combination(n)`, `permutation(n)`, `repeated_combination(n)`, and `repeated_permutation(n)`.

Both combinations and permutations deal with a set of numbers, the number of symbols in that set and the size of the sets to be chosen. To vocally describe the action we might say "Out of this many, pick this many." A [combination][comb] is a list of all possible sets in which the order of the sets is not important eg [1, 2, 3] and [3, 2, 1] are considered equivilent. On the otherhand a [permutation][perm] considers those two sets unique. [Read more][resc].

We knew that we needed 1296 sets to cover each possibility of the game. In accorance, we fired up the irb, made an array of size six, and tested the combination and permutation functions with the argument four along with count. Neither solution worked. However, we examined the output and knew what was missing from the solution. At this point I got back to the task I working on. Within five minutes Laura had found two additional functions repeated_combination and repeated_permutation. The latter function turned out to result in 1296 sets. 

Anyway, a single line function call on an array was able to replace four nested for loops. Dynamic, high level languages provide a lot out of the box! The interpretter allows you to explore what is offered by a language quickly. It is good practice to rely on what is already provided by the language. In addition, using constructs provided by the language are most likely more performant than anything you could construct in the language itself as they are implemented in C! 


[resc]: http://math.stackexchange.com/questions/128048/what-is-the-correct-terminology-for-permutation-combination-formulae-that-allo
[comb]: http://en.wikipedia.org/wiki/Combination
[perm]: http://en.wikipedia.org/wiki/Permutations