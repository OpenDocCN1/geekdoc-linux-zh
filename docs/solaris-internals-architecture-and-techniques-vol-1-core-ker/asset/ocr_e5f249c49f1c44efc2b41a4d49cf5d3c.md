# 106

# Kernel Bootstrap and Initialization

+   * /platform/<arch>/kernel/unix — The platform-dependent component of the core kernel.
* /platform/sun4u/kernel/genunix — A genunix binary optimized for UltraSPARC, but independent of the system (box) type. Only Ultra-SPARC-based systems load this particular binary.
* /kernel/genunix — Platform-independent (generic) core kernel code. Only non-UltraSPARC-based systems load this file.

Note that only one genunix binary gets loaded at boot time: either the UltraSPARC version on sun4u hardware or the /kernel/genunix image on all other SPARC systems. These objects contain all the low-level kernel services and other facilities that need to be memory resident to initialize the system and support the dynamic load environment.

Included within the unix and genunix images are the memory management routines, callback andout facilities, clock and timer support, kernel memory allocator, module facility, the kernel runtime linker, synchronization primitives, thread and lightweight process code, and device driver interfaces.

The remaining bits load as modules from the directories described in Table 4-1 on page 104. For a listing of the modules currently running in a system, use the modinfo(1M) command.

```
# id Loadaddr Size Info Ref Module Name
| 4 f5b28000 3b30 1 specs (filesystem for specs)
| 6 f5b2b3b0 2bc0b 1 TS (time sharing sched class)
| 7 f52b2e6f8 4a4 1 DTSPTL (Time sharing dispatch table)
| 8 f5ce0e00 31a8 1 ufs (filesystem for ufs)
| 11 f5d3c9d8 3b30 1 root (unix root nexus)
| 33 f5b4c90 6d2 1 dma (Direct Memory Access driver)
| 14 f5b4e6f0 aeb 59 1 aft (Administrative driver services)
| 16 f5f6a7e8 31a8 1 lelf (exec module for elf)
| 44 f5bc2d58 012f 1 sfsock (filesystem for sockets)
| 57 f57eb3b0 b4b0 8 1 doors (doors)
| 63 f5bd7d7a0 3586 201 fdfs (filesystem for fd)
| 64 c5f2f1d8 31a8 1 dev (OPNRUM/NVAR driver)
| 65 f9f18100 f0b8 1 openpepr (OPNRUM)
| 72 f52db8f68 6c6 90 katat (kernel statistics driver)
| 73 f76c000f d1ef 11 tmps (filesystem for tmps)
| 92 f5b2f4a0 1cc0 1 shmfs (system shared memory)
| 92 f5defa40 268 1 ipc (common ipc code)
| 93 f5b25cac0 1512 1 le (Lance Ethernet Driver v1.120)
| 106 f61a9900 587a 40 1 mod
| 107 f5ffaaa8 4dl 7 lema (le dm driver)
```

The sample output is a partial listing from running Solaris 7 system. modinfo(1M) provides the name of the kernel object and a brief description. Each kernel module has a unique identifier, shown in the Id column. The kernel virtual address (Loadaddr) and size of the module are also displayed, with module-specific data in the Info column.