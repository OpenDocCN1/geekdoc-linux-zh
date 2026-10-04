![](bbox=[0.1, 0.07, 0.8, 0.5])

# Figure 28.1 Simplified state transition diagram for CPU scheduler.

3. There are several ways for a process to move from the ‘on CPU’ state. Transition 3 is the one which takes the currently running process and places it back on the runnable list. This happens when the process has used up its allocated time slice on the processor and must be pre-empted to give other processes a chance to run.

4. The other main way for a process to lose control of the processor occurs when it requests some I/O operation which will involve a time delay while the machine hardware responds to the request. During this I/O wait, the process is not in a position to run even if the processor becomes totally free. Consequently, when a process blocks waiting for I/O in this way, it cannot be returned to the runnable list, because it simply isn’t runnable. It is therefore transferred via transition 4 into a blocked state awaiting the completion of its I/O request.

5. When the I/O event for which a blocked process has been waiting occurs, the process becomes eligible to run once again. However, the process is not immediately given CPU time to deal with its I/O but is only returned to the runnable list to await selection once more by the scheduler. This is transition 5.

6. The final way to lose control of the processor, shown on this simplified diagram, occurs when a running process terminates. Transition 6 shows the event leading to process termination.

Surprisingly perhaps, this state transition diagram is generally applicable regardless of the actual algorithm used by the CPU scheduler to determine which process should run next.

There are many possible algorithms which can be used for CPU scheduling, including lots of theory about which is best in various sets of circumstances. However, rather than engage in a general discussion of scheduling algorithms here, we shall just concentrate on the details of the Linux scheduling algorithm itself.