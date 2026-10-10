
# **Proof**

We have seen that for all $n \geq 1$, $p(n,1) = (n-1)! = s(n,1)$. (See Exercise 5.1.3A and Problem 5.5.) Also, by Theorems 5.2 and 5.3, the numbers $s(n,k)$, $p(n,k)$ satisfy the same recurrence relation. It follows that for all integers $k$, $n$ with $1 \leq k \leq n$, $p(n,k) = s(n,k)$. Finally, for each positive integer $n$, $p(n,n) = 1 = s(n,n)$. Hence for all integers $k$, $n$, $1 \leq k \leq n$, $p(n,k) = s(n,k)$.

If you compare the entries in Tables 5.1 and 5.2 you will find that we always have $S(n,k) \leq s(n,k)$. Does this state of affairs persist? Theorem 5.5 shows that the answer is in the affirmative.

### **THEOREM 5.5**

For all integers $k$, $n$, such that $1 \leq k \leq n$, we have $S(n,k) \leq s(n,k)$.

### **Proof**

$S(n,k)$ is the number of partitions of the integers $\{1,2,3,...,n\}$ into $k$ disjoint, nonempty subsets. To each such partition $P = \{a_1,a_2,...,a_k\} \cup \{b_1,b_2,...,b_j\} \cup ... \cup \{z_{i_1}z_{i_2}...,z_i\}$, we associate the permutation $P'$ written in cycle notation as $a_{i_1}a_{i_2}...a_{i_k}(b_1b_2...b_j)...(z_{i_1}z_{i_2}...z_i)$. $P$ is a permutation of $\{1,2,3,...,n\}$ made up of exactly $k$ cycles, that is, $P \in \text{Perm}(n,k)$. The mapping $P \to P'$ is injective. It follows that $S(n,k) < \#(\text{Perm}(n,k)) = s(n,k)$.

### **Exercises**

- **5.2.1A** Find a general formula for $p(n,n-2)$, with $n \geq 4$.
- **5.2.1B** Find general formulas for $p(n,n-3)$.
- **5.2.2A** Show that, for each integer $n > 1$, $0!S(n,1) - 1!S(n,2) + ... + (-1)^{n-1}(n-1)!S(n,n) = 0$.
- **5.2.2B** Show that, for all positive integers $k$, $n$, with $k \leq n$, $k^n = C(k,1)S(n,1) + C(k,2)S(n,2) + ... + C(k,k)S(n,k)$.
- **5.2.3A** Show that, for all positive integers $k$, $n$, with $k \leq n$, $\sum_{r=1}^{n} C(n,r)S(n,r) = S(n+1,k+1)$.
- **5.2.3B** Show that, for all positive integers $k$, $n$, with $k \leq n$, $\sum_{r=1}^{n} C(n,r)S(n,r) = s(n+1,k+1)$.

## **5.3 CATALAN NUMBERS**

Applying hindsight, we begin with a definition "out of the blue."

### **DEFINITION 5.3**

For each integer, $n \geq 0$, we define the *nth Catalan number* $c_n$ by

$$c_n = \frac{1}{n+1}C(2n,n).$$

These numbers are singled out because they occur in a large number of combinatorial problems. It is not immediately obvious that $C(2n,n)$ must be divisible by $n+1$. However, this follows from the alternative formula for $C_n$ given at the end of the proof of Theorem 5.6, and also from the result of Exercise 5.3.1A.

The Catalan numbers first came to prominence in the work of Euler in the late 1750s when he determined the number of ways that the area of a convex polygon could be split into triangles when joining vertices by “diagonals” no two of which intersect, except at a vertex. We discuss this problem below (see Theorem 5.9). They had previously appeared in the work of the Mongolian astronomer and mathematician Ming Antu (called Myangat in Mongolian) circa 1730. Euler’s problem was fully solved, in 1758, by J. A. von Segner (1704–1777), who used a recurrence relation¹ of the form $T_{n+1}=T_1T_n+T_2T_{n-1}+...+T_{n-1}T_2+T_nT_1$ (see Theorem 5.8). Catalan first came across the numbers (subsequently named after him by Netto in 1901) in 1838 in a paper asking, “how many ways can one evaluate the product of $n$ different factors?” (See the discussion after Problem 5.8). He solved the problem by use of the above recurrence relation.¹ (We shall solve it by a different method here.) As happens from time to time in mathematics, the name of the first investigator is not always that which is attached to a concept!

As we have already said, there are very many ways in which the Catalan numbers arise.† We shall start with a curious problem involving sequences of 1s and -1s since the proof we offer is especially pretty and rather clever, and several other problems involving Catalan numbers can be easily reduced to it.

### **THEOREM 5.6**

The number of sequences $a_1,a_2,...,a_{2n}$ that can be formed using $n$ 1s and $n$ -1s for which each *partial sum* $s_k=a_1+a_2+...+a_k$ satisfies $s_k \geq 0$ is the $n$th Catalan number, $C_n$.

### **Proof**

Using one ploy (but not yet the clever one!) we shall head toward the desired result by first counting the total number of sequences in the set, $A$, comprising $n$ 1s and $n$ -1s and then subtract the number of sequences in the subset, say $F$, of those that are “forbidden” by the conditions of the theorem.

The number of sequences of $n$ 1s and $n$ -1s is the number of ways of selecting the $n$ positions in a sequence of $2n$ 1s in which to insert a minus sign. Thus $\#(A)=C(2n,n).$ So, now, how do we calculate $\#(F)$?

Let $S=a_1,a_2,...,a_{2n}$ be a sequence in $F$. At the definition of $F$, at least one of the partial sums of this sequence is negative. Let $r$ be the least integer such that $s_r=a_1+a_2+...+a_r<0.$ It must then be that $a_r=-1$, and, if $r>1$, $s_{r-1}=0$ and so $r-1$ must be even. Suppose $r-1=2k$.

The sequence $a_1,a_2, ...,a_{n-1}$ includes equal numbers of 1s and $-1$s. Now comes the clever idea, a "reflection" method due, in the form we present it, to D. Miramoff (1923).${}^{*}$

We produce, from $S$, a new sequence, $S'=b_1,b_2, ..., b_{2n}$, by changing the sign of each of the first $r$ terms of $S$. We then count the number of 1s and $-1$s in this new sequence. In the subsequence $a_1,a_2, ...,a_r$ there are $k$ 1s and $k+1$ -1s, and hence in the subsequence $a_{r+1}, ...,a_{2n}$ there are $n-k$ 1s and $n-(k+1)$ -1s. Thus in the new sequence $S'$ there are $(k+1)+(n-k)=n+1$ 1s and $n-1$ -1s.

Conversely, suppose that we have a sequence $S'=b_1,b_2, ..., b_{2n}$ made up of $n+1$ 1s and $n-1$ -1s. Then there is a least integer, $t\leq 2n$, such that $b_1+b_2+...+b_t=1$. We let $S''$ be the sequence obtained from $S'$ by changing the signs of the first $t$ terms. Then $S''$ is a sequence in $F$. Furthermore, it is easy to see that for each sequence $S$ in $F$, $S''=S$, so the mapping $S\to S''$ is a bijection from $F$ to the set $G$ of sequences made up of $n+1$ 1s and $n-1$ -1s. Thus $\#(F)=\#(G)=C(2n,n+1)=C(2n,n-1)$.

We can now deduce that $\#(A)-\#(F)=C(2n,n)-C(2n,n+1)$. Finally, we have that

$$C(2n,n)-C(2n,n+1) = \frac{(2n)!}{n!n!} - \frac{(2n)!}{(n+1)!(n-1)!} = \frac{(2n)!}{n!(n+1)!} \left((n+1)-n\right) = \frac{(2n)!}{n!(n+1)!} = \frac{1}{n+1}\left(\frac{(2n)!}{n!n!}\right) = \frac{1}{n+1}C(2n,n)=C_n.$$

Because of this theorem we will call a sequence of 1s and $-1$s that meets the conditions of Theorem 5.6 a *Catalan sequence* of 1s and $-1$s. Note also that we have shown in the last line of the above proof that $C_n=C(2n,n)-C(2n,n-1)$. It follows that $C_n$ is an integer.

We can picture Catalan sequences in the way shown in the next problem, which is Problem 5B of Chapter 1.

### **PROBLEM 5.8**

Suppose we have an $n\times n$ grid. How many paths are there, following edges of the grid, from the bottom left corner to the top right corner that may touch, but not go above, the diagonal shown in Figure 5.17 (Here by "path" we mean any route from the bottom left-hand corner to the top right corner that always moves along the lines of the grid either upward or to the right.)

### **Solution**

We can describe each path in a grid by a sequence of 1s and $-1$s, with 1 corresponding to a horizontal segment and $-1$ to a vertical segment. For example, the path shown above in a $10\times 10$ grid is described by the sequence $1,1,1,-1,-1,1,1,1,-1,-1,-1,-1,-1,1,1,1,-1,-1$ of 10 1s and 10 $-1$s. More generally, every path in an $n\times n$ grid may be represented by a sequence of $n$ 1s and $n$ -1s. The condition that the path does not go above the diagonal is exactly the condition that all the partial sums of the corresponding sequence

![](img/eb401bf41900fd678cd9d368a197e486_90_0.png)

**FIGURE 5.1**

are nonnegative, that is, the condition that it is a Catalan sequence. Thus, by Theorem 5.6, the number of paths with the given property is the $n$th Catalan number $C_{n}.$

We now come to the problem that engaged Catalan. Suppose that we have three square matrices,* $A, B, C$, all of the same size. If we wish to multiply them together in this order, we could either first evaluate $AB$ and then postmultiply the resulting matrix by $C$, or first evaluate $BC$ and then premultiply the resulting matrix by $A$. That is, we could either calculate the product as $((AB)C)$ or as $(A(BC))$. If you are familiar with matrix multiplication, you will know that $((AB)C) = (A(BC))$. With four matrices $A, B, C, D$, there are five ways of multiplying them together in this order, given by $(((AB)C)D)$, $((A(BC))D)$, $((A(BC))D)$, $(A((BC)D))$, and $(A(B(CD)))$. This raises the question of how many different ways a product of $n$ matrices may be evaluated.

We have seen that a given way of evaluating the product of matrices in a given order can be described by expressions of the kind used above. To tackle this matrix problem it is helpful to give a careful definition of these *expressions*. Although we have used $A, B, C$, and $D$ above, to indicate that the matrices we are multiplying might be different, this is not relevant when it comes to counting the number of ways the product of $n$ matrices may be evaluated. So in counting the number of different expressions, it makes no difference if we replace $A, B$, $C, D$, ... by a single letter that might as well be $X$. This leads us to the following definition.

### **DEFINITION 5.4**

We define the set of *expressions* built up from the letter $X$, the left parenthesis, $($, and the right parenthesis, $)$, as follows.

- a. The letter $X$ by itself is an expression.
- b. If $\Gamma, \Delta$ are expressions, then so also is $(\Gamma\Delta)$.
- c. Nothing is an expression unless this can be deduced from (a) and (b).

\* Do not worry if you have not met matrices before. The combinatorial problem is the same if we regard $A, B, C$ as, for example, real numbers.
