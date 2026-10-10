# Checking Kernel Messages

When Linux boots, it displays a large number of messages about the hardware it finds. These messages scroll by so quickly that you're unlikely to be able to read them; however, you can review them by typing dmesg \| less or print them by typing dmesg \| lp. The dmesg command displays the contents of the kernel ring buffer, where kernel messages are stored. This buffer is of limited size, and as the system continues to operate, the kernel is likely to place additional messages in this buffer. Thus, your original kernel messages may scroll out of the buffer in time. Some distributions store a copy of the kernel ring buffer as it existed when the computer first booted in a log file, such as /var/log/dmesg.

You should review your kernel ring buffer to familiarize yourself with the messages it contains. You needn't study every detail, but try to spot information on important subsystems, such as your hard disk, so that you know what types of messages to expect from a working system. In the event of hardware problems, the kernel ring buffer can be an invaluable resource. You might find that hardware isn't detected (no mention of it appears in the ring buffer), or you might spot error messages relating to the hardware in the ring buffer.

# Criteria for Completion

To complete this task, you should create a disk file or set of printouts that includes information on several hardware features:

+   * Used IRQs
+   * Used I/O addresses
+   * Used DMA channels
+   * Low-level hard disk information (for PATA disks)
+   * Disk formatting information
+   * PCI summary information
+   * USB summary information

You should also review your kernel ring buffer messages and be familiar with the basic format of these messages.

# Task 2.3: Resolve Hardware Conflicts

With Tasks 2.1 and 2.2 completed, you now have the knowledge required to identify certain types of hardware conflicts— for instance, if two devices are attempting to use a single interrupt, thus causing problems. What remains is to do something about such conflicts. Several possibilities exist: You can disable one of the offending devices, you can set jumpers on older plug-in cards to change resource use, you can adjust BIOS settings to avoid the conflict, or you can adjust Linux settings to avoid the conflict.