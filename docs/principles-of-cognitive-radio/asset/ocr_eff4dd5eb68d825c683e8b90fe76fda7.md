$X_{k}^{n}=f_{k}\left(W_{k}\right)$. (2.27)

Thus, in this case a channel input at each source depends only on its own data sequence, which, in turn, is independent of data sequences from other sources. Hence, there is no cooperation (e.g., relaying) between sources in transmitting information about each other's data sequences. The cut-set bound (2.21) can then be tightened to become

$\sum_{s_{k}\in\mathcal{S}_{n},\ d_{k}\in\mathcal{S}_{n}^{c}} R_{k}\leq I\left(X(\mathcal{S}_{n});Y(\bar{\mathcal{S}_{n}})|X(\mathcal{S}_{n}^{c}),V\right)$ (2.28)

for any $p(v)\prod_{k} p(x_{k}|v)$, where $V$, referred to as a *time-sharing random variable*, has the property that the inputs $\{x_{k}\}$ are independent when conditioned on $V$.

Lower bounds to the capacity region are obtained by deploying specific communication techniques in the given network. We next present encoding schemes that achieve capacity for special cases of the two-user interference channel.

# 2.4.2 Two-user interference channel capacity

A two-user discrete-time memoryless interference channel is shown in Fig. 2.11. The interference channel contains only two communicating pairs ($K=2$). Therefore, there are two channel inputs, $X_1$ and $X_2$, and two channel outputs, $Y_1$ and $Y_2$. The discrete-time channel is characterized by the conditional distribution $p(y_1,y_2|x_1,x_2)$. Each source $s_k$, $k=1,2$, wishes to send a data sequence $W_k \in \mathcal{W}=\{1,\dots,2^{nR_k}\}$ to destination $d_k$. Definitions for the channel code, the error probability and the capacity region follow the definitions for the $K$-user interference channel. In particular, an $(R_1,R_2,n)$ code consists of two data sequence sets $\mathcal{W}_1,\mathcal{W}_2$, two encoding functions

$X_{1}^{n}=f_{1}\left(W_{1}\right)$. (2.29)
$X_{2}^{n}=f_{2}\left(W_{2}\right)$ (2.30)

and two decoding functions
$\hat{W}_{k}=g_{k}\left(Y_{k}^{n}\right), \quad k=1,2$. (2.31)

![](bbox=[0.09, 0.87, 0.95, 0.96])