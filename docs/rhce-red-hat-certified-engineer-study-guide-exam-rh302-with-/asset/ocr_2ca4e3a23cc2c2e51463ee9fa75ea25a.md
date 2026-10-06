# Configuring the Runlevel

To change the system runlevel, issue the command
`init n`
where n is the desired new runlevel. Table 9.1 summarizes the runlevels used by Red Hat Linux.

# TABLE 9.1 Red Hat Linux Runlevels

| Runlevel | Definition |
| --- | --- |
| 0 | Reserved: Setting this runlevel halts the system. |
| 1 | Reserved: Setting this runlevel sets single-user mode. |
| 2 | Multiuser mode without networking. |
| 3 | Multiuser mode with networking. |
| 4 | Not used: essentially identical to runlevel 3. |
| 5 | X-based log in. |
| 6 | Reserved: Setting this runlevel reboots the system. |

To select the initial runlevel that the system assumes when booted, select Config > Miscellaneous Services > Initial System Services. The Default Runlevel screen will appear. Figure 9.6 shows the graphical version of this screen. Click the radio button corresponding to the desired default runlevel, and click Accept. The next time you boot the system, it should enter the specified runlevel.