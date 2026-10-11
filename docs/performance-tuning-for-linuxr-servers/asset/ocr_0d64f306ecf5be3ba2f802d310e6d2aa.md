CPU 6  IDLE= 99.78, BUSY= 0.00, INTR= 0.22  
CPU 7  IDLE= 99.85, BUSY= 0.00, INTR= 0.15

The example was run on an eight-way SMP machine and shows data collected over 3 seconds.

# ## Per-Thread Time

When active, per-thread time (PTT) accumulates the amount of time spent by each process within the system, as well as idle time and interrupt time. If you are processing on an Intel IA 32-bit system, you can use a performance event counter instead of using the real-time clock. For example, a measurement can be made that identifies the number of instructions executed by each process, the idle process, and the interrupts. The totals for process time, IRQ time, and idle time are provided for each processor in the system, as well as a system total of all processors.

PTT is activated via an API call, PTInit, or an external program called _pnt_. In both cases, you specify the measurement medium as system timer or performance counter. After it is activated, you can run a program called _prstats_ to display the current times for idle, process, and interrupt times. You can run the _prstats_ program any number of times. A terminate command stops the measurement. The last counts before the terminate command is issued remain stored in the buffers until another _init_ command is received. The following shows a sample PTT report:

```
```
Tools version 2040024
PTT_STATISTICS_SIZE = 263096
IBM_NR_CPUS = 16

Per Thread Time Summary

Total Dispatches:              3763
Total IRQs:                    334
Total Thread Time:             151469140
Total IRQ Time:                721564
Total Idle Time:               2158895609
Total tool time:               81755
Total Measurement:             2311086313
Total Period:                  0

Per Thread Time Detail

Details by CPU

                  IRQ         Dispatch
CPU     Count     Count       Times
--------------------------------------------------
    1       334      3763

Thread Time:                 151469140
IRQ Time:                    721564
Idle Time:                   2158895609
Tool Time:                   81755
Total Time:                  5311168068

Details by Process

             Dispatch      IRQ         Process
PID     Count       Count       Time
--------------------------------------------------
    0       703        303       2158895609
    1       5          0         34407
    2       83         0         139154
    3       1          0         7162
    7       15         0         168819
   11       5          0         3466
  324       1          0         6799
  409      11          0         30641
  671     1281        24        113156655
  722       3          0         30128
```
```