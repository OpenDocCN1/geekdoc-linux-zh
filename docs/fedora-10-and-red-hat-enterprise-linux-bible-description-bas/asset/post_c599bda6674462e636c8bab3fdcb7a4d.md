
# Part III: Administering Fedora and RHEL

2. **Start boot loader** — After checking that no bootable operating system is ready to boot in its floppy, CD, or DVD drive, the BIOS checks the master boot record on the primary hard disk to see what to load. With Fedora or RHEL installed, the GRUB boot loader is started, allowing you to choose to boot Fedora, RHEL, or another operating system.

3. **Boot the kernel** — Assuming that you select to boot Fedora or RHEL, the Linux kernel is loaded. That kernel manages the basic file systems and transfers control to the init process. The rest of this section describes what happens after the kernel handles control of system startup to the init process.

# Starting init

In the boot process, the transfer from the kernel phase (the loading of the kernel, probing for devices, and loading drivers) **init** is indicated by the following lines:

> Welcome to Fedora
Press "I" to enter interactive startup.

The init program, part of the always RPM package, is now in use. The output from ps lists **init** (known as "the father of all processes") as PID (process identifier) 1.

Prior to Fedora 9, a special script, `/etc/initab`, directed the actions of the init program. Starting in Fedora 9, a new initialization system replaced the older SysV Unix-init program.

With upstart, `/etc/initab` controls only the default run level. Everything else gets run from a special script for each run level, `/etc/event.d/rc5` for run level 5. Upstart is based on the concept of launching programs based on events rather than run levels. Upstart can restart services, and it's as fragile as the older SysV init system.

Since many Linux programs make assumptions about the init system, though, upstart operates under a compatibility mode. To understand upstart, init run levels, you need to understand the older Linux and Unix run levels, described in the following section. For a number of Fedora releases, upstart will gradually fade out methods to initialize Linux. For now, though, the concepts still apply.

# The inittab file

The following example shows the contents of the `/etc/inittab` file as it is delivered with Fedora and RHEL in versions prior to Fedora 9:

```
# inittab          This file describes how the INIT process should set up
               the system in a certain run level.
#                  
```

# Chapter 12: Automating System Tasks 511

```
id:5:initdefault:
```

```
# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:0:wait:/etc/rc.d/rc 1
12:0:wait:/etc/rc.d/rc 2
13:0:wait:/etc/rc.d/rc 3
14:0:wait:/etc/rc.d/rc 4
15:0:wait:/etc/rc.d/rc 5
16:0:wait:/etc/rc.d/rc 6

# Trap CTRL-ALT-DELETE
ca::ctrlaltd:/sbin/shutdown -t3 -r now
```

- * When our UPS power has failed, assume we have a few minutes of power left. Schedule a shutdown for 2 minutes from now.
- * This does, of course, assume you have power installed and the UPS connected and working correctly.
pf:powerfail:/sbin/shutdown -f -h v2 "Power Failure; System Shutting Down"

- * If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

- Run getys in standard runlevels
1:22345:respawn:/sbin/minetty tty1
2:22345:respawn:/sbin/minetty tty2
3:22345:respawn:/sbin/minetty tty3
4:22345:respawn:/sbin/minetty tty4
5:22345:respawn:/sbin/minetty tty5
6:22345:respawn:/sbin/minetty tty6

- * Run xdm in runlevel 5
x5:0:once:/etc/X11/prefdm -nodaemon

The plain-text initab file contains several colon-separated fields in the format:

```
id:runlevels:action:command
```

The id field is a unique identifier, one to four alphanumeric characters in length, that represents a particular action to take during system startup. The runlevels field contains a list of run levels in which the command will run. Common run levels are 0, 1, 2, 3, 4, 5, and 6 (s and S single-user mode, which is equivalent to 1). Run levels 7, 8, and 9 can also be used for the special run levels associated with the on-demand action (a, b, and c, which are equivalent to A, B, and C). The next field represents the type of action to be taken by init (valid actions and the results of those actions are listed in Table 12-3), and the last field is the actual command that is to be executed.

![](img/63c86e1d25a0e2be7e9f6de6b6f02)

# Table 12-3: Valid Actions

| Action | How it Is |
|---|---|
| once | The command is executed once. |
| wait | The command is executed and then waits for an event. |
| respawn | The command is restarted repeatedly if it exits. |
| powerfail | The command is executed when power failure occurs. |
| powerokwait | The command is executed and waits until power is restored. |
| powerfailnow | The command is executed immediately when power failure occurs. |
| demand | The command is executed as an on-demand action. |
| sysinit | The command is executed during system initialization. |
| boot | The command is executed during the boot process. |
| bootwait | The command is executed during boot and waits for completion. |
| default | The command is executed in the default run level. |
| off | Nothing is executed. |
| ctrlaltd | The command is executed when Ctrl-Alt-Del is pressed. |
| krequest | The command is executed upon a keyboard reboot request. |

# Table 12-4: Possible Run Levels

| Run Level | What Happens in This Level |
|---|---|
| 0 | All processes are terminated and the machine comes to an orderly halt. |
| 1, s, S | This is single-user mode, used for system maintenance. |
| 2 | Multiser mode. Multiple users are logged in, all configured file systems are mounted. |
| 3 | Multiser mode with network services. This is the typical value for initdefault on a server. |
| 4 | Run level 4 is available as a user-defined run level. |
| 5 | Multiser mode with network services and X. This is a common initdefault for a desktop. |
| 6 | All processes are terminated and the machine is gracefully rebooted. |
| 7, 8, 9 | Generally unused and undefined. |
