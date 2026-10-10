![](bbox=[0.25, 0.09, 0.75, 0.31])

FIGURE 17.3

| | (i) | (ii) | (iii) | (iv) | (v) | (vi) | (vii) | (viii) |
|---|---|---|---|---|---|---|---|---|
| TABLE 17.1 | | | | | | | | | | | | | Boards |
| 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| k 1 | 3 | 2 | 4 | 2 | 1 | 3 | 3 | 5 |
| 2 | 1 | 0 | 2 | 0 | 0 | 1 | 2 | 7 |
| 3 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 3 |

to find obtain $r_{k}(B)$ for "large" boards, it is useful to have some information available concerning "smaller" boards. This we can gain merely by inspection, and it is with this that we begin.

# **PROBLEM 17.1**

Consider the various boards in Figure 17.3.
Calculate the values of $r_{k}(B)$ for $0 \le k \le 3$, for each of these boards.

# Solution

Most of the values in Table 17.1 are, we hope, obvious, so we confine ourselves to just a few words of explanation. The values in the first two rows arise from our observation above that for every board, $B$, $r_{n}(B)=1$, and $r_{n}(B)$ is the number of white squares on the board. We can place $k$ nonattacking rooks on an board only if we have available squares in at least $k$ rows and at least $k$ columns. This explains the zeros in rows 3 and 4 of Table 17.1. Since none of these boards have more than three rows, for each board $r_{k}(B)=0$ for $k > 3$. Column (vi) is the same as column (i) because the third row of black squares in (vi) has no effect on the values of $r_{k}(B)$. The only case where some care is needed is board (viii), where we have obtained the answers by carefully enumerating all the possibilities. We use the notation $S_{rs}$ for the square in row $r$ and column $s$, with the rows and columns numbered so that the square in the bottom left-hand corner is $S_{11}$. Then the seven ways we can place two nonattacking rooks on board (viii) are given by the following seven pairs of squares:

$(S_{13}, S_{22}),\ (S_{13}, S_{11}),\ (S_{14}, S_{22}),\ (S_{14}, S_{23}),\ (S_{18}, S_{13}),\ (S_{22}, S_{31}),\ \text{and}\ (S_{23}, S_{31}).$