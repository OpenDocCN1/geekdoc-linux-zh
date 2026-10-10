# 4.2 DERANGEMENTS

We now come to the "Snap" problem from Chapter 1, there called Problem 4. As we said, the answer may come as a surprise.

# PROBLEM 4.5

Two fully shuffled standard packs of 52 cards are placed face down and side by side. One after another, pairs of cards, one from each pack, are turned over. What is the probability that, as all 52 pairs are turned over, at least one pair of cards will be the same?

# *Comment*

Before reading the solution below, try to estimate this probability or, better still, solve the problem for yourself.

# *Solution*

We can calculate the required probability, say $p_{52}$, by assuming that the order of the cards in one of the packs is fixed and then counting the number of arrangements of the second pack where there is at least one coincidence with the first pack. Then $p_{52}$ is this number divided by the total number of arrangements of the cards in the second pack, which is, of course, 52!

For $1 \leq i \leq 52$ we let $A_i$ be the set of those arrangements of the second pack in which the $i$th card coincides with the $i$th card of the first pack. Then

```
$$p_{52} = \frac{\left(\# \bigcup_{i=1}^{52} A_i\right)}{52!}$$
```

Given $1 \leq i_1 < ... < i_k \leq 52$, $A_{i_1} \bigcap ... \bigcap A_{i_k}$ is the set of those arrangements of the second pack in which the card in each position $i_1, ..., i_k$ is identical to the card in the same position in the first pack. The other $(52-k)$ cards can be arranged in any order in the remaining $(52-k)$ positions. Therefore $\#(A_{i_1} \bigcap ... \bigcap A_{i_k}) = (52-k)!$ Hence, by the inclusion-exclusion theorem,

```
$$egin{aligned} \left(\# \bigcup_{i=1}^{52} A_i\right) &= \sum_{k=1}^{52} (-1)^{k+1} \sum_{1 \leq i_1 < ... < i_k \leq 52} \#(A_{i_1} \bigcap ... \bigcap A_{i_k}) \\ &= \sum_{k=1}^{52} (-1)^{k+1} C(52, k)(52-k)! \end{aligned}$$
```

The good thing is that this last expression simplifies because

```
$$C(52, k)(52-k)! = \frac{52!}{k!(52-k)!} \times (52-k)! = \frac{52!}{k!}$$
```