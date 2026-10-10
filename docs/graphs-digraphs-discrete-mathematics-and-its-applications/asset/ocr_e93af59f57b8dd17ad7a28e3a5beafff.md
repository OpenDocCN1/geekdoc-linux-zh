# 7.3. EULERIAN AND HAMILTONIAN DIGRAPHS

**Theorem 7.8** (Meyniel’s Theorem) If D is a nontrivial strong digraph of order n such that

```
```
deg u + deg v ≥ 2n − 1
```
```

for every pair u, v of nonadjacent vertices, then D is Hamiltonian.

Among the consequences of Theorem 7.8 is a result obtained by Douglas Woodall [259].

**Corollary 7.9** If D is a nontrivial digraph of order n such that

```
```
od u + id v ≥ n
```
```

whenever u and v are distinct vertices with $(u, v) \notin E(D)$, then D is Hamiltonian.

The proof of the following theorem (due to Alain Ghouila-Houri [104]) is an immediate consequence of Theorem 7.8.

**Corollary 7.10** If D is a strong digraph of order n such that deg $v \geq n$ for every vertex v of D, then D is Hamiltonian.

Corollary 7.10 also has a corollary. We provide a proof of this result.

**Corollary 7.11** If D is a digraph of order n such that

```
```
od v ≥ n/2  and  id v ≥ n/2
```
```

for every vertex v of D, then D is Hamiltonian.

**Proof.** Suppose that the theorem is false. Since the theorem is clearly true for $n = 2$ and $n = 3$, there exists some integer $n \geq 4$ and a digraph D of order n that satisfies the hypothesis but which is not Hamiltonian. Let C be a cycle in D of maximum length k. It follows from Theorem 7.2 and the assumption that D is not Hamiltonian that $1 + n/2 \leq k < n$. Also, let P be a path of maximum length such that no vertex of P lies on C. Suppose that P is a $u - v$ path of length $\ell \geq 0$. Therefore, $k + \ell + 1 \leq n$. (See Figure 7.10.)

```
```
ℓ ≤ n − k − 1 ≤ n − (1 + n/2) − 1 = n/2 − 2,
```
```

it follows that $\ell \leq n/2 - 2$ and that there are at least two vertices adjacent to u which do not lie on P. Since P is a longest path all of whose vertices do not lie on C, it follows that there are at least two vertices that lie on C that are adjacent to u and at least two vertices adjacent from v which lie on C.

Let a denote the number of vertices on C that are adjacent to u. Thus, $a \geq 2$. For every vertex x on C that is adjacent to u, the $\ell + 1$ vertices immediately following x on C are not adjacent from v, for otherwise, D has a cycle of length exceeding k. Since C contains vertices adjacent from v, there must be a vertex