To make this definition even more precise, we should really say what we mean by a “curve in the plane from $\Phi(a)$ to $\Phi(b)$” rather than just relying on geometric intuition. For those with a taste for this level of precision, we could add that, by a curve in the plane from a point $p$ to a point $q$, we mean a continuous injective (one-one) function $\gamma:[0,1]\to\mathbb{R}^{2}$, such that $\gamma(0)=p$ and $\gamma(1)=q$. Note the requirement that these curves should not go through (the point corresponding to) any other vertex, but we do allow curves to cross.*

In most of the pictures we have drawn above, the curves joining the points are all straight lines. However, our definition allows for edges to be represented by curves of any shape. For example, Figure 9.7 is a second representation in the plane of the graph that is represented by Figure 9.4.

We are now ready to give the definition of two graphs “being the same.” If we look at the graphs represented by the pictures (ii) and (iii) in Figure 9.5 we see that each graph consists of four vertices connected, as it were, in a string, so we can redraw the pictures so that they look the same, as shown in Figure 9.8.

In other words, we can match up the vertices of the graphs in such a way that two vertices of the first graph are connected by an edge if and only if the corresponding vertices of the second graph are also connected by an edge. Here is the formal definition.

# DEFINITION 9.3
Isomorphism of Graphs

The two graphs $G_{1}=\left(V_{1}, E_{1}\right)$ and $G_{2}=\left(V_{2}, E_{2}\right)$ are said to be isomorphic$‡$ if there is a bijection $\Phi: V_{1} \rightarrow V_{2}$ such that for all $a, b \in V_{1},[a, b] \in E_{1} \Longleftrightarrow[\Phi(a), \Phi(b)] \in E_{2}$. Such a mapping $\Phi$ is said to be an isomorphism between the two graphs.

![](bbox=[0.35, 0.71, 0.6, 0.82])

![](bbox=[0.2, 0.84, 0.85, 0.89])

* For gluttons for formality, we require that there is mapping, say F, such that for each edge $[a, b] \in E, \Gamma(a, b)=\gamma$ is a curve with the property that $\gamma(0)=a, \gamma(1)=b$, and for each vertex $v \notin[a, b]$, and all $t \in \mathbb{R}$ with $0 \leq t \leq 1, \gamma(t) \neq \Phi(v)$.

\u2021 From the Greek $\iota \sigma \omega \varsigma+\mu \varphi \sigma \varphi \eta$ (isos-morphe), meaning “same form.” Isomorphic is used throughout mathematics to mean “having the same structure,” the exact definition depending on which mathematical structures are being considered.