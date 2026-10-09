PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
31323 zach 25 0 9020 6960 396 S 63 0.3 0:17.58 bzip2
31327 zach 18 0 2092 596 492 R 57 0.0 0:00.92 cp
31311 root 15 0 0 0 0 S 16 0.0 0:00.38 pdflush
6870 zach 27 12 331m 190m 37m R 2 9.4 198:42.98 firefox-bin
31303 root 15 0 0 0 0 S 2 0.0 0:00.42 firefs
1 root 15 0 2912 1808 488 S 0 0.1 0:01.55 systemd

The htop utility (htop package) is similar to top but it is psuedographical. Using htop, you can scroll vertically and horizontally, allowing you to view all processes and full command lines.

**Table 15-2** top: interactive commands

Command Function
h or ? Displays a Help screen.
k (kill) Prompts for a PID number and type of signal and sends the process that signal. Defaults to signal 15 (SIGTERM); specify 9 (SIGKILL) only when 15 does not work.
F Displays a page that allows you to specify a sort field.
f Displays a page that allows you to specify which fields top displays.
o Displays a page that allows you to specify the order of the displayed fields.
q Quits top.
s Prompts for time between updates in seconds. Use 0 (zero) for continuous updates; such updates can slow the system by consuming a lot of resources.
SPACE Updates the display immediately.
u Prompts for username and displays only processes owned by that user.
W Writes a startup file named ~/.toprc so that the next time you start top, it uses the same parameters it is currently using.

# MAINTAINING THE SYSTEM

This section discusses several tools and concepts that are important to a system administrator. It covers setting the system clock, using parted to work with partitions on a hard disk, how to avoid creating problems, and how to solve system problems.

# LPI timedetect: REPORTS ON AND SETS THE SYSTEM CLOCK

The timedetect! utility, which is part of systemd (page 438), displays more information about the system clock than does date (page 218). You can also use it to set the system clock. Following, timedetect! sets the system clock and displays information about the system clock, time zone, NTP, and DST.