The orbit of the point $(0,0)$ is the set of points

$\{t \bullet (0,0): t \in \mathbf{R}\} = \{(0 + t, 0 + 2t): t \in \mathbf{R}\} = \{(t, 2t): t \in \mathbf{R}\}.$

This set makes up the line with equation $y = 2x$. Similarly, $Orb(0, 1) = \{(0 + t, 1 + 2t): t \in \mathbf{R}\} = \{t, 1 + 2t\): t \in \mathbf{R}\}$, this set makes up the line with equation $y = 2x + 1$. Also, $Orb(1, 2) = \{(1 + t, 2 + 2t): t \in \mathbf{R}\}$, and this set makes up the line $y = 2x$.

# 12.4.1A Note that in this solution we omit the symbol, $\bullet$, for the group operation.

+   i. Suppose that $g \bullet h = Z(G)$. Then for each $x \in G$, we have that $g \bullet x = x \bullet g$ and $h \bullet x = x \bullet h$, and hence $(g \bullet h) \bullet x = g(h \bullet x) = g(x \bullet h) = (x \bullet g) \bullet h$. Therefore $g \bullet h \in Z(G)$. So $Z(G)$ satisfies the closure property. We have already noted that $e \in Z(G)$. Finally, suppose $g \in Z(G)$, and $x \in G$. Then, $g \bullet x = x \bullet g$. Hence $g^{\bullet -1}g xg^{\bullet -1} = g^{\bullet -1} xg xg^{\bullet -1}$, and hence $xg^{\bullet -1} = g^{\bullet -1} x$. Therefore $g^{\bullet -1} \in G$. It follows that $Z(G)$ is a subgroup of $G$.

+   ii. Suppose $g \in Z(G)$, then for each $x \in G$, $xg x^{\bullet -1} = (x \bullet g) x^{\bullet -1} = (g \bullet x) x^{\bullet -1} = g(x \bullet x^{\bullet -1}) = g \bullet e = g$. So the conjugacy class of $g$, that is, $\{xg x^{\bullet -1}: x \in G\}$, is just $\{g\}$. Conversely, suppose that the conjugacy class of $g$ is the set $\{g\}$. It follows that for each $x \in G$, $xg x^{\bullet -1} = g$ and hence $xgx^{\bullet -1} = g$, that is, $x \bullet g = g \bullet x$, and so $g \in Z(G)$.

+   iii. We know that the conjugacy classes of $G$ partition $G$, and that number of elements in each conjugacy class divides the order of $G$. Thus if $\#(G) = p^n$, where $p$ is a prime number and $n$ is some positive integer, the possibilities for the number of elements in a conjugacy class are $1, p, p^2, \dots, p^{n - 1}$. Consequently, if $k$ is the number of conjugacy classes of size 1, and there are $t$ other conjugacy classes with sizes $k_1, k_2, \dots, k_t$, we have that for $1 \leq s \leq t$, $p$ is a divisor of $k_s$, and $p^n = k + k_1 + k_2 + \dots + k_t$. Hence, $k = p^n - k_1 - k_2 - \dots - k_t$, and so $p$ is also a divisor of $k$. By part (b), $\#(Z(G)) = k$. We deduce that $\#(Z(G))$ is a multiple of $p$ and hence $\#(Z(G)) \geq p$.

# CHAPTER 13

13.1.1A We use the notation introduced in the solution to Exercise 11.2.2A for the six symmetries of an equilateral triangle. That is, $e$ is the identity, $a$ and $b$ are the rotations through one-third of a turn, counterclockwise and clockwise, and $r$, $s$, and $t$ are the reflections in axes joining one vertex to the midpoint of the opposite side.

![](bbox=[0.4, 0.9, 0.6, 0.98])