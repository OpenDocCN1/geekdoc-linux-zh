the notation in both instances is common and we will never use the terms domination number and the genus of a graph in the same discussion.

The sets $S_1 = \{v_1, v_2, y_1, y_2\}$ and $S_2 = \{w_1, w_2, x\}$ are both dominating sets for the graph $G$ of Figure 12.8, indicated by solid circles. Since the dominating set $S_2$ consists of three vertices, $\gamma(G) \leq 3$. A vertex of degree 4 dominates five vertices. Because $\Delta(G) = 4$ and $G$ has order 11, two vertices of $G$ can dominate at most ten vertices of $G$ and so $\gamma(G) \geq 3$. Thus, $\gamma(G) = 3$.

![](bbox=[0.0, 0.3, 1.0, 0.48])

# Figure 12.8: Dominating sets

Dominating sets appear to have their origins in the game of chess, where the goal is to cover or dominate the squares of a chessboard by certain chess pieces. In 1862 Carl Friedrich de Jaenisch [65] considered the problem of determining the minimum number of queens (which can move either horizontally, vertically or diagonally over any number of unoccupied squares) that can be placed on a chessboard such that every square is either occupied by a queen or can be occupied by one of the queens in a single move. The minimum number of such queens is 5 and one possible placement of five such queens is shown in Figure 12.9.

![](bbox=[0.3, 0.7, 0.7, 0.9])

# Figure 12.9: The minimum number of queens dominating the squares of a chessboard

Two queens on a chessboard are **attacking** if the square occupied by one of the queens can be reached by the other queen in a single move; otherwise, they