
## Tuning the System

won't need many of these drivers. For example, most installations don't need the support that's included for capabilities like Symmetric Multi-Processing (SMP) or Integrated Services Digital Network (ISDN). These "extras" use up memory, impairing system performance. As soon as possible after installation, you should recompile the kernel, leaving out drivers for hardware you don't have and eliminating functionality you won't use.

Another reason for recompiling is the fact that recent kernels allow for optimization based on the processor, but most distributions ship with kernels optimized for 386 systems. A kernel developed for a 386 machine will run slower on a more capable machine than will code compiled for that machine's processor. If the kernel must be portable among a variety of machines, you'll have to compile to the lowest machine's processor type, but other than that, you should select the appropriate processor type for the computer the kernel is to be on.

The number of processor optimization options is growing. Back in kernel 2.2.5, there were five optimization schemes which to choose. Table 9.1 lists the optimization schemes available in the 2.2.17 kernel, and Table 9.2 lists the 2.4.0-test9 kernel's optimization options. (It's possible to apply kernel patches to 2.2.x kernels to increase the number of optimizations they offer, but the effort isn't normally worthwhile.)

## Table 9.1 Optimization Schemes in the 2.2.17 Kernel

| Optimization Scheme | Processors |
|---|--|
| 386 | AMD/Cyrix/Intel 386DX/DX/SL/SLC/SX, Cyrix/TI 486DLC/DLC2 and UMC 486SX-S |
| 486 | AMD/Cyrix/IBM/Intel DX4 or DX2/SL/SX/SX2, AMD/Cyrix 5x86, NexGen Nx586, and UMC U5D or U5S |
| 586/K5/5x86/6x86 | Generic Pentium-class CPUs, possibly lacking the TSC (time stamp counter) register |
| Pentium/K6/TSC | Intel Pentium/Pentium MMX, AMD K6 and K6-3D |
| Ppro | Intel Pentium II/Pentium Pro, Cyrix/IBM/National-conductor 6x86MX and MII |

![](img/4fb617eb648f87def380ef5d92052d01_320_0.png)

## Chapter 9 Performance Tuning

## Table 9.2 Optimization Schemes in the 2.4.0-test9 Kernel

| Optimization Scheme | Processors |
|---|--|
| 386 | All Intel, AMD, and Cyrix 386 CPUs, as well as the Cyrix 486DLC series and NexGen Nx586 |
| 486 | All Intel, AMD, and Cyrix 486 CPUs, as well as the UMC U5D and U5S |
| 586/K5/x5x86/x86/x86MX | Generic Pentium-class CPUs, possibly lacking the TSC register |
| Pentium-Classic | Original Intel Pentium |
| Pentium-MMX | Intel Pentium MMX |
| Pentium-Pro/Celeron/Pentium-II | Intel Pentium Pro, Celeron, and Pentium-II |
| Pentium-III | Intel Pentium-III |
| K6/K6-II/K6-III | AMD K6, K6-2, and K6-III |
| Athlon/K7 | AMD Athlon (K7), including the Duron |
| Crusoe | Transmeta Crusoe series |
| Winchip-C6 | Original IDT Winchip |
| Winchip-2 | IDT Winchip 2 |
| Winchip-2A/Winchip-3 | IDT Winchip with 3dNow capability |

Additionally, the amount of memory is a factor when compiling a new kernel. If your system is blessed with more than a gigabyte of memory, you'll need to turn on Big Memory Support. You do this by selecting 2GB Maximum Physical Memory (instead of the default 1GB) when prompted.

There are many other kernel parameters that might give you a performance. If your system is blessed with more than a gigabyte of memory, you'll need to turn on Big Memory Support. You do this by selecting 2GB Maximum Physical Memory (instead of the default 1GB) when prompted.

There are many other kernel parameters that might give you a performance. If your system is blessed with more than a gigabyte of memory, you'll need to turn on Big Memory Support. You do this by selecting 2GB Maximum Physical Memory (instead of the default 1GB) when prompted.

## Optimizing Applications

Just as the kernel can be recompiled, you can also optimize applications. If you download a tarball, read the README to see if there are any-specific. Chapter 8 covers other options.

## Tuning the X System

Another performance issue involves the startup process, which although Windows, is much slower than it should. What could make it faster? If you watch the output of startx command, you'll see many lines like this:

- SVGA: Removing (640x400)

This line represents a video mode that was looked at and determined not to fall within the capabilities of your video card/monitor. The The line will look like this:

```

Modeline "640x400" 31.50 640 672 736 832 400 401 445 -hsync -vsync

```

Simply comment it by placing a # symbol in front of the word Modeline. The next time X is started, these modes won't be attempted, saving you a little time for each mode. We will not improve performance once X is running.

## Window Managers and Integrated Environments

Window managers and integrated environments (IDEs) can free up memory. Some of these are-specific. We will talk about the in Chapter 16.

## Upgrading

“When should I upgrade my operating system?” is a question that plagues many system administrators. Do you upgrade simply because a newer version has come out? Do you upgrade individual packages whenever there is a bug fix? Do you reinstall from scratch or perform the distribution's upgrade?

It's best to back up the system, reinstall, and dump configuration files and users over the new system. This may cause you some trepidation at first, since you won't be sure that you remembered to put all the configuration data back; you may think you will overlook something. If you use the installation process's upgrade facility, you'll probably never have a problem with it.

You should not blindly upgrade or reinstall a working, configured system just because a new version of the operating system has come out. The distribution's Web will contain detailed information about what prompted the new version and what has been upgraded. Read those notes and a cost-benefit analysis! Is the gain worth the time? Are there risks if you don't upgrade? Perform an upgrade if the new version offers several significant security fixes or a major change in
