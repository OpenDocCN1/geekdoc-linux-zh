
## Answers

- 1. A soft limit is the maximum amount of disk space users can consume without any warnings. When they exceed their soft limit, the system complains but lets them continue. A hard limit is an inviolable constraint and the system will reject user attempts to add new files or even enlarge files.
- 2. The first step is to edit the /etc/fstab (or vfstab on Solaris) to enable quotas at mount time.
- 3. A major limitation is that the quota system doesn't span multiple file systems, so although it's possible to limit users to a specific amount of space per device, there's no built-in mechanism to limit overall disk usage.
- 4. The wall command lets you send an instant message to every user logged in at that moment.
- 5. If you enable quotas, adding a call to quota (or quota -v, as necessary) in every user's .login or .bash_profile is a very smart move.

In the next hour, we'll switch gears and start looking at process and system controls. We'll focus on starting up and shutting down Unix systems, including an extensive discussion of run levels and init states. It's required reading for any system administrator!

![](img/5ced0c78d748bd190e9027e5549a3622_261_0.png)

## PART V

## Process & System Controls

## Hour

- 13 Changing System State 247
- 14 Exploring Processes 265
- 15 Running Jobs in the Future 285
- 16 Managing Your Log Files 301

![](img/5ced0c78d748bd190e9027e5549a3622_263_0.png)

## Hour 13

## Changing System State

Compared to a personal computer operating system, the multiuser, multiprocessing capabilities of Unix can seem a bit alien in some regards. Most notably, have you ever stopped to consider what happens when you either boot up or shut down your Unix system?

In this hour, we’ll dig into the system configuration and learn exactly what processes are started and stopped (and how they’re started and stopped) when you switch states, either booting, halting, rebooting, or switching between single-user and multiuser modes.

In this hour you’ll learn about

- The init process and its configuration file
- Enabling specific services at different run levels
- Shutting down your system the right way

## Configuring and Working with the init Process

The Unix operating system has a number of run levels, each of which define a different state of the OS, and a different set of applications and daemons that are available and running. For example, by convention, run level 0 is the shutdown state—a system that's in run level 0 is stopped.

Run levels are also called init states after the all-important program that defines these different run levels for your computer: init.

### Task 13.1: The init Process and Configuration

To start this hour, let's delve into the internals of the init program and its configuration file /etc/inittab.

1. First off, a quick invocation of ps will confirm that the init daemon is running. This turns out to be easy because on every Unix system, the init program is the very first program run by the operating system. As a result, it's always process ID 1.

On a Linux box:

```
# ps -up 1
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 1 0.0 0.0 1412 52 ? S 00:58 0:06 init
```

On a Solaris box:

```
# ps -fp 1
UID PID PPID C STIME TTY TIME CMD
root 1 0 0 Jan 26 ? 0:00 /etc/init -
```

And on a Mac OS X Darwin box:

```
# ps -up 1
USER PID %CPU %MEM VSZ RSS TT STAT TIME COMMAND
root 1 0.0 0.1 1292 268 ?? SLs 0:00.00 /sbin/init
```

If for any reason the init program wasn't running, your system would be stopped dead in its tracks.

Notice that there aren't any starting options to init. Instead, the program figures out its configuration by reading the /etc/inittab file.

2. Let's focus on Linux for a while now. On Red Hat Linux, the standard /etc/inittab file looks like the following:

```
# cat /etc/inittab
#
#
```

```
# inittab    This file describes how the INIT process should set up
#            the system in a certain run-level.
#
# Author:    Miquel van Smoorenburg, <miquels@drinkel.nl.mugnet.org>
#            Modified for RHS Linux by Marc Ewing and Donnie Barnes
#
id:5:initdefault:

# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit

l0:0:wait:/etc/rc.d/rc 0
l1:1:wait:/etc/rc.d/rc 1
l2:2:wait:/etc/rc.d/rc 2
l3:3:wait:/etc/rc.d/rc 3
l4:4:wait:/etc/rc.d/rc 4
l5:5:wait:/etc/rc.d/rc 5
l6:6:wait:/etc/rc.d/rc 6

# Things to run in every runlevel.
ud::once:/sbin/update
# Trap CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have powerd installed and your
# UPS connected and working correctly.
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
# xdm is now a separate service
x:5:respawn:/etc/X11/prefdm -nodaemon
```

This might seem overwhelming, but all lines in the /etc/inittab file have the same general format:

unique ID : run levels : action : process

For example, the very last line, uniquely identified as inittab line x, only applies to run state (init level) 5, and forces a respawn of the /etc/X11/prefdm program with the -nodaemon flag specified.

![](img/5ced0c78d748bd190e9027e5549a3622_266_0.png)

> The prefdm script manages login screens within the X Window System environment.

3. Let's define the most common init levels in Table 13.1 and the known init actions in Table 13.2.

## TABLE 13.1 Common init Levels

| Level | Meaning |
|---|---|
| 0 | Halt |
| 1 | Single-user mode (also called s mode on some systems) |
| 2 | Multiuser, but no remote file systems mounted; often also no networking daemons running |
| 3 | Full multiuser mode |
| 5 | Full multiuser + X11 graphics |
| 6 | Reboot |

## TABLE 13.2 Defined init Actions

| Action | Meaning |
|---|---|
| boot | Process will be executed during system bootup |
| bootwait | Like boot, but init waits for completion |
| ctrlaltdel | Process will be executed when the console keyboard device driver receives a Control-Alt-Del key sequence |
| initdefault | Specifies the default run level to boot into on system boot |
| once | Like wait, but init doesn't wait for completion |
| respawn | Process is guaranteed to be running—the system will restart it if it dies |
| sysinit | Process will be executed during boot, but before any boot or bootwait entries |
| wait | The process will be started once (as opposed to respawn), and init will wait for it to complete |

![](img/5ced0c78d748bd190e9027e5549a3622_267_0.png)

> Many versions of Unix support a number of actions that let you gracefully interact with an uninterruptible power supply (UPS), including powerwait, powerfail, powerokwait, and powerfailnow. Read the apmd man page in Linux or the powerd man page in Solaris for more details.

It's very rare for your system to not be in init level 3 (if you have a nongraphical Unix environment) or init level 5 (if you have a graphical environment; for example, Mac OS X with Aqua enabled for the fancy graphical user interface).

4. On my Web server, for example, I have the default init level set to 3—I don't need an X Window System environment running, so I save the cycles for the Web server, SSH daemon, and so on. To see what processes init runs at this run level, I simply step through the inittab looking for all lines that contain a 3 in the run levels field.

This brings up the following list:

```
l3:3:wait:/etc/rc.d/rc 3
pr:12345:powerwait:/sbin/shutdown -c 'Power Restored; Shutdown Cancelled'
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```

Of these, the last six are simply processes to ensure that there's a listener program available for virtual consoles. The pr line matches power restore events. (By not specifying an init level in the powerfail action, you can imply that it applies to all states—flip back to the /etc/inittab we just listed to see what I mean.)

Finally, the very first line of output is probably the most important: When moving into init state 3, run /etc/rc.d/rc.3 and wait for it to complete. The rc directories contain a list of all the scripts that are executed (which ends up being the same statement as 'list of all daemons and programs automatically started') for each specific init level. The directory /etc/rc.d/rc.3 contains scripts that control what runs (or doesn't run) at run level 3. Similarly, init state 5 is a multiuser + graphical user interface, typically the X Window System. The entries in the /etc/inittab for run level 5 are the same as for run level 3, with the only exception being that run level 5 references /etc/rc.d/rc.5 instead.

![](img/5ced0c78d748bd190e9027e5549a3622_267_1.png)
