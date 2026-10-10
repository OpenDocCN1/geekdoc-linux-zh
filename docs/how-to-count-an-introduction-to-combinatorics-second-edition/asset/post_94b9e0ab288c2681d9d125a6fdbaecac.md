
If you compare the solutions to Problems 2.11 and 4.2, you will see that, in this case, the use of the inclusion–exclusion theorem does not save a lot of work, as in the solution to Problem 2.11 we needed to consider only five different suit distributions. However, with larger hands, where there are many more possible suit distributions, the use of inclusion–exclusion theorem saves a lot of work. This is illustrated by Exercise 4.1.3A.

The next problem involves an application of the inclusion–exclusion theorem of a different kind.

## PROBLEM 4.3

A set of *n* objects is sampled at random with replacement. What is the probability that, after *s* samples have been drawn, each object has been sampled at least once?

### Solution

“Sampling with replacement” means that the set from which the samples are drawn remains the same throughout. It occurs in many different contexts. For example, both bird watchers and train spotters can be thought of as sampling with replacement. Also, when you throw dice, you are sampling the numbers on the dice with replacement, since the set of numbers that can come up on each throw stays the same. Likewise, tossing a coin can be thought of as sampling with replacement the two sides of the coin. These cases are different from problems involving, for example, hands of cards, where, when a card has been drawn from the pack, it cannot be selected again.

Sampling at *random* is intended to mean that any sequence of *s* samples is as likely to be drawn as any other. So the required probability in Problem 4.3 is just the ratio

$$ \frac{ \text{\#(Sequences of } s \text{ samples in which each object occurs)}}{ \text{\#(All sequences of } s \text{ samples)}} , \quad (4.2)$$

We will use $\theta(n,s)$ for this ratio. The number in the denominator of Equation 4.2 is very easy to calculate. As we are sampling with replacement, each time we draw a sample, we have $n$ objects to choose from. Hence a sequence of $s$ samples can be selected in $n^s$ ways.

To calculate the number in the numerator of Equation 4.2, it is easier first to calculate the number of sequences of $s$ samples in which at least one of the objects does *not* occur. We let $A_i$ be the set of those sequences of $s$ samples in which the $i$-th object is missing. The number in the numerator of Equation 4.2 is therefore $n^s - \#(\cup_{i=1}^n A_i)$. Now, by the inclusion–exclusion theorem,

$$ \# \left( \bigcup_{i=1}^n A_i \right) = \sum_{k=1}^n (-1)^{k+1} \left\{ \sum_{1 \leq i_1 < \ldots < i_k \leq n} \#(A_{i_1} \cap \ldots \cap A_{i_k}) \right\}. $$

Here $A_{i_1} \cap \ldots \cap A_{i_k}$ is the set of those sequences of $s$ samples in which $k$ of the objects do not occur, and hence in which each sample may be chosen in $(n-k)$ ways. It follows that $\#(A_{i_1} \cap \ldots \cap A_{i_k}) = (n-k)^s$. Now, there are $C(n,k)$ ways of choosing the $k$ numbers $i_1, \ldots, i_k$ from the set $\{1,2,\ldots,n\}$. Consequently, the numerator of Equation 4.2 is equal to $n^s - \sum_{k=1}^{n} (-1)^{k+1} C(n,k) (n-k)^s$. We can rewrite this as $\sum_{k=0}^{n} (-1)^{k} C(n,k) (n-k)^s$. So the required probability is given by

$\theta(n,s) = \frac{1}{n^s} \sum_{k=0}^{n} (-1)^k C(n,k) (n-k)^s.$

## PROBLEM 4.4

How many times do you need to toss a fair coin to have a probability greater than 0.99 of throwing at least one head and at least one tail?

### Solution

As we noted above, tossing a coin can be viewed as sampling with replacement from the two-element set {H,T}, where H = head and T = tail. So, it is the case of Problem 4.3 with $n = 2$. Consequently, the probability that both a head and a tail are thrown in $s$ tosses is

$\theta(2,s) = \frac{1}{2^s} \sum_{k=0}^{2} (-1)^k C(2,k)(2-k)^s = \frac{1}{2^s}(2^s - 2^{s-1}) = 1 - \frac{1}{2^{s-1}}.$

(Note that in this particularly simple case, we didn’t really need to use the general formula. With $s$ tosses, there are $2^s$ sequences of possible outcomes, of which just two, HH…H and TT…T, do not include at least one head and at least one tail.)

We therefore seek the least $s$ such that $1 - (1/2^{s-1}) > 0.99$. This inequality is equivalent to $2^{s-1} > 100$. The smallest integer $s$ satisfying this last inequality is $s = 8$.

There is no straightforward way to simplify the formula for $\theta(n,s)$ in general. However, in two special cases we can do this.

## THEOREM 4.3

-   a. For all positive integers $n, s$, if $s < n$, then
    $$ \theta(n,s) = \frac{1}{n^s} \sum_{k=0}^{n} (-1)^k C(n,k)(n-k)^s = 0. $$

-   b. For all positive integers $n$,
    $$ \theta(n,n) = \frac{1}{n^n} \sum_{k=0}^{n} (-1)^k C(n,k)(n-k)^n = \frac{n!}{n^n}. $$

### Proof

-   a. When $s < n$ there cannot be a sequence of $s$ samples that includes all the $n$ objects. So in this case $\theta(n,s) = 0$.
-   b. When $s = n$, a sequence of $s$ samples containing each of the $n$ objects must contain each of them just once, and hence is just a permutation of those objects. Now there are $n!$ permutations of $n$ objects, and so $\theta(n,n) = n! / n^n$.

## Exercises

-   4.1.1A  How many integers are there in the range from 1 to 1,000,000 that are either perfect squares or perfect cubes or both?
-   4.1.1B  How many integers are there in the range from 1 to 1,000,000 that are divisible by 7 or 11 or both?
-   4.1.2A  How many integers are there in the range from 1 to 1,000,000 that are divisible by none of 2, 3, 5, and 7?
-   4.1.2B  How many integers are there in the range from 1 to 1,000,000 that are not powers, that is, not of the form $n^k$ where $k,n$ are positive integers with $k \geq 2$?
-   4.1.3A  How many bridge hands (hands of 13 cards drawn from the standard pack of 52 cards) are there that include at least one void suit?
-   4.1.3B  If a pack consists of cards from p suits with n cards in each suit, find a formula for the probability that a hand of n cards from this pack includes at least one card from each suit.
-   4.1.4A  Euler’s $\phi$-function plays an important role in number theory. For each positive integer $n$, $\phi(n)$ is the number of integers in the range from 1 to $n$ that have no prime factors in common with $n$. For example, $\phi(12) = 4$ since there are four positive integers in the range from 1 to 12 that have no prime factors in common with 12, namely, 1, 5, 7, and 11.

    Use the inclusion–exclusion theorem to show that, if the distinct prime factors of $n$ are $p_1,p_2,\dots,p_k$ then

    $$ \phi(n) = n\left(1 - \frac{1}{p_1}\right)\left(1 - \frac{1}{p_2}\right)\cdots\left(1 - \frac{1}{p_k}\right). $$

-   4.1.4B  Calculate the values of (a) $\phi(1,000,000)$ and (b) $\phi(7!)$, that is, $\phi(5040)$.
-   4.1.5A  How many times do you need to throw a standard die so that there is a probability greater than 0.5 that each of the numbers 1, 2, 3, 4, 5, and 6 is thrown at least once?
-   4.1.5B  If two coins are tossed, there are four equally likely outcomes, HH, HT, TH, and TT. How many times do you need to toss two coins so that there is a probability greater than 0.9 that each of these outcomes occurs at least once?
-   4.1.6A  Suppose that the sets $X_i$ for $1 \leq i \leq n$ are pairwise disjoint, and each contains p elements. Let $X = \bigcup_{i=1}^{n} X_i$. Show that if X is sampled with replacement at random, the probability that a sequence of s samples contains at least one element from each of the sets $X_i$ is $\theta(n,s)$, that is, it is independent of p.
-   4.1.6B  A bag contains equal numbers of red, green, blue, and yellow balls. One ball is drawn at random from the bag and then replaced. If this is done eight times, what is the probability that at least one ball of each color is drawn from the bag?
-   4.1.7A  Cards are drawn at random from a standard pack and then replaced. How many times do you need to do this to have a probability of more than 0.99 that you have drawn at least one card of each rank?
-   4.1.7B  Cards are drawn at random from a standard pack and then replaced. How many times do you need to do this to have a probability of more than 0.99 that you have drawn at least one card of each suit?
