---
layout: post
title: Codility's Genomic Range Query
---

[Genomic Range Query](https://codility.com/demo/take-sample-test/genomic_range_query) is a problem from codility with the goal of finding the minimal nucleotide from a range of sequence DNA. Note that before attempting this problem, you should read the material on [prefix sums](https://codility.com/media/train/3-PrefixSums.pdf).

In order to solve the problem I started by marking the position of each nucleotide in a 2D array. There are 4 nucleotides (A, C, G and T), so `a[0][i]` will mark the position `i` of nucleotide A as `1` if it appears in the string, otherwise `a[0][i]` will have the value of `0`. The same for `a[1][i]` for nucleotide C, and so on.

{% highlight java %}
int[][] a = new int[4][s.length()]; // A, C, G and T
for (int i = 0; i < s.length(); i++) {
    char ch = s.charAt(i);
    switch (ch) {
    case 'A':
        a[0][i]++;
        break;
    case 'C':
        a[1][i]++;
        break;
    case 'G':
        a[2][i]++;
        break;
    case 'T':
        a[3][i]++;
        break;
    default:
        break;
    }
}
{% endhighlight %}

Once we have the position of each nucleotide in the 2D array `a`, we can proceed to compute the prefix sum of each of the nucleotides:

{% highlight java %}
int[][] prefixSum = new int[4][s.length() + 1];
for (int k = 1; k < s.length() + 1; k++) {
    for (int j = 0; j < 4; j++) {
        prefixSum[j][k] = prefixSum[j][k - 1] + a[j][k - 1];
    }
}
{% endhighlight %}

The final step is to return the value of the minimal impact factor of nucleotides contained in the given range. I did that by checking if the difference between the highest range prefix sum and the lowest returns a value above 0, if yes, then it means that a nucleotide of that impact factor must have occured, hence it's our answer and we can break out of the loop.

{% highlight java %}
int[] m = new int[p.length];
for (int i = 0; i < p.length; i++) {
    int x = p[i];
    int y = q[i];
    for (int j = 0; j < 4; j++) {
        if (prefixSum[j][y + 1] - prefixSum[j][x] > 0) {
            m[i] = j + 1;
            break;
        }
    }
}
{% endhighlight %}

The full solution can be found [here](https://github.com/luisramalho/codility/blob/master/L009GenomicRangeQuery.java).
