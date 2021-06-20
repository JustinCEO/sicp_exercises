> Alyssa P. Hacker doesn’t see why if needs to be provided as a special form. “Why can’t I just define it as an ordinary procedure in terms of cond?” she asks. Alyssa’s friend Eva Lu Ator claims this can indeed be done, and she defines a new version of if:

```scheme
(define (new-if predicate
                then-clause 
                else-clause)
  (cond (predicate then-clause)
        (else else-clause)))
```

> Eva demonstrates the program for Alyssa:

```scheme
(new-if (= 2 3) 0 5)
5

(new-if (= 1 1) 0 5)
0
```

> Delighted, Alyssa uses new-if to rewrite the square-root program:

```scheme
(define (sqrt-iter guess x)
  (new-if (good-enough? guess x)
          guess
          (sqrt-iter (improve guess x) x)))
```

> What happens when Alyssa attempts to use this to compute square roots? Explain.

### Short Answer

An infinite loop occurs due to applicative order evaluation and the recursive call in `sqrt-iter`.

### Explanation

The "real" `if` is kind of like a railroad switch that throws the evaluation of the procedure onto one track or the other depending on the truth value of the predicate statement. That's not the general rule though - the general rule is applicative order. `new-if` using a `cond` clause can definitely control what value is returned - we see that with the working examples that Eva demonstrates. But the use of `cond` to build `new-if` doesn't override the applicative order default evaluation order within the body of `new-if`. This means that despite Eva's best intentions, within the body of `sqrt-iter`, the values of the operators and operands will be evaluated. Because there is a recursive call in `sqrt-iter`, this leads to an infinite loop.
