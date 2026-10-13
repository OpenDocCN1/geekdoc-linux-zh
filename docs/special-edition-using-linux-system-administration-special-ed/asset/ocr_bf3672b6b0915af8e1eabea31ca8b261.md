# Alpha, Beta Drivers

+   - AMD AM79C974 (PCI) (Compaq, HP, Zeos onboard SCSI)  
+     `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/AMS3C974-0.3.tgz`
+   - Adaptec ACB-40xx SCSI-MFM/RLL bridgeboard  
+     `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/adaptec-40xx.tar.gz`
+   - Always Technologies AL-500  
+     `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/al500-0.2.tar.gz`
+   - Iomega PC2/2B  
+     `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/iomega_pc2-1.1.x.tar.gz`
+   - Ricoh GSI-8  
+     `ftp://tsx-11.mit.edu/pub/Linux/ALPHA/scsi/gsi8.tar.gz`

# Unsupported

+   - Adaptec AHA 2940UW Pro
+   - Adaptec AAA-13x RAID Adapters
+   - Adaptec AAA-113x Raid Port Cards
+   - Adaptec AIC-7810
+   - NCR chip 53C710 (ISA) (old obsolete chip, but still used in some Compaq models)
+   - Non Adaptec compatible DTC boards (327x, 328x)

# Controllers (I/O)

Any standard serial/parallel/joystick/combo cards. Linux supports 8250, 16450, 16550, and 16550A UARTs. Cards that support nonstandard IRQs (IRQ 9) can be used.

See Neal Samuelson’s “Application Note AN-493” by Martin S. Michael. Section 5.0 describes in detail the differences between the NS16550 and NS16550A. Briefly, the NS16550 had bugs in the FIFO circuits, but the NS16550A (and later) chips fixed those. However, there were very few NS16550’s produced by National, long ago, so these should be very rare. And many of the “16550” parts in actual modern boards are from the many manufacturers of multiple parts, which may not use the National “A” suffix. Also, some multiport boards will use 16552 or 16554 or various other multiport or multifunction chips from National or other suppliers (generally in a dense package soldered to the board, not a 40-pin DIP). Don’t worry about it unless you encounter a very old 40-pin DIP National “NS16550” (no A) chip loose or in an old board, in which case treat it as a 16450 (no FIFO) rather than a 16550A — Zdhahai Stewart at zstewart@hisys.com.