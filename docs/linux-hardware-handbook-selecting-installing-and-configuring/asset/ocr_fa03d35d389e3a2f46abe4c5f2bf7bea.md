The very latest of the Intel Pentium III line is called *Coppermine* (although it doesn’t use the copper trace technology invented by IBM and now used in PowerPC CPUs). Coppermine incorporates several advancements over previous Intel CPUs, such as a 133MHz motherboard bus, integration of the L2 cache into the main CPU wafer, and smaller circuitry. Aside from allowing higher motherboard bus speeds, these enhancements are largely invisible to you as a consumer, except that they produce a faster CPU. In fact, Intel chose not to release Coppermine under a new name; it’s still a Pentium III CPU.

# Advanced Non-Intel x86 CPUs

Through 1999, Intel’s competitors continued to use the Socket 7 design for CPU interface used in most Pentium CPUs. This meant that most competing CPUs used L2 caches on the motherboard rather than the CPU (the exception being AMD’s K6-III), and these CPUs were limited to the 32-bit, 4GB memory address space of Pentiums. In terms of speed, though, some of these CPUs compete with CPUs through mid-range Pentium-IIIs. CPUs in this range include

+   - **AMD K6** The K6 was based largely on designs developed by NexGen for the never-released Nx686. It includes MMX technology and approaches Pentium II speed when run at the same clock rate.

> **CAUTION**
> Some early K6 CPUs contained a bug that caused occasional unreliable operation. This bug isn’t Linux-specific, but for various reasons it manifested itself frequently when using the GCC compiler, and it could cause Linux kernel compiles to fail sporadically, among other problems. If you have an early K6 CPU, therefore, you might want to replace it rather than run Linux on it.

+   - **AMD K6-2 and K6-III** The K6-2 and K6-III are faster versions of the K6 CPU. They both run at faster clock rates and include changes to improve performance when the CPUs are run at the same clock rate.
+   - **Cyrrix MII** The MII is basically a 6x86 run at a higher clock rate. The MII also incorporates MMX instructions. I include the MII CPU here rather than in the Pentium section mainly because it can run at faster clock rates than Intel’s Pentium.
+   - **Transmeta Crusoe** Transmeta (<http://www.transmeta.com>) is the latest entrant in the x86 CPU sweepstakes. The Crusoe is distinguished by its low voltage requirements, which makes it well-suited for use in portable devices such as laptop and palmtop computers.