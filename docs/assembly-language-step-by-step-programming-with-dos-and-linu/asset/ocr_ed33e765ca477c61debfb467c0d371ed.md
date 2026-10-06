Your job is to tell the CPU where the two different components of that 20-bit address are. The customary notation is to separate the segment register and the offset register by a colon. For example:

```
SS : SP
SS : BP
ES : DI
DS : SI
CS : BX
```

Each of these five register combinations specifies a full 20-bit address. ES:DI, for example, specifies the address in DI from the start of the segment called out in ES.

I've drawn a diagram outlining real mode segmented model in Figure 6.9. In contrast to real mode flat model (shown in Figure 6.8), the diagram here shows all of memory, not just the one little 64K chunk that your real mode flat program is allocated when it runs. A program written for real mode segmented model can see all of real memory.

The diagram shows two code segments and two data segments. In practice you can have any reasonable number code and data segments, not just two of each. You can access two data segments at the same time, because you have two segment registers available to do the job: DS and ES. Each can specify a data segment, and you can move data from one segment to another using any of several machine instructions. (We speak more of this in later chapters.) However, you only have one code segment register, CS. CS always points to the current code segment, and the next instruction to be executed is pointed to by the IP register. You don't load values directly into CS to change from one segment to another. Machine instructions called jumps change another code segment as necessary. Your program can span several code segments, and when a jump instruction (there are several kinds) needs to take execution into a different code segment, it changes the value in CS.

There is only one stack segment for any single program, specified by the stack register SS. The stack pointer register SP points to the memory address (relative to SS, albeit in an upside-down direction) where the next stack operation will take place. The stack will require some considerable explaining, which I take up in Chapter 8.

You need to keep in mind that in real mode, there will be pieces of the operating system (and if you're using an 8086 or 8088, that will be