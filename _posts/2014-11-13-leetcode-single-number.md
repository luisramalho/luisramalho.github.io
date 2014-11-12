---
layout: post
title: LeetCode's Single Number
---

LeetCode's [Single Number](https://oj.leetcode.com/problems/single-number/) is a problem where an array of integers is given and every element appears twice except for one. The goal is to find that single one.

[XOR](http://en.wikipedia.org/wiki/Exclusive_or) makes this exercise extremely straight forward. The reason being that when you XOR 3 elements, and two of them are repeated then you get the other element. Say `4 ^ 4 ^3` then you get `3`. Thus, the code below will give us the single element in the array that is not repeated.

{% highlight java %}
public class Solution {
    public int singleNumber(int[] a) {
        int x = 0;
        int n = a.length;
        for (int i = 0; i < n; i++) {
            x ^= a[i];
        }
        return x;
    }
}
{% endhighlight %}
