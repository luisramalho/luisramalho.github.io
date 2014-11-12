---
layout: post
title: Project Euler — Problem 31
category: euler
---

[Coin sums](https://projecteuler.net/problem=31) is a problem where one must count how many different ways a £2 coin can be made using any number of coins. Firstly, I tried to tackle this problem using brute-force, as I usually go about it. However, in this particular case and because there were so many coins (aka 8), creating a `for loop` for each and every coin was not a solution that I'd be happy with.

Thus, and because none of the algorithms that came to mind applied here I turned my eyes to other possible solutions in the www. In this research I found a very clever solution by [Bradley](http://bradleymize.com/project-euler-problem-31-coin-sums/), which introduced me to [Integer Partition](http://en.wikipedia.org/wiki/Partition_(number_theory)). If you are not familiar, basically:

> In number theory and combinatorics, a partition of a positive integer n, also called an integer partition, is a way of writing n as a sum of positive integers. Two sums that differ only in the order of their summands are considered the same partition.

Armed with this new knowledge, I was able to easily implement the [pseudo-code](http://www.algorithmist.com/index.php/Coin_Change) and obtain the right answer for the problem.

{% highlight java %}
int[] coins = {1, 2, 5, 10, 20, 50, 100, 200};
return count(200, coins.length - 1, coins);
{% endhighlight %}

{% highlight java %}
int count(int n, int m, int[] coins) {
    if (n == 0) {
        return 1;
    }
    if (n < 0) {
        return 0;
    }
    if (m < 0 && n >= 1) {
        return 0;
    }
    return count(n, m - 1, coins) + count(n - coins[m], m, coins);
}
return result;
{% endhighlight %}

The full solution can be found [here](https://github.com/luisramalho/euler/blob/master/Problem031.java).
