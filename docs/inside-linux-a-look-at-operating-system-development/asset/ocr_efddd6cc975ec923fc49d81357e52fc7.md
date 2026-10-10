frames. If there is insufficient physical memory, Linux uses space on disk to hold copies of the pages which are moved into and out of memory as needed. This virtual memory is discussed further in Section 4.4.4.

# ### Other uses for Physical Memory

An outstanding feature of Linux is that it puts all physical memory, except that used to hold the kernel code, into a common pool. Memory is taken from this pool to provide frames for the virtual memory system and buffer blocks for disk caching.

The results can be surprising to the uninitiated: when compiling a large program (such as the kernel) on a memory-rich system, one will find the disk rarely operates for the second and successive iterations. This is because all the disk data have been cached in memory. The system can just copy data between the cache buffer block and the user program instead of performing disk I/O.

# ### 1.2.8 Linux Is an Open System

This term requires some explanation because there are several meanings of open system. The first (and formal) sense is that a system conforms to published standards. This is intended to ensure that programs written to those standards can be ported to other open systems. The second (and often implied) sense is that there are no hidden elements. Some systems fail to meet this second meaning because, although they provide all the features of a standard, they provide some additional features which can only be exploited by the knowledgeable. Linux comes closer to meeting the POSIX[3] standards than any other operating system, and if there’s any doubt, all the source code is available for inspection by any interested party. These standards are discussed further in Section 5.1.1.

# ### 1.2.9 Linux Has a Large Development Toolset

Unix has been under development for over twenty-five years. During most of this time, it has been used by its developers for further development. This has led to Unix being the best tool for developing Unix.