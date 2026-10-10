
## Ramsey Theory

### 16.1 WHAT IS RAMSEY'S THEOREM?

In chapter 1 we raised the following problem.

### PROBLEM 16A

### Friends at a Party

There are six people at a party. The people in each pair are either friends or strangers. We claim that, among the six, there are (at least) three people who are all friends or all strangers. Are we correct?

Although this seems a fairly lighthearted problem it is related to other, much more significant questions. In 1930, Frank Ramsey,${}^{a}$ in connection with a problem in mathematical logic, obtained the following very technical theorem. (Do not worry if it is a little bit tricky to grasp in full at the first— even sixth!--reading. You won't need to know it. It just helps with setting the scene.)

#### RAMSEY'S THEOREM

Let positive integers $k$, $s$, $t_{1}$, $t_{2}$, ..., $t_{k}$ be given with $s \geq 2$. Then there exists an integer $F$ such that if the set, $\mathcal{C}$, of all subsets containing $s$ numbers from the set $X = \{1, 2, \dots, F\}$ of the first $F$ positive integers is partitioned into $k$ disjoint sets $C_{1}$, $C_{2}$, ..., $C_{k}$, in any manner you please, then either there are $t_{i}$ elements of $X$ all of whose $s$-element subsets lie in $C_{i}$, or there are $t_{i}$ elements of $X$ all of whose $s$-element subsets lie in $C_{2}$, or ... there are $t_{k}$ elements of $X$ all of whose $s$-element subsets lie in $C_{k}$.

> ${}^{a}$ F. P. Ramsey, On a Problem in Formal Logic, Proceedings of the London Mathematical Society, 30, 1930, pp. 264–286. Frank Plumpton Ramsey was born in Cambridge on January 23, 1903, into an academic family. His father was Arthur Ramsey, an applied mathematician who published standard textbooks of their day on statics and dynamics, and who became president of Magdalen College, Cambridge. His younger brother, Michael, was Archbishop of Canterbury from 1961 to 1974. Frank Ramsey made distinguished contributions to economics, philosophy, and probability, as well as to mathematical logic. While an undergraduate he wrote a perceptive review of Wittgenstein's Tractatus. His combinatorial theorem was a preliminary result to enable him to solve a particular case of the decision problem for quantifier logic, but has proved more interesting and fruitful than the problem from logic that motivated it. He died tragically young in Guy's Hospital, London, on January 19, 1930, after an illness.

What has this to do with Problem 16A? Ramsey’s theorem tells us that there is some number, say $F$, such that if we divided the two-element subsets of a set of $F$ people into two classes (the pairs of *friends* and the pairs of *strangers*—let us call them *red* pairs and *blue* pairs!), then there will be either three *people* all of whose two-element subsets are red or three *people* all of whose two-element subsets are blue. Problem 16A asks whether we can take $F$ to be 6.

The introduction of the colors *red* and *blue* into this discussion suggests a connection with edge colorings of graphs. We can represent a set of people by the vertices of a complete graph, coloring an edge *red* if it joins two people who are friends, and *blue* if it joins two people who are strangers. In these terms, Problem 16A asks whether, given an edge coloring of the complete graph $K_6$ using the two colors red and blue, there will always be either a red triangle or a blue triangle in the graph.

It is convenient to introduce some notation to help us to discuss problems of this kind.

#### DEFINITION 16.1

Given positive integers $k, s, t_1, t_2,\dots,t_s$ with $s \geq 2$, we use the notation $F(s; t_1, t_2,\dots,t_s)$ for the smallest integer $F$ that has the property of Ramsey’s theorem. (Note that it was not obvious, before Ramsey’s proof, whether such a number $F$ even existed!)

Using the notation introduced in this definition, we see that Problem 16A covers the case of Ramsey’s theorem where $s = 2$ and $t_1 = t_2 = 3$, and claims that $F(2;3,3)$ may be taken to be 6. Whether or not $F(2;3,3)$ can be taken to be 5 or less is dealt with below.

As we have seen, in the case where $s = 2$, it is quite easy to interpret Ramsey’s theorem geometrically, as the two-element subsets of $X$ correspond to the edges of the complete graph whose vertices correspond to the elements of $X$, and the partition of $X$ into the disjoint subsets $C_1, C_2,\dots, C_s$ corresponds to a coloring of those edges. Any attempt to visualize Ramsey’s theorem for $s = 3$ will to tricky (since we should have to imagine every plane determined by three points as being colored) and for $s > 3$ impossible for ordinary mortals. On the other hand, working with $k > 2$ (at least in the case of $s = 2$) is not as much of a problem since it is not difficult to picture the edges of a (complete) graph as being adorned by any number of different colors. Nevertheless we will mainly concentrate on the case $s = k = 2$ so that we can continue to use the appealing graphical interpretation in which the edges of a graph are painted in just two colors.

### The Solution of Problem 16A

We shall solve Problem 16A easily by making a trivial application of the pigeonhole principle but will, simultaneously, stir up a bit of a hornets’ nest of more difficult problems.

![](img/eb401bf41900fd678cd9d368a197e486_320_0.png)

First imagine that each pair of the six people is holding the ends of a string, which is red if they are friends and blue if they are strangers as in Figure 16.1. Select any one of the six people present, say *A* (or any one of the six vertices of the graph, etc.). This person is holding five strings, each of which is red or blue. So *A* must be holding either at least three red strings or at least three blue strings. Let us suppose *A* holds at least three red strings. If not, then repeat the argument below with the words *red* and *blue* interchanged.

Now, suppose *B, C, D* are three of the people who share a red string with *A*. If any two of *B, C, D* also share a red string, then this string, together with the red strings these two share with *A*, form a red triangle. If this is not the case, then each of the strings that *B, C, D* share must be blue, which, of course, provides a blue triangle.

With the number of people, six, apparently being plucked from nowhere, you may suspect that, if we could have “got away” with using only five people, we would have said so. And you would be right, as we will show below. Do notice that we are not saying that you will *never* get a set of three mutual friends or a set of three mutual strangers at your party if you invite five people. What we *are* saying is that it would be *possible* for you to invite five people so that, among them, there is no group of three mutual friends and no group of three mutual strangers.

To confirm this we only need produce one suitable *example*. That is most easily done with a graph, as in Figure 16.2, where the vertices represent the five people, the solid lines represent red strings, and the dotted lines represent blue strings. It is easily seen that, in this diagram, there is no solid-line triangle and no dotted-line triangle; hence there is no trio of mutual friends and no trio of mutual strangers.

In graph-theoretic terms, a triangle is nothing other than the complete graph, K₃, with three vertices. So we can summarize the conclusion of Problem 16A as follows: If the 15 edges of the complete graph, K₆, are each colored either red or blue, then there is either a subgraph isomorphic to K₃, all of whose edges are red, or a subgraph isomorphic to K₃, all of whose edges are blue. We then showed by an example that the number 6 could not be replaced by the number 5.

The significance of this way of formulating the result is that when we generalize it, as we are about to do, instead of going from triangles to quadrilaterals, pentagons, and so on, we generalize from K₃ to the other complete graphs K₄, K₅, and so on. Do note that K₄ does not have four edges but has six edges. Many a student has been caught out by

![](img/eb401bf41900fd678cd9d368a197e486_321_0.png)
