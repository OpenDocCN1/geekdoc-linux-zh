# ### 6.5　Simulation and Discussion

In this section, three set of experiments will be carried out to illustrate the convergence of the class of Hyvarinen-Oja’s ICA learning algorithms with constant learning rates.

# #### 6.5.1　Example 1

The DDT algorithms characterize the average evolution of the original algorithms. The convergence of the DDT algorithms can reflect the dynamical behaviors of the original algorithms in the invariant sets. From (6.7), consider four-dimensional DDT algorithms as

$$\begin{bmatrix} z_1(k+1) \\ z_2(k+1) \\ z_3(k+1) \\ z_4(k+1) \end{bmatrix}=\begin{bmatrix} z_1(k) \\ z_2(k) \\ z_3(k) \\ z_4(k) \end{bmatrix}+\eta\begin{bmatrix} \sigma b\\ K\!urt(s_1)z_1^3(k)\\ K\!urt(s_2)z_2^3(k)\\ K\!urt(s_3)z_3^3(k)\\ K\!urt(s_4)z_4^3(k) \end{bmatrix}+(3\sigma\|z(k)\|^2+\eta\alpha(1-\|z(k)\|^2))\begin{bmatrix} z_1(k)\\ z_2(k)\\ z_3(k)\\ z_4(k) \end{bmatrix},$$

for all $k\geq 0$. Let $\eta=0.1$, $a=5$, and $b=0.5$. While $\sigma=1$ and $Kurt(s_1)=-0.6$, $Kurt(s_2)=0$, $Kurt(s_3)=3$, $Kurt(s_4)=0.4$, in Figure 6.1, the evolution of components of $z$ is shown with initial vector $z(0)= [-0.3\ -0.6\ 0.2\ 0.4]^T$ (upper) and $z(0)=[-1\ -0.5\ 0.1\ -0.2]^T$ (bottom). While $\sigma=-1$ and the initial value $z(0)=[-0.4\ -0.8\ 0.2\ 0.4]^T$, Figure 6.2 shows the evolution results of components of $z$ with the kurtosis $Kurt(s_1)=-0.6$, $Kurt(s_2)=0$, $Kurt(s_3)=3$, $Kurt(s_4)=-0.4$ (upper) and $Kurt(s_1)=-0.6$, $Kurt(s_2)=0$, $Kurt(s_3)=-2.5$, $Kurt(s_4)=-0.4$ (bottom).

Since $\mathbb{E}\{w(k)\}=Bz(k)$, the DDT algorithms converge to an independent component direction with a positive kurtosis or a negative kurtosis as all components of $z(k)$ converge to zero except a component. The simulation illustrates the results of Theorems 6.3 and 6.4.

In addition, the initial value and kurtosis together determine which independent component will be extracted in the DDT algorithms. However, in a stochastic environment, the distribution of the variable also affects which independent component will be extracted. The following experiments will further illustrate the theory derived.