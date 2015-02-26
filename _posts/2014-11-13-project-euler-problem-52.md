---
layout: post
title: Project Euler — Problem 52
category: euler
comments: true
---

[Permuted multiples](https://projecteuler.net/problem=52) is a problem in which one must find the smallest positive integer, x, such that 2x, 3x, 4x, 5x, and 6x, contain the same digits.

A brute-force solution is to just loop through integers until 2x, 3x, 4x, 5x, and 6x are permuations of one another, when that happens we have found our integer.

{% highlight java %}
int count;
for (int i = 1; ; i++) {
    count = 0;
    for (int j = 2; j < 7; j++) {
        if (isPermutation(i, i * j)) {
            if (++count == 5) {
                return i;
            }
        } else {
            break;
        }
    }
}
{% endhighlight %}

I have used the method below to find is two integers are permutations of one another. Basically, we create an array of numbers which will have indices 0 to 9, and then count how many occurrences are in the first integer. Then, we just do the inverse to the second integer and if they are permuations then the array should be all zeros.

{% highlight java %}
private boolean isPermutation(int x, int y) {
    int[] numbers = new int[10];

    int t = x;
    while (t > 0) {
        numbers[t % 10]++;
        t /= 10;
    }

    t = y;
    while (t > 0) {
        numbers[t % 10]--;
        t /= 10;
    }

    for (int i = 0; i < 10; i++) {
        if (numbers[i] != 0) {
            return false;
        }
    }

    return true;
}
{% endhighlight %}

The full solution can be found [here](https://github.com/luisramalho/euler/blob/master/Problem052.java).
