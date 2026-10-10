+   - They will always have priority over normal processes when planning

+   - The FIFO scheduling process is performed until it itself gives in to the processor (for example, as a result of suspension or termination) or until it is superseded by a higher-priority real-time process

+   - The same applies to the circular scheduling process, except that it will be further displaced after the quantum of time is exhausted

# ### Traditional Scheduling Algorithm

Consider an algorithm for scheduling ordinary processes. At the core of the algorithm is the allocation of CPU time to the *epoch* (epochs). During the epoch, each process has a quantum of time, the length of which is calculated at the time of the epoch. For the most part, different processes have quanta of different lengths. When the process has exhausted its quantum, it is displaced and during the current era, it will no longer be performed. Management is given to another process. If, however, the process is paused for I / O or due to synchronization, its quantum is not considered exhausted and it may be exhausted by the scheduler during the current era. The era ends when all ready-to-complete processes have exhausted their quanta. In this case, the scheduling algorithm recalculates the quanta for all processes and begins a new era. The quantum, which is set at the beginning of the era, is called the *basic quantum of the processing time*. Its values can be dynamically modified by the *nice* () and *setpriority* () system calls. The descendant process always inherits the basic quantum of its ancestor.

There are two types of process priority: fixed, for real-time processes that are set only during the process creation, and dynamic, for normal processes, which depend on the basic priority and the time remaining until the quantum is exhausted. Dynamic priority to any