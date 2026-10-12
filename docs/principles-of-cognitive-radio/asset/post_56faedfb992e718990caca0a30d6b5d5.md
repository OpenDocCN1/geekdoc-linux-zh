
- a sequence of discrete time steps $n = 0, 1, 2, \dots$;
- an agent $i$;
- a set of possible states of the environment $s \in S$;
- a set of possible actions for the agent in each state $a \in A$;
- a state transition function $\phi : S \times A \times S \rightarrow [0, 1]$ which defines the transition probability $P [s_{n+1} | s_n, a_n]$;
- a reward function $r : S \times A \times S \rightarrow \mathbb{R}$ which gives the agent a reward for taking action $a_n$ in state $s_n$ resulting in new state $s_{n+1}$.

In every state $s_n$ the agent chooses an action $a_n$ according to some policy $\pi$. A policy $\pi$ is a stochastic or deterministic function that determines how the agent selects its action $a_n$ in each state $s_n$. Taking the action $a_n$ in state $s_n$ results in a new state $s_{n+1}$ and a scalar reward $r_{n+1}$ for the agent. The goal of the agent is to try to act in a way that maximizes not just the immediate reward but also the future rewards. A commonly employed goal in reinforcement learning is to optimize the expected sum of discounted rewards

$\mathcal{R}_n = \mathbb{E}\left[ \sum_{k=0}^{\infty} \xi^k r_{n+k+1} \right], \tag{5.77}$

where $r_n$ is the reward at time $n$ and $\xi$, $0 \le \xi < 1$, is the discount rate. This model may not be the most appropriate model in all applications. In particular, in episodic tasks, for which the episode length is known beforehand, models with finite horizon are typically more appropriate. However, the infinite-horizon discounted model is mathematically more tractable than most other models. Other options for defining the goal in reinforcement learning include the ones already introduced for the bandit problems in Section 5.3.2.

A convenient way of optimizing the sum of expected discounted future rewards is to learn an optimal action-value function. The action-value function $Q(s, a)$ evaluates the value of each action in a given state. The action-value function is defined as the expected return (i.e., the sum of discounted rewards) of taking an action $a$ in state $s$ and then following policy $\pi$:

$Q^{\pi}(s, a) = \mathbb{E}_{\pi}\left[ \mathcal{R}_n \mid s_n = s, a_n = a, \pi \right]. \tag{5.78}$

The optimal action-value function $Q^*$ satisfies the Bellman optimality equation [183, p. 76]

$Q^*(s, a) = \max_{\pi} Q^{\pi}(s, a)$
$= \sum_{s' \in S} P[s' | s, a] \left[ r(s, a, s') + \xi \max_{a'} Q^*(s', a') \right]. \tag{5.79}$

where $r(s, a, s')$ is the reward function.

In the following two commonly employed powerful model-free temporal-difference reinforcement learning algorithms, Sarsa [169] and Q-learning [215, 216], for optimizing the action-value functions are introduced. Sarsa is an on-policy temporal-difference algorithm. An on-policy algorithm means that the action-value updates are based on the actually taken actions by the policy. The action-value updates of the Sarsa-algorithm are defined by

$Q_{n+1}(s_n, a_n) = Q_n(s_n, a_n) + \alpha_n \left[ r_{n+1} + \gamma Q_n(s_{n+1}, a_{n+1}) - Q_n(s_n, a_n) \right], \tag{5.80}$

where $\alpha_n$ ($0 < \alpha_n \le 1$) is a step size parameter (learning rate). Thus, the action-value function update is given by the temporal difference between the Q-values of the employed policy at time steps $n$ and $n + 1$ multiplied by the step size $\alpha_n$.

Q-learning is an off-policy temporal-difference algorithm. Thus, the temporal-difference update of Q-learning does not necessarily employ the Q-values of the employed policy as on-policy algorithms, such as Sarsa, do. The action-value updates of Q-learning are given by

$Q_{n+1}(s_n, a_n) = Q_n(s_n, a_n) + \alpha_n \left[ r_{n+1} + \gamma \max_{a' \in A} Q_n(s_{n+1}, a') - Q_n(s_n, a_n) \right]. \tag{5.81}$

The temporal difference update of Q-learning depends on the maximum Q-values of the possible actions. Note that for a greedy policy that always chooses the action with maximum Q-value the Sarsa and Q-learning algorithms are identical.

The convergence of the action-value function $Q_n$ to the optimum $Q^*$ has been established for one-step Sarsa in [181] and for Q-learning in [73, 196, 216]. The convergence is guaranteed with probability one if the agent employs a lookup-table to store the Q-values, visits every state-action pair infinitely many times, and $\sum_{n=0}^{\infty} \alpha_n = \infty$ and $\sum_{n=0}^{\infty} \alpha_n^2 < \infty$. Moreover, to ensure the convergence of one-step Sarsa, the learning policy must become greedy in the limit.

The convergence requires infinite visits to every state-action pair. Intuitively this is easy to understand. In order to find out whether the current policy is optimal the agent must explore other actions than the ones given by the current policy as well. This presents the agent with the tradeoff between exploitation and exploration. That is, whether to exploit the current policy and choose the greedy action or to explore other actions instead to possibly find out some other action that provides a higher return than the greedy action. The $\epsilon$-greedy action selection is a simple method that balances between exploitation and exploration by selecting the action that maximizes the action-value function, i.e., $a^* = \max_a Q(s, a)$, with a probability $1 - \epsilon$, or a random action, uniformly, with a probability $\epsilon$ regardless of the action value function estimates. Another simple, yet effective, action selection method is the softmax action selection method. In the softmax method the action $a$ is selected with probability

$\pi(s, a) = \frac{\exp\left(Q(s, a)/\tau\right)}{\sum_{a' \in A} \exp\left(Q(s, a')/\tau\right)}, \tag{5.82}$

where $a \in A$ and $\tau$ is a positive parameter called the temperature that controls the weighting of different actions. Low temperatures increase the differences in the action selection probabilities while high temperatures cause all actions to be almost equiprobable. In the limit, when $\tau \to 0$, the softmax method corresponds to greedy action selection, and when $\tau \to \infty$, the actions are selected randomly from a uniform distribution. In addition, adaptive algorithms for balancing between exploitation and exploration have been proposed in [195, 204].

We note that the above convergence results apply to a stationary situation only. That is, the convergence results state the conditions under which one-step Sarsa and Q-learning converge to an optimal stationary policy. In dynamic nonstationary environments, such as the one encountered in cognitive radio applications, one is interested in tracking a nonstationary problem. In such cases one of the most commonly employed approaches is to use a constant step size $\alpha_n = \alpha, \forall n$. A constant step size does not satisfy the above conditions for convergence. However, it guarantees that the more recent samples are weighted more heavily than the ones in the distant past which is a desired feature in nonstationary problems. Moreover, in nonstationary environments it is important to continue to explore. This may be accomplished, for example, by employing the $\epsilon$-greedy algorithm with a constant, sufficiently large $\epsilon$.

## Multiagent reinforcement learning

A multiagent reinforcement learning problem can be formulated as a stochastic game [31, 113]. A stochastic game formulation of a multiagent reinforcement learning problem consists of [31]

- a sequence of discrete time steps $n = 0, 1, 2, \dots$;
- a group of agents $\mathcal{N}' = \{1, \dots, N_{SU}\}$;
- a set of possible states $s \in S$;
- a set of possible actions for each agent in each state $a_i \in A_i, i \in \mathcal{N}'$; the combined action space is $A = A_1 \times \dots \times A_{N_{SU}}$;
- a state transition function $\varrho : S \times A \times S \rightarrow [0, 1]$ which defines the transition probability $P \{s_{n+1} = s_n, a_{1,n}, \dots, a_{N_{SU,n}}\}$;
- reward functions $r_i : S \times A \times S \rightarrow \mathbb{R}, i \in \mathcal{N}'$, which give the agents a reward for the joint action $a_{1,n}, \dots, a_{N_{SU,n}}$ of the agents in state $s_n$ resulting in new state $s_{n+1}$.

The rewards in a multiagent reinforcement learning problem depend on the joint actions of all the agents. This complicates the learning problem considerably. The agents have to adapt their own policies not only to the environment but to the other agents' policies as well. Defining the goal of a multiagent reinforcement learning task is a challenging problem. A good learning goal must include components that provide both stability to the learning process of the individual agents and adaptation to the other agents' dynamic behavior [31]. The learning goal depends also on the nature of the learning problem. Multiagent reinforcement learning tasks may be categorized into fully competitive, fully cooperative, and mixed tasks [31]. Mixed tasks are neither fully competitive nor fully cooperative. Each one of these classes requires different goals for the learning algorithm. Moreover, the level of coordination among the agents has a significant effect on both the stability of the learning process and the adaptation to the other agents' policies. The level of coordination depends on the application and its restrictions as well as on the chosen reinforcement learning algorithm and its goal. In some tasks there may be explicit coordination, e.g., in the form of pre-established preferences toward certain
