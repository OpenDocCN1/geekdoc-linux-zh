# 4.4.1 Non-Mapped

Main memory is partitioned according to its use, such as for buffers, system kernel code, or user program. Programs are always loaded into a well-known location⁵ and they can access all of memory. Figure 4.12a shows how memory is split into various elements.

![](bbox=[0.13, 0.29, 0.89, 0.68])

Figure 4.12: Non-mapped memory

While this system is easy to implement, it has disadvantages—foremost are the difficulties in running multiple programs simultaneously. But if there is enough contiguous memory, a second, third,

> ⁵ This location need not be known to the program because the loader may relocate all addresses in the program as the program is loaded. The format of the relocatable executable program is more complicated because it must contain pointers to all the places which must be relocated.