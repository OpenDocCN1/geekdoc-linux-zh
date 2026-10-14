| Parameter | Value |
|---|---|
| io | `(addr)` |
| irq | `(irq)` |

To set up three ports in a PC style, for example, whereby one has the address 0x3bc without an IRQ, one has the address 0x378 with IRQ 7, and one has the address 0x278 with automatically detected IRQ, you should enter (all in one line):

```
Example: modprobe parport_pc io=0x3bc,0x378,0x278
        irq=none,7,auto
```

+   - *Printer driver*
+     Name of module: `lp.o`

| Parameter | Value |
|---|---|
| parport | `{port}` |

```
Example: modprobe lp parport=0,2
```

+   - *Parallel port IDE devices*
+     Name of module: `paride.o`

If you want to use chains of Paride devices on a single parallel port, you must first load parport.o (see Section *The Parallel Port* on the preceding page).

```
Example: modprobe paride
```

The parallel port should, if possible, be operated in “EPP mode”. Set this mode in the BIOS of your computer.

+   - *Parallel port IDE low-level protocol driver*
+     Name of module: `\variable{xxxx}.o`