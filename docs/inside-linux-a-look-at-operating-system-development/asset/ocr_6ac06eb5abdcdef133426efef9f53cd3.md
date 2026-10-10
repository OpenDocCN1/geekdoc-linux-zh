computation can proceed. Really tricky code could use a cycle of “are you done?”—“no”—do useful work—“are you done?”—“no”—do useful work—“are you done?”—“no”—do useful work, but it is still difficult to get the most out of the system.

![](bbox=[0.1, 0.25, 0.9, 0.46])

![](bbox=[0.1, 0.47, 0.9, 0.6])

![](bbox=[0.1, 0.61, 0.9, 0.71])

Figure 4.1: Overlapped I/O with two processes

The advent of the interrupt permits other useful work to be done while I/O is in progress. Figure 4.1b shows these same jobs with over- lapped computation and I/O. The user process merely has to initiate I/O and an interrupt service routine (ISR) can finish it. The user pro- cess has to check status flags only when it is about to consume data that has been ordered for input.

You’ll note that it’s not possible to achieve total overlap. While