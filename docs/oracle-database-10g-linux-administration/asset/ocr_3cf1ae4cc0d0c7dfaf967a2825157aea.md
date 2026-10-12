# CPU

The CPU and its cache(s) are the fastest components of the system. The cache(s) are one or more pieces of very high-speed memory, usually located on the same chip as the CPU, that are used to store recently used data and instructions so that they can provide quick access if this data is used again in a short time. Most modern CPU hardware designs actually take advantage of a cache built into the CPU core. This internal cache is known as a Level 1 (or L1) cache. Typically, an L1 cache is very small, on the order of 8 to 16 kilobytes in size, and is accessible in a few nanoseconds.

When a certain piece of data is wanted, the hardware first looks in the L1 cache. If the data is there, the hardware processes that data immediately. If the data is not available in the L1 cache, the hardware looks in the L2 cache, which is external to the CPU core but resides on the same chip in order to maximize performance. The L2 cache is connected to the CPU chip(s) on the same side of the memory bus as the CPU. To get to main memory, you need to use the memory bus, thereby reducing the speed of the memory access. Although the L2 cache is typically much slower than the L1 cache, it is usually much larger. Its larger size provides a better chance of getting a “cache hit.” Typical L2 caches range from 128K to 4M in size and are accessible in hundredths of nanoseconds.

Slower yet is the speed of the main memory. It is characteristically much slower than the L2 cache, on the order of 2–10 microseconds (roughly 1000 times slower than the L1 cache). The size of system memory can vary widely: 32-bit CPUs are limited to 4GB of directly addressed memory (they can address more through a multiphase operation), while 64-bit CPUs can directly address terabytes of memory directly. A comparison of component speeds is shown in Figure 15-1.

![](bbox=[0.15, 0.64, 0.75, 0.84])

**FIGURE 15-1.** *Component speed comparison*