code also falls in the realm of system programming. Whereas application programming requires users to be savvy in using language libraries, system programming requires a high degree of understanding of the computer hardware, assembly language, and a language like C.

In UNIX jargon, system programming uses the system call interface in order to access hardware resources such as the CPU, disk and files, main memory, and the status of processes and files. Such programs include, for instance, a shell, a language assembler or compiler, tools for providing information about a computer’s hardware resources including the usage of CPU, disk, and main memory; and programs that provide the status of software resources such as processes and files.

# 18.3 ENTRY POINTS INTO THE OS KERNEL

There are several reasons for control to transfer from a user process to the OS kernel. These reasons collectively fall into four categories, known as four entry points into the kernel, as shown in Figure 18.1. Because the purpose of these entry points is to invoke the relevant pieces of codes in the kernel to provide different services, they are also known as service points into the kernel.

Two of these entry points, trap and interrupt, are caused by computer hardware. An interrupt is a “signal” that a peripheral hardware device sends to the CPU in order to get its attention. For example, after a disk controller has finished reading a disk block (or cluster), it needs to inform the CPU about it. For this purpose, it generates an interrupt and the kernel takes over control in order to execute the code to service this interrupt, called the interrupt service routine (ISR) for this interrupt.

Whereas a peripheral device generates an interrupt, the CPU itself generates a trap in order to handle an exception in the code being executed. There are several reasons for the CPU to do so, including execution of an illegal instruction (instruction not in the instruction set of the CPU), a potential run-time error like a divide-by-zero situation, and an instruction trying to access a main memory area outside the process address space.

A signal in UNIX jargon is a mechanism that allows interruption of a process. In the computer science literature, it is also known as software interrupt. In Section 13.4, we discussed this topic in a fair amount of detail. However, the discussion was focused on shell-level handling of signals. Table 13.1 shows some of the commonly used signals and their

![](bbox=[0.3, 0.85, 0.75, 0.98])

FIGURE 18.1 Entry points into the operating system kernel.