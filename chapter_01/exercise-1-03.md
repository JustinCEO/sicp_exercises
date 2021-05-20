Note that I made extensive comments on this exercise on my [blog](https://blog.justinmallone.com/sicp-11-the-elements-of-programming-part-1/#exercise-13-%E2%9C%85), which is where I document my learning process.

**Exercise 1.3**

> Define a procedure that takes three numbers as arguments and returns the sum of the squares of the two larger numbers.


```scheme
(define (square x)
  (* x x))

(define (sum-of-squares x y)
  (+ (square x) (square y)))

(define (sum-of-biggest-squares a b c)
  (cond ((and (<= a b)(<= a c))
         (sum-of-squares b c))
        ((and (<= b c)(<= b a))
         (sum-of-squares a c))
        (else (sum-of-squares a b))))
```

Explanation: The first cond clause checks if *a* is the smallest value and calls sum-of-squares with *b* and *c* if that's the case.

The second cond clause does similar but checks if *b* is the smallest value and calls sum-of-squares with *a* and *c* if that's the case.

If neither *a* nor *b* are the smallest value, then that only leaves *c* as the smallest value, which is addressed in the else clause.
