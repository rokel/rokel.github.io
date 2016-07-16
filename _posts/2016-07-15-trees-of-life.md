---
layout: post
title: "Trees of Life"
categories: programming
---

I had lots of free time in between the end of my final university exams and
graduation to explore some ideas that had surfaced. I decided to take the
opportunity to learn some Rust at the same time (perhaps I'll write my thoughts
in another post).

I'm not sure exactly where the idea came from, but at some point when I was
strolling through Bath I started to get interested in how the anatomy of pretty
much any conceivable lifeform can be represented as an acyclic graph. A simple
example is given by simply assigning nodes to each appendage -- a human has a
head, torso and four limbs. Clearly the granularity of the representation is
somewhat arbitrary, and I'm still not sure what the best approach is.

For example, a creature's neck could simply be the edge between the head and
torso nodes, or a node of its own. This is partly dependent on the graph
datastructure used; some libraries such as **petgraph** allow arbitrary weights
to be assigned to both edges and nodes, favouring the former approach. And then
of course we can descend down the rabbit hole further, assigning a node to each
skeletal joint.

Dwarf Fortress was an obvious inspiration for choosing the right level of
precision for interesting game mechanics. For example, a tree structure allows
limbs to be lopped off or infections to spread realistically. Trees are also
easily visualised, and can even be procedurally animated to show locomotion a la
Maxis' *Spore*.

It's a general truism that given a sufficiently abstract representation with
some well-defined constraints, random generation is an obvious route for
fruitful distraction. Accordingly I came up with a simple way of encoding a
bilateral tree as a simple string of integers -- a basic genome. The genome
describes the branching from the original root node, with the special control
character **0** used to backtrack, allowing lots of leaves. Equivalently the
generated tree is a stack of groups of leaves, which can be popped accordingly.

For example, a very basic stick-man can be represented as the genome:

    [1, 2, 0, 1, 2]
    
where the man's head is the root node, followed by the upper torso, arms, lower
torso and legs.

Here's a video of generating a tree in Unity and applying some simple physics
constraints to get a nice layout:

<video src="/assets/anatomygen.webm" autoplay loop></video>

The next steps are to:

1. Determine a way to intuit how sensory organs and other meaningful entities
   can be placed around the anatomy to allow hands, eyes etc. to be assigned
   realistically.
2. Come up with a fitness function for an evolutionary algorithm to filter out
   non-viable anatomies, favour less complexity and so on.
