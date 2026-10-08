# Chapter 5. The proc File System

Much of the information here is used by the free, top, and ps commands. In fact, the output of the free command is even similar in appearance to the contents and structure of /proc/meminfo. But by looking directly at /proc/meminfo, more details are revealed:

+   - Mem — The current state of physical RAM in the system, including a full breakdown of used, free, shared, and cached memory utilization in bytes.
- Swap — The total, used, and free amount of swap space, in bytes.
- MemTotal — Total amount of physical RAM, in kilobytes.
- MemFree — The amount of physical RAM, in kilobytes, left unused by the system.
- MemShared — Unused with 2.4 and higher kernels but left in compatibility with earlier kernel versions.
- Buffers — The amount of physical RAM, in kilobytes, used for buffers.
- Cached — The amount of physical RAM, in kilobytes, used as cache memory.
- Active — The total amount of buffer or cache pages, in kilobytes, that is active in use.
- Inact_dirty — The total amount of buffer or cache pages, in kilobytes, that may be free and available.
- Inact_clean — The total amount of buffer or cache pages, in kilobytes, that are free and available.
- Inact_target — The net amount of allocations per second, in kilobytes, averaged over one minute.
- HighTotal and HighFree — The free amount of memory, in kilobytes, that is not directly mapped into kernel space. The HighTotal value can vary based on the type of kernel used.
- LowTotal and LowFree — The free amount of memory, in kilobytes, that is directly mapped into kernel space. The LowTotal value can vary based on the type of kernel used.
- SwapTotal — The total amount of swap available, in kilobytes.
- SwapFree — The amount of swap free, in kilobytes.

# 5.2.10. /proc/misc

This file lists miscellaneous drivers registered on the miscellaneous major device, which is device number 10:

```
135 rtc
1 psaux
134 apm_bios
```

The first column is the minor number of each device, while the second column shows the driver in use.

# 5.2.11. /proc/modules

This file displays a list of all modules loaded into the kernel. Its contents will vary based on the configuration and use of your system, it should be organized in a similar manner to this sample /proc/modules file output:

```
ide-cd 27008 0 (autoclean)
cdrom 28960 0 (autoclean) [ide-cd]
soundcore 4100 0 (autoclean)
```