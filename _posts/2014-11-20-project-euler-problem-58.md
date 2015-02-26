---
layout: post
title: Project Euler — Problem 58
category: euler
comments: true
---

[Spiral primes](https://projecteuler.net/problem=58) is a problem in which one must find the side length of the square spiral for which the ratio of primes along both diagonals first falls below 10%.

[Ulam spiral](http://en.wikipedia.org/wiki/Ulam_spiral)

{% highlight java %}
BigInteger current;
BigInteger sum = BigInteger.ZERO;
for (int i = 1; i <= 1000; i++) {
    current = BigInteger.valueOf(i);
    sum = sum.add(current.pow(i));
}
BigInteger m = BigInteger.valueOf(10000000000l);
return sum.mod(m);
{% endhighlight %}

The full solution can be found [here](https://github.com/luisramalho/euler/blob/master/Problem058.java).
