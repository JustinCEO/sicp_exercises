My thoughts on this exercise as I was figuring it out are available on my blog:

https://blog.justinmallone.com/sicp-chapter_1_1-the-elements-of-programming-part-2/#exercise-15-%E2%9C%85

**Exercise 1.5**

> Ben Bitdiddle has invented a test to determine whether the interpreter he is faced with is using applicative-order evaluation or normal-order evaluation. He defines the following two procedures:

```scheme
(define (p) (p))

(define (test x y)
  (if (= x 0)
      0
      y))
```

> Then he evaluates the expression

`(test 0 (p))`

> What behavior will Ben observe with an interpreter that uses applicative-order evaluation? What behavior will he observe with an interpreter that uses normal-order evaluation? Explain your answer. (Assume that the evaluation rule for the special form `if` is the same whether the interpreter is using normal or applicative order: The predicate expression is evaluated first, and the result determines whether to evaluate the consequent or the alternative expression.)

Short summary:

1. in an applicative order language, `test` will infinitely loop due to `p`, which loops infinitely, getting evaluated when `test` is initially invoked.
2. in a normal order language, `test` will return 0, due to only the *x* ever getting evaluated because of how normal order works and how the `if` is constructed.

Explanation:

This problem is testing the reader's understanding of applicative order versus normal order.

[SICP describes](https://sarabander.github.io/sicp/html/1_002e1.xhtml#g_t1_002e1_002e3) the standard evaluation order in Scheme (i.e. applicative) as:

1. Evaluate the subexpressions of the combination.
2. Apply the procedure that is the value of the leftmost subexpression (the operator) to the arguments that are the values of the other subexpressions (the operands).

This contrasts with the normal order approach, [described within section 1.1.5](https://sarabander.github.io/sicp/html/1_002e1.xhtml#g_t1_002e1_002e5), which involves "expanding" the operators until you get down to primitive procedures and only evaluating the operands when you need to.

As applied to this example, the difference in evaluation order is significant.

Since Scheme is an applicative order language, you can test the applicative order result of trying to run `(test 0 (p))` directly. You'll see that you get an infinite loop. Why? Because, as step 1 of the applicative evaluation order we discussed above, Scheme is trying to evaluate the subexpression `(p)`so that it can apply whatever `test` is to it. Because of how `(p)` is written, once it gets evaluated, it loops infinitely.

With normal order evaluation, I think the 0 and `(p)` get passed along unevaluated to the body of `test` until the moment Scheme needs to know the value. I'm not sure this makes much of a difference with 0, since numbers by themselves are just what they are, but it makes a huge difference with `(p)`, because this evaluation order ensures that `(p)` never gets evaluated.  Since the predicate of the `if` in the body of `test`, `(= x 0)`, is true, we just return 0 and never get around to evaluating `(p)`.
