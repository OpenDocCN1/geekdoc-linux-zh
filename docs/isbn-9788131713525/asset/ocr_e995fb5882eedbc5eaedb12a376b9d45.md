These can be displayed by issuing the gdb info breakpoints command. As usual, we use the abbreviated version.

```
(gdb) i b
Num Type Disp Enb Address What
1 breakpoint keep y 0xco016d8 in panic_at kernel/panic.c:74
2 breakpoint keep y 0xc005bd5c in sys_sync at fs/buffer.c:296
3 breakpoint keep y 0xc021a488 in yosemite_setup_arch at
arch/ppc/platforms/4x0s/yosemite.c:308
breakpoint already hit 1 time
(gdb)
```

Now compare the previous breakpoint addresses with the addresses in the gdb remote $m packet in Listing 14-5. The $m packet is a “read target memory” command, and the $M packet is a “write target memory” command. Once for each breakpoint, the address of the breakpoint is read from target memory, stored away locally on the host by gdb (so it can be restored later), and replaced with the PowerPC trap instruction twge r2, r2 (0x7d821008), which results in control passing back to the debugger. Figure 14-4 illustrates this action.

![](bbox=[0.07, 0.46, 0.93, 0.88])

FIGURE 14-4
gdb inserting target memory breakpoints