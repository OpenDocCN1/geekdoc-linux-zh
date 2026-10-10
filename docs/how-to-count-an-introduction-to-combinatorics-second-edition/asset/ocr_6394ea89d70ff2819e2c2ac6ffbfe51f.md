By the inclusion – exclusion theorem,

$$\begin{align} \# \left(\bigcup_{\substack{s \in \d B}} P(S)\right) &= \sum_{j=1}^{k}(-1)^{j+1}\left(\sum_{\substack{S_1, \ldots, S_j \in \d B}} \#(P(S_1) \cap P(S_2) \cap \ldots \cap P(S_j))\right) \\ &= \sum_{j=1}^{k}(-1)^{j+1}\sum_{\substack{S_1, \ldots, S_j \in \d B}} \#(P(S_1, \ldots, S_j)). \end{align}\tag{17.7}$$

We now evaluate the sum

$$\sum_{\substack{S_1, \ldots, S_j \in \d B}} \#(P(S_1, \ldots, S_j))\tag{17.8}$$

that occurs in Equation 17.7.

As we have already observed, if any of the squares $S_1, \ldots, S_j$ are in the same row or column, then $\#(P(S_1, \ldots, S_j))=0$. Thus the number of nonzero terms in the sum 17.8 is the number of ways of placing $j$ rooks on the black squares of $B$ so that no two of them are in the same row or column. But this is just the number of ways of placing $j$ nonattacking rooks on the complementary board $B^c$, that is, $r_j(B^c)$.

Now suppose no two of the squares $S_1, \ldots, S_j$ are in the same row or column. So between them they lie in $j$ rows and $j$ columns. $P(S_1, \ldots, S_j)$ is the set of positions with $j$ rooks on the squares $S_1, \ldots, S_j$ and hence $k - j$ nonattacking rooks in the remaining $m - j$ columns and $n - j$ rows in which none of these squares lie. Thus $\#(P(S_1, \ldots, S_j))$ is the same as the number of ways of placing with $k - j$ nonattacking rooks on an $(m - j) \times (n - j)$ board. So, by Exercise 2.2.4.A, $\#(P(S_1, \ldots, S_j)) = C(m - j, k - j)C(n - j, k - j)(k - j)!$.

It follows that

$$\sum_{\substack{S_1, \ldots, S_j \in \d B}} \#(P(S_1, \ldots, S_j))=C(m - j, k - j)C(n - j, k - j)(k - j)!r_j(B^c).\tag{17.9}$$

Now, by Equations 17.6, 17.7, and 17.9, we have that

$$r_k(B)=C(m,k)C(n,k)k!\sum_{j=0}^{k}(-1)^{j+1}C(m-j,k-j)C(n-j,k-j)(k-j)!r_j(B^c).\tag{17.10}$$

and hence, as $r_0(B^c)=1$, we can rewrite Equation 17.10 as

$$r_k(B)=\sum_{j=0}^{k}(-1)C(m-j,k-j)C(n-j,k-j)(k-j)!r_j(B^c),$$

and this completes the proof.