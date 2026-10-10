62  How to Count: An Introduction to Combinatorics, Second Edition

# Exercises

**4.3.1A** Use the formula in Equation 4.7 to calculate the values of $S(4,2)$ and $S(8,4)$, and check that the values you get agree with those given in Table 3.2.

**4.3.1B** Use the formula in Equation 4.7 to calculate the values of $S(7,k)$ for $1 \le k \le 7$, and check that the values you get agree with those given in Table 3.2.

**4.3.2A** Use the recurrence relation $S(n,k) = S(n-1,k-1) + kS(n-1,k)$ of Theorem 3.4, and the fact that $S(n,1) = 1$ for each positive integer, to give a proof of Theorem 4.5 by mathematical induction.

(Use induction on $n$ to prove that for every positive integer $n \ge 1$, for integers $k$ with $1 \le k \le n$, the formula in Equation 4.7 of Theorem 4.5 holds. This is a good example of a case where *once you know which formula it is you want to prove*, proof by mathematical induction is a useful tool. As you will see, it enables us to prove Equation 4.7 just by algebraic manipulations. However, it wouldn't be much use if all we had was the recurrence relation, and we didn't have any idea what the correct formula was.)

**4.3.2B** Verify that Theorem 4.5 gives the same answers as does Theorem 3.5 of Chapter 3; namely, that for all positive integers $n$, $S(n,1) = S(n,n) = 1$, and for $n \ge 2$, $S(n,2) = 2^{n-1} - 1$.