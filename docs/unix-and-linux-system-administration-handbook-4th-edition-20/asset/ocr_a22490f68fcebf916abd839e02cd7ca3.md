# Chapter 29 Performance Analysis

much CPU power, disk, or network bandwidth that other processes are affected. On occasion, malicious processes hog available resources to intentionally slow a system or network, a scheme known as a "denial of service" or DOS attack.

You can often tell which resource is being hogged without running a diagnostic command. If the system feels "sticky" or you hear the disk grinding, the problem is most likely a disk bandwidth or memory shortfall. If the system feels "sluggish" (everything takes a long time, and applications can't be "warmed up\ the problem may lie with the CPU load.

The first step in diagnosis is to run ps auxww (ps -el on Solaris and HP-UX) or top to look for obvious runaway processes. Any process that's using more than 50% of the CPU is likely to be fault. If no process is getting an innate share of the CPU, check to see how many processes are getting at least 10%. If snag more than two or three (count ps itself), the load average is likely to be quite high. This is, in itself, a cause of poor performance. Check the load average with vmstat and top to check whether the CPU is ever idle.

If no contention is evident, run vmstat to see how much paging is going on. All disk activity is interesting; a lot of page-outs may indicate contention for memory, and disk traffic in the absence of paging may mean that a process is monopolizing the disk by constantly reading or writing files.

There is no way to tie disk operations to processes, but ps can narrow down the suspects for you. Any process that is generating some amount of CPU time. You can usually make an educated guess which of the active processes is the true culprit. Use kill-STOP to suspend the process and test your theory.

Suppose you find that a particular process is at fault—what should you do? Usually, nothing. Some operations require a lot of resources and are bound to slow down the system. It doesn't necessarily mean that they're illegitimate. It is sometimes useful to renice an obtrusive process that is CPU-bound, however.

Sometimes, application tuning can dramatically reduce the demand for CPU resources; this effect is easily visible with custom network soft-ware such as web applications.

Processes that are disk or memory hogs can be dealt with so easily. renice does not help. You have the option of killing or stopping the process, but we recommend against it if this situation does not constitute an emergency. With CPU pigs, you can use the low-tech solution of asking the owner to run the process later.

+   5. If, it takes a long time to switch between applications, but performance is acceptable when an application is repeating a simple task.

+   6. A large virtual address or resident used is a suspicious sign, but shared libraries have made these processes less useful. ps is not very smart about separating system-wide shared library overhead from the address spaces of individual processes. Many processes appear to have tens of megabytes of active memory.