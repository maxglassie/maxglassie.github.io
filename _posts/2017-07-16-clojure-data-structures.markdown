---
layout: post
title:  "Learning Clojure: Data Structure Struggles Doing Exercism Exercises"
date:   2017-07-17 14:30 -0600
categories: clojure
tags:
    -clojure
    -data structures
---

Since I graduated from Turing last month, I've spent time studying Clojure. After starting my programming journey with SICP, I've been fascinated with functional programming languages. The model of understanding the world as streams of data as opposed to objects is powerful for managing concurrency and writing efficient and clean code.

I'm familiar with Scheme LISP from that book and the overarching patterns available to write procedures that conform to a functional style. Clojure is a modern, production ready LISP that has a niche, but important, presence in the industry. I'm drawn to it as a natural path forward from SICP, like a moth to flame.

But I've been getting a little burned. The biggest challenge for me thus far has been getting used to the new and powerful data structures and more advanced syntax that Clojure provides. There is significantly more syntactic sugar - the language uses more than just parens. And I am not used to translating to and from the new data structures that Clojure provides.

I recently tried to solve a simple problem on [Exercism.io](http://exercism.io/exercises/clojure/rna-transcription/readme) of transforming a string containing RNA information to DNA.

My idea was to use map to apply a transformative function to the input string. I created a simple conditional statement to take a letter as an input and return an output. Then I attempted to apply this using map in my `to-rna` function definition.

``` clojure
  (defn toRNA
    "transforms the letter from DNA to RNA"
    [l]
    (cond
              (= l "G") "C"
              (= l "C") "G"
              (= l "T") "A"
              (= l "A") "U"))

  (defn to-rna
    "transcribes from DNA to RNA"
    [string]
    (map toRNA (seq string)))
```

When I tried this out in the REPL, I'd get a sequence of nil. `toRNA` worked to return the letter. Map clearly worked over the string, applying the function to each character.

**100 Functions Operate On One Data Structure**

I knew from reading Clojure for the Brave and True that my issue was the manner that the data structures and functions were interacting.

A little background. Clojure is a language that follows the famous quote from Alan Perlis at the beginning of SICP that "It is better to have 100 functions operate on one data structure than to have 10 functions operate on 10 data structures."

This means that Rich Hickey when designing the language made is so all data structures could be transformed into sequences, the equivalent of lists in Scheme LISP, so functions such as map, reduce, and filter can be applied to any data structure. This is the concept of "programming to abstractions" and you can find a better explanation about it's significance for creating sweet sweet code in Chapter 4 of Clojure for the Brave and True. It's powerful and beautiful but learning to use these new tools has been challenging for me.

I couldn't figure it out after a while and so I submitted my incomplete solution in order to see how others approached the code.

The user Jarak-Jakar had a solution that addressed my problems.

**Translating Data Structures: The Solution**

Here's what I found out.

The `seq` function turns a given data type to a sequence. When applied to a string, each character in the string is transformed to a `char`. This means that my original conditional function that was testing for equality based on `(= (l "D"))` and returning a string, was giving me nil values instead.

The map function, once this was corrected, returned a sequence of `char` values and would need to turn back into a string.

There's a function in Clojure called `apply` that can take a function as an argument and apply that function "inside" a given data structure. See the [Clojure docs](https://clojuredocs.org/clojure.core/apply)

In this case, `(str (map toRNA (seq string)))` errors out because string cannot be applied to a sequence. Apply instead makes the function look essentially look like this `(str \U \G \C \A \C \C \A \G \A \A \U \U)` and so it returns `"UGCACCAGAAUU"`.

It's tricky to move to and from data structures. I'm still getting used to it. I think it will be worth it to learn, but it's slow moving right now.

Add a little error handling in there, and the final function is here:

```clojure
(defn toRNA
  "transforms the letter from DNA to RNA"
  [l]
  (cond
            (= l \G) \C
            (= l \C) \G
            (= l \T) \A
            (= l \A) \U
            :else (throw (AssertionError. "Wrong character"))))

(defn to-rna
  "transcribes from DNA to RNA"
  [string]
  (apply str (map toRNA (seq string))))
```
