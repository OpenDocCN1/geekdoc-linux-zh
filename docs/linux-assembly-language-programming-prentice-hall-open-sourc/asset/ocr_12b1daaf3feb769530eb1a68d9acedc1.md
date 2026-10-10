to actually point to the first entry in the global table. (So it doesn't matter what this entry contains.)

# 13.2.4 Segment Operations

The GDT has to be there for memory references to work in protected mode and the IDT has to be there for interrupts to work. The load commands for these tables are

```
LGDT mem
```

and

```
LIDT mem
```

where mem points to six bytes of memory containing a two-byte limit, followed by a four byte base address. These commands would ordinarily be executed just once while the system was booting in real mode.

Other segment registers are loaded using selectors. Figure 13-5 shows the commands for loading and saving segment registers, as well as the commands for loading and saving the GDT and IDT base and limit registers. When segment registers are loaded, all the other registers associated with them are loaded as well, unless the null selector is used or unless some access violation occurs.

![](bbox=[0.1, 0.38, 0.9, 0.83])

These eight bytes would include the base address and size of the DS segment. These eight bytes would also include a privilege level. Since the privilege carried in DS is only a 3, the privilege level in the segment descriptor would need to be a 3, or the processor would nail us with an error. In protected mode, a command such as

```
MOV DS, AX
```