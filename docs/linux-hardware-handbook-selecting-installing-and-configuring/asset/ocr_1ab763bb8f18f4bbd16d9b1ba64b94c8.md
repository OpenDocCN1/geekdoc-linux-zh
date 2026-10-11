multiuser usage patterns, however, and it’s not clear that this rule of thumb is as useful when applied to single-user Linux computers. Many desktop Linux users have swap space equal to or even less than the amount of physical RAM and seem quite happy with this configuration. In the end, an appropriate amount of swap space depends on how you use the computer; if you regularly, or even just occasionally, run enough programs to substantially exceed the RAM available on your computer, a large amount of swap space is beneficial. If you have enough RAM that its limits are seldom stressed, however, you might need little or no swap space.

The free command’s listing of used RAM includes RAM used by Linux as disk cache—hard disk contents stored in RAM to improve disk access speed. Disk cache is the opposite of swap, and balancing swap and disk cache is a tricky art practiced by kernel programmers; you need not concern yourself with it. You should be aware, however, that your programs actually consume far less RAM than you might think from looking at the first line of free’s output. For this reason, free also reports the amount of RAM used excluding disk caches, on the -/+ buffers/cache line. Use this value, rather than the Mem value, when estimating how much RAM your programs consume.

# Memory Module Types

RAM is built from silicon wafers, just as CPUs and other computer chips are. The silicon wafers, however, are quite delicate. In order to safely handle and transport RAM, it’s necessary to embed the silicon wafers inside a plastic or ceramic package. This package is what we typically think of as a computer chip (see Figure 3.1).

![](bbox=[0.2, 0.59, 0.74, 0.77])

FIGURE 3.1  
A typical memory chip uses a number of metallic pins to interface the silicon wafer within the package to a motherboard or other device.

Early x86 PCs generally included RAM chips soldered directly onto the motherboard, or placed in individual sockets. This approach consumed a great deal of space on the motherboard, however, and made it difficult to upgrade memory or replace defective memory.