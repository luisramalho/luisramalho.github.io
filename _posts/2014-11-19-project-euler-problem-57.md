---
layout: post
title: Project Euler — Problem 56
category: euler
---

[Square root convergents](https://projecteuler.net/problem=57) is a problem in which one must find how many fractions of the square root of 2 contain a numerator with more digits than denominator.

Since we are dealing with big numbers, we should use [BigIntegers](https://docs.oracle.com/javase/7/docs/api/java/math/BigInteger.html). Then, a pattern has emerged:

$$
n_{k+1} = 2\cdot n_k + n_{k-1}
$$

$$
d_{k+1} = 2\cdot d_k + d_{k-1}
$$

Above, \\( n \\) is the numerator and \\( d \\) is the denominator.

{% highlight java %}
ArrayList<BigInteger> n = new ArrayList<>();
n.add(BigInteger.valueOf(3)); // first numerator
n.add(BigInteger.valueOf(7)); // second numerator

ArrayList<BigInteger> d = new ArrayList<>();
d.add(BigInteger.valueOf(2)); // first denominator
d.add(BigInteger.valueOf(5)); // second denominator

BigInteger two = BigInteger.valueOf(2);
for (int i = 1; i < 1000; i++) {
    n.add(n.get(i).multiply(two).add(n.get(i - 1)));
    d.add(d.get(i).multiply(two).add(d.get(i - 1)));
}

int count = 0;
for (int i = 0; i < n.size(); i++) {
    if (n.get(i).toString().length() > d.get(i).toString().length()) {
        count++;
    }
}

return count;
{% endhighlight %}

The full solution can be found [here](https://github.com/luisramalho/euler/blob/master/Problem057.java).
