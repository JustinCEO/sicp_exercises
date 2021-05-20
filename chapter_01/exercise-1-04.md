**Exercise 1.4**

> Observe that our model of evaluation allows for combinations whose operators are compound expressions. Use this observation to describe the behavior of the following procedure:

```scheme
(define (a-plus-abs-b a b)
  ((if (> b 0) + -) a b))
```

How this procedure works:  if *b* is greater than 0, the `+` gets applied as an operator to *a* and *b*. otherwise, the `-` gets applied as an operator to *a* and *b*. The result is that the absolute value of *b* always gets added to *a*.

If we change the value of *b* from positive to negative but leave *a* the same, it won't make a difference to the result, but it will make a difference if we change *a*'s sign. That's just what we see:


![](https://blog.justinmallone.com/content/images/2021/05/test.scm---DrRacket-2021-05-15-19-55-02-1.png)
