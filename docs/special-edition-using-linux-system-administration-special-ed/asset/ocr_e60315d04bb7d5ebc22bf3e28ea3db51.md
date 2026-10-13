```
```text
Memory: 387200k/393216k available (1044k kernel code, 416k reserved, 4184k data,
68k init)
VFS: Diskquotas version quota_6.4.0 initialized
Checking 386/387 coupling... OK, FPU using exception 16 error reporting.
Checking 'hlt' instruction... OK.
POSIX conformance testing by UNIFIX
mtrr: v1.26 (19981001) Richard Gooch (rgooch@atnf.csiro.au)
per-CPU timeslice cutoff: 50.0 usecs.
CPU1: Intel Pentium Pro stepping 09
calibrating APIC timer ...
..... CPU clock speed is 199.4418 MHz.
..... system bus clock speed is 66.4804 MHz.
Booting processor 0 eip 2000
Calibrating delay loop... 199.07 BogoMIPS
OK.
CPU0: Intel Pentium Pro stepping 09
Total of 2 processors active (398.13 BogoMIPS).
enabling symmetric IO mode... ...done.
ENABLING IO-APIC IRQs
init IO-APIC 0
IO-APIC pin 0, 16, 17, 18, 19, 20, 21, 22, 23 not connected.
...MP-BIOS bug: 8254 timer not connected to IO-APIC
...trying to set up timer as ExtINT... .. (found 0) ... works.
number of MP IRQ sources: 16.
number of IO-APIC registers: 24.
testing the IO APIC:.......................
.... register #0: 02000000
........ : physical APIC id: 02
........ register #1: 00170011
........ : max redirection entries: 0017
........ : IO APIC version: 0011
........ register #2: 00000000
........ : arbitration: 00
```
```

# TROUBLESHOOTING

A large number of problems can potentially occur in building, installing, and using a new kernel. These include the following:

+   - Your kernel doesn’t compile.
+   - Your new kernel doesn’t boot.
+   - Your system won’t boot.
+   - Your system can’t find a compressed kernel image file.
+   - You cannot compile other programs after a kernel upgrade.
+   - Your kernel is too large and too slow.
+   - You have problems with your parallel port or printer.
+   - You have problems with your CD-ROM drive.