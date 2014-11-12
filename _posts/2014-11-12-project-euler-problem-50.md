---
layout: post
title: Project Euler — Problem 50
category: euler
---

Today is a good day! I'm among the 7% that solved 50 Euler problems. Woohoo! Ok, ok! Enough bragging, so the problem 50 is called [consecutive prime sum](https://projecteuler.net/problem=50) in which one must find the prime, below one-million, that can be written as the sum of the most consecutive primes.

My first reaction was to compute the sum of all consecutive prime numbers until I got 1 million, then if that number was not a prime itself I would start removing the lowest primes and seeing if there's space to add the next largest prime. 

{% highlight java %}
int limit = 1_000_000;
ArrayList<Integer> primes = getPrimes(0, limit);

int sum = 0;
int i = 0;
while (sum + primes.get(i) < limit) {
    sum += primes.get(i);
    i++;
}

int start = 0;
int end = i;
while (!isPrime(sum)) {
    sum -= primes.get(start);
    while (sum + primes.get(end) < limit) {
        sum += primes.get(end);
        end++;
    }
    end = i;
    start++;
}

return sum;
{% endhighlight %}

The full solution can be found [here](https://github.com/luisramalho/euler/blob/master/Problem050.java).
