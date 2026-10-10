the inequality holds for $t=3$. Suppose that
$$2^{k^{2}/2} < \frac{1}{2}\cdot k!\cdot 2^{\binom{k}{2}}$$
for some integer $k \geq 3$. We show that
$$2^{(k+1)^{2}/2} < \frac{1}{2}(k+1)!2^{\binom{k+1}{2}}.$$ 
Observe that
\begin{eqnarray*} 2^{(k+1)^{2}/2} & = & 2^{k^{2}/2}\cdot 2^{(2k+1)/2} = \sqrt{2}\cdot 2^{k^{2}/2}\cdot 2^{k} \\ & < & \sqrt{2}\left[\frac{1}{2}\cdot k!\cdot 2^{\binom{k}{2}}\right]\cdot 2^{k} = \sqrt{2}\cdot\frac{1}{2}\cdot k!\cdot 2^{\binom{k}{2}+k} \\ & < & \frac{1}{2}(k+1)\cdot k!\cdot 2^{\binom{k+1}{2}} = \frac{1}{2}(k+1)!2^{\binom{k+1}{2}}. \end{eqnarray*}

Thus, the inequality in (20.8) holds for every integer $t \geq 3$ and so, by (20.7),
$$n^{t} < \left(\frac{1}{2}\right)\! t!2^{\binom{t}{2}}. \tag{20.9}$$

Combining (20.6) and (20.9), we conclude that
$$N < \left(\frac{1}{2}\right)2^{\binom{t}{2}}. \tag{20.10}$$

If we list the $N$ graphs with vertex set $V$ that contain a subgraph isomorphic to $K_{t}$, together with their complements, then there are at most $2N<2^{\binom{t}{2}}$ different graphs in the list. Since there are $2^{\binom{t}{2}}$ graphs with vertex set $V$, we conclude that there is a graph $G$ with vertex set $V$ such that neither $G$ nor $\overline{G}$ appears in the aforementioned list; that is, neither $G$ nor $\overline{G}$ contains a subgraph isomorphic to $K_{t}$. $\blacksquare$

Relatively few classical Ramsey numbers $R(s, t)$ are known for $s, t \geq 3$. The table in Figure 20.3 gives the known values of $R(s, t)$ for integers $s$ and $t$ with $s, t \geq 3$. Although it is known that $43 \leq R(5,5) \leq 49$, the value of $R(5,5)$ remains unknown.

| s | 3 | 3 | 3 | 3 | 3 | 3 | 3 | 4 | 4 |
|---|---|---|---|---|---|---|---|---|---|
| t | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 4 | 5 |
| R(s,t) | 6 | 9 | 14 | 18 | 23 | 28 | 36 | 18 | 25 |

Figure 20.3: Some classical Ramsey numbers