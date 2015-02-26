---
layout: post
title: Project Euler — Problem 55
category: euler
comments: true
---

[Lychrel numbers](https://projecteuler.net/problem=55) is a problem in which one must find how many Lychrel numbers are there below ten-thousand. You can read [here](http://en.wikipedia.org/wiki/Lychrel_number) more about Lychrel numbers.

It was clear since the beginning that we would be dealing with large numbers, so my approach was to use [BigIntegers](https://docs.oracle.com/javase/7/docs/api/java/math/BigInteger.html).

{% highlight java %}
int lychrelNumbers = 0;
int i = 0;
BigInteger temp;
BigInteger one = BigInteger.ONE;
BigInteger b = new BigInteger("10");
BigInteger limit = new BigInteger("10000");
for (; b.compareTo(limit) < 0; b = b.add(one), i = 0) {
    temp = b;
    do {
        temp = temp.add(reverse(temp));
        i++;
    } while (!isPalindrome(temp.toString()) && i < 50);

    // Lychrel number
    if (i == 50) {
        lychrelNumbers++;
    }
}
return lychrelNumbers;
{% endhighlight %}

I started with 10 because 0 to 9 are palindromes. Inside the for loop we check if the addition of a number with it's reverse is a palindrome for a maximum of 49 times. If not, then we got a Lychrel numbers.

The full solution can be found [here](https://github.com/luisramalho/euler/blob/master/Problem055.java).
