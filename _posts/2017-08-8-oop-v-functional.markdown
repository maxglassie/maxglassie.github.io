---
layout: post
title:  "Joy Reading SICP: Musings on OOP and functional programming from Chapter 3 "
date:   2017-07-17 14:30 -0600
categories: clojure
tags:
    -clojure
    -data structures
---

Is it weird that I read SICP to relax before bed? Recently, I've been thinking a lot about a quote from the introduction of Chapter 3 - Modularity, Objects, and State.

"To a large extent, then, the way we organize a large program is dictated by our perception of the system to be modeled. In this chapter we will investigate two prominent organizational strategies arising from two rather different ‘‘world views’’ of the structure of systems. The first organizational strategy concentrates on objects, viewing a large system as a collection of distinct objects whose behaviors may change over time. An alternative organizational strategy concentrates on the streams of information that flow in the system, much as an electrical engineer views a signal-processing system."

This is super interesting to me... the contrasting ways of looking at the system to be modeled through object oriented versus a functional programming lens. This idea of visualizing streams of information paradoxically came back into my mind when looking at some similar coding exercises focused on creating objects and classes in Ruby.

It's a simple Door class. It can be queried for a status, which changes. Ex: `door.locked?`
``` ruby
class Door
  attr_accessor :locked

  def initialize
    @locked = true
  end

  def locked?
    @locked
  end

  def unlock
    @locked = false
  end
end
```

I am thinking about how essentially, what this class does is define a data structure using a set of selector and constructor methods, as Hal and Gerry say in 2.1 on data abstraction:

"The basic idea of data abstraction is to structure the programs that are to use compound data objects so that they operate on ‘‘abstract data.’’ That is, our programs should use data in such a way as to make no assumptions about the data that are not strictly necessary for performing the task at hand. At the same time, a ‘‘concrete’’ data representation is defined independent of the programs that use the data. The interface between these two parts of our system will be a set of procedures, called selectors and constructors, that implement the abstract data in terms of the concrete representation. To illustrate this technique, we will consider how to design a set of procedures for manipulating rational numbers."

In Scheme, we could think of a door as a tagged data object, essentially a list that uses symbolic data:
``` racket
('door 'locked? true )
```

And we could also write a predicate procedure that determines if the door object's locked status is set to true.
