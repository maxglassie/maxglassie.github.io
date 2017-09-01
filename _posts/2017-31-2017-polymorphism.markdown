---
layout: post
title:  "The True Value of Polymorphism: Building Abstraction Barriers!"
date:   2017-08-31 14:30 -0600
tags:
    -polymorphism
    -Clojure
    -multimethods
    -functional programming
---

What is polymorphism? And how can it help us write better code? What does it look like in a functional language?

To get started, here’s the definition from [Wikipeida](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)): "polymorphism is the provision of a single interface to entities of different types.""

The fundamental idea behind polymorphism is "dispatch on type." In the simple Ruby example below, we call the `length` method on an array and on a string. From our perspective as programmers, the method looks the same, but under the hood the interpreter is running a different method for each type.

(It's arguable that this is not the best example of polymorphism in Ruby... check out this [blog post](https://robots.thoughtbot.com/back-to-basics-polymorphism-and-ruby) from Thoughtbot for others which may be more clear. I'm choosing to do this because it emphasizes the idea of dispatch on type and an abstraction barrier.)

``` Ruby
array = [1, 2, 3, 4, 5]
string = "12345"

array.length
=> 5

string.length
=> 5
```

It's like the interpreter says, "I'm calling length on a string! Oh, I have to find the length method for an Object of the type string and run it."

The important point is that the interface appears the same to the programmer. The internals of how `length` is run, which are likely different for a string and an array, are abstracted away.

Hal and Gerry talk about how this concept of dispatch on type can help us build abstraction barriers in our programs (SICP 2.4). What does that mean and why do we care?

An abstraction barrier enables me to introduce modularity into my programs. Say, for example, if I was designing the Ruby language and I wanted to change the implementation of `length` for an array to make it more efficient, or for some other reason. I can do this without breaking anyone's programs, since both before and after the changes under the hood, the programmer just calls `array.length`.

A senior developer who is helping me learn Clojure recently assigned me to figure out how to do this.

In this simple example, we have an application that has users and we need a `create-user` function. Clojure is wonderful because it emphasizes modeling the domain using simple data structures rather than objects.

Here we have two maps (like hashes in Ruby) which define a data structure for students and teachers.

``` Clojure
;; def simply binds data to a variable.
;; in Ruby - student = {data}

(def student {:name "Kevin Kool"
              :id "1234"
              :role "student"
              :grade 10})

(def teacher {:name "Teddy Teacher"
              :id "4321"
              :role "teacher"
              :level "Lead Instructor"})
```

Our `create-user` function takes one of these data types as an argument and returns a user. One way that Clojure implements this is using a multimethod.

First, we declare a multimethod using `defmulti`. In essence, what we're doing here is creating a _generic procedure_, which is a "[procedure] that can operate on data that may be represented in more than one way" (SICP 2.4). Our incoming user data is represented differently depending on the type of user - either student or teacher - that is passed to the create-user procedure.

``` Clojure
;; fn is the way to create an anonymous function

(defmulti create-user (fn [user] (:role user)))

```

Then we declare two functions that have the same name. The multimethod will pass the argument to one of these functions depending on the return value of the anonymous function. It simply says, what's the value of the `:role` key in the incoming datum? It's a very simple way of specifying the type of the data.

Clojure abstracts some of this way, but most likely underneath the hood there is something similar to a look-up table, which says, if the role is "student" then pass this datum to the create-user method that takes "student" data types. (Using a lookup table for operations like this is called _data directed programming_ and is covered in SICP 2.4.3.)

``` Clojure
(defmethod create-user "student" [data]
  {:name (:name data)
   :id (:id data)
   :role (:role data)
   :grade (:grade data)
   :access false})

(defmethod create-user "teacher" [data]
  {:name (:name data)
   :id (:id data)
   :role (:role data)
   :level (:level data)
   :access true})
```

Let's take a look at it in the REPL:
```Clojure
(create-user student)

=> {:name "Kevin Kool", :id "1234", :role "student", :grade 10, :access false}

(create-user teacher)
=> {:name "Teddy Teacher", :id "4321", :role "teacher", :level "Lead Instructor", :access true}

```


The real value here is that it enables us to create an abstraction barrier between the create-user function and how it processes new types.

We can build a robust application that only has students and teachers and then if we want to add on a new piece of functionality for a "principal" type user, all we have to do is define a new method for a principal. Everything else will work as it always did.

Or if we want to update the student data type and method, we can work only on that implementation without changing the teacher or principal implementations at all.

This ability to create modularity - meaning that we can take out or change a whole piece of the system without effecting the rest of the system - is at the heart of writing scalable, usable, and ultimately maintainable code.

As Hal and Gerry point out, realistically software evolves over time in response to external demands. It has to change and to get better. It's also important that different people can all work on the same software at the same time, without worrying about whether or not their work will disrupt the work of another team.

It's one of my favorite things to think about in programming.
