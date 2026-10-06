# CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

iteration 6, thread 2

iteration 7, thread 2

iteration 8, thread 2

iteration 3, thread 1

iteration 4, thread 1

iteration 5, thread 1

master thread completed

As shown by our output, three iterations are assigned to each thread. Since the threads are executing in parallel, the print statements from all the threads are shown interleaved in the console. The print message after the parallel region from the master thread always appear at the end of the console output due to the barrier after the parallel region.

OpenMP supports several policies for assigning iterations to threads. By default, the assignment is static, meaning that each thread executes approximately the same number of loop iterations. Since all threads must finish their assigned set of iterations before the program moves beyond the loop, threads whose assigned set of iterations finish faster than other threads will experience a longer waiting time than other threads.

In order to avoid this problem, OpenMP supports dynamic scheduling, where a smaller batch of loop iterations, called a chunk, is assigned to each thread. A new chunk is assigned in turn to each thread that completes its previous chunk. This allows for load balancing, and is best when execution time varies between iterations.

Scheduling in general is only applicable for parallel for directives and can be specified using the schedule option for the parallel directive. By default, for parallel loops are scheduled statically. A directive option specifies dynamic scheduling. For example "#pragma parallel (dynamic)" turns on dynamic scheduling with automatic chunk size; "#pragma parallel for schedule(dynamic,chunksize)" allows programmer to specify a chunksize.

# 2.4.7 OpenMP with performance counters

Perf_event only records events in the master thread so the programmer account for this when calculating metrics that incorporates values not reported by the performance counters, such as the number of floating-point operations. For example, the cnts_dump() function will only count the