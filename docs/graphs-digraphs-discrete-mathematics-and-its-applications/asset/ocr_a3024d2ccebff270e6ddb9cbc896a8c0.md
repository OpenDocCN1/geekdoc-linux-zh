is a **chord** of *G*. Every chord and every region of *G* then lies interior to *C* or exterior to *C*. For $i = 3,4,\dots,n$, let $r_i$ denote the number of regions interior to *C* whose boundary contains exactly $i$ edges and let $r_i^*$ denote the number of regions exterior to *C* whose boundary contains exactly $i$ edges.

The plane graph *G* of Figure 10.17 of order 12 is Hamiltonian. The edges of the Hamiltonian cycle $C = (v_1, v_2, \dots, v_{12}, v_1)$ are drawn with **bold** lines. With respect to *C*, we have

$$ r_3 = r_3^* = 1, \quad r_4 = 3, \quad r_4^* = 2, \quad r_5 = r_5^* = 1, $$

while $r_i = 0$ for $6 \le i \le 12$ and $r_i^* = 0$ for $i = 5,6$ and $8 \le i \le 12$.

![](bbox=[0.25, 0.35, 0.75, 0.52])

In 1968 a necessary condition for a planar graph to be Hamiltonian was discovered by the Latvian mathematician Emauels Ja. Grinberg [109].

# **Theorem 10.27** (Grinberg's Theorem)	For a plane graph *G* of order *n* with Hamiltonian cycle *C*,$

$$ \sum_{i=3}^n (i-2)(r_i - r_i^*) = 0. $$

**Proof.** Suppose that $c$ chords of *G* lie interior to *C*. Then $c+1$ regions of *G* lie interior to *C*. Therefore,

$$ \sum_{i=3}^n r_i = c+1 \text{ and so } c = \sum_{i=3}^n r_i - 1. $$

Let *N* denote the result obtained by summing over all regions interior to *C* the number of edges on the boundary of each such region. Then each edge on *C* is counted once and each chord interior to *C* is counted twice, that is,

$$ N = \sum_{i=3}^n i r_i = n + 2c. $$