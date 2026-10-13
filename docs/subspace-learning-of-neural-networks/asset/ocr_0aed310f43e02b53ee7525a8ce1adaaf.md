![](bbox=[0.128, 0.081, 0.92, 0.282])

# FIGURE 7.7

Bifurcation diagram of (7.2) with $w(0)=0.01$ (left) and $w(0)=-0.01$ (right).

(7.1) where equilibria become unstable and periodic solutions show up. The bifurcation point of (7.2) is $\eta(a-f(w^2))=1$, as shown in Figure 7.7.

To further illustrate the chaotic behavior, the Lyapunov exponents of algorithms (7.1) and (7.2) are computed according to [2, 6]. From (7.1), let

$$y(k):=\frac{dG}{dw(k)}=1-\eta\bigl(a+f(w^2)\bigr)+3\eta bw(k)^2,$$

for $0<\eta(a+f(w^2))<4$ and $k\geq 0$. As for (7.2), let

$$y(k):=\frac{dG}{dw(k)}=1+\eta\bigl(a-f(w^2)\bigr)-3\eta bw(k)^2,$$

for $-2<\eta(a-f(w^2))<2$ and $k\geq 0$. The Lyapunov exponents can be computed by

$$\lim_{k\to+\infty}\frac{1}{k}\sum_{i=1}^{k}\lvert y(i)\rvert.$$

Figures 7.8 and 7.9 plot the Lyapunov exponents of algorithms (7.1) and (7.2) for each parameter value. Clearly, in Figure 7.8, as $\eta(a+f(w^2))\simeq 3.4$, the Lyapunov exponent becomes positive and the evolution begins to become chaotic. In Figure 7.9, as $\eta(a+f(w^2))\simeq 1.4$, the Lyapunov exponent becomes positive and the evolution begins to become chaotic. Thus, it is easy to see that the algorithms (7.1) and (7.2) exhibit chaotic behaviors as learning parameters increase in the invariant sets.

From the previous analysis, it is seen that the existence for chaos is because the learning parameters are chosen in certain range. Thus, it is possible to control the chaotic behavior by adjusting the learning parameters so that this algorithm can work better in practical applications.