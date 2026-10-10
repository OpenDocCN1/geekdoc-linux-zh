**7. You are the Linux system administrator for your IT department. When you normally access your workstation in the morning, you are granted multiuser access with graphical user interface and network connectivity. To perform system maintenance activities, you need to switch runlevels when the system is running. Which command is used to switch runlevels when the system is running?**

+   A. runlevels
+   B. init
+   C. System Rescue
+   D. grub

Correct answer and explanation: **B**. Answer **B** is correct because *init* is used to change runlevels while a Linux system is running.

Incorrect answers and explanations: **A**, **C**, and **D**. Answer **A** is incorrect because *runlevels* is not a command. Answer **C** is incorrect because *System Rescue* is a process that is performed when repairing a corrupted Linux System. This process is accessed when booting up the system from a Linux distribution media. Answer **D** is incorrect because *grub* is used for installing and testing GRUB configuration settings before applying the modifications.

**8. How large is the Master Boot Record (MBR) for a hard disk drive with a sector size of 512 bytes?**

+   A. 1 MB
+   B. 512 bytes
+   C. 0 bytes
+   D. 6 KB

Correct answer and explanation: **B**. Answer **B** is correct; the MBR is 512 bytes in size. The MBR loads GRUB stage 1. The GRUB stage 1 program uses the first 446 bytes. The remaining 64 bytes are allocated to the partition table for the partitioning of the hard disk drives (for example, *Primary partitioning*.)

Incorrect answers and explanations: **A**, **C**, and **D**. Answers **A**, **C**, and **D** are incorrect sizes.

**9. Which order of events represents the proper Linux boot process?**

+   A. System BIOS, bootloader, Linux kernel, user logs into the system
+   B. Bootloader, system BIOS, Linux kernel, user logs into the system
+   C. System BIOS, Linux kernel, bootloader, user logs into the system
+   D. User logs into the system, system BIOS, bootloader, Linux kernel