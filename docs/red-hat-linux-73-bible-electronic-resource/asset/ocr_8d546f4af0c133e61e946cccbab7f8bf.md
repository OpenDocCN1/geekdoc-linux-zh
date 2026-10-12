# Table 12-4 (Continued)

| Run Level | What Happens in This Run Level |
| :--- | :--- |
| 5 | Multiuser mode with network services and X. This run level starts the X server and presents a graphical login window, visually resembling any of the more expensive UNIX-based workstations. This is a common initdefault value for a Red Hat Linux workstation. |
| 6 | All processes are terminated and the machine is gracefully rebooted. Again, the comments in the inittab file mention that this is not a good choice for initdefault, perhaps even worse than run level 0. The effect is a possibly infinite cycle of booting, followed by rebooting. |
| 7, 8, 9 | Generally unused and undefined, these run levels have the potential to meet any needs not covered by the default options. |
| a, b, c, A, B, C | Used in conjunction with the ondemand action. These don't really specify a run level but can launch a program or daemon "on demand" if so instructed. |

> **NOTE: If there is no initdefault specified in the inittab file, the boot sequence will be interrupted and you will be prompted to specify a default run level into which the machine will boot.**

The next line in the inittab file instructs init to execute the /etc/rc.d/rc.sysinit script before entering the default run level. This script performs many initialization routines such as choosing a keymap file, checking and mounting the root and proc file systems, setting the clock and host name, configuring swap space, cleaning up temporary files, and loading system modules.

The seven following lines control the commands executed within each major run level. In each, the /etc/rc.d/rc script is called, using the desired run level as an argument. It, in turn, descends into the appropriate directory tree (for example, the /etc/rc3.d directory is entered for run level 3).

The next line specifies that no matter what run level the machine is in, the update daemon should be running. The update daemon is a program that flushes kernel buffers from memory to disk (generally every 30 seconds) to ensure that, in the event of an unintended shutdown, a minimum amount of data is lost.

The ctrlaltdel tells init to perform exactly what PC users would expect if the Ctrl, Alt, and Delete keys were pressed simultaneously. The system reboots itself in an orderly fashion (a switch to run level 6) after a three-second delay.