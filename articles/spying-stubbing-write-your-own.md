---
author: Maximilianos
status: draft
title: Creating our own Spies and Stubs in Javascript
description: Testing software applications is very important
             but testing comes with its own set of concepts
             and tools that one must become familiar with. In
             this post I want to dive a little deeper into the
             concepts of spying and stubbing in JavaScript
             tests.
---

So the other day at work we were given a presentation by
one of our tech leads on the topic of testing the hybrid
mobile apps our teams are building. After it was done, we
sat around the table chatting away about unit tests,
functional tests, whether we should be writing tests before
we write a feature or after, and so on.

Most of the people in the room had been writing JavaScript
tests for years. For me on the other hand, this was the
first project I was involved with where testing was taken
seriously. So at some point when a few of my team members 
started talking about spying and stubbing in tests, my ears
pricked up because it was something that I had been working
with earlier in the day without really understanding and I 
was eager to sort it out in my head.

Interestingly, though almost everyone in the room had been
using spying and stubbing in the tests they were writing, a
consensus on how they worked was never reached. People 
could not seem to agree on whether a spy was a superset of
a stub for instance or whether