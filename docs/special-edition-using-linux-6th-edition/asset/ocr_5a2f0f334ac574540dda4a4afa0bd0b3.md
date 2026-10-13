# **Figure 12.1**  
BIOS boot sequence.

![](bbox=[0.258, 0.077, 0.661, 0.699])

+   1. The power is turned on.
+   2. The power-good signal triggers POST.
+   3. The system BIOS loads.
+   4. The BIOS, based on CMOS settings, determines where to look for a valid boot sector.
+   5. Control is passed to the master boot record (MBR).
+   6. The MBR passes control to the boot sector of the active partition.
+   7. The boot sector loads the operating system.