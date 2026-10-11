
- Any device drivers that are loaded
- The amount of swap space
- Network adapters and settings

See Chapter 10, “Administrative Tasks,” for more information on this log file and using the dmesg command.

After the kernel has started, it mounts your root filesystem, usually located on your hard disk. After mounting the root, the control is handed over to the hard disk with the kernel remaining in memory.

## The init Daemon

The last thing the kernel does is invoke the init daemon, which stays active until you shut down your system. It is responsible for creating processes that the rest of the system will use, such as login shells. The init daemon will also restart certain processes when they exit. For example, when you log out, init restarts the console so you can log in again.

The init daemon’s actions are controlled by its configuration file, /etc/inittab.

## The /etc/inittab File

Each line of the /etc/inittab file contains four fields separated by a colon:

```
ID:runlevel:action:process
```

Table 2.1 shows what each field contains.

### Table 2.1 Fields and the Purpose of the Lines in the /etc/inittab File

| Field | Contents and Purpose |
| --- | --- |
| ID | One or two characters identifying the entry, usually the device name |
| runlevel | Indicates to which runlevels this line will apply; multiple runlevels can be listed; if blank, will apply to all runlevels |
| action | How to handle the entry; see Table 2.2 for valid entries |
| process | Command to execute |

The action field indicates how to handle the command, such as whether to restart the command if it stops. Table 2.2 shows the valid entries for this field.

### Table 2.2 Valid Entries for the action Field in the /etc/inittab File

| Entry | Description |
| --- | --- |
| boot | Runs when /etc/inittab is first read |
| bootwait | Runs when /etc/inittab is first read after the boot entries |
| initdefault | Sets initial runlevel; stops the process if it is running; starts process only once after |
| ondemand | Keeps process running; restarts if it stops |
| powerfail | Executed upon receipt of a power failure signal |
| sysinit | Execute before executing console |
| respawn | Keeps process running; restarts the process if it stops |
| wait | Starts process once |

The **init** process is used to start the kernel and any processes it needs to get your system up and running. If you want an application to start every time your system boots, enter that command in one of the rc scripts, which are discussed in the next section, “Runlevels.”

## Runlevels

A *runlevel* defines a set of processes to start as part of booting the system. This can range from a minimal amount of processes such as those used for system administration to a configuration supporting all configured devices.

The numbers associated with various runlevels differ depending on the distribution you're using and are listed in the /etc/inittab file. For example, the listing might look like

```
# Default runlevel. The runlevels used by RHS are:
# 0 - halt (Do NOT set initdefault to this)
# 1 - Single user mode
# 2 - Multiuser, without NFS (The same as 3, if you do not have networking)
# 3 - Full multiuser mode
# 4 - unused
# 5 - X11
# 6 - reboot (Do not set initdefault to this)
```

The runlevels **0** and **6** are reserved only for **halt** and **reboot**, respectively. The runlevels can vary from distribution to distribution. No matter what distribution you have installed, the init daemon processes only those lines associated with the current runlevel.

The single-user mode is a little different from all the rest of the available runlevels. This runlevel is often used for system administration tasks such as recovering a corrupt filesystem. No other users can log in while the system is in this runlevel. However, you can still run multiple applications at the same time. This is the only time that init does not read the /etc/inittab file. Rather, the default action is to run the /bin/su command and you are logged in as the superuser or root.

When starting at a runlevel higher than the single-user mode, the system starts up in multiuser mode. In this mode, init executes those lines with an action of sysinit, boot, or bootwait. Frequently, these lines mount the filesystems.

Next, the init daemon will execute all the other lines that are listed with the present run-level in the runlevel field.

Your initial runlevel is defined by the line

```
id:3:initdefault:
```

Notice that this line does not define any processes to start, but rather defines the runlevel with which to start. You can change the runlevel by using the command init. Its syntax is

```
init [runlevel]
```

The init command takes a runlevel as an argument. You can specify how long to wait before changing the runlevel by using the telinit command with the -t seconds option. The default delay is 5 seconds. The telinit command is a link to the init command. Be sure that you notify any logged on users before changing the runlevel.

For example, the command

```
init 5
```

will change the runlevel to level five. init first sends a signal to stop any processes running that are not defined for the new runlevel. After the specified delay, telinit then sends a kill signal to these processes. It then starts any processes defined for the new run-level that are not already running.

You also can change to single-user mode by passing either s or S to the init or telinit commands.

The next section in the /etc/inittab file defines the startup scripts to run, as in

```
si::sysinit:/etc/rc.d/rc.sysinit
```

The ID si at the beginning of the line is used internally by the init daemon. This line starts the script rc.sysinit, which handles tasks such as activating the swap partition, running fsck, and mounting your filesystems. The fsck command checks the filesystem for corrupt entries and is discussed in more detail in Chapter 6, “Maintaining the Filesystem.” This script can vary depending on your distribution. Read the one located on your system to get the details of what it accomplishes.

The next section in the `/etc/inittab` file runs scripts appropriate to your runlevel, which are located in the `/etc/rc.d` directories:

```
1:1:wait:/etc/rc.d/rc 1  
12:2:wait:/etc/rc.d/rc 2  
13:3:wait:/etc/rc.d/rc 3  
14:4:wait:/etc/rc.d/rc 4  
15:5:wait:/etc/rc.d/rc 5  
16:6:wait:/etc/rc.d/rc 6
```

This is accomplished by calling the `rc` script with an argument identifying the runlevel. The `rc` script then runs the scripts located in the `rcn.d` directory, in which `n` represents the runlevel. Your system can execute other startup scripts, such as `/etc/rc.local`, depending on your distribution.

Your `rc` scripts also can call *modules*. These are pieces of kernel code that can be loaded and unloaded while your system is running. These modules are most frequently device drivers for devices you can't use all the time.

You can use the `/etc/conf.modules` file to pass parameters to each module at the time it is loaded. These parameters are frequently `I/O` addresses and interrupts. A sample `conf.modules` file is

```
alias eth0 3c59x  
alias sound 0s1370
```

This loads the modules necessary for the Ethernet card and sound card.

Next are the processes that should be run at every runlevel. These usually include starting a `getty` process, which creates each of the virtual terminals.

Your `inittab` file also can contain instructions as to what to do if a power failure occurs and what to do if the power comes back up. An example is

```
# When our UPS tells us power has failed, assume we have a few minutes  
of power left. Schedule a shutdown for 2 minutes from now.  
# This does, of course, assume you have powered installed and your  
# UPS connected and working correctly.  
  
pf::powerfail:/sbin/shutdown -f -h +2 'Power Failure; System Shutting Down'  
  
# If power was restored before the shutdown kicked in, cancel it.  
pr:12345:powerokwait:/sbin/shutdown -c 'Power Restored; Shutdown Cancelled'  
# Run gettys in standard runlevels  
1:2345:respawn:/sbin/mingetty tty1  
2:2345:respawn:/sbin/mingetty tty2  
3:2345:respawn:/sbin/mingetty tty3
```
