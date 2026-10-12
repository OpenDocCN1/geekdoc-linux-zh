
c, which are equivalent to A, B, and C). The next field represents the type of action to be taken by init (valid actions and the results of those actions are listed in Table 12-3), and the last field is the actual command that is to be executed.

## Table 12-3: Valid init Actions

| Action | How the Command Is Run |
| :--- | :--- |
| `once` | The command is executed once when entering the specified run level. |
| `wait` | The same as `once`, but init waits for the command to finish before continuing with other inittab entries. |
| `respawn` | The process is monitored, and a new instance is started if the original process terminates. |
| `powerfail` | The command is executed on receiving a SIGPWR signal from software associated with an UPS unit. |
| `powerwait` | The same as `powerfail`, but init waits for the command to finish. |
| `powerwaitok` | The command is executed on receiving a SIGPWR signal if the `/etc/powerstatus` file contains the word OK. This is generally accomplished by the UPS software, and indicates that a normal power level has been restored. |
| `ondemand` | The command is executed when init is manually instructed to enter one of the special run levels a, b, or c (equivalent to A, B, and C, respectively). No change in run level actually takes place. The program is restarted if the original process terminates. |
| `sysinit` | The command is executed during the system boot phase; the runlevels field is ignored. |
| `boot` | The command is executed during the system boot phase, after all `sysinit` entries have been processed; the runlevels field is ignored. |
| `bootwait` | The same as `boot`, but init waits for the command to finish before continuing with other inittab entries; the runlevels field is also ignored. |
| `initdefault` | The run level to enter after completing the `boot` and `sysinit` actions. |
| `off` | Nothing happens (perhaps useful for testing and debugging). |
| `ctrlaltdel` | Traps the Ctrl+Alt+Del key sequence, and is typically used to gracefully shut down the system. |
| `kbdrequest` | Used to trap special key sequences, as interpreted by the keyboard handler. |

### Breakdown of the inittab file

Because the inittab file is a configuration file and not a sequential shell script, the order of lines is not significant. Lines beginning with a # character are considered comments and are not processed.

The first noncommented line in the preceding sample inittab file sets the default run level to 3. A default of 3 means that, following the completion of all commands associated with the sysinit, boot, and bootwait actions, run level 3 will be entered (booting to a text-based login). The other common initdefault level is run level 5 (booting to a GUI). Table 12-4 describes each of the run levels and helps you choose the run level that is best suited as the default in your environment.

### Table 12-4: Possible Run Levels

| Run Level | What Happens in This Run Level |
| :--- | :--- |
| 0 | All processes are terminated and the machine comes to an orderly halt. As the inittab comments point out, this is not a good choice for initdefault, because as soon as the kernel, modules, and drivers are loaded, the machine will halt. |
| 1, s, S | This represents single-user mode, which is most frequently used for system maintenance and in situations where it may be preferable to have few processes running and no services activated. In single-user mode, the network is nonexistent, the X server is not running, and it is possible that some file systems are not mounted. |
| 2 | Multiuser mode. Multiple user logins are allowed, all configured file systems are mounted, and all processes except X, the at daemon, the xinetd daemon, and NIS/NFS are started. If your machine doesn't have (or perhaps doesn't need) a permanent network connection, this is a good choice for initdefault. |
| 3, 4 | Multiuser mode with network services. Run level 3 is the typical value for initdefault on a Red Hat Linux server, but run level 4 (generally left to be user-defined) is almost identical in a default Red Hat Linux configuration. |
| 5 | Multiuser mode with network services and X. This run level starts the X server and presents a graphical login window, visually resembling any of the more expensive UNIX-based workstations. This is a common initdefault value for a Red Hat Linux workstation. |
| 6 | All processes are terminated and the machine is gracefully rebooted. Again, the comments in the inittab file mention that this is not a good choice for initdefault, perhaps even worse than run level 0. The effect is a possibly infinite cycle of booting, followed by rebooting. |
| 7, 8, 9 | Generally unused and undefined, these run levels have the potential to meet any needs not covered by the default options. |
| a, b, c, A, B, C | Used in conjunction with the ondemand action. These don't really specify a run level but can launch a program or daemon "on demand" if so instructed. |

> **NOTE: If there is no initdefault specified in the inittab file, the boot sequence will be interrupted and you will be prompted to specify a default run level into which the machine will boot.**

The next line in the inittab file instructs init to execute the /etc/rc.d/rc.sysinit script before entering the default run level. This script performs many initialization routines such as choosing a keymap file, checking and mounting the root and proc file systems, setting the clock and host name, configuring swap space, cleaning up temporary files, and loading system modules.

The seven following lines control the commands executed within each major run level. In each, the /etc/rc.d/rc script is called, using the desired run level as an argument. It, in turn, descends into the appropriate directory tree (for example, the /etc/rc3.d directory is entered for run level 3).

The next line specifies that no matter what run level the machine is in, the update daemon should be running. The update daemon is a program that flushes kernel buffers from memory to disk (generally every 30 seconds) to ensure that, in the event of an unintended shutdown, a minimum amount of data is lost.

The ctrlaltdel tells init to perform exactly what PC users would expect if the Ctrl, Alt, and Delete keys were pressed simultaneously. The system reboots itself in an orderly fashion (a switch to run level 6) after a three-second delay.

The next two lines (with their comments) deal with graceful shutdowns if you have an uninterruptible power supply (UPS) and software installed. The first line initiates a halt (a switch to run level 0) two minutes after receiving a signal from the UPS indicating a power failure. The second line cancels the shutdown in the event that power is restored.

The six getty lines start up virtual consoles to allow logins. These processes are always running in any of the multiuser run levels. When someone connected to a virtual console logs out, that getty process dies, and the *respawn* action instructs *init* to start a new *getty* process.

The last line indicates that as long as the system is in run level 5, the “preferred display manager” (*xdm*, *gnome*, *KDE*, etc.) will be running. This presents a graphical login prompt rather than the usual text-based login, and eliminates the need to run *startx*.

## System Start-up and Shutdown

During system start-up, a series of scripts are run to start the services that you need. These include scripts to start network interfaces, mount directories, and monitor your system. Most of these scripts are run from subdirectories of */etc/rc.d*. The program that starts most of these services up when you boot and stops them when you shut down is the */etc/rc.d/rc* script. The following sections describe run-level scripts and what you can do with them.

### Starting run-level scripts

As previously mentioned, the */etc/rc.d/rc* script is a script that is integral to the concept of run levels. Any change of run level causes the script to be executed, with the new run level as an argument. This simple yet powerful script is shown and discussed here:

```bash
#!/bin/bash
#
# rc        This file is responsible for starting/stopping
#           services when the runlevel changes. It is also
#           responsible for the very first setup of basic
#           things, such as setting the hostname.
#
# Original Author:
#       Miquel van Smoorenburg, <miquels@cdrinker.nl.mugnet.org>
#
# Now find out what the current and what the previous runlevel are.
argvi="$1"
set `/sbin/runlevel`
runlevel=$2
previous=$1
export runlevel previous

# Source function library.
```
