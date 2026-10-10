these inequalities. In other words, we sum over all the $k$-element subsets of the set $\{1,2,...,n\}$.

We are now ready for the proof.

# **Proof**

Take an element $x\in A_{1}\cup...\cup A_{n}$. We calculate how many times $x$ is included by the formula on the right-hand side of Equation 4.1.

Suppose that $x$ is an element of exactly $m$ of the given sets, say $A_{i_{1}},...,A_{i_{m}}$. Then $x\in A_{i_{1}}\cap...\cap A_{i_{m}}$ if and only if $\{i_{1},...,i_{k}\}\supseteq \{j_{1},...,j_{m}\}$. This can happen only if $1\leq k\leq m$, in which case the set $\{j_{1},...,j_{k}\}$ has $C(m,k)$ subsets of size $k$. Thus $x$ is counted $C(m,k)$ times in the sum $\sum_{1\leq k_{1}<...<k_{k}\leq n}#(A_{k_{1}}\cap...\cap A_{k_{k}})$ that occurs on the right-hand side of our equation. Thus, taking account of the alternating signs, $x$ is altogether counted $\sum_{k=m}^{n}(-1)^{k+1}C(m,k)$ times. Now $\sum_{k=m}^{n}(-1)^{k}C(m,k) = 0$ (see Exercise 2.3.3).

It follows that $\sum_{k=m}^{n}(-1)^{k+1}C(m,k) = C(m,0) = 1$, and thus each element of $A_{1}\cup...\cup A_{n}$ is counted just once by the formula, which therefore gives the correct value for $#(A_{1}\cup...\cup A_{n})$.

We can now use the inclusion–exclusion theorem to modify our calculation in Chapter 2 of the number of five-card hands with at least one suit with no cards in it (Problem 2.11).

# **PROBLEM 4.2**

How many hands of five cards are there in which there is at least one suit with no cards in it?

# **Solution**

We let $V_{S}$, $V_{H}$, $V_{D}$, and $V_{C}$ be those five-card hands with no spades, hearts, diamonds, or clubs, respectively. We wish to calculate $#(V_{S}\cup V_{H}\cup V_{D}\cup V_{C})$. By the inclusion–exclusion theorem this is equal to

```
(#(V_{S}) + #(V_{H}) + #(V_{D}) + #(V_{C})) – (#(V_{S}\cap V_{H}) + ... + #(V_{S}\cap V_{H}\cap V_{D}\cap V_{C}))
– #(V_{S}\cap V_{H}\cap V_{D}\cap V_{C}).
```

A hand in $V_{S}$ contains 5 cards drawn from the 39 cards that are not spades. Thus $#(V_{S}) = C(39,5)$, and similarly for each of the terms in the first pair of large brackets of the above expression. A hand in $V_{S}\cap V_{H}$ consists of 5 cards drawn from the 26 cards that are neither spades nor hearts. Thus $#(V_{S}\cap V_{H}) = C(26,5)$, and similarly for the other terms in the second pair of brackets. These terms correspond to all the ways of choosing two suits from the four suits in the pack, so there are $C(4,2)$ terms in the second pair of brackets. In the same way we see that there are $C(4,1)$ terms in the third pair of brackets, each of them equal to $C(13,5)$. Finally, of course, there are no five-card hands that contain no card of any suit and so $#(V_{S}\cap V_{H}\cap V_{D}\cap V_{C}) = 0$. Therefore

```
#(V_{S}\cup V_{H}\cup V_{D}\cup V_{C}) = C(4,1)C(39,5) – C(4,2)C(26,5) + C(4,3)C(13,5)
= 4\times575,757 – 6\times65,780 + 4\times1,287 = 1,913,496,
```

which agrees with our earlier solution to Problem 2.11 in Chapter 2.