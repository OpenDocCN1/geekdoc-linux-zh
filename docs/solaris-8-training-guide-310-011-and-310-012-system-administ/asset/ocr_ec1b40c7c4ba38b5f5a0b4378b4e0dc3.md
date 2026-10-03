based on the interactive programming language Forth. In Forth, sequences of user commands can be combined to form complete programs. This capability provides a powerful tool for debugging hardware and software. Another benefit of version 3 is the flash update feature. You can update the version 3 firmware without replacing the PROM chip.

> NOTE
The Intel environment has no OpenBoot PROM or NVRAM. On Intel systems, before the kernel is started, the system is controlled by the read-only-memory (ROM) Basic Input/Output System (BIOS), the firmware interface on a PC.

# Single Versus Multiple CPU Systems

The following system types have only one system board, and hold only one boot PROM and NVRAM chip:

+   - SPARCstation 4, 5, 10, and 20
- ULTRA 1, 2, 5, 10, 30, 60, 80, 220, 250, 240, 420, and 450

All other systems can be configured with multiple system boards, and have a special boot PROM and NVRAM arrangement. The following list provides some things of which you should be aware on multiple CPU systems:

+   - These systems have a clock board to oversee the backplane communications.
- The HOSTID and Ethernet address are on the clock board, and are automatically downloaded to the NVRAM on all CPU boards when the Power-On Self-Test (POST) is complete.
- PROM contents on each CPU are compared and verified by checksums.
- The CPU located in the lower most card cage slot is the master CPU board.
- Each CPU runs its own individual POST.

# Accessing the OpenBoot Environment

You can get to the OpenBoot environment by using any one of the following commands previously discussed in Chapter 1:

+   - By halting the operating system.
- By pressing the Stop and A keys simultaneously (Stop+A). On terminals connected to the serial port, press the Break key.