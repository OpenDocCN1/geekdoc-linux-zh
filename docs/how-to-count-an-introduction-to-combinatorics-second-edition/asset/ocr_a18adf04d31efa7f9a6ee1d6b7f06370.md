same as the number of ways of choosing 20 horses in order from a set of 20 horses, and so we could have obtained this by using Theorem 2.1, which tells us that this number is P(20,20) = 20!/0! = 20! (Recall the standard convention that 0! = 1.) Thus we have:

# **THEOREM 2.2**

The number of different permutations of n objects is n!

The values of n! grow very rapidly. Even for quite small values of n, the factorial n! is very large. For example, 10! = 3,628,800 and 100! is larger than 10⁴⁵⁷.

# **PROBLEM 2.3**

In how many ways can eight counters be placed on a square 8 × 8 chessboard in such a way that no two counters lie either in the same row or in the same column? Note that we can reword this problem as: In how many ways can eight rooks be placed on a chessboard so that no two rooks are “attacking” each other? This latter problem is generalized in Chapter 17.

# Solution

Let us place one counter in each row in turn. For the first row there are eight columns in which the counter may be put. Having placed this counter, when it comes to the second row, there are just seven columns where we may place a counter, as it must not be in the same column as the counter in the first row. As we place counters in successive rows, the number of possible columns where the next counter may be placed goes down by one at each stage. So the total number of permissible arrangements of the counters is 8 × 7 × ... × 2 × 1, that is, 8! (= 40,320). One of these arrangements is shown in Figure 2.2.

Clearly there are, more generally, n! different ways to place n counters on the squares of an n × n chessboard so that there are neither two counters in the same row nor in the same column. In Exercise 2.2.4A you are asked to generalize this to the case of placing any number of counters on rectangular boards of any size.

![](bbox=[0.35, 0.66, 0.66, 0.86])

FIGURE 2.2