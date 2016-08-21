---
layout: post
title: Codility's CountFactors
category: codility
comments: true
---

[CountFactors](https://codility.com/demo/take-sample-test/count_factors) is a problem where one must compute the factors of a given number. Note that before attempting this problem, you should read the material on [prime and composite numbers
](https://codility.com/media/train/8-PrimeNumbers.pdf).

We incremente the count by two because based on one divisor, we can find the symmetric divisor. In other words, if _a_ is a divisor of _n_ then _n/a_ is also one. The only case when that does not happen is when is if the number is in the form _k^2_, meaning that the symmetric divisor of _k_ is also _k_.

{% highlight java %}
int i = 1;
int result = 0;
while (i < Math.sqrt(n)) {
    if (n % i == 0) {
        result += 2;
    }
    i++;
}
if (Math.pow(i, 2) == n) {
    result += 1;
}
return result;
{% endhighlight %}

The full solution can be found [here](https://github.com/luisramalho/codility/blob/master/L08E2CountFactors.java).
