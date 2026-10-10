Setting the scene. To introduce the proof gently, we begin with an example that indicates the general method. Consider, then, a typical partition into distinct parts, say $27 = 8 + 7 + 6 + 4 + 2$, whose dot diagram is shown on the left-hand side of Figure 8.1. This has five distinct parts, the smallest of which, 2, we call the base.

Notice that the final dots in the first three (but not four) rows lie on a line at 45° to the horizontal. Such a line of maximal length, and starting on the top row, is called the top diagonal. To change the given partition into one with four distinct parts, we move the dots of the base, adding one dot to the end of each of the first two original rows, both of which end with a dot on the top diagonal. The new partition, $27 = 9 + 8 + 6 + 4$, is shown on the right-hand side of Figure 8.1.

This process converts one partition into distinct parts into another partition of the same number into distinct parts, but with one fewer part. The process can be reversed by taking the two dots that form the top diagonal in the new partition and returning them to their former base position. Since the first partition has one more part than the second, it has an even number of parts if and only if the second partition has an odd number of parts.

At first sight this process sets up a one–one correspondence between the partitions of $n$ into an even number of distinct parts, and the partitions of $n$ into an odd number of distinct parts. If this always worked, we would have a proof that $u_{e,d}(n) - u_{o,d}(n) = 0$, for all positive integers $n$.

But does this argument ever break down? Well, yes. For example, the (forward) process breaks down when the number of dots in the base exceeds the number of dots in the top diagonal! Fortunately, this situation can be kept under control. Here is the proof.

# PROOF OF THEOREM 8.5

Let $D$ be any dot diagram corresponding to a partition of $n$ into distinct parts and let $b, t$ be the number of dots in the base and the top diagonal of $D$, respectively. We deal with the three cases (i) $b < t$, (ii) $b = t$, and (iii) $b > t$ separately.

Case (i), $b < t$. Here the $b$ dots of the base are moved to sit at the right-hand end of the first $b$ rows of the dot diagram, as described above. In this way, a diagram with an even number of distinct parts has associated with it a diagram with an odd number of distinct parts, and vice versa.

Case (ii), $b = t$. Here the same argument applies except where the final dot of the base is also the lowest dot of the top diagonal, so that removing all of the base would, at the same time, also remove the last element of the top diagonal—as in Figure 8.2, which corresponds to the partition $22 = 7 + 6 + 5 + 4$.

![](bbox=[0.17, 0.82, 0.88, 0.94])