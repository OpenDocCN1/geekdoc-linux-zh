# 6.3.  TOUGHNESS OF GRAPHS

![](bbox=[0.15, 0.12, 0.85, 0.52])

Figure 6.8: The Bauer-Broersma-Verlman graph: 
A 2-tough graph that is not Hamiltonian

A **decision problem** is a question that can be answered *yes* or *no*. A decision problem belongs to the class **P** if there is a polynomial-time algorithm that solves every instance of the problem in polynomial time. There are decision problems that are difficult to solve but once a solution is revealed, it is easy to verify that this is in fact a solution. For example, it is difficult in general to determine whether a given graph $G$ is Hamiltonian but it is easy to verify that a cyclic sequence of vertices of $G$ constitutes a Hamiltonian cycle of $G$. The class of such difficult-to-solve easy-to-verify problems is denoted by **NP**.

The problems in **NP** and the problems in **P** have one property in common, namely: Given a solution to a problem in either class, the solution can be verified in polynomial-time. Thus, $\mathbf{P} \subseteq \mathbf{NP}$. One of the best known problems in mathematics asks whether every problem in **NP** is also in **P**. This is called the **$\mathbf{P} = \mathbf{NP}$ Problem** and is considered by many as the most important problem in theoretical computer science. Its importance and fame have only been magnified because of a million dollar prize offered by the Clay Mathematics Institute for its solution.

A problem in the set **NP** is called **NP-complete** if a polynomial-time algorithm for a solution to the problem would result in polynomial-time solutions for all problems in **NP**. The **NP-complete** problems are among the most difficult in the set **NP** and can be reduced from and to all other **NP-complete**