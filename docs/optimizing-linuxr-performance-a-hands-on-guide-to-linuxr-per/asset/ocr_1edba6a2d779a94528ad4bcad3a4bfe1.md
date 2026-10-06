# 4.1. Process Performance Statistics

The tools to analyze the performance of applications are varied and have existed in one form or another the early days of Unix. It is critical to understand how an application is interacting with the operating system, CPU, and memory system to understand its performance. Most applications are not self-contained and make many calls to the Linux kernel and different libraries. Calls to the Linux kernel (or system calls) may be as simple as "my PID" or as complex as "read 12 blocks of data from the disk." Different systems will have different performance implications. Consequently, the library calls may be as simple as memory allocation or as complex as graphics creation.

# 4.1.1. Kernel Time Versus User Time

The most basic split of where an application spend its time is between kernel and user time. Kernel time is the amount of time spent in application or library code. Linux has tools such time and ps that enable (appropriately) whether an application is spending its time in application or kernel code. It also has commands such as profile and strace that enable you to trace which kernel calls are made on the behalf of the process, as well as how long those calls took to complete.

# 4.1.2. Library Time Versus Application Time

Any application with even a minor amount of complexity relies on system libraries to perform complex actions. These libraries may cause performance problems, so it is important to be able to see how much an application spends in a particular library. Although it might not always be practical to modify the source code of libraries directly to fix a problem, it may be possible to change the application code to call different or fewer library functions. The ltrace command and profile suite provide a way to analyze the performance of libraries when they are used by applications. Tools built in to the Linux loader, id, help you determine the use of many libraries slows down an application's start time.

# 4.1.3. Subdividing Application Time

When the application is known to be the bottleneck, Linux provides tools that enable you to profile an application to figure out where time is spent within an application. Tools such as gprof and profile can generate profiles of an application exactly which source line is causing large amounts of time to be spent.