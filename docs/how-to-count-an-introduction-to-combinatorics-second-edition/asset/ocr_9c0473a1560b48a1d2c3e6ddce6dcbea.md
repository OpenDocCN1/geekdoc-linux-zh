$t_3-t_2$, $t_4-t_3$, $t_5-t_4$, $t_6-t_5$, and $51-t_6$ is at least 2. (All the differences now being on equal footing, namely, “greater than or equal to 2,” makes life a little easier.) Now, putting $T_1=t_1-(-1)$, $T_2=t_2-t_1$, $T_3=t_3-t_2$, $T_4=t_4-t_3$, $T_5=t_5-t_4$, $T_6=t_6-t_5$, and $T_7=51-t_6$, we see that $T_1+T_2+\dots+T_7=52$. Hence the number of sextuples $(t_1,t_2,t_3,t_4,t_5,t_6)$ satisfying Equation 3.3 is the same as the number of positive integer solutions, $(T_1,T_2,T_3,T_4,T_5,T_6,T_7)$, of the equation $T_1+T_2+\dots+T_7=52$ with $T_i \ge 2$ for $1 \le i \le 7$. Copying the method used in the proof of Theorem 3.2, by putting $S_i=T_i-2$, for $1 \le i \le 7$, this is the same as the number of nonnegative integer solutions of $S_1+S_2+\dots+S_7=52-(7\times 2)=38$. By Theorem 3.1, this number is $C(38+(7-1),7-1)$, that is, $C(44,6)$.

Hence the probability that a lottery draw (of 6 balls from 49) will contain no pair of successively numbered balls is

$\frac{C(44,6)}{C(49,6)} = \frac{44!}{6!38!} \bigg/ \frac{49!}{6!43!} = \frac{44 \times 43 \times 42 \times 41 \times 40 \times 39}{49 \times 48 \times 47 \times 46 \times 45 \times 44} = \frac{22,919}{45,402} \approx 0.505$

to three decimal places. So the probability of a pair of consecutive numbers appearing when six (different) numbers are drawn from numbers 1 to 49 is, approximately, $1-0.505=0.495$. In other words, it is only slightly *less* likely than not!

Another variation on Problem 3.1 is the following.

# PROBLEM 3.4

How many nonnegative integer solutions are there of the inequality $x+y+z+w+t<14$?

# Solution

An unthinking attempt at this problem might say: “Let us find the number of solutions to each of the equations $x+y+z+w+t=n$ for $n=0,1,2,\dots,13$ and then add up the answers.” There is nothing actually wrong with this approach, and, by Theorem 3.1, this gives the answer as $C(4,4)+C(5,4)+\dots+C(17,4)$.

However, the problem can be answered more briefly as follows. To each solution, say $(a,b,c,d,e)$, of the equation $x+y+z+w+t=n$, with $0 \le n \le 13$, there is a solution, $(a,b,c,d,e,f)$, of the equation $x+y+z+w+t+u=13$ where $f=13-n$, and vice versa, with the newly introduced term, $f$, taking up the slack. Hence the number of nonnegative integer solutions of $x+y+z+w+t<14$ is the same as the number of nonnegative solutions of $x+y+z+w+t+u=13$. It follows immediately from Theorem 3.1 that this number is $C(18,5)$.

The reader who wonders if (or, perhaps better, *why*) these answers are the same should reread Theorem 2.8.

The second method used in the solution of Problem 3.4 clearly leads to the following further generalization of Theorem 3.1.

# THEOREM 3.3

Let $k$, $n$ be positive integers. Then the number of nonnegative integer solutions of the inequality $x_1+x_2+\dots+x_k<n$ is $C(n+k-1,k)$ or, equivalently, $C(n+k-1,n-1)$.