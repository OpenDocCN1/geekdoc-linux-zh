# # Partitions and Dot Diagrams

# ## 6.1 PARTITIONS

In Section 3.3 of Chapter 3 we saw how the problem of placing *n* identical balls in *k* identical boxes could be looked at in a different way by thinking of it as being about expressing *n* as the sum of at most *k* positive integers, when the order of the terms does not matter. For example, we wrote 6 as the sum of at most three positive integers in the following seven ways:

6, 5 + 1, 4 + 2, 4 + 1 + 1, 3 + 3, 3 + 2 + 1, 2 + 2 + 2,

and this corresponds to the fact that six identical balls may be placed in three identical boxes, with some of these boxes possibly remaining empty, in seven ways. Note that we count 6, *by itself*, as one way of writing 6 as the sum of positive integers.

We have introduced the notation $p_k(n)$ for the number of ways expressing *n* as the sum of at most *k* positive integers. Using this notation, we have that $p_3(6) = 7$. We call the above representations of the number 6 *partitions* of *n* into at most three *parts*. The functions $p_k$ are not too difficult to deal with. However, much more attention has been paid to the function *p*, where $p(n)$ is the total number of ways of expressing *n* as the sum of *any* number of positive integers. For example, $p(6) = 11$, since if we drop the restriction of having at most three parts, we obtain the following four other partitions of 6,

3 + 1 + 1 + 1, 2 + 2 + 1 + 1, 2 + 1 + 1 + 1 + 1, 1 + 1 + 1 + 1 + 1 + 1,

making 11 partitions altogether. The problem of finding a succinct formula for $p(n)$ is very hard, but in this chapter we shall be able to use some nice theorems about the $p_k$ functions to get some kind of grip on the values of $p(n)$. We now record the definitions of the functions $p_k$ and *p* formally.

# DEFINITION 6.1

For each positive integer *n*, $p(n)$ is the number of ways in which *n* can be expressed as a sum of positive integers, with the order not counting. Each such sum is called a *partition* of *n*. For