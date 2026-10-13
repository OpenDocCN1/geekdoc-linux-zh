
![](img/5d1bf22d32ba379cbf31221a5347fdb6_212_0.png)

**FIGURE 9.2**  
The noise-disturbed data set used for surface fitting, which is obtained by adding Gaussian noise with zero means and variance $\sigma^2 = 0.3$ in the way given by (9.5).

![](img/5d1bf22d32ba379cbf31221a5347fdb6_212_1.png)

**FIGURE 9.3**  
The data points obtained after applying the improved Oja+’s algorithm to each $10 \times 10$ block with $\mu = 40$.

![](img/5d1bf22d32ba379cbf31221a5347fdb6_213_0.png)

**FIGURE 9.4**  
The data points obtained after applying the improved Oja+’s algorithm to the grouped data with $\mu = 40$, that is, the final result of surface fitting by using multi-block-based MCA on the data set given by Figure 9.2.

Dominated by noise much stronger than $x, y$, we generate a noise observation data set $D' = \{(x_i', y_i', z_i'), i = 0, 1, \ldots, 1600\}$ by adding Gaussian noise to $z$-axis observation data as follows:

$$z_i' = z_i + n_z, \quad x_i' = x_i, \quad y_i' = y_i, \quad i = 1, 2, \ldots, 1600. \tag{9.5}$$

The Gaussian noise is with zero means and variance $\sigma^2 = 0.3$. Figures 9.1 and 9.2 show the original ellipsoid segment and the noise-disturbed data set $D'$, respectively.

We partition the noise-disturbed data points into 16 blocks, and each block size is $10 \times 10$. MCA is then applied to each block by using the improved Oja+’s algorithm (9.2) according to the process mentioned in Section 9.2.3. After reconstructing the data points in each block, we group all the blocks into one to form a matrix. The result after applying the improved Oja+’s MCA algorithm to blocks individually is shown in Figure 9.3. Subsequently, we apply the improved Oja+’s algorithm (9.2) one more time to the grouped matrix. Figure 9.4 shows the final result of surface fitting by using multi-block-based MCA.

Comparing with applying MCA direct method, the simulation results of multi-block-based MCA on the same data are shown in Table 9.1. The absolute error between the true parameter vector $\mathbf{w}$ and the estimated $\tilde{\mathbf{w}}$, defined as $\varepsilon_w = \|\tilde{\mathbf{w}} - \mathbf{w}\|$, is used to compare the accuracy.

**TABLE 9.1**  
The solution obtained by different methods on the same noisy data set. The average values of $w$ obtained from 20 simulations are given.

|  | $w_1$ | $w_2$ | $w_3$ | $\varepsilon_w$ |
|---|---:|---:|---:|---:|
| True values | 0.0400 | 0.0625 | 0.1111 |  |
| MCA direct method | 0.0368 | 0.0590 | 0.1125 | 0.0051 |
| Multi-block-based MCA | 0.0375 | 0.0604 | 0.1084 | 0.0045 |

![](img/5d1bf22d32ba379cbf31221a5347fdb6_214_0.png)

**FIGURE 9.5**  
The original data points taken from the saddle segment (9.6).

### 9.4.2 Simulation 2: Saddle

To illustrate the effectiveness of our method, we give another surface fitting simulation on a data set $D=\{(x_i,y_i,z_i), i=0,1,\ldots,1600\}$ sampled from a saddle

$$z = 0.3615x^2 - 0.4820y^2,$$
$$(-4 < x \le 4,\quad -4 < y \le 4). \tag{9.6}$$

This time the noise-disturbed data set $D'=\{(x'_i,y'_i,z'_i), i=0,1,\ldots,1600\}$ is obtained by adding noise with a uniform distribution on the interval $[-\sigma,\sigma]$ and variance $\sigma^2=0.5$ to $z$-axis observation data, in the way given by (9.5). The original saddle and the noise-disturbed data set $D'$ are, respectively, shown in Figures 9.5 and 9.6.

![](img/5d1bf22d32ba379cbf31221a5347fdb6_215_0.png)

**FIGURE 9.6**  
The noise-disturbed data set used for surface fitting, which is obtained by adding Gaussian noise with zero means and variance $\sigma^2 = 0.5$ in the way given by (9.5).

![](img/5d1bf22d32ba379cbf31221a5347fdb6_215_1.png)

**FIGURE 9.7**  
The data points obtained after applying the improved Oja+’s algorithm to each $10 \times 10$ block with $\mu = 30$.

![](img/5d1bf22d32ba379cbf31221a5347fdb6_216_0.png)

**FIGURE 9.8**  
The data points obtained after applying the improved Oja+’s algorithm to the grouped data with $\mu = 50$, that is, the final result of surface fitting by using multi-block-based MCA on the data set given by Figure 9.6.

Different from simulation 1, we generally fit a parameterized model

$$a_1x^2 + a_2y^2 + a_3z + c_0 = 0$$

to the noise-disturbed data points, that is, $\bar{f} = f - E(f)$ is used to train the neural network, where $f = [x^2, y^2, z]$. In this simulation, as the original real data set has zero means, the true $c_0$ is zero, while the estimated $c_0$ we obtain is close to zero. The block size we use in this simulation is $10 \times 10$. Figure 9.7 shows the result after partition and applying MCA to each block, and Figure 9.8 shows the final result of fitting using multi-block-based MCA. Table 9.2 shows the simulation results of applying multi-block-based MCA and MCA direct method, respectively, on the same saddle data set disturbed by strong Gaussian noise.

From the simulation results (Tables 9.1 and 9.2), we see that the estimated solution by multi-block-based MCA is considerably good, and the multi-block-based MCA outperforms the MCA direct method in terms of accuracy.

**TABLE 9.2**  
The solution obtained by different methods on the same noisy data set. The average values of $w$ obtained from 20 simulations are given.

|  | $w_1$ | $w_2$ | $w_3$ | $\varepsilon_w$ |
|---|---:|---:|---:|---:|
| True values | 0.3615 | 0.4820 | 1.0000 |  |
| MCA direct method | 0.3646 | 0.4844 | 1.0000 | 0.0046 |
| Multi-block-based MCA | 0.3644 | 0.4846 | 1.0000 | 0.0044 |

### 9.5 Conclusion

In this chapter, a multi-block-based MCA method is proposed for nonlinear surface fitting. The proposed method shows good performance in terms of accuracy, which is confirmed by the simulation results.

## An ICA Algorithm for Extracting Fetal Electrocardiogram

### 10.1 Introduction

Fetal electrocardiogram (FECG) extraction is an interesting and challenging problem in biomedical engineering. The antepartum FECG is usually obtained through skin electrodes attached to the mother’s body [89]. Unfortunately, the desired fetal heartbeat signals appear at the electrode output buried in an additive mixture of undesired disturbances, such as the mother’s heartbeat signal with extremely high amplitude, the noise caused by mother’s respiration, and electronic equipment. Appropriate signal processing techniques are required to recover the wanted FECG components from the corrupted potential recordings.

Many approaches have been reported to get the FECG, such as singular-value decomposition (SVD) [95], multireference adaptive noise cancellation [200], and so on. But the results are not satisfactory or highly sensitive to electrode placement. Recently, it was shown in [107] that the problem can be modeled as blind source separation (BSS) [43, 83]. It was reported that the results by BSS were more satisfactory than those by classical methods [5, 174, 200]. However, separating all the sources from a large number of observed sensor signals takes a long time and is not necessary, so the blind source extraction (BSE) method is preferred. The basic objective of BSE is estimating one or part of source signals from their linear mixtures. Such signals are usually with specified stochastic properties and bring the most useful information.

Many BSE algorithms use the property of sparseness [209] or high-order statistics [46, 115, 205] to extract a specific signal. High-order methods address the BSE problem in a completely blind context, since they require few assumptions aside from the statistical independence of the sources. The second-order statistics (SOS) [11, 45, 206], however, operate in a semiblind setting, since their derivation usually requires the certain additional assumptions made on the nature of the source signals, such as statistical nonstationarity of the sources, presence of time correlations in stationary signals, or cyclostationarity. Nonetheless, such information is available in practical applications and should be exploited. Furthermore, the high-order approaches often have higher
