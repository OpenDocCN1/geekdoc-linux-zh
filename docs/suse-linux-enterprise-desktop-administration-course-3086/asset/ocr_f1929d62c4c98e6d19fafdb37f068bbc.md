+   - Objective 4—Perform Tasks as a Different User
+   - Objective 5—Use Encrypted File Systems

# Objective 1—Understand the Multiuser Environment

One of the goals of UNIX was to enable a number of users to use the system simultaneously (multiuser capability).

Because several users might also want to use several different programs simultaneously, mechanisms must be available to allow these programs to run simultaneously (multitasking capability).

The implementation of a multiuser and multitasking system only appears to be simultaneous in a single processor system. Real multitasking is only possible in a multiprocessor system.

Even in a single-processor system, advantages can be gained through multitasking because waiting times for input or output from processes can be used for other processes.

UNIX implements preemptive multitasking—each process is allowed a certain amount of time during which it can work. When this time has expired, the operating system temporarily stops the execution of one process and executes another process that is waiting to run.

Other operating systems (such as versions older than the MAC OS version X) do not enforce this sharing of processing time. Instead, control over the processor must be released by the running process before another process can run.

This can lead to one process hijacking the processor, leaving other processes without processing time and blocking the system.

The operating system coordinates access to the resources (such as hard drives, tapes, or interfaces) available in the system. If there is competition among processes, only one process can be granted access. The others must be rejected.

This coordination task is very complex and no operating system is able to implement an ideal solution. The classic problem involves a situation in which two or more processes need the same resources exclusively, as illustrated in the resource conflict shown in Figure 9-1.

![](bbox=[0.105, 0.682, 0.407, 0.88])