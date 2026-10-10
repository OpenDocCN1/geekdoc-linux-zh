
The next problem shows how Definition 5.4 can be used to prove facts about expressions.

## PROBLEM 5.9

Prove that in any expression containing $n$ letters, there are $n-1$ left-hand parentheses and $n-1$ right-hand parentheses.

### Solution

We prove this by mathematical induction. An expression containing just one letter must be $X$ by itself. So it contains one letter and zero parentheses. Hence the result is true in the case $n = 1$. Now suppose that the result is true for all expressions with fewer than $n$ letters, and let $\Sigma$ be an expression containing $n$ letters. By Definition 5.4, $\Sigma$ must be of the form $(\Gamma\Delta)$ where $\Gamma$ and $\Delta$ are expressions. Suppose $\Gamma$ contains $c$ letters. Then $\Delta$ contains $n-c$ letters. As $c, n-c < n$, it follows from the induction hypothesis that $\Gamma$ contains $c-1$ pairs of parentheses and $\Delta$ contains $(n-c)-1$ pairs of parentheses. Thus $(\Gamma\Delta)$ contains $(c-1)+((n-c)-1)+1 = n-1$ pairs of parentheses. So the result holds also for expressions containing $n$ letters. Hence, by mathematical induction, the result is true for all expressions.

## THEOREM 5.7

For each integer $n > 1$, there are $\mathcal{C}_{n-1}$ expressions containing $n$ $X$s.

### Comment

The idea behind the proof is to find a one–one correspondence between the set of expressions and the set of Catalan sequences of 1s and $-1$s. The first idea that comes to mind is to associate 1 with a left-hand parenthesis, (, and $-1$ with a right-hand parenthesis, ). However, this natural idea doesn’t work, as, for example, the different expressions $((XX)X)$ and $(X(XX))$ both correspond in this way to the same Catalan sequence $1, 1, -1, -1$.

Another idea would be to associate 1 with a left-hand parenthesis and $-1$ with an $X$. At first glance it seems that this is no good either since, for example, the expression $((XX)(XX))$ corresponds to the sequence $1, 1, -1, 1, -1, -1, -1$, which is not a Catalan sequence, as it consists of one more $-1$ than a 1. What can we do? In fact, we can “forget” the last $X$. For, in each expression, as we read from left to right, there must be at least one $X$ after the final left-hand parenthesis, (, and hence the associated sequence of 1s and $-1$s must end with a $-1$. (Why is this true? It can be proved using mathematical induction, in a similar way to Problem 5.9 – see Exercise 5.3 4A.)

### Proof

We associate with each expression, say $\Gamma$, a sequence, $\Gamma^*$, of 1s and $-1$s obtained by replacing each left-hand parenthesis by 1 and each letter, *except the final letter*, with a $-1$. $\Gamma^*$ will be a Catalan sequence. (See Exercise 5.3 4A.)

We need to show that the mapping $\Gamma \rightarrow \Gamma^*$ is a bijection between the set of expressions containing $n$ letters and the set of Catalan sequences of length $2n-2$. We tackle this by dealing with the following issue. Given a Catalan sequence, say $C$, can we find a unique expression $\Gamma$, such that $\Gamma^* = C$?

We describe a general process for doing this, but to help fix ideas, we explain this with reference to the following the Catalan sequence made up of seven $1$s and seven $-1$s.

$C = 1,1,1,-1,-1,1,1,-1,1,-1,1,-1,-1,1,-1$ (5.5)

We first replace each term $1$ in $C$ by a left-hand parenthesis, and each of the $-1$ terms by the letter $X$, with an additional $X$ at the end. In this way the Catalan sequence $C$ becomes the sequence $C^+$

$(((XX)(X)(XXXX$ (5.6)

As $C$ is a Catalan sequence, the sequence $C^+$ includes one more letter than “(”. Since the sequence must start with a “(”, at some point there are three successive symbols consisting of “(” followed by two letters. We consider the first place where this occurs. In $C^+$ these symbols are $(XX$. We let $\Gamma_1$ be this sequence followed by “)” and we replace the given three successive symbols by $\Gamma_1$, so $\Gamma_1 = (XX)$, and the new sequence is, say $\Sigma_1$, where

$\Sigma_1 = (((\Gamma_1)(X)(XXXX$ (5.7)

In going from Equation 5.6 through Equation 5.7 we have replaced the two letters $XX$ by the single symbol $\Gamma_1$, and we have deleted one left-hand parenthesis, “(”. So if we count $\Gamma_1$ as a letter, we still have a sequence beginning with “(” and with one more letter than “(”. Therefore, continuing to use letter in an extended sense to include symbols of the form $\Gamma_i$, where $i$ is an integer, there is again a first place from the left in Equation 5.7 where the symbol “(” is followed by two letters. We let $\Gamma_2$ be the sequence consisting of “(” and the two letters followed by “)” and substitute $\Gamma_2$ for them in Equation 5.7. In this way we obtain:

$\Gamma_2 = (XX) \quad \text{and} \quad \Sigma_2 = (((\Gamma_1)(X\Gamma_2)XX$

We can now continue in this way, as follows:

$\Gamma_3 = (X\Gamma_2) \quad \text{and} \quad \Sigma_3 = (((\Gamma_1(\Gamma_3)XX$

$\Gamma_4 = (X\Gamma_3) \quad \text{and} \quad \Sigma_4 = (((\Gamma_1(\Gamma_4)XX$

$\Gamma_5 = (\Gamma_4X) \quad \text{and} \quad \Sigma_5 = (((\Gamma_1\Gamma_5)X$

$\Gamma_6 = (\Gamma_5X) \quad \text{and} \quad \Sigma_6 = (\Gamma_6X, \text{and}$

$\Gamma_7 = (\Gamma_6X) \quad \text{and} \quad \Sigma_7 = \Gamma_7$

Since there are seven $1$s in the Catalan sequence $C$, this process ends after seven steps, and substituting backwards we see that

$\Sigma_7 = (((XX)(X(X(XXX))))X)X$

It should be clear that this process converts a Catalan sequence, $\mathcal{C}$, into a uniquely determined expression, say $\Gamma^{*}$ . Furthermore, if we start with an expression $\Gamma$, then $\Gamma^{* *}=\Gamma$. We leave it to you to check this.

Thus there is a one-one correspondence between the set of expressions containing $n$ $X$s and the set of Catalan sequences made up of $n$ 1s and $n-1$ -1s. Since there are $\mathcal{C}_{n-1}$ such sequences, Theorem 5.7 is proved. It is convenient to specify that $\mathcal{C}_{0}=1$, so that the result of Theorem 5.7 holds also for the case where $n=1$ .

We can use Theorem 5.7 to prove the following relationship between the Catalan numbers.

## THEOREM 5.8

For each integer $n \geq 1$, $\mathcal{C}_{n+1}=\sum_{k=0}^{n} \mathcal{C}_{k} \mathcal{C}_{n-k}$.

### Proof

By Theorem 5.7 there are $\mathcal{C}_{n+1}$ expressions involving $n+2$ letters. Suppose that $\Sigma$ is one such expression. It follows from Exercise 5.3.4B that there are unique expressions $\Sigma_{1}, \Sigma_{2}$ such that $\Sigma$ is the expression $\left(\Sigma_{1} \Sigma_{2}\right)$. Then $\Sigma_{1}$ contains $k+1$ $X$s for some integer $k$, where $0 \leq k \leq n$. Therefore $\Sigma_{2}$ contains $(n+2)-(k+1)=(n-k)+1$ $X$s. Thus, for $0 \leq k \leq n$ there are $\mathcal{C}_{k}$ choices for $\Sigma_{1}$ and there are $\mathcal{C}_{n-k}$ choices for $\Sigma_{2}$, and hence $\mathcal{C}_{k} \mathcal{C}_{n-k}$ choices for the pair $\Sigma_{1}, \Sigma_{2}$. It follows that, by taking together all the cases as $k$ runs from 0 to $n$, $\mathcal{C}_{n+1}=\sum_{k=0}^{n} \mathcal{C}_{k} \mathcal{C}_{n-k}$.

In Chapter 7, Section 7.8, we show how the recurrence relation of Theorem 5.8 may be used to find the formula for $\mathcal{C}_{n}$ as given in Definition 5.3.

We now look at Problem 5C, first considered by Euler, to which the answer is given by the Catalan numbers. By a *triangulation* of a polygon we mean a way of dividing the polygon into triangles by nonintersecting diagonals, that is, lines joining two vertices. For example, Figure 5.2 shows two different triangulations of a square.

Note that we count the two triangulations of the square as different even though one can be obtained from the other by a rotation or reflection of the square. In fact, a square has just two different triangulations, namely, the two shown in Figure 5.2.

For each integer $n \geq 1$, we let $T_{n}$ be the number of different triangulations of a polygon with $n+2$ edges. Note that $n$ diagonals are needed to triangulate a polygon with $n+2$ edges. Thus $T_{1}=1$ and $T_{2}=2$. It turns out to be a useful convention to put $T_{0}=1$, as this simplifies some of the formulas.

![](img/eb401bf41900fd678cd9d368a197e486_93_0.png)

FIGURE 5.2
