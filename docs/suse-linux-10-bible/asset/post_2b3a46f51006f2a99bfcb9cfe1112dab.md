
# 114 Part II ♦ The SUSE System

## Table 4-1
Runlevels and Their Descriptions

| Runlevel | Description |
|-----------|-------------|
| 0 | This runlevel is used to halt a system. The machine is shut down, and all services are terminated. |
| 1, s, S | Single-user mode. The root user is allowed to log in. No services are running. |
| 2 | Multiserver, no network. Users can log in only locally. No network services have been exported. |
| 3 | Multiserver, with network. The network has been initialized and any user can log in or over the network. |
| 4 | Unused. |
| 5 | Multiserver with X Windows and network. Same as runlevel 3, but the X Window system is loaded, allowing users to use a window manager, GNOME, KDE, and so on. |
| 6 | Reboot. This runlevel shuts down all services, the network, and so on, and reboots the machine. |

## Switching Runlevels Manually

If you want to switch runlevels, you can use the `init` or `telinit` commands, which are located in the `/sbin` directory on SUSE systems. The `telinit` command is a symbolic link to the `init` command. The `init` command behaves slightly different when invoked as `telinit`, the `-t` flag followed by an integer of seconds. The `init` command will wait the specified number of seconds before switching to the specified runlevel.

The `init` process is fondly referred to as the grandfather process on Unix and Linux systems, as it is the first process started by the kernel after the kernel has finished initializing and is the process that controls the startup of all processes on the system. The `init` process always has process ID 1 and exists on a Linux system.

When `init` is executed by the kernel, it reads the system's default runlevel from the file `/etc/inittab`. The entry for the system's default runlevel in this file looks like the following:

```
id:3:initdefault:
```

# Chapter 4 ✦ Booting the System 115

The number in the second field identifies the system's default runlevel, which is the runlevel that the system will boot to whenever it is powered on and allowed to start up normally.

When the init process identifies the runlevel that it will enter by default, it checks the remainder of the /etc/inittab file to determine what to execute for each runlevel. The entries in /etc/rc.d for each runlevel look like the following:

```
10:wait://etc/rc.d/0
11:wait://etc/rc.d/1
12:wait://etc/rc.d/2
13:wait://etc/rc.d/3
14:wait://etc/rc.d/4
15:wait://etc/rc.d/5
16:wait://etc/rc.d/6
```

These entries tell the init process to go to a directory in /etc whose name is based on the runlevel it needs to load, and execute any startup commands that it finds there. Table 4-2 shows the correlation between the number of a runlevel and the runlevel directly determines the name of the directory used to specify what to start on your system.

## Table 4-2
Runlevels and Their Respective Directories

| Runlevel | Directory |
|-----------|-----------|
| 0 | /etc/init.d/rc0.d |
| 1 | /etc/init.d/rc1.d |
| 2 | /etc/init.d/rc2.d |
| 3 | /etc/init.d/rc3.d |
| 4 | /etc/init.d/rc4.d |
| 5 | /etc/init.d/rc5.d |
| 6 | /etc/init.d/rc6.d |

The directories associated with different runlevels contain both scripts (known as "Start" scripts) and scripts that it will execute when it leaves a runlevel (known as "Kill" scripts). Start scripts are scripts whose name begins with an uppercase s. Kill scripts are those whose name begins with an uppercase k.

# 116 Part II + The SUSE System

When we enter and leaves with respect to runlevels, we are talking about changing one runlevel to another using the init or telinit process, or booting down the system.

You never stop a runlevel in Unix—you move from one runlevel to another. For example, if the system loads runlevel 5 by default, it will continue to run at runlevel until you tell it to move to another one. If you wanted to shut down the machine, you would move into runlevel 0. This would trigger init to run all of the Kill scripts in /etc/init.d/rc0.d and then all of the Start scripts (of which there are none).

The Start and Kill scripts in a runlevel are actually symbolic links to files in /etc/init.d, which are all the service scripts for daemons and processes that can be controlled by init. Using symbolic links rather than runlevel specific scripts enables the system to share scripts across different runlevels. The directory associated with each runlevel to start a service can simply contain a symbolic link to the same master script, saving disk space and simplifying maintenance of the service scripts. Updating the master service script in /etc/init.d automatically makes these changes available to any other runlevel that refers to the Start script.

The files in /etc/init.d contains a few features that are unique to the init system. The scripts are nearly always bash scripts that take at least two arguments, start and stop. If you directly run one of these scripts with the start option, it would try to load the application that the script controls. Similarly, if you pass the stop parameter to the script, it attempts to shut down the application cleanly. In the SUSE world, we use rcservename scripts to control this behavior instead of accessing the /etc/init.d directly. If you wanted to stop the Apache web server process, you could type the command rcapache2 stop.

If you move to the specific runlevel directory and take runlevel 3 as an example, you will see many symbolic links in /etc/rc.3.d that begin with an S or a K, but you will notice that some of these point to the same script in the directory /etc/init.d.

When the init process runs a Start script, it calls the script that the link points to with the argument start. When the init process runs a Kill script, it calls the script that the link points to with the argument stop.

Start and Kill scripts usually have numbers after the S or K. This number signifies the relative order that the scripts are executed. A lower number means that the scripts are executed earlier than one with a higher number when entering or leaving a runlevel. Sequencing Start and Kill scripts is a very significant part of the boot process.

# Chapter 4 ♦ Booting the System

If a service needs the network to be initialized before it can run (for example, the Apache web server), its start order will have to be higher than that of the network. Similarly, to cleanly shut down Apache, you would have to shut it down before the network when leaving the runlevel.

When all the Start scripts associated with a specific runlevel have finished execution, the system is said to be in runlevel.x. This means it has successfully completed initializing all associated services and is now in the specified runlevel.

When the system is in a specific runlevel, you can control a switch to another runlevel with init or telinit processes. If you were in runlevel 5 and wanted to cleanly shut down X and move to runlevel 3, you would issue the command init 3. If you were able to wait ten seconds before moving to runlevel 3, you should use the command init -t 10 3. Thinking back, you should be able to trace what the init program does with regards to these "init scripts" (a common name for runlevel scripts). The init process executes all of the scripts in the directory /etc/rcX.d that start with an S in the order of the numbering in the filename. When finished killing processes, it runs all of the scripts in /etc/rc3.d that begin with an s in the sequence specified by the filename. When it has completed these scripts, the system will successfully be in runlevel 3.

> If you find need to change the default runlevel before your system boots, you can pass the desired runlevel to the boot loader (for example, append a 1 to the boot parameters in GRUB).

If there are services that should be running in runlevel 3 that were running in runlevel 5, the system is clever enough to not kill off those services and allows them to continue because those services are common to both runlevels.

## Using chconfig to Control Runlevels

Those of you familiar with Red Hat may recognize the chconfig system script. This is a program that allows you to add and remove services from the runlevel directory of a specific runlevel. If this program did not exist, you create your links to move from one level to another—for example, in the directory /etc/init.d/rc3.d or /etc/rc/rc3.d (these are the same directory) to /etc/init.d to make sure process starts and stops in an order you dictate. The services that you can control with the chconfig command are all of the scripts in the /etc/init.d/directory.
