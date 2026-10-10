The sequence $a_1,a_2, ...,a_{n-1}$ includes equal numbers of 1s and $-1$s. Now comes the clever idea, a "reflection" method due, in the form we present it, to D. Miramoff (1923).${}^{*}$

We produce, from $S$, a new sequence, $S'=b_1,b_2, ..., b_{2n}$, by changing the sign of each of the first $r$ terms of $S$. We then count the number of 1s and $-1$s in this new sequence. In the subsequence $a_1,a_2, ...,a_r$ there are $k$ 1s and $k+1-1$s, and hence in the subsequence $a_1, ...,a_{2n}$ there are $n-k$ 1s and $n-(k+1)-1$s. Thus in the new sequence $S'$ there are $(k+1)+(n-k)=n+1$ 1s and $n-1-1$s.

Conversely, suppose that we have a sequence $S'=b_1,b_2, ..., b_{2n}$ made up of $n+1$ 1s and $n-1-1$s. Then there is a least integer, $t\leq 2n$, such that $b_1+b_2+...+b_t=1$. We let $S''$ be the sequence obtained from $S'$ by changing the signs of the first $t$ terms. Then $S''$ is a sequence in $F$. Furthermore, it is easy to see that for each sequence $S$ in $F$, $S''=S$, so the mapping $S\to S''$ is a bijection from $F$ to the set $G$ of sequences made up of $n+1$ 1s and $n-1-1$s. Thus $\#(F)=\#(G)=C(2n,n+1)=C(2n,n-1)$.

We can now deduce that $\#(A)-\#(F)=C(2n,n)-C(2n,n+1)$. Finally, we have that

```
$C(2n,n)-C(2n,n+1) = \frac{(2n)!}{n!n!} - \frac{(2n)!}{(n+1)!(n-1)!} = \frac{(2n)!}{n!(n+1)!} \left((n+1)-n\right) = \frac{(2n)!}{n!(n+1)!} = \frac{1}{n+1}\left(\frac{(2n)!}{n!n!}\right) = \frac{1}{n+1}C(2n,n)=C_n.$
```

Because of this theorem we will call a sequence of 1s and $-1$s that meets the conditions of Theorem 5.6 a *Catalan sequence* of 1s and $-1$s. Note also that we have shown in the last line of the above proof that $C_n=C(2n,n)-C(2n,n-1)$. It follows that $C_n$ is an integer.

We can picture Catalan sequences in the way shown in the next problem, which is Problem 5B of Chapter 1.

# PROBLEM 5.8

Suppose we have an $n\times n$ grid. How many paths are there, following edges of the grid, from the bottom left corner to the top right corner that may touch, but not go above, the diagonal shown in Figure 5.17 (Here by "path" we mean any route from the bottom left-hand corner to the top right corner that always moves along the lines of the grid either upward or to the right.)

# Solution

We can describe each path in a grid by a sequence of 1s and $-1$s, with 1 corresponding to a horizontal segment and $-1$ to a vertical segment. For example, the path shown above in a $10\times 10$ grid is described by the sequence $1,1,1,-1,-1,1,1,1,-1,-1,-1,-1,-1,1,1,1,-1,-1$ of 10 1s and 10 $-1$s. More generally, every path in an $n\times n$ grid may be represented by a sequence of $n$ 1s and $n-1$s. The condition that the path does not go above the diagonal is exactly the condition that all the partial sums of the corresponding sequence