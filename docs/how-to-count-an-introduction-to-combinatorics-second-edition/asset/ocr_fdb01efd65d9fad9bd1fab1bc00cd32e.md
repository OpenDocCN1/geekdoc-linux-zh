that the result holds also for an expression ($\Gamma\Delta$) with $k$ pairs of brackets, and hence in which $\Gamma$ and $\Delta$ are expressions with fewer than $k$ pairs of brackets. Let $S_{\Gamma}$ and $S_{\Delta}$ be the sequences of $1$'s and $-1$'s, associated with $\Gamma$ and $\Delta$, respectively. Since, by (i), the final $X$ in $\Gamma$ occurs after the final left-hand bracket, the sequences of $1$'s and $-1$'s associated with the expression $(\Gamma\Delta)$ is $1S_{\Gamma} - 1S_{\Delta}$, and it should be clear that as $S_{\Gamma}$ and $S_{\Delta}$ satisfy the "$s_i \geq 0$" condition, so also does the sequence $1S_{\Gamma} - 1S_{\Delta}$. Hence, $(\Gamma\Delta)$ is also a Catalan sequence.

**5.3.5A** Given a sequence $a_1, a_2, \ldots, a_n$ of $n$ nonnegative integers we define a path of points on an $n \times n$ grid, by considering the elements of the sequence in turn as follows. We start at the point $(0,0)$. Suppose the last point we have defined is $(x,y)$ and the next term we consider is $a_k$. If $a_k > 0$, we add to our path the points $(x+i, y)$ and $(x+1, y+a_i)$, while if $a_k = 0$, we just add the point $(x+1, y)$. For example, in the case $n = 6$, corresponding to the sequence $1,0,0,3,0,2$, we obtain the sequence of points

$$(0,0), \quad (1,0), \quad (1,1), \quad (2,1), \quad (3,1), \quad (4,1), \quad (4,4), \quad (5,4), \quad (6,4), \quad (6,6),$$

and hence the path shown in the diagram below.

![](bbox=[0.435, 0.47, 0.565, 0.59])

The condition that $a_1 + a_2 + \cdots + a_n = n$ means that the path ends at the point $(n,n)$, and the condition that $a_1 + a_2 + \cdots + a_k \leq k$ ensures that the path does not go above the bottom-left to top-right diagonal. Hence, by the result of Problem 5.8, there are $C_n$ sequences with the specified properties.

**5.3.6A** If each up-sloping arrow is replaced by $1$ and each down-sloping arrow by $-1$ we see that there is a one-one correspondence between “mountain paths” made up of $2n$ arrows, and Catalan sequences of length $2n$ So, by Theorem 5.6, there are $C_n$ such mountain paths.

**5.3.7A** With H corresponding to $1$ and T corresponding to $-1$, each sequence of five heads and five tails, with at least as many heads as tails at each stage, corresponds to a Catalan sequence of length 10 and vice versa. Thus, there are $C_5 = \frac{1}{6}\binom{10}{5} = 42$ such sequences.

**5.3.8A** The votes, as they are counted, correspond to a sequence of $a$ A's and $a$ B's. The total number of these sequences is the number of ways of choosing the positions for the