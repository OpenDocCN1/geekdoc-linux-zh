
Once the repair process is complete, exit the shell by typing **exit**, and the system will attempt to boot again. It should succeed this time.

After the root file system is mounted, the kernel starts a program called **init**. This program starts all other programs. After init starts up all the necessary programs, the system is up and running and the boot process is complete.

What init runs as part of the bootup process is highly customizable. The following sections discuss init in detail.

The init program comes in two flavors—Unix System V init and BSD init. The Red Hat distribution comes with the Unix System V init program. The difference between the two flavors is that System V init uses run levels (discussed later in this section), and BSD init does not. Because the Red Hat distribution uses Unix System V init, this book limits discussion of init to that flavor.

Because init is the first program run by the kernel, its process ID (PID) is 1. When init starts, it reads a configuration file called `/etc/inittab`. The `/etc/inittab` file in a typical Red Hat Linux system is shown in Listing 2-1.

# Listing 2-1 A typical /etc/inittab file

```
# inittab - This file describes how the init
process should set up the system in a
certain run level.

#
# Author: Miguel van Snoorenburg,
<miquels@drinkel.nl.mugnet.org>

#
# Modified for RHS Linux by Marc Ewing and Donnie Barnes

#

# Default runlevel. The runlevels used by RHS are:
#	0 - halt (Do NOT set initdefault to this)
#	1 - Single-user mode
#	2 - Multiuser, without NFS (The same as 3, if you
do not have networking)
#	3 - Full multiuser mode
# 4 - unused
# 5 - X11
# 6 - reboot (Do NOT set initdefault to this)
#
id:3:initdefault:

# System initialization.
si:sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# Things to run in every runlevel.
ud::once:/sbin/update

# Trap Ctrl+Alt+Delete
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have
# a few minutes of power left. Schedule a shutdown for
# 2 minutes from now.

# This does, of course, assume you have powerd installed
# and your UPS connected and working correctly.

pf:powerfail:/sbin/shutdown -f -h +2 "Power Failure; \
System Shutting Down"

# If power was restored before the shutdown kicked in,
# cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; \
Shutdown Cancelled"

# Run getty's in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
x:5:respawn:/etc/X11/prefdm -nodaemon
```

This file defines how init behaves during server startup or shutdown events. The following discussion takes a closer look at this file.

The init program ignores all the blank and comment lines (that is, lines that start with a #) in the `/etc/inittab` file. The lines with colon-delimited fields are the init configuration lines. The syntax for such a line is as follows:

`id:runlevels:action:process arguments`

The first field is a unique label field to identify an entry in the file. An *id* can be 2 to 4 characters long. The second field, *runlevels*, defines which run levels this line applies to. The third field defines what action needs to be taken. The last field (*process*) defines which process needs to be run. Optionally, you can also specify command-line arguments for the process in the fourth field.

As mentioned before, a run level specifies a state of the system. The nine run levels are described in Table 2-1.

# Table 2-1 The Run Levels for init

| Run Level | Description |
| :--- | :--- |
| 0 | Halt – used to halt the system. |
| 1 | Single-user – used to set the system in a minimal configuration suitable for a single user. |
| 2 | Not used. |
| 3 | Multiuser – used to set the system in a configuration that supports multiple users. |
| 4 | Not used. |
| 5 | Used to start X Window System and the xdm program. |
| 6 | Reboot – used to reboot the system. |
| S or s | Used internally by scripts that run in run level 1. |
| a, b, c | On-demand run levels – typically not used. |

Note that you can specify multiple run levels in a single init configuration line. For example, if you want init to run a process for both single- and multiuser modes, you can specify a line such as the following:

`id:13:action:process arguments`

Table 2-2 shows the possible values for actions.

# Table 2-2 Possible Actions for a Specific Run Level

| Action | Description |
| --- | --- |
| respawn | The process is restarted whenever it terminates. |
| wait | The process is run once, and init waits until it terminates. |
| once | The process is run once. |
| boot | The process is run during system boot, and init ignores the run level field. |
| bootwait | The process is run during system boot, and init waits for the process to terminate. |
| off | No action is taken. This can be used to disable a configuration line without removing it. However, you can simply comment out the line by using a leading # instead. |
| ondemand | Useful only when the run level is a, b, or c. The process is run whenever init is called with any of the three ondemand run levels. Typically not used. |
| initdefault | Sets the default run level for the system. The process field is ignored. |
| sysinit | The process is run once during system boot. A sysinit action takes precedence over boot or bootwait actions. |
| powerwait | The process is run when init receives a SIGPWR signal. Typically, UPS monitoring software detects a power problem and issues such a signal to init. In such a case, init waits until the process terminates. |
| powerfail | Same as powerwait, but init does not wait for the process to complete. |
| powerokwait | The process is run when init receives a SIGPWR signal and a text file called `/etc/powerstatus` contains an “OK” string. Typically, a UPS monitoring program creates this file and sends the SIGPWR signal to init to indicate that the power problem has been fixed. |
| ctrlaltdel | The process is run when init receives a SIGINT signal. |
| kbrequest | The process is run when init receives a KeyboardSignal from the keyboard handler. |

The Unix System V flavor of init, which is what Red Hat Linux init is, uses the following directory structure:

```
/etc
+--rc.d
+--init.d (dir)
+--rc0.d (dir)
+--rc1.d (dir)
+--rc2.d (dir)
+--rc3.d (dir)
+--rc4.d (dir)
+--rc5.d (dir)
+--rc6.d (dir)
+--rc.sysinit (script)
+--rc.local (optional script, supplied with Red Hat Linux)
+--rc.serial (optional script)
+--rc (script)
```

## The /etc/rc.d/rc.sysinit script

As you already know, when a Red Hat Linux system boots, the kernel runs init, which in turn runs the `/etc/rc.d/rc.sysinit` script before processing any other scripts for the desired run level. The following line in the `/etc/inittab` file causes init to run this script before running anything else:

`si:sysinit:/etc/rc.d/rc.sysinit`

Notice that the run level field is empty, because *init* recognizes *sysinit* as a system initialization action. The *rc.sysinit* script does many things, including setting the host name, enabling the swap partition, checking the file systems, loading kernel modules, and more. Typically, you do not need to modify this script.

## The /etc/rc.d/init.d directory

The *init.d* subdirectory is used to store all the scripts needed for all the run levels. Keeping all the scripts in one location makes managing them easier. Each script is used to start and stop a particular service — Domain Name Service (DNS), Web service, or another such service. All of these scripts follow a special command-line argument syntax. For example, to start NFS (Network File System) service, run the following script:

```
/etc/rc.d/init.d/nfs start
```

To stop the same service, run the same script as follows:

```
/etc/rc.d/init.d/nfs stop
```

The *nfs* script takes *start* and *stop* as arguments. This is true for all the scripts in this directory, which are symbolically linked to the *rc0.d* through *rc6.d* directories, as needed.

## The /etc/rc.d/rc script

When *init* is told to change the run level to one of the seven commonly used run levels, it runs a script specified in one of the following lines in the `/etc/inittab` file:

```
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```
