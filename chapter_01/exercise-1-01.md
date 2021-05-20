**Exercise 1.1**

> Below is a sequence of expressions. What is the result printed by the interpreter in response to each expression? Assume that the sequence is to be evaluated in the order in which it is presented.

`10`

The result is **10**.

`(+ 5 3 4)`

The result is **12**.

`(- 9 1)`

The result is **8**

`(/ 6 2)`

The result is **3**

`(+ (* 2 4) (- 4 6))`

The result is **6**

`(define a 3)`

Nothing is printed here, though an association between a name *a* and a value **3** is made.

`(define b (+ a 1))`

Nothing is printed here either, though an association between a name *b* and a value *4* is made.

`(+ a b (* a b))`

The result is **19**.

`(= a b)`

The result is **\#f**. 3 does not equal 4.

```scheme
(if (and (> b a) (< b (* a b)))
    b
    a)
```

The result is **4** because the predicate `(and (> b a) (< b (* a b)))` evaluates to true.

```scheme
(cond ((= a 4) 6)
      ((= b 4) (+ 6 7 a))
      (else 25))
```

The result is **16** because the predicate `(= b 4)` is true.

`(+ 2 (if (> b a) b a))`

The result is **6**

```scheme
((* (cond ((> a b) a)
          ((< a b) b)
          (else -1))
    (+ a 1))
```

The result is **16**.
