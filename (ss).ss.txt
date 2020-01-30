(Scheme R GNU/Linux Emacs Csound C Haskell)
(Cryptography Probability Statistics Bayesian Strategy Categories)
 
; 12/21/2019 16:30. Discussion with CC at FG. Scheme. Org-Mode. Medtronic.
; Focus on making Scheme Toolkit based on Dybvig-2009 and any other code below in this document.

(Formal Syntax)

(Interaction -> Chapter 2)
"yo"
42
22/7
3.141592653
+
(+ 76 31)
(* -12 10)
'(a b c d)

(car '(a b c))
(cdr '(a b c))
(cons 'a '(b c))
(cons (car '(a b c))
      (cdr '(d e f)))

(define square
  (lambda (n)
    (+ n n)))

(square 5)
(square -200)
(square 0.5)
(square -1/2) 

(define reciprocal
  (lambda (n)
    (if (= n 0)
        "grim"
        (/ 1 n))))


Step 0.
-------
Stare at the below Table of Contents from Dybvig-2009. This is the high-level architectural plan of the R6 Scheme language.

1. Introduction
2. Getting Started
3. Going Further
4. Procedures and Variable Bindings
5. Control Operations
6. Operations on Objects
7. Input and Output
8. Syntactic Extension
9. Records
10. Libraries and Top Level Programs
11. Exceptions and Conditions
12. Extended Examples

Step 0
------
Stare at the below Table of Extended Examples from Dybvig-2009. These represent various interesting applications and programming techniques.

1. Matrix and Vector Multiplication
2. Sorting
3. A Set Constructor
4. Word Frequency Counting
5. Scheme Printer
6. Formatted Output
7. A Meta-Circular Interpreter for Scheme
8. Defining Abstract Objects
9. Fast Fourier Transform
10. A Unification Algorithm
11. Multitasking with Engines  

Primary Foci
------------
(2. "Getting Started" 11 57)



; 12/20/2019. (ss).ss begins.

; Four Documents to Work on: ((ss).ss Lu.c El.org Pal.ss (Tr-808))

; (Tr-808)



(ss).ss -> Create this around Cybersecurity/Applied Training Solutions [sic]

(12.7. A Meta-Circular Interpreter for Scheme)

(library (tspl interpreter)
  (export interpret)
  (import (rnrs) (rnrs mutable-pairs))

; primitive-environment contains a small number of primitive
; procedures; it can be extended easily with additional primitives.
(define primitive-environment (...))

; new-env returns a new environment from a formal parameter
; specification, a list of actual parameters, and an outer
; environment. The symbol? test identifies "improper"
; argument lists. Environments are association lists,
; associating variables with values.
(define new-env (...))

; lookup finds the value of the variable var in the environment
; env, using assq. Assumes var is bound in env.
(define lookup
  (lambda (var env)
    (cdr (assq var env))))



(Formal Syntax
  (Datums)
  (Booleans)
  (Characters)
  (Strings)
  (Symbols)
  (Numbers)
  (Lists)
  (Vectors)
  (Bytevectors))


;;; (gcd a b) from SICP
(define (gcd a b)
  (if (= b 0)
      a
      (gcd a (remainder a b))))

GCD(a, b) = GCD(b, r)

GCD(206,40) = GCD(40,6)
            = GCD(6,4)
            = GCD(4,2)
            = GCD(2,0)
            = 2

(Introduction)
(Getting Started)
(Going Further)
(Procedures and Variable Bindings)
(Control Operations)
(Operations on Objects)
(Input and Output)
(Syntactic Extension)
(Records)
(Libraries and Top-Level Programs)
(Exceptions and Conditions)
(Extended Examples)

(Introduction Scheme-Syntax Scheme-Naming-Conventions Typographical-and-Notational-Conventions)

(Sources
  (Abelson-Sussman-1996)
  (Dybvig-2009))

(Hacker Mindset Guide: Shaw Chapter 27, Grimes, etc)


(5.5 "Mapping and Folding")
(-------------------------)
(map abs '(1 -2 3 -4 5 -6)) => (1 2 3 4 5 6)

(map (lambda (x y) (* x y))
     '(1 2 3 4)
     '(8 7 6 5)) => (8 14 18 20)

; Contents (Sections Only)
(1 1.1 "Scheme Syntax" 6)
(2 1.2 "Scheme Naming Conventions" 8)
(3 1.3 "Typographical and Notational Conventions" 9)
(4 2.1 "Interacting with Scheme" 13)
(5 2.2 "Simple Expressions" 16)
(6 2.3 "Evaluating Scheme Expressions" 21)
(7 2.4 "Variables and Let Expressions" 23)
(8 2.5 "Lambda Expressions" 26)
(9 2.6 "Top-Level Definitions" 30)
(10 2.7 "Conditional Expressions" 34)
(11 2.8 "Simple Recursion" 41)
(12 2.9 "Assignment" 47)
(13 3.1 "Syntactic Extension" 59)
(14 3.2 "More Recursion" 65)
(15 3.3 "Continuations" 73)
(16 3.4 "Continuation Passing Style" 78)
(17 3.5 "Internal Definitions" 81)
(18 3.6 "Libraries" 85)

"yo" => "yo"
42 => 42
22/7 => 22/7
3.141592653
+ => #<procedure>
(+ 76 31) => 107
(* -12 10) => = -120
'(a b c d) => (a b c d)

(car '(a b c)) => a
(cdr '(a b c)) => (b c)
(cons 'a '(a b c)) => (a b c)
(cons (car '(a b c))
      (cdr '(d e f))) => (a e f)

(define square
  (lambda (n)
    (* n n)))

(square 5)      => 25
(square -200)   => 40000
(square 0.5)    => 0.25
(square -1/2)   => 1/4

(define reciprocal
  (lambda (n)
    (if (= n 0)
        "Grim!"
        (/ 1 n))))

(load "reciprocal.ss")

(reciprocal 10)                => 1/10
(reciprocal 1/10)              => 10
(reciprocal 0)                 => "Grim!"
(reciprocal (reciprocal 1/10)) => 1/10

