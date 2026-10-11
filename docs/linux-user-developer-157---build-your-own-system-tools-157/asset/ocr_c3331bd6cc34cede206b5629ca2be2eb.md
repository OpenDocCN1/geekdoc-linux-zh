# OpenSource

Your source of Linux news & views

# OPINION

# The kernel column

Jon Masters summarises the latest happenings in the Linux kernel community, including the release of the latest Linux 4.2 series kernel

![](bbox=[0.07, 0.35, 0.27, 0.53])

**Jon Masters**

is a Linux kernel hacker who has been working on Linux for some 19 years, since he first attended university at the age of 13. Jon lives in Cambridge, Massachusetts, and works for a large enterprise Linux vendor, where he is driving the creation of standards for energy efficient ARM-powered servers

> RCU is an extremely sophisticated and sometimes difficult to understand code, but it does bring many performance benefits to fast-path lookup code.

Linux 4.2 was released by Linus Torvalds, following a slightly longer cycle than usual (eight weeks, rather than the typical seven following the first RC or Release Candidate kernel). The new features in kernel 4.2 mostly concern internal optimisations and enhancements that are more or less transparent to the average end user. Examples include support for System Management Mode (SMM), emulation in KVM that effectively enables KVM-based virtual machines to implement Secure Boot (as used by some Linux and many new Windows systems). This is as well as a completely rewritten implementation of the floating-point context management code on x86 (the bit that preserves the floating-point unit state between task switches) that has "substantial regression risk" for user-visible problems to be discovered as end users hammer it hard with floating-point apps.

Linus noted in his 4.2 release announcement that his decision to wait an extra week might have been a little overkill, since "little happened this week" in terms of bug fixes, but he actually had good reason for being cautious. A race condition had been discovered in the Linux Virtual Filesystem (VFS) code's support for optimised directory lookups using a modern RCU (Read-Copy-Update mechanism). This means that under certain conditions, users would look up a directory path component (such as /usr/local/bin) and discover that the kernel was reporting "ENOTDIR" (not a directory) on a path component that clearly is a directory. This would then break various applications.

The cause of the problem turned out to be a flaw in the use of RCU within the "link_path_walk" filesystem path walking code. RCU is an extremely sophisticated and sometimes difficult to understand code, but it does bring many performance benefits to fast-path (lookup) code – such as that used in filesystem and network code to quickly walk through a linked list. In this case, it was realised that a dentry (an object representing a cached view of a Linux filesystem directory component) might be evicted from (in-kernel) memory cache (to free up memory needed elsewhere) just as a process (task) is checking to see if a given filesystem path component is itself a directory. In that case, the kernel could return ENOTDIR (not a directory) when in fact the path did represent a directory entry (and instead should use a slower path error handler to catch this situation).

This was a rare corner case that had been tickled by another unrelated change to dentry flag clearing code in recent kernels, but it had actually existed as a rare glitch in all kernels since Linux 3.12.

# Non-maskable interrupts (NMIs)

Modern x86 systems implement a feature known as non-maskable interrupts (NMIs). These are, as the name implies, interrupts that cannot be disabled by the operating system. Interrupts are electrical signals that are delivered to the central microprocessing unit(s) (by an interrupt controller (in Intel parlance, an IO-APIC) and they are used to indicate that an external device requires attention. Modern systems implement one interrupt signal into a generic interrupt-controller hardware device for each peripheral device; for example, the USB controller to which your keyboard is attached, even in a contemporary laptop. The controller then signals that it wishes to deliver an interrupt to the microprocessor by asserting a single electrical signal (pin) on the processor (in Intel parlance, to the LAPIC). That action typically causes the CPU to interrupt (hence the name) ongoing activity and very briefly switch into the Linux kernel code responsible for handling interrupt management.

Normal interrupts are maskable, meaning that the OS (eg Linux) can disable their delivery on a temporary basis. This is necessary because the code that manages interrupt delivery, known as an "interrupt handler", needs to preserve certain assumptions around atomicity and "re-entrancy". It is generally assumed by the kernel that for the brief period that an interrupt is recognised by the OS, another cannot be delivered simultaneously. But it will be marked as pending in the hardware and delivered immediately upon the current interrupt-handling activity indicating its completion. Sometimes, however, there is a need to deliver a critical notification to the operating system without any delay. Usually, this is as a result of an error or reliability concern that must be immediately handled.

NMIs are used to deliver such critical notices to the operating system; for example "the power has failed, all activity will stop in 50ms", which might be enough

16