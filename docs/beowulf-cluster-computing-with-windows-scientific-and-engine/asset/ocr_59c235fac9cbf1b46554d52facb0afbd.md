```
% forkjoin
t10001c t40149 tc0037
Length 4, Tag 11, Tid t40149
Length 4, Tag 11, Tid tc0037
Length 4, Tag 11, Tid t10001c
% forkjoin 4
t10001e t10001d t4014b tc0038
Length 4, Tag 11, Tid t4014b
Length 4, Tag 11, Tid tc0038
Length 4, Tag 11, Tid t10001d
Length 4, Tag 11, Tid t10001e
```

Figure 11.3
Output of fork/join program.

length of vectors to compute. Each spawned process will receive $n/nproc$ elements of $X$ and $Y$, where $n$ is the length of the vectors and $nproc$ is the number of processes being used in the computation. If $nproc$ does not divide $n$ evenly, then the master will compute the dot product on extra the elements. The subroutine SGENMAT randomly generates values for $X$ and $Y$. PSDOT then spawns $nproc - 1$ copies of itself and sends each new task a part of the $X$ and $Y$ arrays. The message contains the length of the subarrays in the message and the subarrays themselves. After the master spawns the worker processes and sends out the subvectors, the master then computes the dot-product on its portion of $X$ and $Y$. The master process then receives the other local dot products from the worker processes. Notice that the PVMFREECV call uses a wild card $(-1)$ for the task id parameter. This indicates that a message from any task will satisfy the receive. Using the wild card in this manner results in a race condition. In this case the race condition does not cause a problem since addition is commutative. In other words, it doesn't matter in which order we add up the partial sums from the workers. Unless one is certain that the race will not affect the program adversely, race conditions should be avoided.

Once the master receives all the local dot products and sums them into a global dot product, it then calculates the entire dot product locally. These two results are then subtracted and the difference between the two values is printed. A small difference can be expected due to the variation in floating-point roundoff errors.

If the PSDOT program is a worker, then it receives a message from the master process containing subarrays of $X$ and $Y$. It calculates the dot product of these subarrays and sends the result back to the master process. In the interests of brevity we do not include the SGENMAT and SDOT subroutines.