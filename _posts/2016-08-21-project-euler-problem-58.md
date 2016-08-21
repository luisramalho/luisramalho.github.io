---
layout: post
title: Project Euler — Problem 58
category: euler
comments: true
---

[Spiral primes](https://projecteuler.net/problem=58) is a problem in which one must find the side length of the square spiral for which the ratio of primes along both diagonals first falls below 10%. More information on this spiral can be found on [Ulam spiral](http://en.wikipedia.org/wiki/Ulam_spiral).

In order to solve this problem I started by creating an `ArrayList` of all the diagonal numbers and check for their primality. However, creating an `ArrayList` from scratch for every loop was inefficient and soon I have implemented a method to return just the diagonal numbers for the current loop:

{% highlight java %}
private ArrayList<Integer> getDiagonalNumbersForLoop(int n) {
    ArrayList<Integer> diagonalNumbers = new ArrayList<>();
    if (n < 1) return diagonalNumbers;

    int offset = (n * 2) - 2;
    int currentDiagonalNumber = getFirstDiagonal(n);
    int lastDiagonalNumber = getLastDiagonal(n);

    diagonalNumbers.add(currentDiagonalNumber);
    while (currentDiagonalNumber != lastDiagonalNumber) {
        currentDiagonalNumber += offset;
        diagonalNumbers.add(currentDiagonalNumber);
    }

    return diagonalNumbers;
}

private int getFirstDiagonal(int n) {
    return getLastDiagonal(n) - (n - 1) * 6;
}

private int getLastDiagonal(int n) {
    int sideLength = n * 2 - 1;
    return sideLength * sideLength;
}
{% endhighlight %}

The `getLastDiagonal()` returns the bottom right diagonal number in the square spiral, so for `n = 2` it returns 9. Afterwards it is straight forward to obtain the first diagonal number with the method `getFirstDiagonal()`, so we get 3 as the first diagonal number in the second spiral square.

Having the first and last diagonal numbers, and the offset between each diagonal number in a certain size `n` square spiral makes it easy to return all the diagonal numbers. 

Thus, one just needs to accumulate the number of primes as we keep adding square spirals and divide by the total number of diagonal numbers.

{% highlight java %}
public int solution() {
    int primes = 0;
    double diagonalNumbers;
    double percentageOfPrimes = 100;
    ArrayList<Integer> numbers;

    int count = 2;
    while (percentageOfPrimes > 10) {
        numbers = getDiagonalNumbersForLoop(count);
        diagonalNumbers = (double) (count * 4 - 3);
        primes += getNumberOfPrimes(numbers);
        percentageOfPrimes = (primes / diagonalNumbers) * 100;
        count++;
    }
    return (count - 1) * 2 - 1;
}
{% endhighlight %}

Took: 136ms.

The full solution can be found [here](https://github.com/luisramalho/euler/blob/master/Problem058.java).
