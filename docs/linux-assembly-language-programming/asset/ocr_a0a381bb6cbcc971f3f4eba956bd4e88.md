remaining hex digits will be 0s added to the top end or Fs added to the bottom. The value 000FFFFFH may be encoded using either scheme. If we use G = 0 for byte granularity, then inserting the 20 limit bits, FFFFFH, gives us:

```
02 XF XX 00 00 00 FF FF
```

In the CS segments, the D bit is extremely important. In x86 code, there is a coding default which may either be for 16-bit code or 32-bit code. See *chapter 5, section 5.5* for details on how this works. In protected mode, the default is determined by the D bit of the CS segment descriptor. D = 1 means that the default is 32-bit code, D = 0 means it is 16. In real mode, the default is always 16-bit code. With G = 0, D = 1 and bits 52 and 53 as 0, we get

```
02 4F XX 00 00 00 FF FF
```

Bit 51, P for present, should be marked 1. If this is to be a user accessible segment, then the DPL bits must be 3. DPL stands for *descriptor privilege level*. If this is a data segment, then E = 0, i.e., it is not executable, and W = 1, i.e., it is writable. Making the remaining two bits, 40 and 42, 0 yields

```
02 4F F2 00 00 00 FF FF
```

# 13.2.6 Task Isolation via Local Descriptor Tables

A process can only access memory segments that are listed in two tables, its own table called the *local descriptor table*, and another table called the *global descriptor table*. The system has only one one global descriptor table. All processes have access to the global table, but local tables need not be shared. Consequently one method the operating system could use to isolate tasks from one another would be to hand out different local descriptor tables to different processes. If a segment is not listed in either the global descriptor table or the process's own local descriptor table, then the process can't get to it. Before discussing protection further, we need to look at some of the details of descriptors, selectors, and the descriptor tables.

Segmentation on the 80286 was designed to allow different tasks to have their own memory segments to which other tasks would not have access. Each task can have its own local descriptor table. Descriptors of private memory segments can be stored in these local tables. The x86 architecture implements local descriptor tables as segments, complete with descriptors in the global table. In the memory shown in *Figure 13-7*, there are eight memory segments. Each of these memory segments is defined by a descriptor situated in a descriptor table. Although the global table is like a segment, it is not a segment. There is no descriptor for it anywhere in memory and no selector for it anywhere in the processor.

![](bbox=[0.2, 0.78, 0.8, 1.0])