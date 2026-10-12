
joint actions, negotiation of action selections among agents, or actions may be selected in turn and communicated to other agents. On the other hand, in the absence of any explicit coordination mechanism the agents may be able to observe the behavior of the other agents and try to learn a model of their policies.

For more advanced discussions on reinforcement learning, its challenges, benefits, and different learning algorithms, the reader is referred to [24, 31, 32, 78, 183, 184, 226] and the references therein.

## Reinforcement learning-based spectrum sensing and access policies

Reinforcement learning-based methods have been proposed for spectrum sensing and access in cognitive radio networks. Both single- and multiagent reinforcement learning methods have been proposed. In the following we will give an overview of the state-of-the-art in reinforcement learning in cognitive radio systems.

### Energy-efficient cooperative multiband sensing policy for cognitive radio systems

In [148, 149] a two-stage reinforcement learning-based collaborative multiband sensing policy for centralized cognitive radio systems is proposed. The fusion center operates as the learning agent of the cognitive radio network consisting of a group of secondary users. The actions determine which frequency bands are sensed and which frequency band each secondary user senses. The actions are chosen in two stages. In the first stage the frequency bands to be sensed are chosen. In the second stage the secondary users are assigned to sense the frequency bands chosen in the first stage. Thus, in the first stage the action corresponds to choosing the frequency bands and in the second stage the action corresponds to choosing the secondary users for each frequency band. The policy employs $\epsilon$-greedy action selection and single-state Q-learning with discount rate $\xi = 0$. Thus, the update of the action Q-values is given by

$$Q_{n+1}(a) = Q_n(a) + \alpha_n [r_{n+1} - Q_n(a)].\tag{5.83}$$

A separate Q-value is kept for each frequency band. In addition, for each secondary user a separate Q-value is kept for each frequency band. The reward $r$ is the obtained throughput for the frequency bands, and for the secondary users the reward is defined as follows:

$$r_{n+1,k} = \begin{cases} u_{n+1,k}, & u_{n+1,FC}=1, \\ Q_n(a), & u_{n+1,FC}=0, \end{cases}\tag{5.84}$$

where $u_{n+1,k}$ is the local decision of the $k$th secondary user and $u_{n+1,FC}$ is the global decision at the fusion center for that frequency band. Here, decision $u = 1$ denotes that the frequency band is occupied by a primary system. The secondary user Q-values are updated only when the decision at the fusion center is considered to be correct with high certainty, i.e., the global test statistic exceeds the decision threshold with a certain safety margin.

In the exploitation phase, the first stage of the sensing policy chooses greedily the $L$ best frequency bands to sense. In the second stage the following sensing assignment problem (SAP) is solved to assign the secondary users to sense each of the $L$ frequency bands:

$$\min_A \sum_{i=1}^{n_B} \sum_{k=1}^{N_{SU}} g_k a_{ki} \quad (5.85)$$
s.t.
$$P^{it}_{MD,FC}(A) \le \beta_i, \quad i = 1, \dots, n_B, \quad (5.86)$$
$$\sum_{i=1}^{n_B} a_{ki} \le L_k, \quad k = 1, \dots, N_{SU}, \quad (5.87)$$

where $n_B$ and $N_{SU}$ are the number of frequency bands and the number of secondary users, respectively, $L_k$ is the number of frequency bands secondary user $k$ can sense simultaneously, $g_k$ is the weight of user $k$ which can be used to favor or unfavor certain users, e.g., due to a high or low level of remaining battery power, $A$ is an $N_{SU} \times L$ binary sensing assignment matrix where the components $[A]_{ki} = a_{ki}$ are 0 or 1, $P_{MD,FC}(A)$ is the estimate of the probability of missed detection for the frequency band $b$ at the fusion center given $A$, and $\beta_i$ is the probability of missed detection constraint for the frequency band $i$. The estimates $P^{it}_{MD,FC}(A)$ are formed from the Q-values of the secondary users for each band.

The SAP is a binary integer programming problem. It optimizes energy efficiency by minimizing the number of secondary users sensing given the probability of missed detection constraints. This is accomplished by assigning the users with the best propagation channel to each primary user to sense the corresponding frequency band. Moreover, during exploration a pseudorandom frequency hopping policy [145, 147] is employed that guarantees a given diversity order, i.e., the number of secondary users sensing each frequency band simultaneously; see Fig. 5.11. Figure 5.12 depicts the throughput and probability of missed detection of the proposed scheme in a scenario with ten frequency bands and six secondary users.

![](img/2d42983cf592ef4fc8a22646ddc49799_259_0.png)

Figure 5.11 An example pseudorandom frequency hopping table indicating the index of the frequency band sensed by each secondary user (SU) in each time slot [145, 147]. In this example, there are four secondary users, three frequency bands, and the employed sensing diversity order is two.

![](img/2d42983cf592ef4fc8a22646ddc49799_260_0.png)

Figure 5.12 Throughput and probability of missed detection as a function of the sensing instance for the two-stage multiuser Q-learning-based sensing policy with $\epsilon$-greedy action selection [148]. With an appropriately chosen $\epsilon$ the proposed algorithm is able to achieve high throughput while minimizing the probability of missed detection. The ideal policy accesses always the unoccupied frequency bands providing the best throughput.

### Single-agent reinforcement learning-based spectrum sensing and access

Single-agent reinforcement learning-based spectrum sensing and access policies have been proposed in [18, 54, 55, 67, 227]. In [55] a model-based reinforcement learning algorithm, called the tiling algorithm, is proposed for balancing between exploitation and exploration in single-user spectrum sensing. A single frequency band case is considered in which the secondary user's policy determines how long the secondary user waits until it senses the frequency band again, depending on the previous sensing result. Sensing is assumed to incur a fixed cost. In the proposed scheme the secondary user first performs an exploration phase to learn the model parameters. Then in the second phase a fixed sensing policy based on the learned parameters is employed to exploit the spectrum. In [54] a single secondary user multiband sensing and access policy is proposed. State transition probabilities of the primary users are assumed to be known and value iteration with a discretized state space is employed to optimize the policy. An actor-critic reinforcement learning-based multiband sensing policy is proposed in [18] for deciding which frequency band to sense as well as for balancing between sensing, transmission, and switching between different frequency bands. In [227] a single-agent Q-learning-based approach for dynamic frequency band selection for secondary access is proposed. The secondary user receives a negative reward whenever its transmission collides with a primary user. Hence, the secondary user learns to avoid collisions with the primary users. A single-user spectrum sensing and access scheme based on Q-learning is proposed in [67]. At each time step the secondary user makes a decision based on Q-learning whether to explore for new spectral opportunities or to exploit its home band. The secondary users are assumed to have license to use the home band at all times. The secondary user may decide to search for new spectral opportunities if the quality of its home band degrades too much. During the exploration phase the secondary user (or a group of secondary users) senses frequency bands in a sequential order until it finds an available frequency band.

### Multiagent Q-learning for Aloha-like multiband spectrum access

In [107] a Q-learning multiagent, multiband Aloha-like spectrum access policy is proposed. The secondary users in the cognitive radio network are assumed to be employing an Aloha-like transmission scheme without any explicit collision avoidance. There is no communication or negotiation among the secondary users. Thus, two or more secondary users transmitting simultaneously on the same frequency band will collide with each other resulting in a failed transmission for all involved parties.

In the cognitive radio scenario considered in [107] there are $N_{SU}$ secondary users and frequency bands. Moreover, the spectral opportunities (and thus the primary user occupancy statistics) are assumed to be identical for each secondary user. Each secondary user employs a reinforcement learning-based sensing and access policy individually without any information exchange with the other secondary users. The other secondary users are considered as part of the environment. Thus, in addition to learning the primary user occupancy statistics, the secondary users have to learn how to avoid other secondary users as well. However, the users are assumed to be synchronized in the time domain and using a slotted time structure with alternating sensing and access slots.

Both fully observable and partially observable spectrum occupancy scenarios are considered. The more interesting scenario is the partially observable scenario in which each secondary user is able to sense only one frequency band in each time slot. In this case, the state of the environment as observed by the secondary user $i$ is defined as

$$s_{i,n} = [\tau_{i,b,n}, \dots, \tau_{i,n_B,n}, u_{i,1,n}, \dots, u_{i,n_B,n}], \quad (5.88)$$

where $\tau_{i,b,n}$, $b = 1, \dots, n_B$, denotes the number of time slots that have passed since the user $i$ sensed frequency band $b$ the last time. And $u_{i,b,n}$, $b = 1, \dots, n_B$, denotes the corresponding occupancy state of the frequency band $b$ the last time it was sensed by user $i$. Each user employs independently the Q-learning algorithm with softmax action selection to maximize the expected sum of its discounted throughputs. It is shown
