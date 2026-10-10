# 14.3 THE CYCLE INDEX OF A GROUP

We now begin our description of an algebraic method to calculate the pattern inventory in cases where a group acts on the set of colorings of a figure. Our starting point is the *cycle type* of a permutation, which we introduced in Chapter 11, Section 11.5. Recall that a permutation is said to have cycle type

```
$$x_{k_{1}}^{n_{1}}\ldots x_{k_{s}}^{n_{s}}$$
```

if, in its disjoint cycle form, it has $r_{s}$ cycles of length $k_{s}$, for $1\leq s\leq r$, including cycles of length 1. We use $ct(\pi)$ for the cycle type of a permutation $\pi$. Now comes a key definition.

# **DEFINITION 14.2**

Let $G$ be a group of permutations. The *cycle index* of $G$, written $CI(G)$, is defined to be the polynomial

```
$$\frac{1}{\#(G)}\sum_{\pi \in G} ct(\pi).$$
```

Notice that the cycle index of a group of permutations is a polynomial in the unknowns $x_{1},x_{2},x_{3},\ldots$, and that the sum of the coefficients in this polynomial is 1, because there are $\#(G)$ terms in the sum, $\sum_{\pi \in G} ct(\pi)$, and we obtain the cycle index by dividing this sum by $\#(G)$.

We illustrate the above definition by calculating the cycle index of the groups $S_{n}$ for $n = 2,3,4$. (The case $n = 1$ is too simple to be of any interest.)

First consider the group $S_{2}$ of all permutations of the set $\{1,2\}$. There are two permutations in $S_{2}$: the identity, (1)(2), which has cycle type $x_{1}^{2}$; and the permutation (1 2), which has cycle type $x_{2}$. Hence the cycle index, $CI(S_{2})$, of the group $S_{2}$, is the polynomial

```
$$\frac{1}{2}(x_{1}^{2}+x_{2}).$$
```

The six permutations in the group $S_{3}$ and their cycle types are shown in Table 14.1. It follows that the cycle index, $CI(S_{3})$, of the group $S_{3}$, is the polynomial

```
$$\frac{1}{6}(x_{1}^{3}+3x_{1}x_{2}+2x_{3}).$$
```

| TABLE 14.1 |
| Permutation | Cycle Type |
| --- | --- |
| (1)(2)(3) | $x_{1}^{3}$ |
| (1 2) { (1 3) { (2 3) | $x_{1}x_{2}$ |
| (1 2 3) { (1 3 2) | $x_{3}$ |