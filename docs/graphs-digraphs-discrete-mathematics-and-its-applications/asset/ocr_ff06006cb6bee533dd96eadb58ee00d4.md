# Discharging

Heinrich Heesch introduced the idea of assigning what is called a “charge” to each vertex of a planar graph as well as **discharging rules** which indicate how charges can be redistributed among the vertices. In a maximal planar graph $G$, every vertex $v$ of $G$ is assigned a **charge** of $6 - \deg v$. In particular, every vertex of degree 5 receives a charge of $+1$, every vertex of degree 6 receives a charge of 0, and every vertex of degree 7 or more receives a negative charge. By appropriately redistributing positive charges, some useful results can often be obtained. According to equation (10.3) in the proof of Theorem 10.12, the sum of the charges of the vertices of a maximal planar graph of order 4 or more is 12. This is restated below.

> **Theorem 10.13** If $G$ is a maximal planar graph of order $n \ge 4$, size $m$ and maximum degree $\Delta(G) = \Delta$ such that $G$ has $n_i$ vertices of degree $i$ for $3 \le i \le \Delta$, then
> $\displaystyle\sum_{i=3}^{\Delta}(6-i)n_i = 12$.

According to Theorem 10.10, every vertex of a maximal planar graph of order 4 or more has degree 3 or more. Consequently, no vertex can contribute more than 3 to the sum in Theorem 10.13. Because this sum is 12, we have the following corollary, which is an extension of Corollary 10.5.

> **Corollary 10.14** If $G$ is a maximal planar graph of order at least 4, then $G$ contains at least four vertices whose degrees are at most 5.

We now use the discharging method to give an alternative proof of Theorem 10.11.

> **Theorem 10.15** If $G$ is a maximal planar graph of order 4 or more, then $G$ contains at least one of the following: (1) a vertex of degree 3, (2) a vertex of degree 4, (3) two adjacent vertices of degree 4, (4) two adjacent vertices, one of which has degree 5 and the other has degree 6.

**Proof.** Assume, to the contrary, that there exists a maximal planar graph $G$ of order $n \ge 4$, where there are $n_i$ vertices of degree $i$ for $3 \le i \le \Delta = \Delta(G)$ such that $G$ contains none of (1)\u2013(4). Thus, $\delta(G) = 5$. To each vertex $v$ of $G$ assign the charge $6 - \deg v$. Hence, each vertex of degree 5 receives a charge of $+1$, each vertex of degree 6 receives no charge, and each vertex of degree 7 or more receives a negative charge. By Theorem 10.13, the sum of the charges of the vertices of $G$ is
$\displaystyle\sum_{i=3}^{\Delta}(6-i)n_i = 12$.