also causes oscillation at the beginning phase of the training. A small ξ will make the evolution smoother with a relatively low convergent rate. Figure 3.8 shows that evolution trajectories of the same initial vector with the different ξ converge along the correct direction.

![](bbox=[0.116, 0.197, 0.916, 0.437])

**FIGURE 3.8**
Convergence of (3.4) with ξ = 0.7 (left) and ξ = 0.01 (right).

In the following simulation, to observe the evolution trajectories clearly, let ξ = 0.01. Three distinct initial vectors are generated randomly. In Figure 3.9, Figure 3.10, Figure 3.11, the eight components trajectories in the weight vector are shown in left pictures and the right ones present the learning rate evolution, respectively. It can be observed that the weight vectors with different initial values fast converges to the principal component direction as the learning rates trend to a constant. Clearly, convergent rates derived are very fast.

Next, let ξ = 0.5, and we will further study the global convergence and convergent rate of (3.4). The eight arbitrarily initial values are selected apart from the origin, and each is repeatedly tested 20 times. The average results are shown in Table 3.2. It is clear that the arbitrary initial weight vector always converges along the correct direction with 100% success rate and the learning rate η(k) converges to a constant such that the evolution rate derived does not become slower and slower. At the same time, the first principal component is extracted and the image is reconstructed. The average SNR has also been presented in Table 3.2. The reconstructed image is shown in Figure 3.12 with the initial value 2.3083e + 011 and SNR 35.7643.