# FST Oriented Programming

A modern take on an old pattern.

Or

A software developer applies an old hardware concept to his code.

> What has been will be again,
> what has been done will be done again;
> there is nothing new under the sun.

## What is it?

FST is short for Finite State Transducer.
A Finite State Transducer is a special class of Finite State Machine.

FST Oriented Programming means you write your software to fit the model of an FST.

## Why should I care?

Computers are physical machines that execute physical operations in the physical world. As software developers, we do not physically operate these machines. Instead, we use language to tell computers what to do through various programming languages, patterns, and idioms. Language is an abstraction that allows us to represent complex physical operations in small words and phrases. Abstractions can distill large, complex things into small things, but they can also be misleading.

I believe that using languages, patterns, and idioms that are 'closer' to what a computer physically does leads to better software. Computers are state machines. Embodying that concept in the language of programs is just a gosh-darn good idea.

#### Also...

It's a really good development pattern for building asynchronous non-blocking systems.

### First an aside. An Abstraction distraction, if you will.

There are some words that are going to come up over and over again. Make note of them.

- Language
- Abstraction
- Symbol
- Encoding

What does it mean that language is an abstraction? At a dinner party, I can use language to ask another physical person to hand me the salt instead of miming the action or operating their body for them by walking over and grabbing their arm, and moving it to the salt, and putting their fingers around the salt, and then moving their arm over towards my seat at the table. That would make for a very awkward dining experience. Language allows us to use symbols to represent things and actions in the physical world. We can encode things from the physical world in a compact format. We abstract away every little detail and preserve just enough information to represent the important features.

So, in computer land, I can write the 22 character phrase

```
println("Hello World")
```

instead of manually flipping however many hundreds or thousands or millions of bits required to make the computer physically display the string `Hello World`. In this case, we have built up many layers of abstraction. The command `println` is an abstraction for some lower level language operations, which itself is probably an abstraction for some lower level language operations, and so on, until we get to the physical hardware.

Abstraction is powerful. It allows us to perform complex computing operations with relatively small commands. However, it can also cause a great deal of confusion. Remember, an abstraction for something is different than the thing itself. If I say "that bird is beautiful", I am using the word "bird" to represent a particular real bird. I am encoding the real bird in 4 letters. All kinds of information is lost - what kind of bird? what color? how big? where is it?

Now, think about layers of abstraction. If each abstraction can lose information, what happens when you have 2 layers of abstraction? Or 3? Or 10? You can compound the information loss to the point where the top layer looks nothing like the bottom layer.

In software development, many of the best abstractions are those that preserve the character of the underlying physical operations as much as possible. It easy to understand and reason about code that maps clearly to what the computer is actually doing.

Alright, let's get back to some state machines.

## State Machines

Computers are state machines.
Take a look at the early computational models which informed the design of today's computers.
TODO - Turing, Von neumann, etc. put some diagrams in here.

### Finite State Machine

In a Finite State Machine (FSM for short), there is:

- A set of possible states
- A set of possible inputs
- A transition function which maps a (state, input) pair to a state (the 'next' state).

In programming terms, an FSM has:

- A type S, representing possible states
- A type I, representing possible inputs
- An idempotent function whose signature is `(S, I) => S`. This is called the transition function.

The transition function is idempotent because...
For a given a pair `(s: S, i: I)`, calling `f(s, i)` must always return the same value.
Put another way, the following test should always pass:

```
let r1 = f(s, i)
let r2 = f(s, i)

assertEquals(r1, r2) // true
```

### Finite State Transducer

A Finite State Transducer extends the concept of a Finite State Machine to include outputs.

In programming terms, an FST has:

- A type S, representing possible states
- A type I, representing possible inputs
- A type O, representing possible outputs
- An idempotent function whose signature is `(S, I) => (S, Array<O>)`. This is called the transition function.

Again, calling the transition function with the same arguments should always yield the same return values. Aka, the following test should always pass:

```
let (r1_s, r1_o) = f(s, i)
let (r2_s, r2_o) = f(s, i)

assertEquals(r1, r2) // true
```

TODO - compare to early computer model diagrams - very similar

TODO - link these to redux, elm, zio, etc. remark on how these 'new' libraries are just using a very old concept.
