![](bbox=[0.14, 0.11, 0.86, 0.48])

provides us with a possible schedule for the soccer tournament taking place over a minimum of six days.

Example 17.11 One year it is decided to have a charity tennis tournament consisting entirely of doubles matches. Five tennis players (denoted by A, B, C, D, E) have agreed to participate. Each pair {W, X} of tennis players will play a match against every other pair {Y, Z} of tennis players, where then {W, X} \cap {Y, Z} = \emptyset, but no 2-person team is to play two matches on the same day. What is the minimum number of days needed to schedule such a tournament? Give an example of such a tournament using a minimum number of days.

Solution. We construct a graph G whose vertex set is the set of 2-element subsets of {A, B, C, D, E}. Thus, the order of G is binom{5}{2} = 10. Two vertices {W, X} and {Y, Z} are adjacent if these sets are disjoint. The graph G is shown in Figure 17.9. Thus, G is the Petersen graph. To answer the question, we determine the chromatic index of G, which we have seen is 4. A 4-edge coloring of G is given in Figure 17.9 together with a possible schedule of tennis matches over a period of four days.

# Overfull Subgraphs

As we have seen, the size of a graph G of Class one and having order n cannot exceed \lfloor \frac{n}{2} \rfloor \cdot \Delta(G). Since the size of any overfull graph of order n exceeds this number, every overfull graph is therefore of Class two. There are related subgraphs such that if a graph G should contain one of these, then G must also be of Class two.