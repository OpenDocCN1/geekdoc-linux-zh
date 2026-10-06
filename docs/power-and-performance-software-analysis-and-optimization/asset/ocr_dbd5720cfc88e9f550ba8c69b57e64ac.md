# 1.3 Intel® 80286 and 80287

is, segmented addresses consisting of a segment selector and offset, and physical addresses, and for enforcing memory protection. Therefore, each process on the
system could be isolated in a separate address space.

# 1.3.1 PROTECTED AND REAL MODE

Because this represented a paradigm shift in the processor's programming model,
two models were split into two processor modes. The legacy mode, which
was utilized by the 8086 and 80186, was called Real-Address mode, or simply
real mode. The new MMU with memory protections was called Protected
Virtual-Address mode, or protected mode. To retain compatibility with legacy
applications for the 8086 and 80186, the processor booted into real mode, ensuring
that applications would use the 80286 as a faster and better 8086.
Applications that would take advantage of the features in the new model would
boot into real mode and then switch into protected mode. This technique, making
new software request features, a common problem in x86 for making disruptive
changes to the architecture while maintaining backwards compatibility.

Transitioning from real mode to protected mode is a fairly straightforward
process. The first step is to create and load all of the protected mode
structures, so that the protected environment operates immediately after the
switch. The PE in the first control register, CR0, is set, which effectively\enters protected mode. Finally, a jump instruction is performed to flush any processor
caches. At this point, the processor is now executing in protected mode and any new
functionality can be utilized. Once protected mode was entered, there was no method
of returning to real mode, without resetting the processor.

The 80286 introduced the concept of a privilege level, ranging from level 0, which
had the most, to level 3, which had the least. These privilege levels were
enforced by an MMU, which wouldn't permit a task operating at a lesser privilege
access to a memory region marked at a greater privilege level. Four levels were
provided in order to provide fine level of control for operating systems that desired it.
For example, an operating system's core functionality might run at level 0,
t kernel drivers at level 1, the user drivers at level 2, and user applications at
level 3. This privilege system is part of modern x86, although the Linux kernel only
 utilizes level 0, for kernel space, and level 1, for user space.

# 1.3.2 PROTECTED MODE SEGMENTATION

Support for these protected memory regions meant that the current segmentation
memory model had to be extended. Originally, segments had been fixed in size; how-
ever, that memory protection became more cumbersome, since the fixed sizes were too
large for fine grained task. In order to solve this, segments in protected mode
were now of variable size. All of these changes, combined with additional changes
designed to allow for the implementation of advanced features, as swapping-
simple wouldn't work within the confines of the existing segment register format.