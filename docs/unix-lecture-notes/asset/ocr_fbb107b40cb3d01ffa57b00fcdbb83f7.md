from them. In particular, the program will display the addresses of various local and global symbols in hexadecimal and decimal notation. These locations are clues to how the process is laid out in its logical address space.

![](bbox=[0.22, 0.28, 0.78, 0.78])

Figure 7.1: Typical layout of a process in virtual memory.

# 7.6.1 Overview

To start, we look at the big picture of what a process looks like in its logical address space. This picture should enable you to construct a mental image of the physical layout of a process in its own logical address space, how it looks in a file, and how that file relates to the virtual memory image of the process. Different UNIX systems use different layouts for processes, but for the most part, most modern systems adhere to a format known as the Executable and Linkable Format (ELF).

The resources needed by a process executing in user mode include the CPU state (general purpose