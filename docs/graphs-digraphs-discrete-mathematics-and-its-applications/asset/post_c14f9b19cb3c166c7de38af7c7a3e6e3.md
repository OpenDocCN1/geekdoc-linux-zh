
The notation in both instances is common, and we will never use the terms *domination number* and *the genus of a graph* in the same discussion.

The sets $S_1 = \{v_1, v_2, y_1, y_2\}$ and $S_2 = \{w_1, w_2, x\}$ are both dominating sets for the graph $G$ of Figure 12.8, indicated by solid circles. Since the dominating set $S_2$ consists of three vertices, $\gamma(G) \leq 3$. A vertex of degree 4 dominates five vertices. Because $\Delta(G) = 4$ and $G$ has order 11, two vertices of $G$ can dominate at most ten vertices of $G$ and so $\gamma(G) \geq 3$. Thus, $\gamma(G) = 3$.

![](img/598a6ae3fd44120830ada34717906f29_334_0.png)

## Figure 12.8: Dominating sets

Dominating sets appear to have their origins in the game of chess, where the goal is to cover or dominate the squares of a chessboard by certain chess pieces. In 1862 Carl Friedrich de Jaenisch [65] considered the problem of determining the minimum number of queens (which can move either horizontally, vertically or diagonally over any number of unoccupied squares) that can be placed on a chessboard such that every square is either occupied by a queen or can be occupied by one of the queens in a single move. The minimum number of such queens is 5 and one possible placement of five such queens is shown in Figure 12.9.

![](img/598a6ae3fd44120830ada34717906f29_334_1.png)

## Figure 12.9: The minimum number of queens dominating the squares of a chessboard

Two queens on a chessboard are **attacking** if the square occupied by one of the queens can be reached by the other queen in a single move; otherwise, they are **nonattacking queens**. Clearly, every pair of queens on the chessboard of Figure 12.9 are attacking. The minimum number of nonattacking queens such that every square of the chessboard can be reached by one of the queens is also 5. A possible placement of five nonattacking queens is shown in Figure 12.10.

![](img/598a6ae3fd44120830ada34717906f29_335_0.png)

## Figure 12.10: The minimum number of nonattacking queens dominating the squares of a chessboard

The connection between the chessboard problem described above and dominating sets in graphs is immediate. The 64 squares of a chessboard are the vertices of a graph $G$ and two vertices (squares) are adjacent in $G$ if each of the two squares can be reached by a queen on the other square in a single move. The graph $G$ is referred to as the **queen’s graph**. Then the minimum number of queens that dominate all the squares of a chessboard is $\gamma(G)$. The minimum number of nonattacking queens that dominate all the squares of a chessboard is the minimum cardinality of a dominating set in $G$ that is also independent.

Domination as a theoretical area in graph theory was formalized by Claude Berge in 1958 [22, p. 40] and Oystein Ore [180, Chapter 13] in 1962. Since 1977, when Ernest Cockayne and Stephen Hedetniemi [60] presented a survey of domination results, domination theory has received considerable attention.

## Minimal Dominating Sets

A **minimal dominating set** in a graph $G$ is a dominating set that contains no dominating set as a proper subset. A minimal dominating set of minimum cardinality is, of course, a minimum dominating set and consists of $\gamma(G)$ vertices. For the graph $G$ of Figure 12.8, the set $S_1=\{v_1, v_2, y_1, y_2\}$ is a minimal dominating set that is not a minimum dominating set. Minimal dominating sets were characterized by Ore [180, p. 206].

## Theorem 12.15

A dominating set $S$ of a graph $G$ is a minimal dominating set of $G$ if and only if every vertex $v$ in $S$ satisfies at least one of the following two properties:

- ($i$) there exists a vertex $w$ in $V(G)-S$ such that $N(w) \cap S = \{v\}$;
- ($ii$) $v$ is adjacent to no vertex of $S$.

**Proof.** First, observe that if each vertex $v$ in $S$ has at least one of the properties $(i)$ and $(ii)$, then $S - \{v\}$ is not a dominating set of $G$. Consequently, $S$ is a minimal dominating set of $G$.

Conversely, assume that $S$ is a minimal dominating set of $G$. Then certainly for each $v \in S$, the set $S - \{v\}$ is not a dominating set of $G$. Hence, there is a vertex $w$ in $V(G) - (S - \{v\})$ that is adjacent to no vertex of $S - \{v\}$. If $w = v$, then $v$ is adjacent to no vertex of $S$ and $(ii)$ holds. Suppose then that $w \neq v$. Since $S$ is a dominating set of $G$ and $w \notin S$, the vertex $w$ is adjacent to at least one vertex of $S$. However, $w$ is adjacent to no vertex of $S - \{v\}$. Consequently, $N(w) \cap S = \{v\}$ and so $(i)$ holds.

Theorem 12.15 can be reworded as follows: A dominating set $S$ of a graph $G$ is a minimal dominating set of $G$ if and only if for every vertex $v$ in $S$ either

- (1) $v$ dominates some vertex of $V(G)-S$ that is not dominated by any other vertex of $S$ or
- (2) no other vertex of $S$ dominates $v$.

The following result of Ore [180, p. 207] gives a property of the complementary set of a minimal dominating set in a graph without isolated vertices.

## Theorem 12.16

If $S$ is a minimal dominating set of a graph $G$ without isolated vertices, then $V(G)-S$ is a dominating set of $G$.

**Proof.** Let $v \in S$. Then $v$ has at least one of the two properties $(i)$ and $(ii)$ described in the statement of Theorem 12.15. Suppose first that there exists a vertex $w$ in $V(G)-S$ such that $N(w) \cap S = \{v\}$. Hence, $v$ is adjacent to some vertex in $V(G)-S$. Suppose next that $v$ is adjacent to no vertex in $S$. Then $v$ is an isolated vertex of the subgraph $G[S]$. Since $v$ is not isolated in $G$, the vertex $v$ is adjacent to some vertex of $V(G)-S$. Thus, $V(G)-S$ is a dominating set of $G$.

For graphs $G$ without isolated vertices, we now have an upper bound for $\gamma(G)$ in terms of the order of $G$.

## Corollary 12.17

If $G$ is a graph of order $n$ without isolated vertices, then
$$ \gamma(G) \leq n/2. $$

**Proof.** Let $S$ be a minimal dominating set of $G$. By Theorem 12.16, $V(G)-S$ is a dominating set of $G$. Thus, $\gamma(G) \leq \min \{|S|, |V(G)-S|\} \leq n/2$.

Nearly all connected graphs attaining the bound in Corollary 12.17 can be produced with the aid of the following operation. The **corona** $cor(H)$ of a graph $H$ is that graph obtained from $H$ by adding a pendant edge to each vertex of $H$. Let $G = cor(H)$, where $G$ has order $n$. Then $G$ has no isolated vertices and $\gamma(G) = n/2$. Indeed, Charles Papan and Nguyen Huy Xuong [184] showed that every component of a graph $G$ of order $n$ without isolated vertices having $\gamma(G) = n/2$ is either $C_4$ or the corona of some (connected) graph.

Vladimir Arnavutov [7] and, independently, Papan [183] obtained an upper bound for the domination number that is an improvement to that given in Corollary 12.17 when $\delta(G) \geq 5$. We will see this again in Chapter 21.

## Theorem 12.18

If $G$ is a graph of order $n$ and $\delta(G) \geq 2$, then
$$\gamma(G) \le \frac{n + n \ln (\delta(G) + 1)}{\delta(G) + 1}.$$

Béla Bollobás and Ernest Cockayne [31] showed that every graph without isolated vertices contains a minimum dominating set in which every vertex satisfies property (i) described in the statement of Theorem 12.15.

## Theorem 12.19

Every graph $G$ without isolated vertices contains a minimum dominating set $S$ such that for every vertex $v$ of $S$, there exists a vertex $w$ of $G - S$ such that $N(w) \cap S = \{v\}$.

**Proof.** Among all minimum dominating sets of $G$, let $S$ be one such that $G[S]$ has maximum size. Suppose, to the contrary, that $S$ contains a vertex $v$ that does not have the desired property. Then by Theorem 12.15, $v$ is an isolated vertex in $G[S]$. Moreover, every vertex of $V(G) - S$ that is adjacent to $v$ is adjacent to some other vertex of $S$ as well. Since $G$ contains no isolated vertices, $v$ is adjacent to a vertex $w$ in $V(G) - S$. Consequently, $(S - \{v\}) \cup \{w\}$ is a minimum dominating set of $G$ whose induced subgraph contains at least one edge incident with $w$ and hence has a greater size than $G[S]$. This produces a contradiction.

![](img/598a6ae3fd44120830ada34717906f29_337_0.png)

The domination number of a graph without isolated vertices is also bounded above by all of the independence and covering numbers.

## Theorem 12.20

If $G$ is a graph without isolated vertices, then
$$\gamma(G) \le \min\{\alpha(G), \alpha'(G), \beta(G), \beta'(G)\}.$$

**Proof.** Since every vertex cover of a graph without isolated vertices is a dominating set, as is every maximum independent set of vertices, $\gamma(G) \le \beta(G)$ and $\gamma(G) \le \alpha(G)$. Let $X$ be an edge cover of cardinality $\beta'(G)$. Then every vertex of $G$ is incident with at least one edge in $X$.

Let $S$ be a set of vertices, obtained by selecting an incident vertex with each edge in $X$. Then $S$ is a dominating set of vertices and $\gamma(G) \le |S| \le |X| = \beta'(G)$.

Next, let $M$ be a maximum matching in $G$. We construct a set $S$ of vertices consisting of one vertex incident with an edge of $M$ for each edge of $M$. Let
