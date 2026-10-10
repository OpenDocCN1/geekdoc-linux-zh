We see from the form, $38!(20!11!7!)$, of our final expression for the number of sequences made up of 20, 11, and 7, respectively, of the three symbols that we would also obtain this answer if we had, for example, first placed the 11 Ds, then the 7 Ls, and finally the 20 Ws. It also suggests the general result, given as Theorem 2.10.

First, we generalize Problem 2.12. As we know, if we have $k$ different objects, they can be arranged in order in $k!$ ways. However, if all the $k$ objects are indistinguish-able, all these arrangements look the same, and, from this point of view there is just one way to arrange the objects in order. In general, whenever we have a set com-prising both distinguishable and indistinguishable objects, by “different” arrange-ments, we mean arrangements of those objects that can be distinguished from one another. For example, the letters $A, B, C, D$, and $E$ may be arranged in order in $5!$ different ways. However, if all we are interested in is whether a letter is a vowel (V) or a consonant (C), then the sequences $A, B, C, D, E$ and $E, B, C, D, A$ would both be recorded as $V, C, C, C, V$. Regarding the two vowels as indistinguishable and the three consonants as indistinguishable, there are just 10, that is, $C(5,2)$, different ways of arranging these five letters, corresponding to the number of ways of choosing the positions of the two Vs.

# **THEOREM 2.10**

Suppose that for $1 \leq r \leq k$, we have $n_{i}$ objects of type $T_{i}$, where the objects of any given type are indistinguishable but may be distinguished from the objects of any other type. Suppose also that we have $n$ objects in total, so that $\sum_{i=1}^{k} n_{i}=n$. Then the number of different ways of arranging the $n$ objects in order is $n! /\left(n_{1}! n_{2}! \ldots n_{k}!\right)$.

# **Proof**

We have $n$ positions to fill. We can choose $n_{1}$ of these for the objects of type $T_{1}$ in $C\left(n, n_{1}\right)$ ways. When these positions have been chosen, there remain $n-n_{1}$ positions to be filled, and hence positions for the $n_{2}$ objects of type $T_{2}$ may be chosen in $C\left(n-n_{1}, n_{2}\right)$ ways. Then the positions for the $n_{3}$ objects of type $T_{3}$ may be chosen in $C\left(n-n_{1}-n_{2}, n_{3}\right)$ ways, and so on. Therefore, the total number of different ways of choosing positions for the $n$ objects is

```
$\begin{aligned} \mathrm{C}\left(n, n_{1}\right) \times \mathrm{C}\left(n-n_{1}, n_{2}\right) & \times \mathrm{C}\left(n-n_{1}-n_{2}, n_{3}\right) \times \ldots \times \mathrm{C}\left(n-n_{1}-n_{2}-\ldots-n_{k-1}, n_{k}\right) \\ =\frac{n !}{n_{1}!\left(n-n_{1}\right) !} \times \frac{\left(n-n_{1}\right) !}{n_{2}!\left(n-n_{1}-n_{2}\right) !} & \times \frac{\left(n-n_{1}-n_{2}\right) !}{n_{3}!\left(n-n_{1}-n_{2}-n_{3}\right) !} \times \ldots \times \frac{\left(n-n_{1}-n_{2}-\ldots-n_{k-1}\right) !}{n_{k}! 0 !} \\ & =\frac{n !}{n_{1}! n_{2}! \ldots n_{k}!} \end{aligned}$
```

after a lot of canceling. Having obtained the simplified formula by an algebraic argument, we should look for a combinatorial argument that shows why it is correct and that gives us a better understanding of why it is true.

Ignoring first the fact that the objects of each type are indistinguishable, we see that the $n$ objects may be arranged in order in $n!$ different ways. However, since the $n_{1}$ objects of type $T_{1}$ are indistinguishable, we need to divide by $n_{1}$! to allow for the fact