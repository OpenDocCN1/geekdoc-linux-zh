# Text-Based Installation with YaST2

# Background Information

In addition to installation with the assistance of a graphical interface, SuSE Linux can also be installed with the help of the YaST2 text menus (console mode). All modules described in Chapter *Installation with YaST2* on page 5 are also available in this text mode. The text mode is especially useful if you do not need a graphical interface (e.g., for server systems) or if the graphics card is not supported by the X Window System.

# The Start Screen

Insert CD 1 into the drive and restart the computer. If the computer does not boot the CD, reset the boot sequence in the BIOS to CDROM, C, A.

The start screen appears (Figure 2.1 on page 7). Select ‘Manual Installation’ within ten seconds so YaST2 does not automatically start. Enter boot parameters in the boot options after manual, if your hardware requires such parameters. However, such parameters are usually not needed. To switch to text mode, select F2=Text, then press Enter.

Now, a box will appear with the progress display "Loading Linux kernel". The kernel boots and linuxrc is started. The menu-driven linuxrc application waits for user entries.

# Possible Problems

+   - If your CD-ROM drive (ATAPI) crashes when booting the system, refer to Section *ATAPI CD-ROM Hangs While Reading* on page 46.
+   - CD 1, which features an optimized kernel for Pentium processors, is not recognized as a boot medium. Try the “boot floppy” or CD 2. Refer to Sections *Booting from Disk (SYSLINUX)* on page 43 and *Booting with CD 2* on page 43.
+   - For graphics cards, including FireGL 1, 2, and 3, the graphical mode does not boot (framebuffer). In this case, text-based installation is required.
+   - Other booting problems can usually be circumvented via kernel parameters. Refer to Section *Kernel Parameters at the Boot Prompt* on page 240. The start option ‘Installation – Safe Settings’ is provided whenever DMA leads to difficulties.