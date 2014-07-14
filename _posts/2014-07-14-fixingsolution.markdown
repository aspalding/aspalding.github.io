---
layout: post
title: "Fixing a problem... By removing code?"
date: 2014-07-14
---

Today I was able to root out a bug that I'd been trying to root out for a couple days. Turns out the solution was to remove several lines of code (an unnecessary set of conditionals) and to add another two lines to a separate source file. The problem I was having resulted from the code smell needless repetition. 

The problem had to do with serving an index.html file automatically if it existed in the current directory. I had a set of conditionals in both my Request and Response classes. I was having trouble rooting out the source of the problem and was almost positive that that both conditionals were required. On a whim I eliminated the conditional in my Request class and tested each of the individual blocks in that conditional. It seemed as if only one of them was required. 

Duplicating the logic in each of my classes introduced needless repetition which also resulted in needless complexity in my code. Simply determining which of the conditionals was required. A big part of agile and TDD is holding off adding more complexity before it is required. Adding that complexity resulted in a lot of confusion, I simply could not trace down where my solution was failing. By rooting out the smell I was able to come to my senses and get rid of redundant code that prevented my program from functioning correctly. 