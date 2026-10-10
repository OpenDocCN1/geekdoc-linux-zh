![](bbox=[0.28, 0.08, 0.75, 0.23])

FIGURE 9.20

this not the case for region $C$. Because the graph of Figure 9.17 has two vertices joined by two edges, there is one region, namely $E$, which has a boundary made up of just two edges. This cannot happen in a simple graph, where the boundary of a region must be made up of at least three edges. This simple observation has a useful consequence.

# **THEOREM 9.7**

If $G$ is a connected planar simple graph with $v$ vertices and $e$ edges, then $e \leq 3v - 6$.

# **Proof**

Suppose that $G$ is drawn in the plane with $f$ regions. Then, by Euler's formula,

```
$f = e - v + 2.$  \(9.4\)
```

Since each region has a boundary made up of at least three edges, and each edge can be part of the boundary of at most two regions, we have

```
$3f \leq 2e.$  \(9.5\)
```

From Equation 9.4 and inequality 9.5 we obtain

```
$3(e - v + 2) \leq 2e,$
```

from which it immediately follows that

```
$e \leq 3v - 6.$
```

This inequality enables us to answer the question as to whether the complete graph $K_{5}$ is planar. In this graph there are five vertices, and, as each pair of vertices is joined by an edge, there are 10 edges. Thus $e(=10) > 3v - 6(=9)$, and hence, by Theorem 9.7, $K_{5}$ is not planar.

And now, what about our utilities problem? This was Problem **9B** of Chapter 1. Recall that the problem is whether the graph shown in Figure 9.21 in nonplanar form is in fact planar.

We now reveal that the utilities problem *cannot be solved*; that is, the graph of Figure 9.21 is not planar. We don't mean that, so far, no one has been clever enough to find a way to do it. We *do* mean that someone *has been* clever enough to *prove* that no one will ever be able to do it because *it can't be done!*