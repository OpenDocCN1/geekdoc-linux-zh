
## 5.2.3 Memory bottlenecks

To further investigate the problem, it is necessary to find which process is consuming the CPU. In case of Linux, this could be a user process or a kernel thread. Figure 5-16 summarizes the action points in each case.

![](img/f332344337ca8bf6846cb313a66ee0b3_195_0.png)

Figure 5-16 Flow of problem determination - investigate what consumes CPU

kswapd is a Linux kernel thread that acquires pages when the free memory decreases. So, a high CPU utilization by kswapd means that there is memory shortage and CPU is getting consumed because of that.

kjournald is a Linux kernel thread that commits the transaction of file systems using a journal such as the ext3 file system. High CPU utilization by kjournald indicates that a lot of CPU is being consumed for file system transaction commit to the journal area due to lot of disk I/O.

pdflush is a kernel thread that writes dirty page cache to the disk. High CPU utilization by pdflush indicates that there is lot of disk I/O since it is actually writing dirty page caches to the disk very often.

When software IRQ load on the Linux system increases, the ksoftirqd kernel thread is executed. This is done on a per-CPU basis. So, if the ksoftirqd is taking more than a tiny percentage of CPU time, it means that the system is under heavy software interrupt load. This can happen because of very high disk I/O, heavy network traffic, and so on.

What happens if we do not find a specific process using a lot of CPU but the individual CPU utilization is reported as high? There is still a chance that the CPU is really getting utilized. The time taken by the CPU to perform the context switch is considered as the system time. This is the system overhead since it is not used by any process directly. An increase in this time means that more and more CPU is used for context switch. Other tasks that are considered as overhead are swap processing and a large amount of I/O. As summarized in Figure 5-17, the number of context switches, and swapping, large I/O are the reasons behind the increase in system overhead and hence high CPU utilization.

![](img/f332344337ca8bf6846cb313a66ee0b3_196_0.png)

Figure 5-17 Problem determination flow - investigate system overhead

In case of z/VM the ratio of user time to emulation time or the service time (called as the T/V ratio) is a measurement that shows whether the user can efficiently use the resource. Similarly, the capture ratio is a measurement that shows whether the system can efficiently use the resource. The capture ratio is the ratio of user time to (system time + user time). This is illustrated in Figure 5-18.

![](img/f332344337ca8bf6846cb313a66ee0b3_197_0.png)

Figure 5-18 VM overhead check

Linux executes each process in a virtual address space. The translation from the virtual address to the real address is executed as a page based on the page translation table. The page size is fixed at 4 KB. This is illustrated in Figure 5-19. The virtual memory is a logical layer between the application memory requests and the physical memory.

![](img/f332344337ca8bf6846cb313a66ee0b3_198_0.png)

Figure 5-19 Linux memory management

When the main memory is not enough for the system to execute processes, the system will try to move some data from the main memory to the disk. This process is called swapping or paging. Swapping occurs when the system needs more memory that is available. But swapping has the downside of slowing down the system since the disk is a slow device compared to the main memory. So, accessing the disk for swapping will slow down the system.

When the swapped-out pages are to be accessed, they are swapped-in to the memory again. Figure 5-20 illustrates swapping.

![](img/f332344337ca8bf6846cb313a66ee0b3_199_0.png)

Figure 5-20 Swapping

In case of z/VM, there is a main storage area where the processes are executed. There is an expanded storage that is used for paging. DASD space is also used for paging. This is illustrated in Figure 5-21. The CS in the figure indicates main storage and the ES indicates expanded storage.

![](img/f332344337ca8bf6846cb313a66ee0b3_200_0.png)

Figure 5-21 z/VM paging mechanism

Figure 5-22 on page 186 shows the memory bottleneck problem determination flow. As usual, first we start by examining the current configuration. Depending on the configuration, how much memory assigned as main storage, how much as expanded storage, virtual memory setting for each guest (z/VM), shared memory settings for middleware, and so on, are examined. When the same memory space is shared with multiple processes, then it is called as the shared memory area. Under Linux, this is typically used with middleware such as DB2®, Oracle, and so on. It is possible to control whether the shared memory should be swapped. The area in the memory where the data necessary for application execution is stored is called the JVM™ heap in the case of Java. Memory utilization of JVM cannot be viewed from the operating system and should be viewed from the JVM side.

- Confirm the configuration
- Confirm whether swapping occurs or not
- Investigate memory utilization

![](img/f332344337ca8bf6846cb313a66ee0b3_201_0.png)

Figure 5-22 Memory bottleneck problem determination flow

The next step is to check whether swapping occurs. Figure 5-23 summarizes this.

![](img/f332344337ca8bf6846cb313a66ee0b3_202_0.png)

Figure 5-23 Problem determination flow - check for swapping

Figure 5-24 illustrates how to check whether swapping occurs from the Linux side by using the free command.

![](img/f332344337ca8bf6846cb313a66ee0b3_202_1.png)

Figure 5-24 Confirming swapping by using free

Figure 5-25 illustrates how to check the paging activity from z/VM using the Performance Toolkit. Paging happens if there is a guest that gives overhead in the >2GB> memory area, when pages are migrated between the expanded and the main memory (X>MS and MS>X), and when pages are migrated between the expanded memory area and the disk storage area (X>DS). Large values for the Working Set Size (WSS) also cause paging.

![](img/f332344337ca8bf6846cb313a66ee0b3_203_0.png)

Figure 5-25 Confirming swapping by using z/VM Performance Toolkit

The next step is investigating where the memory is getting consumed. As shown in Figure 5-26, the memory may be getting consumed by a user process, shared memory areas, JVM heaps, file system cache, and so on. As discussed earlier in this chapter, it is not sufficient if we have only one snapshot of the memory utilization. We need such snapshots generated at regular intervals to understand the nature of the problem.

![](img/f332344337ca8bf6846cb313a66ee0b3_204_0.png)

Figure 5-26 Problem determination flow - investigating the memory utilization

Figure 5-27 shows a sample top output with the output data related to memory explained.

![](img/f332344337ca8bf6846cb313a66ee0b3_205_0.png)

Figure 5-27 Checking memory utilization by using top

Figure 5-28 shows a sample ipcs output illustrating how to check the shared memory usage.

![](img/f332344337ca8bf6846cb313a66ee0b3_205_1.png)

Figure 5-28 Checking memory utilization by using ipcs

Linux uses the free memory as the file system cache. So, it is normal to find that Linux does not have any free memory if it is running for a long period of time. Such a cache gets released when a processes is executed.

Figure 5-29 shows a sample output z/VM Performance Toolkit indicating general storage utilization. The output indicates the utilization of the usable area for paging in the main storage, the number of pages under the 2 GB memory area, and the utilization of the expanded storage, in addition to many other details. If the number of pages under the 2 GB memory area is above 1000, then it should be investigated.

![](img/f332344337ca8bf6846cb313a66ee0b3_206_0.png)

Figure 5-29 Confirming memory utilization by using z/VM Performance Toolkit
