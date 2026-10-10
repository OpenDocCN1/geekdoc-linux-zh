$n \equiv 1 \pmod{4}$. (See Exercise 29.) The self-complementary graphs of order 5 or less are shown in Figure 1.20.

![](bbox=[0.08, 0.17, 0.92, 0.28])

# The Union and Join of Graphs

We next describe some common binary operations defined on graphs. This discussion introduces notation that will be especially useful in giving examples. Over the years, different authors have used different notation for the operations we are about to describe. In the following definitions, we assume that $G_1$ and $G_2$ are two graphs with disjoint vertex sets.

The **union** $G = G_1 + G_2$ of $G_1$ and $G_2$ has vertex set $V(G) = V(G_1) \cup V(G_2)$ and edge set $E(G) = E(G_1) \cup E(G_2)$. The union $G + G$ of two disjoint copies of $G$ is denoted by $2G$. Indeed, if a graph $G$ consists of $k\ (k \geq 2)$ disjoint copies of a graph $H$, then we write $G = kH$. The graph $2K_1 + 3K_2 + K_{1,3}$ is shown in Figure 1.21(a). The **join** $G = G_1 \vee G_2$ of $G_1$ and $G_2$ has vertex set $V(G) = V(G_1) \cup V(G_2)$ and edge set

$$E(G) = E(G_1) \cup E(G_2) \cup \{uv : u \in V(G_1), v \in V(G_2)\}.$$

Using the join operation, we see that $\overline{K_s} \vee \overline{K_t} = K_{s,t}$. Another illustration is given in Figure 1.21(b).

![](bbox=[0.08, 0.7, 0.92, 0.9])