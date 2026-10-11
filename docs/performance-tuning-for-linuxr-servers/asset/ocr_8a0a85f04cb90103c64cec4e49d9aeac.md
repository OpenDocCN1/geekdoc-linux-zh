```
LAB TKS %% NAMES

PID 19094 75.22 SystemProcess_0000
TID 19094 75.22 tid_0000
MOD 19094 75.22 vmlinux
SYM 19094 75.22 default_idle

PID 6284 24.76 /space/piperf/bin/WatchedPot_057c
TID 6284 24.76 tid_057c
MOD 6284 24.76 /space/piperf/bin/WatchedPot
SYM 3154 12.43 ThirtyTwo
SYM 1615 6.36 Sixteen
SYM 808 3.18 Eight
SYM 404 1.59 Four
SYM 202 0.80 Two
SYM 101 0.40 One

==================================================
)) Module
==================================================

LAB TKS %% NAMES

MOD 19096 75.23 vmlinux
MOD 6284 24.76 /space/piperf/bin/WatchedPot

==================================================
)) Module_Symbol
==================================================

LAB TKS %% NAMES

MOD 19096 75.23 vmlinux
SYM 19094 75.22 default_idle

MOD 6284 24.76 /space/piperf/bin/WatchedPot
SYM 3154 12.43 ThirtyTwo
SYM 1615 6.36 Sixteen
SYM 808 3.18 Eight
SYM 404 1.59 Four
SYM 202 0.80 Two
SYM 101 0.40 One
```

When profiling applications, the level of optimization used when the application is compiling can have an effect on the trace output. With optimization on, functions that execute the same base code are all rolled up into the application instead of reported on separately by symbol name. Therefore, it is a good idea to make the first few profiling runs on applications that have not been compiled with optimization turned on.

# # Instruction Tracing

A special version of trace profiling that sets up the system to use the hardware’s instruction trace capabilities is available on Intel IA32 systems. Instruction tracing starts from the branch instruction signal and then creates trace records every time a code branch, jump, or call is performed. Instruction profiling provides a detailed trace of the execution path in the system without the need to have a debugger installed or code compiled with the debug option enabled.

Use instruction tracing only for very short, controlled measurement periods, because it can produce a significant number of tracing records. Instruction tracing is primarily useful for determining the exact execution path through the entire system for the function being executed.

A small command file, *run.itrace*, is provided to simplify the taking of an instruction trace profile.

The following example shows a small output of *run.itrace*.