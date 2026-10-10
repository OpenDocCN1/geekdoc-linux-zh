
Substituting from Equation 2 into Equation 1, we obtain

$$
\begin{aligned} S(m+1, k) = & \frac{1}{(k-1)!} \sum_{i=1}^{k-1} (-1)^{i-1} C(k-1, s-1)(k-s)^m + \frac{1}{(k-1)!} \sum_{i=1}^{k-1} (-1)^i C(k, s)(k-s)^m \\
= & \frac{1}{(k-1)!} \sum_{i=1}^{k-1} (-1)^{i-1} C(k-1, s-1)(k-s)^m + \frac{1}{(k-1)!} \left\{ C(k, 0)k^m + \sum_{i=1}^{k-1} (-1)^i C(k, s)(k-s)^m \right\} \\
= & \frac{1}{(k-1)!} \sum_{i=1}^{k-1} (-1)^{i-1} (k-s)^m [C(k-1, s-1) - C(k, s)] + \frac{1}{(k-1)!} k^m. \end{aligned}
$$

Now by Theorems 2.7 and 2.4,

$$
C(k-1, s-1) - C(k, s) = -C(k-1, s) = \frac{k-s}{k} C(k, s). \quad (4)
$$

By Equations 3 and 4,

$$
\begin{aligned} S(m+1, k) = & \frac{1}{(k-1)!} \sum_{i=1}^{k-1} (-1)^{i-1}(k-s)^m \left( -\frac{k-s}{k} C(k, s) \right) + \frac{1}{(k-1)!} k^m \\
= & \frac{1}{k!} \sum_{i=1}^{k-1} (-1)^i C(k, s)(k-s)^{m+1} + \frac{1}{(k-1)!} k^m. \end{aligned} \quad (5)
$$

Finally, $((1/k-1)!)k^m = (1/k!)k^{m+1}$, which is the same as $((1/k!)(-1)^i C(k, 0)(k-s)^{m+1}$ when $s=0$. So Equation 5 is equivalent to

$$
S(m+1, k) = \frac{1}{k!} \sum_{i=0}^{k-1} (-1)^i C(k, s)(k-s)^{m+1},
$$

and hence the result holds also for $n = m + 1$.

This completes the proof, by mathematical induction, that the result is true for all integers $n \geq 1$.

# CHAPTER 5

## 5.1

### 5.1.1.A
$[x]_6 = x(x-1)(x-2)(x-3)(x-4)(x-5) = x^6 - 15x^5 + 85x^4 - 225x^3 + 274x^2 - 120x$ (either by direct expansion, or by reading off the coefficients from Table 5.3).

### 5.1.2.A
All we need do is multiply the relevant matrices, and check that we get the appropriate identity matrix in each case. Although matrix multiplication is not in general commutative, the theory tells us that if $P$, $Q$ are square matrices with $PQ = I$, then $QP = I$, so we need only check one product in each case. Here we have

$$
P_{2}Q_{2} = \begin{pmatrix} 1 & 0 \\ -1 & 1 \end{pmatrix}\begin{pmatrix} 1 & 0 \\ 1 & 1 \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}
$$
and
$$
P_{3}Q_{3} = \begin{pmatrix} 1 & 0 & 0 \\ -1 & 1 & 0 \\ 2 & -3 & 1 \end{pmatrix}\begin{pmatrix} 1 & 0 & 0 \\ 1 & 1 & 0 \\ 1 & 3 & 1 \end{pmatrix} = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}.
$$

### 5.1.3.A
$s(n,1)$ is the modulus of the coefficient of $x$ in the polynomial $x(x-1)(x-2)...(x-(n-1))$. Thus $s(n,1) = |(-1)(-2)...(-(n-1))| = (n-1)!$.

### 5.1.4.A
$x(x-1)(x-2)...(x-(n-1)) = s(n,n)x^{n} - s(n,n-1)x^{n-1}+...+(-1)^{n-1}s(n,1)x$. Putting $x = -1$, this gives $(-1)(-2)...(-n) = (-1)^{n}s(n,n) + (-1)^{n}s(n,n-1)+...+(-1)^{n}s(n,1)$. That is, $(-1)^{n}n! = (-1)^{n}(s(n,n)+s(n,n-1)+...+s(n,1))$ and therefore $s(n,1)+...+s(n,n)=n!$.

### 5.1.5.A
Again, we begin with the equation $x(x-1)(x-2)...(x-(n-1)) = s(n,n)x^{n}-s(n,n-1)x^{n-1}+...+(-1)^{n-1}s(n,1)x$, but this time the answer we are seeking suggests that we put $x = -k$. This gives
$$
-k(-(k+1))(-(k+2))...(-(k+n-1)) = (-1)^{n}(s(n,n)k^{n}+s(n,n-1)k^{n-1}+...+s(n,1)k).
$$
That is, $(-1)^{n}k(k+1)...(k+n-1) = (-1)^{n}\sum_{r=1}^{n}s(n,r)k^{r}$, and hence
$$
\sum_{r=1}^{n}s(n,r)k^{r} = \frac{(k+n-1)!}{(k-1)!} = n!\frac{(k+n-1)!}{n!(k-1)!} = n!C(k+n-1,n).
$$

### 5.1.6.A
$s(n,k)$ is the modulus of the coefficient of $x^{k}$ in $x(x-1)(x-2)...(x-(n-1))$. The terms involving $x^{k}$ in this product are obtained by choosing $x$ from $k$ of the brackets, and $n-k$ of the constants $\{0,1,2,...,n-1\}$ from the remaining brackets. If 0 is one of the chosen constants, the product is 0. Thus $s(n,k)$ is the sum of all the products of $n-k$ different integers chosen from $\{1,2,...,n-1\}$.

### 5.1.7.A
$\Theta^{5} = \Theta(\Theta^{4}) = xD(xD^{4}+7x^{2}D^{3}+6x^{3}D^{2}+x^{4}D^{1})$ (using the solution to Problem 5.3)
$$
= x(D+x^{2}D+x^{4}D^{2}+7x^{2}D^{3}+18x^{3}D^{2}+6x^{4}D^{1}+4x^{5}D^{1}+x^{6}D^{1})
$$
$$
= xD+15x^{2}D^{2}+25x^{3}D^{3}+10x^{4}D^{4}+x^{5}D^{5}.
$$
Thus we see from Table 5.2 that the coefficients are the required Stirling numbers.

## 5.2

### 5.2.1.A
A permutation of the set $\{1,2,...,n\}$, with $n \geq 4$, made up of $n-2$ cycles, must consist of either
- (a) one cycle of length 3 and $n-3$ cycles of type 1, or
- (b) two cycles of length 2 and $n-4$ cycles of length 1.

To get a permutation of type (a), we first choose the three numbers to make up a cycle of length 3. This can be done in $C(n,3)$ ways. Each three numbers can be arranged to form two different cycles of length 3, and there is no further choice involved, as the remaining $n-3$ numbers must all be in separate cycles of length 1. So there are $2C(n,3) = \frac{n(n-1)(n-2)}{3}$ permutations of this type.

To get a permutation of type (b), we first choose two numbers to make up the first cycle of length 2, and then two further numbers to make up the second cycle of length 2. The order in which we make these choices does not matter. So there are
$$
\frac{1}{2}C(n, 2)C(n-2, 2)=\frac{1}{2} \times \frac{n!}{(n-2) ! 2 !} \times \frac{(n-2) !}{(n-4) ! 2 !} = \frac{n(n-1)(n-2)(n-3)}{8}
$$
permutations of this type. Hence
$$
p(n, n-2)=\frac{n(n-1)(n-2)}{3}+\frac{n(n-1)(n-2)(n-3)}{8} = \frac{n(n-1)(n-2)(3n-1)}{24}.
$$

### 5.2.2.A
We start from the identity of Theorem 5.1, $x^{n}=\sum_{k=1}^{n} S(n, k)\left[x\right]_{k}$ that is, $x^{n}=\sum_{k=1}^{n} S(n, k) x(x-1) . .(x-(k-1))$. If we divide both sides by x, we obtain $x^{n-1}=\sum_{k=1}^{n} S(n, k)(x-1) . .(x-(k-1))$, and now, putting $x=0$, we deduce that $0=\sum_{k=1}^{n}(-1)^{k-1} S(n, k)(k-1) !$

### 5.2.3.A
$S(n+1, k+1)$ is the number of ways of placing $n+1$ distinct balls in $k+1$ identical boxes. Consider one particular ball, say b. We first choose r of the other n balls to go in different boxes from that in which we put b. Since there are k other boxes that all must have at least one ball in them, $k \leq r \leq n$. These r balls can be chosen in $C(n, r)$ ways, and they can be placed in the remaining k boxes in $S(r, k)$ ways. Thus, for $k \leq r \leq n$, we can place the $n+1$ balls in $k+1$ boxes with r balls not in the same box as b, in $C(n, r) S(r, k)$ ways. Hence
$$
S(n+1, k+1)=\sum_{r=k}^{n} C(n, r) S(r, k)
$$

## 5.3

### 5.3.1.A
i. $C(2n-1, n-1)-C(2n-1, n+1)=\frac{(2n-1) !}{(n-1) ! n !}-\frac{(2n-1) !}{(n+1) !(n-2) !}$
$$
\begin{aligned}
& =\frac{(2n-1) !(n+1) !(n-2) !}{(n+1) !(n-2) !} \cdot \frac{1}{n !}\cdot \frac{(2n) !}{n !(n-1) !} \\
& =\frac{(2n-1) !(2n) !}{n !(n+1) !} = \frac{1}{n+1} \cdot \frac{(2n) !}{n ! n !} = \frac{1}{n+1} C(2n, n)=C_{n}
\end{aligned}
$$
ii. As $C(2n-1, n-1)$ and $C(2n-1, n+1)$ are both integers, it follows from (i) that $C_{n}$ is an integer.

### 5.3.2.A
We prove this result by induction. Since $C_{1}=1$, the result holds for $n=1$. Now suppose that the result holds for all $m \leq n$. By Theorem 5.8, $C_{n+1}=\sum_{k=0}^{n} C_{k} C_{n-k}$ We first consider the case where $n+1$ is even, say $n+1=2s$, so that $n=2s-1$, and thus $C_{n+1}=\sum_{k=0}^{2s-1} C_{k} C_{2s-k-1}=\sum_{k=0}^{s-1} C_{k} C_{2s-k-1}+\sum_{k=s}^{2s-1} C_{k} C_{2s-k-1}$. Now putting $l=2s-k-1$, we see that
$$
\sum_{k=s}^{2s-1}C_kC_{2s-k-1}=\sum_{j=0}^{s-1}C_{2s-1-j}C_j=\sum_{j=0}^{s-1}C_jC_{2s-1-j}
$$
on replacing the "dummy variable" $l$ by $j$. Hence $C_{n+1}=2\sum_{k=0}^{s-1}C_kC_{2s-k-1}$ and consequently is even. Next, when $n+1$ is odd, say $n+1=2s+1$ (implied from context "n is even"), we have similarly that $C_{n+1}=2\sum_{k=0}^{s}C_kC_{2s+1-k}+C_{s+1}C_{s+1}$. It follows that $C_{n+1}$ is odd, if and only if $n+1$ is odd and $C_{((n+1)/2)}$ is odd. Thus, by the induction hypothesis, $C_{n+1}$ is odd if and only if, for some integer $t$, $\frac{n+1}{2}=2^t-1$. Now, this holds if and only if $n+1=2(2^t-1)+1=2^{t+1}-1$, for some integer $t$. Hence the result holds also for $n+1$. This completes the proof.

### 5.3.3.A
We consider a path, joining the corners of an $n\times n$ grid, that apart from its endpoints lies below the diagonal. Such a path must never cross the "subdiagonal" marked by a dotted line in the diagram below.

![](img/eb401bf41900fd678cd9d368a197e486_371_0.png)

Thus the number of such paths is the same as the number of paths joining the corners of the shaded $(n-1)\times(n-1)$ grid that do not cross the diagonal; that is,
$$
C_{n-1}=\frac{1}{n}C(2n-2,n-1).
$$

### 5.3.4.A
We can prove these results using mathematical induction on the number of pairs of brackets in an expression.

- i. The result is clearly true for expressions with no brackets and hence consisting of a single $X$. Suppose the result holds for expressions with fewer than $k$ pairs of brackets.
- An expression with $k$ pairs of brackets will have the form $(\Gamma\Delta)$ where $\Gamma$ and $\Delta$ are expressions with fewer than $k$ pairs of brackets. Hence, by the induction hypothesis, there is an $X$ in $\Delta$ after the last left-hand bracket. This $X$ also occurs after the last left-hand bracket in the expression $(\Gamma\Delta)$. So the result holds also for expressions with $k$ pairs of brackets.

- ii. The sequence of $1$s and $-1$s associated with a single $X$ is an empty sequence that counts as a Catalan sequence, so the result is true for expressions with no brackets. Suppose the result holds for expressions with fewer than $k$ pairs of brackets. We show
