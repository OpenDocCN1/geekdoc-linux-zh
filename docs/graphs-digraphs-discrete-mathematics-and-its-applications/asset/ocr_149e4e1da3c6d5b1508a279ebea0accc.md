of $H$, where $0 < s < ˇ < t < k$, such that $v_{a}$ and $v_{ˇ}$ are the only vertices of $P$ that belong to $C$. (See Figure 10.10.) In fact, the path $P$ must be ($v_{s}$, $v_{ˇ}$); for otherwise, if there is an interior vertex $w$ on $P$, then, since $G$ is 3-connected, there are three internally disjoint paths from $w$ to $C$, creating a new cycle $C'$ containing $u$ and $v$ such that $C'$ has more regions interior to it than $C$ has, which is a contradiction.

![](bbox=[0.25, 0.25, 0.75, 0.55])

Figure 10.10: A step in the proof of Theorem 10.18

Let $S$ be the set of vertices on $C$ different from $v_{s}$ and $v_{ˇ}$, that is,

$S=V(C)-\{v_{s},v_{ˇ}\}$, and let $H_{1}$ be the component of $H-S$ that contains $P$. By the defining property of $C$, the subgraph $H_{1}$ cannot be moved to the interior of $C$ in a plane manner. This fact together with the fact that $G=H+e$ is nonplanar implies that the interior subgraph of $H$ must contain one of the following:

+   (1) A $v_{a}-v_{b}$ path with $0 < a < s$ and $ˇ < b < t$ such that only $v_{a}$ and $v_{b}$ belong to $C$. (See Figure 10.11(a).)

+   (2) A vertex $w$ not on $C$ that is connected to $C$ by three internally disjoint paths such that the terminal vertex of one such path $P'$ is one of $v_{0}, v_{s}, v_{ˇ}$ and $v_{k}$. If, for example, the terminal vertex of $P'$ is $v_{0}$, then the terminal vertices of the other two paths are $v_{a}$ and $v_{b}$, where $s ≤ a < ˇ$ and $ˇ < b ≤ t$ where not both $a = s$ and $b = t$ occur. (See Figure 10.11(b).) If the terminal vertex of $P'$ is one of $v_{s}, v_{ˇ}$ and $v_{k}$, then there are corresponding bounds for $a$ and $b$ for the terminal vertices of the other two paths.

+   (3) A vertex $w$ not on $C$ that is connected to $C$ by three internally disjoint paths $P_{1}$, $P_{2}$ and $P_{3}$ such that the terminal vertices of these paths are three of the four vertices $v_{0}, v_{s}, v_{ˇ}$ and $v_{k}$, say $v_{0}, v_{ˇ}$ and $v_{s}$, respectively, together with a $v_{c}-v_{ˇ}$ path $P_{4}$ ($v_{c} \neq v_{0}, v_{s}, w$), where $v_{c}$ is on $P_{3}$ and $P_{2}$ and $P_{4}$ is disjoint from $P_{1}$, $P_{2}$ and $C$ except for $v_{c}$ and $v_{ˇ}$. (See Figure 10.11(c).) The remaining choices for $P_{1}$, $P_{2}$ and $P_{3}$ produce three analogous cases.