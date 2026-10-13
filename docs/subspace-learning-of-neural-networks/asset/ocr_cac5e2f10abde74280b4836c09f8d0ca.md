(2.1) into a discrete time deterministic algorithm. The DDT algorithm can be formulated as follows. Applying the conditional expectation operator $E\{w(k+1)/w(0), x(i), i<n\}$ to (2.1) and identifying the conditional expected value as the next iterate in the system [210], a DDT system can be obtained and given as

$$w(k+1)=w(k)+\eta\left[Cw(k)-w^{T}(k)Cw(k)w(k)\right], \tag{2.2}$$

for $k\geq 0$, where $C=E\left[x(k)x^{T}(k)\right]$ is the covariance matrix. The DDT method has some obvious advantages. First, it preserves the discrete time nature as that of the original learning algorithm. Second, it is not necessary to satisfy some unrealistic conditions of the DCT approach. Thus, it allows the learning rate to be constant. The main purpose of this section is to study the convergence of (2.2) subject to the learning rate $\eta$ being some constant.

Clearly, from (2.2), (1.7), (1.8), it holds that

$$z_i(k+1)=\left[1+\eta\left(\lambda_i-w^{T}(k)Cw(k)\right)\right]z_i(k),\quad (i=1,\ldots,n), \tag{2.3}$$

for $k\geq 0$.

**Definition 2.1** A point $w^*\in\mathbb{R}^n$ is called an equilibrium of (2.2), if and only if

$$w^*=w^*+\eta\left[Cw^*-(w^*)^TCw^*w^*\right].$$

Clearly, the set of all equilibrium points of (2.2) is

$$\{v_1,\ldots,v_n\}\cup\{-v_1,\ldots,-v_n\}\cup\{0\}.$$

# 2.3.3    Invariant Sets and Convergence Results

Some trajectories of (2.2) may diverge. Consider a simple example of a one dimensional equation.

$$w(k+1)=w(k)+\eta\left[1-w^2(k)\right]w(k),\quad k\geq 0.$$

If $w(k)\geq 1+1/\eta$, it holds that

$$\eta w^2(k)-w(k)-\eta-1\geq 0.$$

Then,

$$|w(k+1)|=w^2(k)\cdot\frac{\eta w^2(k)-\eta-1}{w(k)}\geq w^2(k).$$

Clearly, the trajectory approaches infinity if $w(0)\geq 1+1/\eta$. Other examples about divergence of Oja’s algorithm can be found in [210]. A problem to address is therefore to find out the conditions under which the trajectories can be bounded. The results forthcoming will be very important for applications. Next, we will prove an interesting theorem, which gives an invariant set of (2.2). The trajectories, thus, can be guaranteed to be bounded.