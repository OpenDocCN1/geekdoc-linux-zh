Obviously, the algorithms have many equilibria, thus, the study of dynamics belongs to a multistability problem [192].

According to the Lyapunov indirect method, an equilibrium of an algorithm is stable if the absolute of each eigenvalue of the Jacobian matrix of the algorithm at this point is less than 1 [2]. For the algorithms (7.1) and (7.2), we will compute the eigenvalues of Jacobian matrix at each equilibrium point.

**Theorem 7.4** For the algorithm (7.1), if $w(k) \in S_1$, the equilibrium $0$ is stable if $0 < \eta(a+f(\|w(k)\|^2)) < 2$. The points $\pm\sqrt{\frac{a+f(\|w(k)\|^2)}{b}}$ are unstable if $\eta(a+f(\|w(k)\|^2)) > 0$.

*Proof:* Let

$$G=w(k)+\eta[-(aw(k)-bw^3(k))-f(\|w(k)\|^2)w(k)].$$

We have

$$\frac{dG}{dw(k)}=1-\eta a-\eta f(\|w(k)\|^2)+3\eta b w^2(k).$$

Clearly, $\left.\frac{dG}{dw(k)}\right|_0=1-\eta a-\eta f(\|w(k)\|^2)$. If $0<\eta(a+f(\|w(k)\|^2))<2$, it holds that $\left|\frac{dG}{dw(k)}\right|<1$. Thus, $0$ is a stable point. As for equilibria $\pm\sqrt{\frac{a+f(\|w(k)\|^2)}{b}}$, $\left|\frac{dG}{dw(k)}\right|=|1+2\eta(a+f(\|w(k)\|^2))|$. If $\eta(a+f(\|w(k)\|^2))>0$, $\left|\frac{dG}{dw(k)}\right|>1$.

Thus, $\pm\sqrt{\frac{a+f(\|w(k)\|^2)}{b}}$ are unstable points for $\eta(a+f(\|w(k)\|^2))>0$. The proof is completed. Theorem 7.4 shows that in invariant set $S_1$, the algorithm (7.1) converges to 0 if $0<\eta(a+f(\|w(k)\|^2))<2$, as shown in Figure 7.4.

**Theorem 7.5** For the algorithm (7.2), if $w(k)\in S_2$, the equilibrium $0$ is stable if $-2<\eta(a-f(\|w(k)\|^2))\leq 0$. The points $\pm\sqrt{\frac{a-f(\|w(k)\|^2)}{b}}$ are stable points if $0<\eta(a-f(\|w(k)\|^2))b<1$.

*Proof:* Let

$$G=w(k)+\eta[(aw(k)-bw^3(k))-f(\|w(k)\|^2)w(k)].$$

We have

$$\frac{dG}{dw(k)}=1+\eta a-\eta f(\|w(k)\|^2)-3\eta b w^2(k).$$

Clearly, $\left.\frac{dG}{dw(k)}\right|_0=1+\eta a-\eta f(\|w(k)\|^2)$. If $-2<\eta(a-f(\|w(k)\|^2))<0$, it holds that $\left|\frac{dG}{dw(k)}\right|<1$. Thus, $0$ is stable for $-2<\eta(a-f(\|w(k)\|^2))<0$.