are **nonattacking queens**. Clearly, every pair of queens on the chessboard of Figure 12.9 are attacking. The minimum number of nonattacking queens such that every square of the chessboard can be reached by one of the queens is also 5. A possible placement of five nonattacking queens is shown in Figure 12.10.

![](bbox=[0.15, 0.23, 0.85, 0.49])

The connection between the chessboard problem described above and dominating sets in graphs is immediate. The 64 squares of a chessboard are the vertices of a graph $G$ and two vertices (squares) are adjacent in $G$ if each of the two squares can be reached by a queen on the other square in a single move. The graph $G$ is referred to as the **queen’s graph**. Then the minimum number of queens that dominate all the squares of a chessboard is $\gamma(G)$. The minimum number of nonattacking queens that dominate all the squares of a chessboard is the minimum cardinality of a dominating set in $G$ that is also independent.

Domination as a theoretical area in graph theory was formalized by Claude Berge in 1958 [22, p. 40] and Oystein Ore [180, Chapter 13] in 1962. Since 1977, when Ernest Cockayne and Stephen Hedetniemi [60] presented a survey of domination results, domination theory has received considerable attention.

# Minimal Dominating Sets

A **minimal dominating set** in a graph $G$ is a dominating set that contains no dominating set as a proper subset. A minimal dominating set of minimum cardinality is, of course, a minimum dominating set and consists of $\gamma(G)$ vertices. For the graph $G$ of Figure 12.8, the set $S_1=\{v_1, v_2, y_1, y_2\}$ is a minimal dominating set that is not a minimum dominating set. Minimal dominating sets were characterized by Ore [180, p. 206].