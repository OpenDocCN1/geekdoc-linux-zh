flows T io quickly follow the instructions of their ranges CPU and then move to the IO. After that, T CPU will again capture the processor for a long time, etc.

# ## Circular Planning

The easiest to understand and the fairest algorithm is a *circular plan* algorithm (round-robin scheduling). In the Middle Ages, the term “round-robin ” was coined in petitions where signatures were done in a circle so that one could not know who signed up first (this name indicates that for such an algorithm all flows are equal).

Each stream allocated time period in which this stream is allowed to run is called a *time slice* ( or time quantum ). When the thread is still running after the time quantum is exhausted, it is interrupted and the processor switches to perform instructions from another thread. When it blocks or completes its execution until the time quantum runs out, the processor is also passed to another thread. The length of time quantum for the whole system is the same.

Such an algorithm is quite easy to implement. For this, the turn of the ready threads should be a cyclic list. When a stream has exhausted its quantum of time, it is moved to the end of the list, where new flows are provided. Checking the exhaustion of the quantum of time is performed in the interrupt handler from the system timer.

The only characteristic that affects the operation of the algorithm is the length of the quantum of time. The balance between time spent switching contexts and having to respond to many simultaneous interactive queries should be kept in mind here.

Tasking too short a quantum of time leads to a lot of context switches, and a significant percentage of CPU time is spent not on useful work, but on those switches. On the other hand, the task of a too-long quantum, while saving CPU time, also reduces the response time for interactive queries because if ten users press a