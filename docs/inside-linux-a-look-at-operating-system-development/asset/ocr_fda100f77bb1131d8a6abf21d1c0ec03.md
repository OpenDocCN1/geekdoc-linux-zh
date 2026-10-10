of physical memory and the “Boundary value” holds the size of that chunk. As the processor generates a “Logical address” (for instruction fetch, data storage, stack, etc.), the hardware simultaneously adds that address to the base address and compares it with the boundary value. If the logical address is positive and doesn’t violate the size limit, the physical address is used to access memory. If the logical address is negative or too large, the memory access is regarded as an error.

![](bbox=[0.28, 0.3, 0.72, 0.6])

Figure 4.15: Hardware memory mapping

With this hardware in place, the system and the program have different images of memory. With multiple programs running, the system must also change the base and bounds registers when it switches among the programs. As shown in Figure 4.16a, the system can see all of memory, but Figures 4.16b and 4.16c show the user programs only see the portion starting at the base address and the size given in the bounds register—and they see this memory as starting at location 0.

If you’ve noticed, the user program can no longer directly access the system kernel or run-time library. This is not a flaw because there exist special instructions which allow the execution to switch from code in a user program to code in the system kernel.