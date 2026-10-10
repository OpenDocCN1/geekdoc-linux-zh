The next problem shows how Definition 5.4 can be used to prove facts about expressions.

# **PROBEM 5.9**

Prove that in any expression containing $n$ letters, there are $n-1$ left-hand parentheses and $n-1$ right-hand parentheses.

# **Solution**

We prove this by mathematical induction. An expression containing just one letter must be $X$ by itself. So it contains one letter and zero parentheses. Hence the result is true in the case $n = 1$. Now suppose that the result is true for all expressions with fewer than $n$ letters, and let $\Sigma$ be an expression containing $n$ letters. By Definition 5.4, $\Sigma$ must be of the form $(\Gamma\Delta)$ where $\Gamma$ and $\Delta$ are expressions. Suppose $\Gamma$ contains $c$ letters. Then $\Delta$ contains $c-n-c$ letters. As $c, n-c < n$, it follows from the induction hypothesis that $\Gamma$ contains $c-1$ pairs of parentheses and $\Delta$ contains $(n-c)-1$ pairs of parentheses. Thus $(\Gamma\Delta)$ contains $(c-1)+((n-c)-1)+1 = n-1$ pairs of parentheses. So the result holds also for expressions containing $n$ letters. Hence, by mathematical induction, the result is true for all expressions.

# **THEOREM 5.7**

For each integer $n > 1$, there are $C_{n-1}$ expressions containing $n$ $X$s.

# **Comment**

The idea behind the proof is to find a one–one correspondence between the set of expressions and the set of Catalan sequences of 1s and $-1$s. The first idea that comes to mind is to associate 1 with a left-hand parenthesis, (, and $-1$ with a right-hand parenthesis, ). However, this natural idea doesn’t work, as, for example, the different expressions $((XX)X)$ and $(X(XX))$ both correspond in this way to the same Catalan sequence $1, 1, -1, -1$. 

Another idea would be to associate 1 with a left-hand parenthesis and $-1$ with an $X$. At first glance it seems that this is no good either since, for example, the expression $((XX)(XX))$ corresponds to the sequence $1, 1, -1, 1, -1, -1, -1$, which is not a Catalan sequence, as it consists of one more $-1$ than a 1. What can we do? In fact, we can “forget” the last $X$. For, in each expression, as we read from left to right, there must be at least one $X$ after the final left-hand parenthesis, (, and hence the associated sequence of 1s and $-1$s must end with a $-1$. (Why is this true? It can be proved using mathematical induction, in a similar way to Problem 5.9 – see Exercise 5.3 4A.)

# **Proof**

We associate with each expression, say $\Gamma$, a sequence, $\Gamma^*$, of 1s and $-1$s obtained by replacing each left-hand parenthesis by 1 and each letter, *except the final letter*, with a $-1$. $\Gamma^*$ will be a Catalan sequence. (See Exercise 5.3 4A.)

We need to show that the mapping $\Gamma \rightarrow \Gamma^*$ is a bijection between the set of expressions containing $n$ letters and the set of Catalan sequences of length $2n-2$. We tackle this by dealing with the following issue. Given a Catalan sequence, say $C$, can we find a unique expression $\Gamma$, such that $\Gamma^* = C$?