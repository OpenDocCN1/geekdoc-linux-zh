# 11

Because the inittab file is a configuration file, not a sequential shell script, the order of lines is not significant. Lines beginning with a hash (#) character are comments and are not processed.

The first non-commented line in the preceding sample inittab file sets the default run level to 5. A default of 5 (which is the common run level for desktop systems) means that, following the completion of all commands associated with the *sysinit*, *boot*, and *bootwait* actions, run level 5 is entered (booting to a GUI-based login).

The other common *initdefault* level is run level 3 (often used for servers that boot up in text mode and often have no GUI). Table 11-4 describes each of the run levels and helps you choose the run level that is best suited as the default in your environment.

> If there is no *initdefault* specified in the inittab file, the boot sequence will be interrupted, and you will be prompted to specify a default run level into which the machine will boot.

The next line in the inittab file instructs *init* to execute the */etc/rc.d/rc.sysinit* script before entering the default run level. This script performs many initialization routines such as choosing a keymap file, checking and mounting *root* and *proc* file systems, setting the clock and hostname, configuring swap space, cleaning up temp files, and loading modules.

The seven following lines control the commands executed within each major run level. In each, the */etc/rc.d/rc*script* is called, using the desired run level as an argument. In turn, it descends into the appropriate directory tree (e.g., the */etc/rc3.d* directory is entered for run level 3).

The *ctrlaltdel* action in the inittab file tells *init* to perform exactly what PC users would expect if the [Ctrl]+[Alt]+[Delete] keys were pressed simultaneously. The system reboots itself in an orderly fashion (a switch to run level 6) after a 3-second delay.

The next two lines (with their comments) deal with graceful shutdowns you have an uninterrupted power supply (UPS) and software installed. The first line initiates a halt (a switch to run level 0) 2 minutes after receiving a signal from the UPS indicating a power failure. The second line cancels the shutdown in the event that power is restored.

The six *getty* lines start up virtual consoles to allow logins. These processes are always running in any of the multiplier run levels. When someone connected to a virtual console logs out, that *getty* process dies, and then *respawn* action tells *init* to start a new *getty* process. You can switch between virtual consoles by pressing [Ctrl]+[Alt]+[F1], [Ctrl]+[Alt]+[F2], and so on.

The last line indicates that as long as the system is in run level 5, the "preferred display manager" (*xdm*, *gdm* (Gnome), *kdm* (KDE), etc.) will be running.

This presents a graphical login prompt rather than the usual text-based login and eliminates the need to run *startx* to start the GUI.