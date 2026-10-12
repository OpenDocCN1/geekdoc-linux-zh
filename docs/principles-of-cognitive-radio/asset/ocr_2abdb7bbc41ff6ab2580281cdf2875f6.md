![](bbox=[0.18, 0.16, 0.82, 0.44])

Figure 5.2 Parallel topology with a fusion center (FC) and ad hoc scenarios where decision statistics and side information are shared among the nodes

also valuable in designing sensing and access policies, i.e., how the sensing task is allocated to the sensors for different subbands of interest over time and when and who gets access to the idle spectrum. The selected detection strategy is also intimately related to interference management and accessing the underutilized spectrum. If missed detections are not properly controlled, there will be collisions with the primary signal, and retransmissions are required from both the primary users and the secondary users. On the other hand, if there are too many false alarms, there will be fewer opportunities to access the spectrum and the improvements in spectrum efficiency obtained by cognitive radios are reduced. These considerations lead to the Neyman–Pearson scheme for distributed detection which can be stated as follows (see also Chapter 4): for a predefined global probability of false alarm $P_{FA}$, find (optimum) local and global decision rules $\Gamma = \{\nu_0(\cdot), \nu_1(y_1),..., \nu_{N_{SU}}(y_{N_{SU}})\}$, where $\nu_0(\cdot)$ is the global decision rule and $\nu_i(\cdot), i = 1,...,N_{SU}$ are the local rules, that minimize the global probability of missed detection $P_{MD}$.

A crucial assumption that leads to a tractable solution to the distributed detection problem is conditional independence of sensor observations, conditioned on the hypothesis:

$p(y_1,...,y_{N_{SU}} \mid \mathcal{H}_l) = \prod_{i=1}^{N_{SU}} p(y_i \mid \mathcal{H}_l), \quad l = 0,1, \tag{5.3}$

where $p(\cdot)$ is used here and elsewhere generically to denote probability densities or mass functions of its argument(s). If the assumption holds, the local mapping rules as well as the global decision rule at the fusion center become likelihood-ratio $\Lambda(\cdot)$ based threshold rules [194]. The likelihood ratio is given by

$\Lambda(\mathbf{u}) = \frac{p(\mathbf{u} \mid \mathcal{H}_1)}{p(\mathbf{u} \mid \mathcal{H}_0)}. \tag{5.4}$

This hypothesis $\mathcal{H}_0$ at the fusion center is that no signal is present and the alternative hypothesis $\mathcal{H}_1$ is that a signal is present. The decision between these two is made by comparing $\Lambda(\mathbf{u})$ to a threshold value $\psi_0$. If $\Lambda(\mathbf{u}) > \psi_0$, we decide $\mathcal{H}_1$, and if