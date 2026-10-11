at the end of their time slice, to let other processes have a chance at the processor. Similarly, processes that have been idle while waiting for I/O (such as an interactive text editor) are given a higher priority so that they can respond to the I/O when it happens. In short, the kernel makes sure that all processes, averaged over time, get their “fair share” of the CPU. Raising and lowering priorities are part of this process.

Designing a good process scheduler for the kernel is an art; the nitty-gritty details are beyond the scope of this book. However, a process can influence the kernel’s priority assignment algorithm by way of its *nice value*.

The *nice value* is an indication of “how nice” the process is willing to be toward other processes. Thus, higher *nice* values indicate increasingly more patient processes; that is, ones that are increasingly *nice* toward others, lowering their priority with respect to that of other processes.

A negative *nice* value, on the other hand, indicates that a process wishes to be “less nice” towards others. Such a process is more selfish, wanting more CPU time for itself.¹ Fortunately, while users can increase their *nice* value (be more nice), only *root* can decrease the *nice* value (be less nice).

The *nice* value is only one factor in the equation used by the kernel to compute the priority; the *nice* value is not the priority itself, which varies over time, based on the process’s behavior and the state of other processes in the system. To change the *nice* value, use the `nice()` system call:

```
```
#include <unistd.h>   XSI

int nice(int inc);
```
```

The default *nice* value is 0. The allowed range for *nice* values is –20 to 19. This takes some getting used to. The more negative the value, the higher the process’s priority: –20 is the highest priority (least *nice*), and 19 is the lowest priority (most *nice*).

The `inc` argument is the increment by which to change the *nice* value. Use ‘`nice(0)`’ to retrieve the current value without changing it. If the result of ‘`current_nice_value` + `inc`’ would be outside the range –20 to 19, the system forces the result to be inside the range.

> ¹ Such processes often display childlike behavior.