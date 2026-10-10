NOTE
Other targets you can jump to include reboot, poweroff, and halt. For example, just type **systemctl isolate reboot** to reboot your system.

Notice in Listing 6.16 that when the **systemctl is-system-running** command is issued, the response is **maintenance** instead of **running**. Also, when the **list-units** command is employed, it shows that the **emergency.target** is active. The **systemctl default** command will cause the system to attempt to jump into the default target.

TIP
If you are using GRUB2 as your bootloader, you can reach a different target via the bootloader menu. Just move your cursor to the menu option that typically boots your system and press the **E** key to edit it. Scroll down and find the line that starts with the **linux16** command. Press the **End** key to reach the line's end. Press the **spacebar** and type **systemd.unit=target-name.target**, where *target-name* is the name of the target you want your system to activate. This is useful for emergency situations.

A handy systemd component is the **systemd-analyze** utility. With this utility, you can investigate your system's boot performance and check for potential system initialization problems. Table 6.8 contains common commands you can use with the **systemd-analyze** utility.

# TABLE 6.8 Common systemd-analyze commands

| Command | Description |
| :--- | :--- |
| blame | Displays the amount of time each running unit took to initialize. Units and their times are listed starting from the slowest to the fastest. |
| time | Displays the amount of time system initialization spent for the kernel, and the initial RAM filesystem, as well as the time it took for normal system user space to initialize. (Default) |
| critical-chain | Displays time-critical units in a tree format. Can pass it a unit file argument to focus the information on that particular unit. |
| dump | Displays information concerning all the units. The display format is subject to change without notice, so it should be used only for human viewing. |
| verify | Scans unit files and displays warning messages if any errors are found. Will accept a unit file name as an argument, but follows directory location precedence. |