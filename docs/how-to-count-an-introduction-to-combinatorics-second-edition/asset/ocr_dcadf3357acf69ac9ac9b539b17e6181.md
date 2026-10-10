If you look at Table 10.3 you will see that in carrying out Dijkstra's algorithm for a graph with eight vertices, we need to calculate some of the entries in an $8 \times 8$ table. We hope that this makes it plausible that the number of steps needed to implement the algorithm grows proportionately to $n^2$ where $n$ is the number of vertices in the table. For a detailed justification of this see the book *Algorithmic Graph Theory*.4

![](bbox=[0.3, 0.2, 0.75, 0.45])

FIGURE 10.20

![](bbox=[0.2, 0.5, 0.8, 0.6])

FIGURE 10.21

TABLE 10.4

| Edge | Weight |
|------|--------|
| $ub$ | 3 |
| $uc$ | 4 |
| $ae$ | 7 |
| $av$ | 5 |
| $bd$ | 7 |
| $bf$ | 4 |
| $cd$ | 2 |
| $cg$ | 3 |
| $df$ | 5 |
| $dg$ | 7 |
| $ev$ | 2 |
| $fg$ | 6 |