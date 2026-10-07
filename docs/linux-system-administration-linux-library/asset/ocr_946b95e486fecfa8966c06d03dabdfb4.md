# Tuning the System 293

won't need many of these drivers. For example, most installations don't need the support that's included for capabilities like Symmetric Multi-Processing (SMP) or Integrated Services Digital Network (ISDN). These "extras" use up memory, impairing system performance. As soon as possible after installation, you should recompile the kernel, leaving out drivers for hardware you don't have and eliminating functionality you won't use.

Another reason for recompiling is the fact that recent kernels allow for optimization based on the processor, but most distributions ship with kernels optimized for 386 systems. A kernel developed for a 386 machine will run slower on a more capable machine than will code compiled for that machine's processor. If the kernel must be portable among a variety of machines, you'll have to compile to the lowest machine's processor type, but other than that, you should select the appropriate processor type for the computer the kernel is to be on.

The number of processor optimization options is growing. Back in kernel 2.2.5, there were five optimization schemes which to choose. Table 9.1 lists the optimization schemes available in the 2.2.17 kernel, and Table 9.2 lists the 2.4.0-test9 kernel's optimization options. (It's possible to apply kernel patches to 2.2.x kernels to increase the number of optimizations they offer, but the effort isn't normally worthwhile.)

# Table 9.1 Optimization Schemes in the 2.2.17 Kernel

| Optimization Scheme | Processors |
|---|--|
| 386 | AMD/Cyrix/Intel 386DX/DX/SL/SLC/SX, Cyrix/TI 486DLC/DLC2 and UMC 486SX-S |
| 486 | AMD/Cyrix/IBM/Intel DX4 or DX2/SL/SX/SX2, AMD/Cyrix 5x86, NexGen Nx586, and UMC U5D or U5S |
| 586/K5/5x86/6x86 | Generic Pentium-class CPUs, possibly lacking the TSC (time stamp counter) register |
| Pentium/K6/TSC | Intel Pentium/Pentium MMX, AMD K6 and K6-3D |
| Ppro | Intel Pentium II/Pentium Pro, Cyrix/IBM/National-conductor 6x86MX and MII |

![](bbox=[0.893, 0.563, 0.977, 0.635])