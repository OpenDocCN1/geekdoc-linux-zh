Table 1-3 Quadrants in 64-bit Mode

| Quadrant | Virtual Address Range |
|---|---|
| Quadrant 1 | 0x00000000 00000000 to 0x000003ff ffffffff |
| Quadrant 2 | 0x40000000 00000000 to 0x400003ff ffffffff |
| Quadrant 3 | 0x80000000 00000000 to 0x800003ff ffffffff |
| Quadrant 4 | 0xc0000000 00000000 to 0xc00003ff ffffffff |

# 32-Bit Address Space Layout

Figure 1-5 shows the layout of memory in both 32-bit user mode and 32-bit kernel mode. Thirty-two-bit kernel mode is used only on PA-RISC 1.1 systems. On a PA-RISC 2.0 system, the kernel itself is always in 64-bit mode. Applications on a PA-RISC 2.0 system can be either 32- or 64-bit applications. On a PA-RISC 1.1 system, applications are always in 32-bit mode.

![](bbox=[0.16, 0.48, 0.86, 0.82])

# 64-bit Address Space Layout

Figure 1-6 shows the layout of memory in 64-bit mode, both for the kernel and for 64-bit user applications. One of the requirements for the 64-bit user mode is that a 64-bit application must