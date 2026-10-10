![](bbox=[0.2, 0.12, 0.4, 0.24])

Automorphisms:
$\epsilon$, $\alpha_1 = (u \ v \ w \ x)$
$\alpha_2 = (u \ w)(v \ x)$, $\alpha_3 = (u \ x \ w \ v)$
$\phi_1 = (u \ w)$, $\phi_2 = (v \ x)$
$\phi_3 = (u \ v)(w \ x)$, $\phi_4 = (u \ x)(v \ w)$

Figure 9.3: A 4-cycle and the elements of its automorphism group

**Theorem 9.1** *For every graph $G$, $\mathrm{Aut}(G) \cong \mathrm{Aut}(\overline{G})$.*

We mentioned previously that $\mathrm{Aut}(K_n) \cong S_n$ for every positive integer $n$. Certainly, if $G$ is a graph of order $n$ containing adjacent vertices as well as nonadjacent vertices, then $\mathrm{Aut}(G)$ is isomorphic to a proper subgroup of the symmetric group $S_n$. Combining this observation with Theorem 9.1 and Lagrange’s Theorem on the order of a subgroup of a finite group (which states that the order of a subgroup of a finite group divides the order of the group), we arrive at the following.

**Theorem 9.2** *The order $|\mathrm{Aut}(G)|$ of the automorphism group of a graph $G$ of order $n$ is a divisor of $n!$ and equals $n!$ if and only if $G = \overline{K}_n$ or $G = \overline{K}_n$.*

Recall that two labelings of a graph $G$ of order $n$ from the same set of $n$ labels are considered distinct if they do not produce the same edge set. With the aid of the automorphism group of a graph $G$ of order $n$, it is possible to determine the number of distinct labelings of $G$.

**Theorem 9.3** *The number of distinct labelings of a graph $G$ of order $n$ from a given set of $n$ labels is $n! / |\mathrm{Aut}(G)|$.*

**Proof.** Let $S$ be a set of $n$ labels. Certainly, there exist $n!$ labelings of $G$ using the elements of $S$ without regard to which labelings are distinct. For a given labeling of $G$, each automorphism of $G$ gives rise to an identical labeling of $G$; that is, each labeling of $G$ from $S$ determines $|\mathrm{Aut}(G)|$ identical labelings of $G$. Hence, there are $n! / |\mathrm{Aut}(G)|$ distinct labelings of $G$. $\blacksquare$

As an illustration of Theorem 9.3, consider the graph $G = P_3$ of Figure 9.4 and the set $S = \{1, 2, 3\}$. Since $\mathrm{Aut}(G) \cong Z_2$, the number of distinct labelings of $G$ is $3! / 2 = 3$. The three distinct labelings of $G$ from the set $\{1, 2, 3\}$ are shown in Figure 9.4.