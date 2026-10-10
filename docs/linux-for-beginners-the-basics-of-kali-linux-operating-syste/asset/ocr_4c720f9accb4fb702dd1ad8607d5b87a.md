processes. With the increasing number of ready processes in the system, it is unprofitable to view the queue from start to finish during each call of the scheduling procedure

+   • If the number of processes is very large, it will take a long time to list all the dynamic priorities at the beginning of a new era. On the other hand, epochs change less often with more processes in the system

+   • The algorithm is designed to reduce response time for processes with limited I/O capabilities, even if they are not interactive (eg, background search engine indexing) and do not require a short response time

+   • With the increase in the number of processors, maintaining common queues that do not take into account the presence of different processors becomes unprofitable

# Modern Approaches To Planning Implementation

These shortcomings began to significantly affect the operation of the system when it was operating under load conditions. Under normal circumstances, traditional Linux scheduling worked quite effectively. Work on fixing the shortcomings has continued. As a result, a new implementation of the scheduling algorithm has been integrated into the kernel of version 2.6. Consider briefly how it helps the solution ' bind previously mentioned problems.

First of all, this algorithm supports separate queues of finishing processes for each processor, ensuring efficient operation under conditions of multiprocessing. Another problem that has solutions connected with the need to rely on the old algorithm for the dynamic priority of all ready processes during each procedure call planning. The decisions are as follows: each queue of the digestion processes is an array of ready-made process queues, where the elements are sorted by dynamic priority. As a result, when choosing a process to execute, it is enough to look at the highest priority queue for the first process that can be started. This procedure does not depend on the number of ready processes with a STEM.