![](bbox=[0.26, 0.11, 0.82, 0.34])

![](bbox=[0.26, 0.36, 0.76, 0.56])

13. Let $N$ be a network with capacity function $c$ and suppose that $[X, \overline{X}]$ is a minimum cut in $N$. Prove or disprove:

+   (a) If $f_1$ and $f_2$ are flows in $N$ that agree on $[X, \overline{X}]$ and $[\overline{X}, X]$, then $f_1$ and $f_2$ are maximum flows in $N$.
+   
+   (b) If $f_1$ and $f_2$ are maximum flows in $N$, then $f_1$ and $f_2$ agree on $[X, \overline{X}]$ and $[\overline{X}, X]$.

14. Define a **generalized network** $N$ to be a digraph $D$ with two distinguished vertices $u$ and $v$ called the *source* and *sink*, respectively, together with two nonnegative integer-valued functions $c_1$ and $c_2$ on $E(D)$. A *flow* in $N$ is a real-valued function $f$ on $E(D)$ that satisfies (8.3) (that is, $f^+(x) = f^-(x)$ for each intermediate vertex $x$ of $D$) as well as

```
$$c_1(a) \leq f(a) \leq c_2(a) \text{ for every arc } a \text{ of } D. \quad (8.10)$$
```

Give an example of a nontrivial generalized network $N$ that has no (legal) flow.

# **Section 8.3. Menger Theorems for Digraphs**

15. Use the proof of Theorem 8.11 to find the maximum number of internally disjoint $u-v$ paths in the digraph $D$ shown in Figure 8.20.