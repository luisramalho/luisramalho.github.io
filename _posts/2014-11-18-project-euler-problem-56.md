---
layout: post
title: Project Euler — Problem 56
category: euler
comments: true
---

[Powerful digit sum](https://projecteuler.net/problem=56) is a problem in which one must find the maximum digital sum considering natural numbers of the form, a^b, where a, b < 100.

Since we are dealing with big numbers, we should use [BigIntegers](https://docs.oracle.com/javase/7/docs/api/java/math/BigInteger.html). This library has the method [pow()](https://docs.oracle.com/javase/7/docs/api/java/math/BigInteger.html#pow(int)) which makes our life easier when calculating powers of BigIntegers.

{% highlight java %}
int max = 0;
BigInteger n;
for (int a = 0; a < 100; a++) {
    for (int b = 0; b < 100; b++) {
        n = BigInteger.valueOf(a).pow(b);
        max = Math.max(digitalSum(n), max);
    }
}
return max;
{% endhighlight %}

Then, it is just a matter of calculating the sum of all the digits in the BigInteger, and returning the maximum.

{% highlight java %}
int sum = 0;
String digits = n.toString();
for (int i = 0; i < digits.length(); i++) {
    sum += (int) digits.charAt(i) - '0';
}
return sum;
{% endhighlight %}

The full solution can be found [here](https://github.com/luisramalho/euler/blob/master/Problem056.java).
