![](bbox=[0.2, 0.12, 0.85, 0.32])

$y$ on $C$ that is adjacent to $u$ such that none of the $\ell + 1$ vertices immediately following $y$ on $C$ are adjacent to $u$ or adjacent from $v$.

For each of the $a - 1$ vertices on $C$ that are distinct from $y$ and adjacent to $u$, the vertex immediately following it cannot be adjacent from $v$. Hence, at least $(a - 1) + (\ell + 1) = a + \ell$ vertices on $C$ are not adjacent from $v$, for otherwise again, $D$ has a cycle of length exceeding $k$. Since $P$ is a longest path in $D$ containing no vertices of $C$, every vertex adjacent to $u$ is either on $C$ or on $P$.

Because $iu \geq n/2$ and the only vertices of $D$ that can be adjacent to $u$ belong to $C$ or $P$, it follows that $a + \ell \geq n/2$. Therefore, $v$ is adjacent to at most $(n - 1) - (a + \ell) \leq (n - 1) - n/2 = n/2 - 1$ vertices, producing a contradiction.

# ## 7.4 Tournaments

There are sporting events involving teams (or individuals) that require every two teams to compete against each other exactly once. This is referred to as a round robin tournament. Men's soccer has been part of the Summer Olympic Games since 1900. Teams from 16 countries participate, divided into four pools of four teams each. In each pool, a round robin tournament takes place, in which the top two teams in each pool advance to play for Olympic medals. This also occurs during the World Cup for soccer supremacy when 32 countries participate, divided into eight pools of four teams each.

Round robin tournaments give rise quite naturally to a class of digraphs that we mentioned earlier. Recall that a **tournament** is an orientation of a complete graph. Therefore, a tournament can be defined as a digraph such that for every pair $u, v$ of distinct vertices, exactly one of $(u, v)$ and $(v, u)$ is an arc. A tournament $T$ then models a round robin tournament in which no ties are permitted. The vertices of $T$ are the teams in the round robin tournament and $(u, v)$ is an arc in $T$ if team $u$ defeats team $v$.