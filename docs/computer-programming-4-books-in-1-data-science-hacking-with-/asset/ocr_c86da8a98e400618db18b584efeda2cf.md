In each round, the ads are displayed, and it’s indicated which one/ones were clicked (0 if not clicked, 1 if clicked). As discussed earlier, the goal is to explore first, pick the winner, and then exploit it. One popular way to achieve this is by Thompson Sampling. Simply, it addresses the exploration-exploitation dilemma (trying to achieve a balance) by sampling or trying promising actions while ignoring or discarding actions that are likely to underperform. The algorithm works on probabilities and this can be expressed in code.

When we run the code and visualize:

![](bbox=[0.25, 0.25, 0.73, 0.53])

Notice that the implementation of Thompson sampling can be very complex. It’s an interesting algorithm which is widely popular in online ad optimization, news article recommendation, product assortment, and other business applications.

There are other interesting algorithms and heuristics such as Upper Confidence Bound. The goal is to earn while learning. Instead of later analysis, our algorithm can perform and adjust in real-time. We’re hoping to maximize the reward by trying to balance the tradeoff between exploration and exploitation (maximize immediate performance or “learn more”) to improve future performance. It’s an interesting topic itself, and if you want to dig deeper, you can read more online resources.