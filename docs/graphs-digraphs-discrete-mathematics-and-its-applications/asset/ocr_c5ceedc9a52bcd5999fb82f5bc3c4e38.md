problems in polynomial time. The concept of **NP**-completeness was initiated in 1971 by Stephen Cook [61] who gave an example of the first **NP**-complete problem. The following year Richard M. Karp [139] described some twenty diverse **NP**-complete problems. There are now known to be thousands of **NP**-complete problems. For example, the problem of determining whether a graph is Hamiltonian is **NP**-complete.

# ## 6.4 Highly Hamiltonian Graphs

As we have already remarked, obtaining an applicable characterization of Hamiltonian graphs remains an unsolved problem in graph theory. In view of the lack of success in developing such a characterization, it is not surprising that special classes of Hamiltonian graphs have been singled out for investigation. We now discuss several types of such *highly Hamiltonian* graphs.

# ### Hamiltonian-Connected Graphs

A graph $G$ is **Hamiltonian-connected** if for every pair $u, v$ of vertices of $G$, there is a Hamiltonian $u-v$ path in $G$. Necessarily, every Hamiltonian-connected graph of order 3 or more is Hamiltonian but the converse is not true. The cubic graph $G_1 = C_3 \square K_2$ of Figure 6.9 is Hamiltonian-connected, while the 3-cube $G_2 = C_4 \square K_2 = Q_3$ is not Hamiltonian-connected. The graph $G_2$ contains no Hamiltonian $u-v$ path, for example. (See Exercise 36.)

![](bbox=[0.17, 0.73, 0.83, 0.9])

There is a sufficient condition for a graph to be Hamiltonian-connected that is similar in statement to the sufficient condition for a graph to contain a Hamiltonian cycle presented in Theorem 6.1. The following theorem is also due to Oystein Ore [181] and provides a sufficient condition for a graph to be Hamiltonian-connected.

> **Theorem 6.15** Let $G$ be a graph of order $n$. If $\sigma_2(G) \geq n+1$, then $G$ is Hamiltonian-connected.

**Proof.** Let $u$ and $v$ be two vertices of $G$ and let $H$ be the graph of order $n+1$ obtained from $G$ by adding a new vertex $w$ that is joined to $u$ and $v$. We now