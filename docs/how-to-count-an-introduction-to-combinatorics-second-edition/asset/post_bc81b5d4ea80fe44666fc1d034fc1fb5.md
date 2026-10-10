
![](img/eb401bf41900fd678cd9d368a197e486_224_0.png)

FIGURE 10.9

Let $w$ be the one vertex to which it is joined. We let $a_1$ be the label that is assigned to the vertex $w$.

Now we delete the vertex $v$ and the edge $vw$, and let $T'$ be the resulting graph. $T'$ will also be a tree. We apply the same process to $T'$. That is, we pick the vertex of degree 1 in $T'$ with the lowest label, say $v'$, and let $a_2$ be the label associated with the one vertex, say $w'$, to which $v'$ is joined by an edge. Then we obtain the tree $T''$ by deleting the vertex $v'$ and the edge $v'w'$ from $T'$, and so on, until there are just two vertices left. The resulting sequence $(a_1, a_2, \dots, a_{n-2})$ is called the Prüfer code of the original tree $T$.

For example, we apply this process to the following labeled tree in Figure 10.9(i).

The vertex of degree 1 with the lowest label is the vertex labeled 3. It is joined to the vertex labeled 2. Thus $a_1 = 2$. Deleting the vertex labeled 3 and its adjacent edge, we obtain the tree in Figure 10.9(ii). In this tree the vertex of degree 1 with the lowest label is the vertex labeled 2. It is joined to the vertex labeled 4. So $a_2 = 4$. We delete the vertex labeled 2 and its adjacent edge to obtain the tree in Figure 10.9(iii). Now the vertex of degree 1 with the lowest label is the vertex labeled 5, and we see that it is joined to the vertex labeled 1. So $a_3 = 1$. Proceeding this way we see that $a_4 = 4$ and $a_5 = 1$. So the Prüfer code of the original tree is $(2, 4, 1, 4, 1)$.

To complete the proof we need to show that there is a one-to-one correspondence between labeled trees and all possible Prüfer codes. We do this by showing how, given a Prüfer code, say $(a_1, a_2, \dots, a_{n-2})$, we can construct a tree to which it corresponds.

The procedure is as follows. Throughout, "number" means one of the integers $1, 2, \dots, n$. We join vertices labeled $1, 2, \dots, n$ using the following process. First, find the least number, say $b_1$, that does not occur in the sequence $(a_1, a_2, \dots, a_{n-2})$, and join the vertex labeled $b_1$ to the vertex labeled $a_1$. Next, find the least number, say $b_2$, that does not occur in the sequence $(a_2, \dots, a_{n-2})$, and join the vertex labeled $b_2$ to the vertex labeled $a_2$, and then find the least number, say $b_3$, other than $b_1$ and $b_2$, that does not occur in the sequence $(a_3, \dots, a_{n-2})$, and so on. Then when there are no numbers left in the sequence we join the two vertices not in the list $b_1, \dots, b_{n-2}$.

We illustrate this process by applying it to the Prüfer code $(2, 4, 1, 4, 1)$ as shown in Figure 10.10.

![](img/eb401bf41900fd678cd9d368a197e486_225_0.png)

FIGURE 10.10

We see that this process ends up with the original tree. It is not difficult to prove, by induction on $n$, that this always happens. We ask you to do this in Exercise 10.2.3A.

It follows that there is a one-to-one correspondence between the labeled trees with $n$ vertices and the Prüfer codes. A Prüfer code for a tree with $n$ vertices is a sequence of $n - 2$ positive integers taken from the set $\{1, 2, \dots, n\}$. So there are $n^{n-2}$ different Prüfer codes, and hence there are $n^{n-2}$ labeled trees with $n$ vertices.

## Exercises

- **10.2.1A** Find the Prüfer codes for the labeled trees shown in Figure 10.11.
- **10.2.1B** Find the Prüfer codes for the labeled trees shown in Figure 10.12.
- **10.2.2A** Draw the trees whose Prüfer codes are (i) $(1,2,1,2,1,2)$ and (ii) $(1,2,3,1,2,3)$.
- **10.2.2B** Draw the trees whose Prüfer codes are (i) $(1,2,2,3,3,3)$ and (ii) $(3,3,3,2,2,1)$.
- **10.2.3A** Let $T$ be a tree. Prove that the labeled tree constructed from the Prüfer code, $P$, of $T$ using the method described in the proof of Theorem 10.2 is isomorphic to $T$.

![](img/eb401bf41900fd678cd9d368a197e486_226_0.png)

FIGURE 10.11

![](img/eb401bf41900fd678cd9d368a197e486_226_1.png)

FIGURE 10.12

- **10.2.3B**
  - i. Two labeled trees have Prüfer codes (a) $(1,2,3,4,5,6)$ and (b) $(1,4,2,5,3,6)$, respectively. Are their underlying (unlabeled) graphs isomorphic?
  - ii. Prove that if, in a labeled graph, the vertex with label $r$ has degree $k$, then the number $r$ occurs $k - 1$ times in its Prüfer code.

- **10.2.4A**
  We define an *edge-labeled graph* to be a triple $(V,E,I)$, where $(V,E)$ is a graph and $I: E \to \{1,2,\dots,n\}$ is a bijection, where $n$ is the number of edges. Two edge-labeled trees $(V_1,E_1,I_1)$ and $(V_2,E_2,I_2)$ are said to be *isomorphic* if there is bijection $\Theta: V_1 \to V_2$ that is an isomorphism between the trees $(V_1,E_1)$ and $(V_2,E_2)$ and that matches edges with the same label. That is, for each edge, $uv \in E_i$, $I_i(\{u,v\}) = I_j(\{u,v\})$. Show that there are $m^{m-3}$ different (that is, nonisomorphic) edge-labeled trees with $m$ vertices.

- **10.2.4B**
  Use Cayley's Theorem to show that there are at least $n^{n-2}/(n-1)!$ (unlabeled) trees with $n$ vertices.

### 10.3 SPANNING TREES AND MINIMAL CONNECTORS

In this section we discuss some practical problems to which graph theory contributes solutions. Suppose that you want to build bridges to connect four islands. If you want it to be possible to walk, or drive, directly from any one island to any other island, you would need to build six bridges altogether. Six bridges would be needed because this is the number of edges in the complete graph with four vertices. However, as bridges are expensive to build, it might be considered better just to build enough bridges to connect up all the islands. What is the smallest number of bridges that you would need to build?

It is easily seen that only three bridges are needed. They can be chosen in more than one way. One possibility is shown in Figure 10.13. In the language of graph theory we have constructed a tree, and we can regard this tree as a subgraph of the complete graph, $K_4$, with four vertices. We say that the tree *spans* $K_4$ since each vertex is connected to each other vertex using only the edges of this tree.

We are ready for a formal definition.

#### DEFINITION 10.4

Let $G$ be a graph. We say that the subgraph $G'$ *spans* $G$ if it has the same vertices as $G$. A *spanning tree* of $G$ is a subgraph that spans $G$ and that is a tree.

Which graphs have spanning trees? If $G$ is not connected, then no subgraph with the same set of vertices can be connected, and so $G$ does not have a spanning tree. On the other hand it is not difficult to show that every connected graph has a spanning tree. In particular, for large $n$, the complete graph $K_n$ has lots of spanning trees. If we label the vertices of the complete graph, $K_n$, with $n$ vertices with the numbers $1,2,\dots,n$, then the spanning trees for $K_n$ correspond to the labeled trees with $n$ vertices, and so by Cayley’s theorem, $K_n$ has $n^{n-2}$ different spanning trees.

In many practical applications we seek more than just a spanning tree. We illustrate this with the following problem, before discussing the general case.

#### PROBLEM 10.4

It is desired to connect five islands by tunnels. The graph in Figure 10.14 shows the cost (in suitable units, for example, 1 unit = £10,000,000) of building a tunnel between pairs of islands for which this is feasible. Which tunnels should be built so as to connect the islands for the smallest total cost?

![](img/eb401bf41900fd678cd9d368a197e486_227_0.png)

![](img/eb401bf41900fd678cd9d368a197e486_227_1.png)

**Solution**

Tunnels should be built corresponding to the edges $ab$, $ae$, $de$, and $ce$. This incurs a total cost of $3 + 5 + 6 + 8 = 22$ units.

**Comment**

For the time being we just assert that this is the minimal cost of a spanning tree, say $T$, for the graph shown in Figure 10.14. We know that a tree with five vertices will have four edges, and so the solution must involve four tunnels. In a case as small as this, it is possible to find these tunnels just by trying possibilities. But even in this case, the solution is not completely obvious, as our solution does not simply consist of the four cheapest tunnels. In fact there is an algorithm, that is, a systematic procedure, for finding an optimal solution. (See Exercise 10.3.1A for the application of this algorithm to the solution to Problem 10.4.) Before we describe this, we need set up the theoretical framework for this and similar problems.

In the graph in Figure 10.14 each edge has associated with it a number. The magnitudes of these numbers are significant, unlike the case with labeled graphs where the numbers associated with the vertices serve merely as labels and so could be replaced by other symbols. In Figure 10.14 these numbers represent costs. In other cases they could represent distances or times. The general term for these numbers is *weights*, and a graph that has weights associated with its edges is called a *weighted graph*. In our example the weights are normally positive integers, but there is no need to impose this restriction. However, it is convenient to require that the weights are nonnegative numbers. Thus we phrase our definition as follows.

#### DEFINITION 10.5

A *weighted graph* is a pair $(G, \mu)$, where $G = (V,E)$ is a graph and $\mu : E \to \mathbb{R}$ is a mapping that associates with each edge, $e$, a nonnegative real number, $\mu(e)$. Given a weighted graph $(G,\mu)$, and a subgraph $G' = (V',E')$ of the graph $G = (V,E)$, the *weight* of $G'$ is the sum of the weights of the edges in $E'$. We let $\mu(G')$ be the weight of $G'$. Therefore, $\mu(G') = \sum_{e \in E'} \mu(e)$.

Often, we represent a weighted graph by a picture of the graph with numbers alongside the edges to indicate their weights. For example, we can regard Figure 10.14 as a picture of a weighted graph. The spanning tree $T$ given in our solution to Problem 10.4 has weight 22. Our claim in giving $T$ as the solution to Problem 10.4 is that there is no other spanning tree with a lower weight. Since a spanning tree connects all the vertices of the original graph, we frame the following definition.

#### DEFINITION 10.6

Given a weighted graph $(G,\mu)$ and a spanning tree, $T$ of $G$, we say that $T$ is a *minimal connector* of $G$ if for every spanning tree $T'$ of $G$, $\mu(T) \leq \mu(T')$.

In general, a weighted connected graph will have more than one minimal connector. The extreme case is where all the edges have the same weight. Then all the spanning
