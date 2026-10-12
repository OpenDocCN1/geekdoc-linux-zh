```
0x150: 92 88 D6 BA 16 77 01 3B 06 75 01 77 13 86 C4 D0
0x160: CB 0C C6 0A 78 01 89 C1 5B BB 01 92 CD 13 C3
0x170: 58 31 C0 F9 C3 00
0x180: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0x190: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0x1A0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0x1B0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01
0x1C0: 01 00 83 3F FF DE 3F 00 00 01 F8 3C 00 00 00 00
0x1D0: C1 DF 82 3F FF FF 4B F8 3C C0 07 82 00 00 00 00
0x1E0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0x1F0: 00 00 00 00 00 00 00 00 00 00 00 00 55 AA
```

```
Expert command (m for help): r

Command (m for help): q
```

As you can see, fdisk is quite simple to use. If you require more information on the command menus than the brief descriptions provided by the m command, you should refer to the manual page.

# Partitioning with cfdisk

If you prefer a screen-oriented partitioning tool, similar to the MS-DOS fdisk utility, try out cfdisk. This utility provides most of the same functionality as fdisk, but uses curses to display the information in a full screen display, as shown in Figure 7.1.

Interacting with cfdisk is very simple. You select the partition to work on using the up and down arrow keys, and select the action to perform on it using either the single letter commands, which you can display using the Help option, or by selecting one of the commands displayed at the bottom of the screen using the left and right arrow keys.

As you can see from Figure 7.1, cfdisk is an interactive command and therefore, like the fdisk utility, it has few command-line options. The command-line options that are available, however, are described in Table 7.2.