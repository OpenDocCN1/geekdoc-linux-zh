(2.2) can really converge fast, we randomly generated three symmetric non-negative definite matrices with dimensions of 5 × 5, 50 × 50, and 500 × 500, respectively. Figure 2.4 shows the performance of (2.2) with iteration step variations corresponding to the value of ησ from 0.2 to 0.8890. It clearly shows

![](bbox=[0.289, 0.171, 0.739, 0.41])

**FIGURE 2.4**  
Iteration step variations with respect to ησ.

that the algorithm (2.2) converges fast if the value of ησ is selected between 0.6 and 0.7. The simulation in Figure 2.4 also shows that the convergence of (2.2) does not appear to be sensitive to the dimension of (2.2) because the three curves are very close. Besides the above simulation results, we further and extensively simulated the convergence of (2.2) with high dimensions. The ensuing simulation results persist to show similarly satisfactory results.

The above simulations further confirm our important result: the learning rate can assume some constant to guarantee convergence providing the initial weight vector selected from an invariant set. Moreover, the above simulations also show that setting ησ around 0.618 can expedite the convergence of (2.2). To calculate η, we need to estimate σ, the largest eigenvalue of C. In some applications, based on the problem-specific knowledge, a upper bound of σ can be often estimated [20] without computing the covariance matrix C. However, in some practical applications, especially for online computing, it is difficult to estimate σ. Can we find another method to estimate η? Next, we give a way to estimate η. To make the illustration clearer, let us use the following version [31] of algorithm (2.1) for online computing:

$$w(k+1)=w(k)+\eta(k)\left(C_k w(k)-w^T(k)C_k w(k)w(k)\right)$$  
(2.8)

where $C_k$ is a online observation for $C$ [31] and $\lim_{k\to +\infty} C_k=C$. Noting that

$$\lim_{k\to +\infty} w^T(k)C_k w(k)\to \sigma$$