Finally, the regular icosahedron:

| Type of Rotation | Number of this Rype | Cycle Type | #(Fix(g)) |
| :--- | :---: | :---: | :---: |
| Identity | 1 | $x_1^{20}$ | $c^{20}$ |
| Rotations through $\pm \frac{2}{3}\pi$ about axes joining the midpoints of opposite faces | 20 | $x_1 x_3^6$ | $c^8$ |
| Rotations through $\pi$ about axes joining the midpoints of opposite edges | 15 | $x_2^{10}$ | $c^{10}$ |
| Rotations through $\pm \frac{2}{5}\pi$ and $\pm \frac{4}{5}\pi$ about axes joining opposite vertices | 24 | $x_5^4$ | $c^4$ |

It follows from Frobenius's counting theorem that the number of different colorings is

$\frac{1}{60} (c^{20} + 15c^{10} + 20c^8 + 24c^4)$.

# CHAPTER 14

**14.1.1A** $f \circ \pi^{-1}(1) = f(\pi^{-1}(1)) = f(4) = 1$; $f \circ \pi^{-1}(2) = f(\pi^{-1}(2)) = f(3) = 0$;

$f \circ \pi^{-1}(3) = f(\pi^{-1}(3)) = f(5) = 2$; $f \circ \pi^{-1}(4) = f(\pi^{-1}(4)) = f(1) = 1$; and

$f \circ \pi^{-1}(5) = f(\pi^{-1}(5)) = f(2) = 2$.

**14.1.2A** We have that

$\pi_1 \triangleright (\pi_2 \triangleright f) = \pi_1 \triangleright (f \circ \pi_2^{-1})$, by the definition of the group action,

$= ((f \circ \pi_2^{-1}) \circ \pi_1^{-1})$, by the definition of the group action,

$= f \circ (\pi_2^{-1} \circ \pi_1^{-1})$, because the operation $\circ$ is associative,

$= f \circ ((\pi_1 \circ \pi_2)^{-1})$, by Lemma 14.1, and

$= (\pi_1 \circ \pi_2) \triangleright f$, by the definition of the group action.

**14.2.1A** The store enumerator is $\sum_{w \in G} w(c) = b + b + b + r + r + r = 3b + 2r$. The inventory of all the mappings from $D$ to $C$ is $(3b + 2r)^5$.