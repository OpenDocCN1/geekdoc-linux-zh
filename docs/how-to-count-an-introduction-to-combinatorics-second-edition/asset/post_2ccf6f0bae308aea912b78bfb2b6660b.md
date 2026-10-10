
![](img/eb401bf41900fd678cd9d368a197e486_297_0.png)

FIGURE 14.7

**14.4.3B** How many different positions can occur during a game of noughts and crosses? (Consider both the rotations and reflections of the noughts and crosses grid.)

## 14.5 PÓLYA'S COUNTING THEOREM: THE PROOF

We now set about giving a proof of Pólya's counting theorem. Throughout this section we suppose that $D$ and $C$ are two sets, that $w$ is a weight function on $C$, and that $G$ is a group of permutations of $D$ that acts on the set $X$ of all mappings from $D$ to $C$ in the standard way; that is,

$$\text { for } \pi \in G, \text { and } f \in X, \quad \pi \triangleright f := f \circ \pi^{-1} \text {.}$$

The strategy of the proof is to partition $X$ according to the weights of the mappings, to observe that $G$ acts on each set of this partition separately, and to use Frobenius's counting theorem to count the number of different orbits in each case. Our proof proceeds by a series of lemmas.

In Chapter 13, when we calculated the values of $\#(Fix(g))$, we used the idea that a coloring of a chessboard is fixed by a particular permutation of its squares if and only if all the squares in any one cycle of the permutation have the same color. In general, a coloring $f$ is fixed by a permutation $\pi$ if and only if $f$ takes a constant value on each cycle of $\pi$. That is, for each cycle $(d_{1}, d_{2}, \ldots, d_{k})$ of $\pi$, we must have $f(d_{1}) = f(d_{2}) = \ldots = f(d_{k})$. Note also that $(d_{1}, d_{2}, \ldots, d_{k})$ is a cycle of $\pi$ if and only if $d_{2} = \pi(d_{1})$, $d_{3} = \pi(d_{2})$, $\ldots$, $d_{k} = \pi(d_{k-1})$, and $d_{1} = \pi(d_{k})$. Thus each cycle of $\pi$ has the form $(d \; \pi(d) \; \pi(\pi(d)) \; \ldots)$. It follows that $f$ is constant on each cycle of $\pi$ if and only if

$$\text { for all } d \in D, \quad \quad\quad\quad f(d) = f(\pi(d)), \quad\quad(14.11)$$

since Equation 14.11 is equivalent to $f(d) = f(\pi(d)) = f(\pi(\pi(d))) = \ldots$ .

We now give a general proof of this result.

### LEMMA 14.4

Let $\pi$ be a permutation of $D$. Then for each $f \in X$,

$$f \in Fix(\pi) \Leftrightarrow f \text{ is constant on each cycle of } \pi .$$

We have that

$$\begin{align*} f \in Fix(\pi) & \Longleftrightarrow \pi \circ f = f \\ & \Longleftrightarrow f \circ \pi^{-1} = f \\ \Longleftrightarrow & \text{for all } x \in D, f(\pi^{-1}(x)) = f(x). \tag{14.12}\end{align*}$$

Now, as $\pi$ is a permutation of $D$, $\{\pi^{-1}(x) : x \in D\} = D$, and hence, writing $d$ for $\pi^{-1}(x)$, so that $x = \pi(d)$, we have

$\text{for all } x \in D, f(\pi^{-1}(x)) = f(x) \Longleftrightarrow \text{for all } d \in D, f(d) = f(\pi(d)),$

and so by Equation 14.12,

$$\begin{align*} f \in Fix(\pi) & \Longleftrightarrow \text{for all } d \in D, f(d) = f(\pi(d)) \\ & \Longleftrightarrow f \text{ is constant on each cycle of } \pi.\end{align*}$$

The next lemma leads us to a formula for the inventory of $Fix(\pi)$. By Lemma 14.4 this is the inventory of all functions that are constant on each cycle of $\pi$. The cycles of $\pi$ partition $D$ into disjoint sets. So we first consider the inventory of all functions that are constant on each set making up a partition of $D$.

### LEMMA 14.5

Let $D_1 \cup D_2 \cup \dots \cup D_k$ be a partition of $D$ into disjoint sets. The inventory of those functions in $X$ that are constant on each of the sets $D_i$ is

$$\begin{align*} \prod_{i=1}^{k} \sum_{c \in \mathcal{C}} w(c)^{\#(D_i)}. \tag{14.13}\end{align*}$$

Choosing a function, say $f$, that is constant on each set $D_i$ is equivalent to choosing, for $1 \leq i \leq k$, an element, say $c_i$, from $\mathcal{C}$ to be the value of $f(d)$ for all $d \in D_i$. Since $f$ then takes this value $\#(D_i)$ times, such a choice of $c_i$ contributes $w(c_i)^{\#(D_i)}$ to the weight of $f$. So the weight of $f$ is obtained by choosing, for $1 \leq i \leq k$, the appropriate term from the sum $\sum_{c \in \mathcal{C}} w(c)^{\#(D_i)}$ and then multiplying all these terms together. So the inventory of all the functions in $X$ that are constant on each set $D_i$ is the sum of all the terms obtained in this way. Hence this inventory is given by the product in the expression 14.13.

The formula 14.13 is beginning to look like the formula in Pólya's theorem. The next lemma brings in the cycle types of the permutations. Recall that we use $ct(\pi)$ for the cycle type of a permutation $\pi$.

### LEMMA 14.6

If $ct(\pi) = x_{k_1}^{k_1} \cdots x_{k_r}^{k_r}$, then the inventory of $Fix(\pi)$ is

$$\left(\sum_{c \in C} w(c)^{k_1}\right) \times \left(\sum_{c \in C} w(c)^{k_2}\right) \times \ldots \times \left(\sum_{c \in C} w(c)^{k_r}\right) \tag{14.14}$$

or, equivalently,

$$ct(\pi)\left\{\sum_{c \in C} w(c), \sum_{c \in C} w(c)^2, \sum_{c \in C} w(c)^3, \ldots\right\}. \tag{14.15}$$

#### Proof

The cycles of $\pi$ partition $D$ into $r_1$ sets of size $k_1$, $r_2$ sets of size $k_2$, and so on. By Lemma 14.4, $Fix(\pi)$ is the set of functions that are constant on all these sets, and hence, by Lemma 14.5, the inventory of $Fix(\pi)$ is as given by the formula 14.14. This formula is obtained from the cycle type of $\pi$ by replacing each occurrence of $x_k$ for $k=1,2,3, \ldots$ by $\sum_{c \in C} w(c)^k$. Hence we can rewrite this formula as given in the formula 14.15. This completes the proof.

We now partition $X$ into sets of functions with the same weight. Clearly, the relation $\sim$ defined on $X$ by

$f \sim g \Leftrightarrow W(f) = W(g)$

is an equivalence relation. We let $x_1, x_2, \ldots, X$, be the equivalence classes of this relation. So they form a partition of $X$. (For example, in our example of the colorings of a $2 \times 2$ chessboard, the set $X$ of all 16 colorings is partitioned according to the numbers of black and white squares in a particular coloring. So one of the equivalence classes is the set of all colorings with two black squares and two white squares, namely, $\{C6, C7, C8, C9, C10, C11\}$. Note that within this equivalence class there are two different patterns. You will also note that all the colorings of any one particular pattern lie in the same equivalence class. Our next result generalizes this observation.)

The next lemma implies that $G$ acts on each set of this partition separately.

### LEMMA 14.7

Suppose that $f,g \in X$ have the same pattern; that is, they occur in the same orbit of the group action. Then $W(f) = W(g)$.

#### Proof

Suppose $f$ and $g$ are in the same orbit of the group action. Then for some $\pi \in G$, $\pi \circ f = g$, and thus $f \circ \pi^{-1} = g$, and hence

$$W(g) = \prod_{d \in D} w(g(d)) = \prod_{d \in D} w(f(\pi^{-1}(d))) \tag{14.16}$$

Since $\pi$ is a permutation of $D$, the set of values taken by $\pi \circ (d)$ as $d$ runs through $D$ is just $D$ itself. Hence the product in the right-hand term of Equation 14.16 is the same as $\prod_{d \in D} w(f(d)) = W(f)$. Thus it follows that $W(g) = W(f)$.

We have now seen that for each set $X_i$ of the partition of $X$ determined by the weight of the functions, if $f \in X_x$, then $\pi \circ f \in X_x$. In this sense $G$ acts separately on each set $X_x$. We use the notation $\pi_x$ to indicate that we are restricting our attention to the action of the permutation $\pi$ on the set $X_x$. We can then apply Frobenius's counting theorem to count the number of orbits of the action of $G$ on each set $X_x$. This enables us to prove Pólya's counting theorem, which, for convenience, we restate.

### THEOREM 14.3

**Pólya's Counting Theorem**

Let $X$ be the set of all mappings from a set $D$ to a set $C$, and let $w$ be a weight function on $C$. Let $G$ be a group of permutations of $D$ whose action on $X$ is given by:

> $\forall \pi \in G, \text{ and } f \in X, \quad \pi \circ f = f \circ \pi^{-1}.$

Then the pattern inventory is obtained from the cycle index of $G$, by substituting $\sum_{c \in C} w(c)^k$ for $x_k$, for $k = 1,2,3,\ldots$. Thus if $CI(G)(x_1,x_2,x_3,\ldots)$ is the cycle index of $G$, the pattern inventory is

> $$CI(G)\bigg( \sum_{c \in C} w(c), \sum_{c \in C} w(c)^2, \sum_{c \in C} w(c)^3, \ldots \bigg) . \qquad (14.8)$$

#### Proof

We let $PI$ be the pattern inventory. Suppose that $W_i$ is the common weight of all the functions in the set $X_i$ of the partition, and that there are $m_i$ different patterns represented by the functions in $X_i$. We have seen, from Lemma 14.7, that no pattern is represented by functions in more than one of the sets of the partition. It follows that

> $$PI = \sum_{i=1}^{N} m_i W_i. \qquad$$

By Frobenius's counting theorem,

> $$m_i = \frac{1}{\#(G)} \sum_{\pi \in G} \#(\text{Fix}(\pi_i)), \qquad$$

and hence

> $$PI = \frac{1}{\#(G)} \bigg( \sum_{i=1}^{N} \sum_{\pi \in G} \#(\text{Fix}(\pi_i)) \, W_i \bigg). \qquad (14.17)$$
