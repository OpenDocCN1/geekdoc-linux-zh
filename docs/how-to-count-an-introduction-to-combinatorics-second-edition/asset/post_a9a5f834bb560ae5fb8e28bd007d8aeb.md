
## 16.2 Exercises

### 16.2.1A

- i. Use Theorems 16.6 and 16.8 to determine lower bounds for $R(5,5)$ and $R(6,6).$
- ii. Explain how you can “see” that the lower bound for $R(p,p)$ given by Theorem 16.6 will be less than the lower bound given by Theorem 16.8, for all but finitely many values $p$ (so that, for almost all integers $p$, Theorem 16.8 gives the better result).

### 16.2.1B

Find the least value of $p$ for which the lower bound for $R(p,p)$ given by Theorem 16.8 is larger than the lower bound given by Theorem 16.6.

### 16.2.2A

Prove, using mathematical induction, that for every integer $n \geq 2, \frac{1}{4}3^n \le C(2n,n) \le \frac{3}{4}4^n.$

### 16.2.2B

Prove that for every $\varepsilon$, with $0 < \varepsilon < 4$, and every positive constant $K$, there is a positive integer $N$ such that for all integers $n > N$, $K(4-\varepsilon)^n < C(2n,n)$. [In fact, it can be shown that $C(2n,n)$ is asymptotic to $4^n/\sqrt{\pi n}$, using Stirling’s formula* for $n!$]

## 16.3 GRAPHS OF MANY COLORS

You will obviously be asking if similar results are available if we color complete graphs with more than two colors. Again Ramsey’s theorem says that there are. The next theorem, which is essentially Ramsey’s full theorem with $s = 2$, allows us to prove such results.

### THEOREM 16.10

Let $m$ and $n_1$, $n_2$, ..., $n_m$ be positive integers, and let $C_1, C_2, \ldots, C_m$ be $m$ different colors. Then there is a positive integer $M$ such that if the edges of the complete graph $K_M$ are painted using these colors, then for some integer $i$ with $1 \le i \le m$, $K_M$ has a $K_{n_i}$ of color $C_i$ (that is, there are $n_i$ vertices of $K_M$ such that all the edges joining them have been painted the color $C_i$).

### Proof

We call the argument we use here the *tangerine argument*.$^\dagger$ We give a proof using mathematical induction. The result is obviously true for $m = 1$. Suppose now that it holds for $m = k$, and consider the case where $m = k + 1$. We suppose that $C_{k+1}$ is tangerine and, for the time being, describe all the other colors as *dull*.

There are $k$ dull colors, $C_1, C_2, \ldots, C_k$. Hence, by the induction hypothesis, there is a positive integer $L$ such that if the edges of $K_L$ are painted using these colors, then for some integer $i$ with $1 \le i \le k$, $K_L$ has a $K_{n_i}$ of color $C_i$.

Now let $M = R(L, n_{k+1})$. If the edges of the complete graph $K_M$ are painted either dull or tangerine, then $K_M$ has either a $K_L$ all of whose edges are dull or a tangerine $K_{n_{k+1}}$. Now, by the choice of $L$, in the first case for some $i$, with $1 \le i \le k$, $K_M$ has a $K_{n_i}$ of color $C_i$. In the second case, $K_M$ contains a $K_{n_{k+1}}$ of color $C_{k+1}$.

* Stirling’s formula says that $n!$ is asymptotic to, that is, very closely approximated by, $\sqrt{2\pi n}(n/e)^n$. For a proof of this, see the first edition of this book. We have not managed to find space for it in this expanded edition.

$^\dagger$ Tangerine is the color of Blackpool Football Club, of which one of the authors is a very keen follower. For some unfathomable reason, the other author cannot abide soccer (footnote added by the Blackpool supporter).

Thus for some $i$, with $1 \leq i \leq k+1$, $K_{n_i}$ has a $K_6$ of color $C_i$. Thus the result holds also for $m = k+1$. This completes the proof.

The least such number $M$ that satisfies the conditions of Theorem 16.10 is usually denoted by $R(n_1, n_2, \ldots, n_m)$ and is called the $(n_1, n_2, \ldots, n_m)$ *Ramsey number*. The only Ramsey number with $m \geq 3$ whose actual value is known is $R(3, 3, 3)$, which is 17 (see Exercise 16.3.1B).

As we have already noted, we could also generalize the above result by replacing the two-element subsets, that is, graph edges, by three-, four-, and one-element subsets of a given set. If we go in the other direction and consider one-element subsets of a set, that is, we color the elements of a set (rather than pairs, triples, quadruples, etc., of elements), we obtain Theorem 15.3, one of the generalizations of the pigeonhole principle. We therefore see that Ramsey theory is a vast generalization of Dirichlet’s pigeonhole principle.

## 16.3 Exercises

### 16.3.1A

a. Use the proof of Theorem 16.10 to show that for each positive integer $k$ and all positive integers $n_1, \ldots, n_k, n_{k+1}$, $R(n_1, \ldots, n_k, n_{k+1}) \leq R(R(n_1, \ldots, n_k), n_{k+1})$, and deduce that for all positive integers $p, q$, and $r$:

$$R(p, q, r) \leq \min\{R(R(p, q), r), R(R(p, r), q), R(R(q, r), p)\}.$$

b. Prove that, for all positive integers $p, q, r \geq 2$,

$$R(p, q, r) \leq R(p-1, q, r) + R(p, q-1, r) + R(p, q, r-1) - 1.$$

### 16.3.1B

Suppose the edges of $K_{17}$ are colored using red, blue, or green. Let $v$ be a vertex of $K_{17}$. Show that:

- i. At least six of the edges with $v$ as endpoint must be of the same color (say red).
- ii. Consider the subgraph whose vertices are six vertices joined to $v$ by red edges. Note that either this subgraph has at least one red edge, or all its edges are blue or green. Show that in the first case $K_{17}$ has a red triangle, and in the second either a green or a blue triangle.
- iii. Deduce that $R(3, 3, 3) \leq 17$.

## 16.4 EUCLIDEAN RAMSEY THEORY

There are some fascinating Ramsey-type problems of a geometric nature. Here are some involving either coloring all points on the real line (or, if you prefer, the $x$-axis, or any other infinite straight line) or coloring all the points in the plane.

### PROBLEM 16.1

Suppose that, with each point on the real line, we associate either the color red or the color blue (loosely, “we color each point of the line red or blue”). Show that we can always find points $A$, $B$, $C$, on the line, all of the same color and with $B$ the midpoint of $AC$.

![](img/eb401bf41900fd678cd9d368a197e486_332_0.png)

FIGURE 16.5

### Solution

We can certainly find points X, Z of the same color, say red. If the midpoint of XZ, say Y, is also red, then we can put A = X, B = Y, and C = Z, and there is nothing left to prove.

So, let us suppose that Y is blue. Now choose points U, V as in Figure 16.5 so that the lengths of the line segments UX, XZ, and ZV are all equal.

Now, if U is red, then A = U, B = X, C = Z forms a red trio of the required kind. If V is red, then A = X, B = Z, C = V is a red trio of the required kind. If neither U nor V is red, then each is blue and A = U, B = Y, C = V is a blue trio of the required kind.

Another example of similar type is:

### PROBLEM 16.2

Prove that if every point of the plane is colored red or blue, the plane contains a monochromatic rectangle, that is, a rectangle with all four vertices of the same color.

### Solution

Draw any three (horizontal) parallel lines in the plane and, at right angles to those, seven vertical (and so mutually parallel) lines. (Do you wonder why seven? You’ll see!) In our example in Figure 16.6 we have numbered the vertical lines to make it easy to refer to them.

On each of these seven vertical lines we write three letters, for example r, r, b, indicating the colors (in order from top to bottom) of the points of intersection of the line with the three horizontal lines. If two of these trios begin with r, r, then there is a rectangle with four red vertices. If two of these trios begin with b, b, there is a rectangle with four blue vertices. If neither of these cases occurs, at least five of these trios begin either r, b or b, r (on the vertical lines 2, 3, 4, 6, and 7 in our example). So there are either at least three lines where the trio begins b, r or at least three lines where the trio begins r, b. Without loss of generality we can assume there are three lines where the trio begins b, r (lines 2, 4, and 7 in our example). So the trios on these three lines are all either b, r, b or b, r, r, and hence at least two of these must be the same. If there are two lines with the trio b, r, b, there is a rectangle with all vertices blue (formed by the vertices shown on lines 2 and 7 in our example), and if there are two lines with the trio b, r, r, there is a rectangle with all vertices red. So in each case there is a monochromatic rectangle.

You will note that the hypothesis that every point of the plane is colored red or blue is much, much stronger than is needed to draw the conclusion that there is a monochromatic rectangle. Our solution shows that we can deduce this conclusion from the much weaker hypothesis that we have a 3 × 7 rectangular array of points of the plane each of which is colored red or blue. This suggests that from the assumption that every point of the plane is colored red and blue, more interesting conclusions can be drawn than just the existence of the monochromatic rectangle. We give a few examples.
