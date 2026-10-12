# # 2.4 Interference channels without cognition

The error probability of the code is

$$P_{\mathrm{e}}=P\left[\left[\hat{W}_{1} \neq W_{1}\right] \cup\left[\hat{W}_{2} \neq W_{2}\right]\right].$$

A rate pair $(R_{1}, R_{2})$ is achievable if, for any $\epsilon>0$, there exists for sufficiently large $n$ an $(R_{1}, R_{2}, n)$ code such that $P_{\mathrm{e}} \leq \epsilon$. The capacity region of the interference channel is the closure of the set of all achievable rate pairs $(R_{1}, R_{2})$.

We will also consider the two-user AWGN interference channel, defined by

$$\begin{array}{l}Y_{1}=X_{1}+h_{12} X_{2}+Z_{1}, \\ Y_{2}=h_{21} X_{1}+X_{2}+Z_{2},\end{array}$$

where $h_{12}$ and $h_{21}$ are the (real) cross-channel gains of the interfering links, $\mathbb{E}\left[X_{k}^{2}\right] \leq$ $\mathcal{P}_{k}$ are power constraints, and $Z_{k} \sim \mathcal{N}(0,1)$ for $k=1,2$, where $\mathcal{N}(0, \sigma^{2})$ denotes the Gaussian distribution with variance $\sigma^{2}$.

The capacity of the interference channel is known in the case of $strong$ interference $[15]$. In this regime, the interfering signal at each receiver is strong enough that the other user's data sequence carried by that signal can be decoded and hence removed. It is then optimal for each receiver to decode both data sequences. In the AWGN interference channel (2.33), the strong interference conditions are given by $[40,74]$

$$\begin{array}{l}\left|h_{12}\right| \geq 1, \\ \left|h_{21}\right| \geq 1,\end{array}$$

implying that in this regime the cross-channel gains are larger than the direct link gains.

In general discrete memoryless channels, the strong interference conditions can be expressed in terms of the conditional mutual information inequalities. These conditions require that

$$\begin{array}{l}I\left(X_{1} ; Y_{1} \mid X_{2}\right) \leq I\left(X_{1} ; Y_{2} \mid X_{2}\right), \\ I\left(X_{2} ; Y_{2} \mid X_{1}\right) \leq I\left(X_{2} ; Y_{1} \mid X_{1}\right)\end{array}$$

are satisfied for every distribution $p\left(x_{1}\right) p\left(x_{2}\right)$. From (2.35) we observe that $Y_{2}$ contains more information about input $X_{1}$ than $Y_{1}$, given $X_{2}$. Hence, $X_{1}$ conveys more information to receiver 2 than to receiver 1. A similar interpretation can be made for (2.36).

The capacity region in strong interference is given by

$$\begin{gathered}\mathcal{C}=\bigcup\left\{\left(R_{1}, R_{2}\right): R_{1} \geq 0, R_{2} \geq 0,\right. \\\left.\begin{array}{l}R_{1} \leq I\left(X_{1} ; Y_{1} \mid X_{2}, V\right), \\ R_{2} \leq I\left(X_{2} ; Y_{2} \mid X_{1}, V\right), \\ R_{1}+R_{2} \leq \min \left\{I\left(X_{1}, X_{2} ; Y_{1} \mid V\right), I\left(X_{1}, X_{2} ; Y_{2} \mid V\right)\right\}\end{array}\right\}\end{gathered}$$

where the union is over distributions of the form $p(v) p\left(x_{1}|v\right) p\left(x_{2}|v\right)$ and $V$ is once again a time-sharing random variable for which the inputs are independent when conditioned on it.