# post

post produces various reports based on the trace profiling data. When a trace profiling report is produced, it is written to a file called tprof.out. When you install the Performance Inspector, you identify the directory where this file will be saved. If you want to keep the current tprof.out file, you must rename it something else before running another run.tprof command.

One option supported by the post command is -show. -show Creates a file called post.show, which is a dump in a readable format of all the trace records. When all the trace hooks are enabled, post.show gives a detailed look at the sequence of events that occurred in the system, from execs to dispatches to interrupts.

# pipcntr

pipcntr controls and displays the performance counters when PI is running on Intel IA32 platforms. This program can start and stop counters and display the contents of the counter registers and the counter control register settings. You can use this utility to start a performance counter and then run the per-thread time utility using this counter. The same holds true for the trace profiling function.

# ptt

ptt starts and stops the per-thread time measurement. When starting, you can also specify what metric to use to perform the measurement.

# pttstats

pttstats displays the per-thread time of every process in the system. On Intel IA32 systems, the measurement metric can be either the real-time clock or a performance monitor counter.