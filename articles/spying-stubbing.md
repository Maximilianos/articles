---
status: published
published: 08/12/2016
title: Spying & Stubbing in JavaScript
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

[Aside]

[AsideHeader]
If you have not seen what a spy or stub is before, this is 
my understanding of when they are both used:
[/AsideHeader]

In your tests, given you have a function you want to test 
that takes another function as an argument, you may want to
check whether the function you passed in is being called
when you call the parent function. So for example, given:

```javascript
function parent(bool, func) {
  if (bool) {
    func();
  }
}
```

you would test whether the passed in `func` was called
using a **Spy**. In our test suite at work, we use the
Mocha, Chai and Sinon libraries so this would look
something like this for us:

```javascript
it('should call the given function once if bool is true', () => {
  // 1. set up the spy
  const spy = sinon.spy();

  // 2. call the function being tested passing in the spy
  parent(true, spy);

  // 3. test our expectation
  expect(spy.calledOnce).to.be(true);
});

it('should NOT call the given function if bool is false', () => {
  const spy = sinon.spy();
  parent(false, spy);
  expect(spy.called).to.be(false);
});
```

Alternatively it may be the case that the output of the 
function being passed in may be important to the function
being tested. For example, given:

```javascript
function parent(func) {
  return func() ? 'So true' : 'Really false';
}
```

you would test this function by passing in a **Stub** as
the `func` argument and controlling what the stub returns
when it is called; something like this:

```javascript
it('should return "So true" when the given function returns true', () => {
  // 1. set up the stub
  const stub = sinon.stub();
  
  // 2. define what the stub returns when called
  stub.returns(true);
  
  // 3. call the function being tested passing in the stub
  const output = parent(stub);
  
  // 4. test our expectation
  expect(output).to.equal('So true');
});

it('should return "Really false" when the given function returns false', () => {
  const stub = sinon.stub()
  stub.returns(false);
  const output = parent(stub);
  expect(output).to.equal('Really false');
});
```

These are the basics of how you would use spies and stubs
in your tests. We have only scratched the surface of what
libraries like Sinon give you, but I believe this is a good
starting point to be able to understand the concept.

[/Aside]

Interestingly, though almost everyone in the room had been
using spying and stubbing in the tests they were writing, a
consensus on how they worked was never reached. People 
could not seem to agree on whether a spy was a superset of
a stub for instance or whether 

