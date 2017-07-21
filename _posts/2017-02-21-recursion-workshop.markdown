---
layout: post
title:  "We Had a Blast Running a Recursion Workshop"
date:   2017-07-17 14:30 -0600
categories: recursion, LISP, workshop
tags:
    -recursion
    -LISP
    -SICP
---

One of the highlights of Module Two at Turing last February was running a recursion workshop with Courtney Meyerhofer. Recursion can be tricky. We wanted to give an understanding of how recursion works and to provide tools for approaching writing recursive procedures. We used examples in LISP from the Structure and Interpretation of Computer Programs (SICP) by Hal Abelson and Gerry Sussman for the workshop.

You can checkout our [Github Repo](https://github.com/maxglassie/recursion_workshop) for implementation of some simple recursive procedures in both LISP and Ruby.

### Goals
1. Learning to read code
2. Learning to run code on a whiteboard
3. Tools: patterns to use

### What is Recursion Anyway?
Simply put, recursion is a procedure that calls itself in its definition. We'll provide some examples below.

### Reading Code
One of my favorite aspects of programming is the syntax. LISP is a wonderful language because it's simple enough to learn in an afternoon. That simplicity allows us to get to theoretical depth much faster than with other languages.

I find it very valuable (and fun) to read code. I like looking at a procedure and breaking it down into it's syntax. We had our students look at a simple LISP procedure and then articulate the syntax.

```racket
(define (square x) (* x x))
```
This breaks down to:
```racket
(define (<name><formal parameters>) (<procedure body>)
```
When we increase the complexity of a procedure, this becomes more helpful.
```racket
; define a procedure named "abs" that takes an argument "x"
(define (abs x) 
; procedure body
; if (<predicate>) evaluates to true
  (if (> x 0)
; return <consequent>
      x
; else, return <alternative>
      (- x)))
```

### Running Code on a Whiteboard
Sometimes our computers become a crutch. Running simple procedures on a whiteboard really helps me understand how the function works and how the inputs flow through the procedure.

Here's our first example of a recursive procedure. We'll write out the syntax and then run it. 
```racket
(define (factorial n)
  (if (= n 1)
       1
      (* n (factorial (- n 1)))))
```

```racket
; a procedure with the name "factorial" that takes an argument "n"
(define (factorial n)
; procedure (<body>)
; if "n" is equal to 1 (a predicate expression)
  (if (= n 1)
; return the consequent
       1
; else, multiply n by the procedure factorial with the argument "n" minus 1
      (* n (factorial (- n 1)))))
```

For my Rubyists:
```ruby
def factorial(number)
  return 1 if number == 1
  number * (factorial(number - 1))
end
```
We can see that this is a recursive procedure - it calls itself in the definition. It's worthwhile pausing here to point out something that all recursive procedures have in common: a stopping condition. In this case, the procedure body says "when n = 1, return 1" rather than running the procedure again with "n - 1" as the argument. If this stopping condition wasn't present, we would create an infinite loop. 

Now let's run the code. Say (= n 3)
```racket
(factorial 3)
; is three equal to one? no, so return 
(if (= 3 1)) 
; the alternative
(* 3 (factorial (2)))

; it's worthwhile noting here that we don't evaluate the full expression until the stopping condition is met
; so go ahead and run (factorial (2))
; is two equal to one? no, so return 
(if (= 2 1))
; the alternative - which gives us this
(* 3 (* 2 (factorial (1))))
; is one equal to one? yes! so 
(if (= 1 1))
; return the consequent
(1)
; and evaluate the expression, starting with the innermost expression
(* 3 (*2 (1)))
(* 3 (2))
(6)
; and now we know that 3! equals 6.
```

### Patterns to Use
I once read somewhere that factorial should be defined as "the function used to teach recursion to computer science students." It's a simple procedure but it shows some key patterns that are at the heart of writing recursive procedures. I can see a few patterns. 

* All recursive procedures involve case logic. This means the presence of an "if-else" statement or something similar. 
* The case must always include a stopping condition. Without a stopping condition, we will create an infinite loop.   

There is another deeper, hidden pattern here. The way that we evaluated the expression above shows that frequently in recursive procedures, we see "delayed evaluation." From the above example, it's only after we hit the stopping condition that the multiplication takes place. 

Here with a larger factorial to show this more concretely:
```racket
(* 6 (* 5 (*4 (*3 (* 2 (1))))))
```
We can think of these variables as staying on the bottom of a "stack", waiting to be evaluated until the stopping condition is met. A recursive procedure that has this delayed evaluation property creates a "linear recursive" process.

This is in contrast to the following procedure, which creates a "linear iterative" process. Not all languages are capable of evaluating an procedure like this in constant space, those that can are called "tail recursive" languages. Both LISP and Elixir are tail recursive. Essentially what happens is that the variables are updated in current memory rather than having their values pushed onto the stack. (For more discussion on how this works see both 1.2.1 "Linear Recursion and Iteration" and 5.4.2 "Sequence Evaluation and Tail Recursion" of SICP.)

If you want to see the difference in evaluation, go ahead and run the procedure on a whiteboard!

```racket
(define (factorial n)
  (fact-iter 1 1 n))

(define (fact-iter product counter max-count)
  (if (> counter max-count)
      product
      (fact-iter (* counter product)
                 (+ counter 1)
                 max-count)))
```

Here's to get you started
```racket
(fact-iter 1 1 6)
(fact-iter 1 2 6)
(fact-iter 2 3 6)
...
```
