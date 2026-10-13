the /etc/rc.d/rc.modules script. Line ID s2 configures the serial ports, but only if you’ve enabled the /etc/rc.d/rc.serial script (disabled by default). These three lines execute at the same time, line s0 displaying on the screen the status of the modules as the si script loads them. The line ID bw is one you’ll not notice until your system shuts down abnormally. This line calls rc.boot, which handles checking the status of the disk drives to ensure that they were properly unmounted, and if not, runs fsck or continues with mounting the disks. This script drops you into a shell at runlevel 1 if fsck is not able to repair the disks without assistance. Because the system cannot continue until this script completes, the action column is bootwait.

```
```text
~1:S:wait:/etc/rc.d/rc 1
~~:S:wait:/sbin/sulogin
```
```

These two lines are two scripts that run whenever you enter maintenance (single-user) mode. You’ll look at the rc script later. The sulogin program is a special program to make your system a little more secure by preventing anyone who has physical access to the machine from rebooting into single-user mode and gaining access to the system without knowing the root password. Without this line, booting into single-user mode presents a root shell to the user without prompting for a password. However, this does not present a sophisticated user from breaking into the system if he has physical access to the machine. In fact, one of the ways to bypass sulogin is discussed at the end of this chapter in the “Emergencies” section, as well as the significance of the tilde (~) as the first character in the ID.

```
```text
l0:0:wait:/etc/rc.d/rc 0
l1:1:wait:/etc/rc.d/rc 1
l2:2:wait:/etc/rc.d/rc 2
l3:3:wait:/etc/rc.d/rc 3
l4:4:wait:/etc/rc.d/rc 4
l5:5:wait:/etc/rc.d/rc 5
l6:6:wait:/etc/rc.d/rc 6
```
```

The lines with IDs l0–l6 are run when you change to the particular runlevel. Each run-level change runs the rc script with the argument for the particular runlevel that is being entered. Remember that runlevels 7–9 are legitimate runlevels that can be used if necessary. If you want to make use of any of these nonstandard runlevels, you need to add lines to customize those runlevels because you almost certainly want to run the rc script if you are going to use any of these runlevels.

```
```text
z6:6:respawn:/sbin/sulogin
```
```

Line ID z6 is designed to present a root password prompt in case a machine doesn’t properly reboot when it enters runlevel 6. This is only precautionary. At the time of this writing, I am unaware of any machine that doesn’t correctly respond to a reboot command.

```
```text
ca:12345:ctrlaltdel:/sbin/shutdown -t3 -r now
```
```

Line ID ca traps the keyboard sequence Ctrl+Alt+Delete and performs a shutdown and reboot. If desired, this line can be modified to change the -r to -h to halt the system, or