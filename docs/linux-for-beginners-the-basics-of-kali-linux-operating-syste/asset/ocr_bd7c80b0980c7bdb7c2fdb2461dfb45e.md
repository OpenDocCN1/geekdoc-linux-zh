# ## Technology Expanded Memory (Mapped Memory)

In a number of operating systems, the displayed memory is the basic system mechanism on which other types of interprocess interaction and system decisions are based. Of course, the display memory used in conjunction with the file system interface, in this case, talking about *the files displayed in the memory* ( memory-mapped files ).

This technology is to ensure that a special system call (usually mmap () ) a part of the process address space uniquely floor containing the file. After that, an operation to write to such memory causes the contents of the displayed file to change, which immediately becomes available to all applications that have access to that file. Other applications can also display the same file in their address space and communicate with one another through it.

# ## Conclusions

+   * Streams of one interacting process have access to shared data hosted in the address space of that process. Any stream is able to change this data at any time and cause a state of competition when the outcome depends on the flow sequence.

+   * Flow synchronization mechanisms are used to ensure correct access to shared data; the main one is to ensure mutual exclusion when only one stream can access such data at a particular time. Blocking is used to organize mutual exclusion.

+   * Various synchronization primitives can be used to solve synchronization problems. The simplest primitives include semaphores, mutexes, conditional variables, read-write locks, and barriers.

+   * A higher-level mechanism is a monitor concept that combines mutexes and conditional variables and sets some rules for their interaction to protect shared data. Using