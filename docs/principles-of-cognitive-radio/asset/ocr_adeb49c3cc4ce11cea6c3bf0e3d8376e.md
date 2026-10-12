$$\inf_{N_S} \{ P[N_S < m] + c\,\mathbb{E}[(N_S - m + 1)^+] \}, \qquad (5.39)$$

where $c$ is a positive constant and $(N_S - m + 1)^+ = \max\{0, N_S - m + 1\}$. The constant $c$ controls the relative importance of minimizing the probability of false alarm $P[N_S < m]$ and the expected detection delay $\mathbb{E}[(N_S - m + 1)^+]$.

Let us assume a geometric prior distribution for the change point:

$$P[m = n] = \begin{cases} \omega, & n = 0, \\ (1 - \omega) q (1 - q)^{n-1}, & n = 1,2,\dots, \end{cases} \qquad (5.40)$$

where $\omega$ is the probability that the change has already occurred before the first observation is obtained and $q$ is the conditional probability that the sequence transfers to the post-change state at any given time. Both $\omega$ and $q$ are constants in $(0,1)$.

Under the above assumptions, Shiryaev [177] showed that the stopping point that minimizes the Bayes risk in (5.39) is given by

$$N_S = \inf \{ n \ge 0 \mid \omega_n \ge \omega^* \}, \qquad (5.41)$$

where $\omega^*$ is a certain appropriately chosen constant threshold in $[0,1]$ and $\omega_n = P[m \le n \mid y_1,\dots,y_n]$ is the posterior probability that a change has already happened given the observations up to that point. In addition Shiryaev [177] showed that if the threshold $\omega^*$ is chosen to satisfy a given false alarm constraint $P[N_S < m] = \alpha$ then the stopping rule in (5.41) minimizes the expected detection delay among all rules satisfying the false alarm constraint $P[N_S < m] \le \alpha$. Shiryaev's quickest change detection test is illustrated in Fig. 5.8.

The Bayes optimal stopping time may be written also as

$$N_S = \inf \{ n \ge 0 \mid U_{n,q} \ge \nu \}, \qquad (5.42)$$

![](bbox=[0.15, 0.85, 0.85, 0.93])

Figure 5.8 Illustration of a Bayesian quickest change detection test.