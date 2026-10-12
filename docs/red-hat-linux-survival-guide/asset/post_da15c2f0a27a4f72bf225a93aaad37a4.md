
## Shutting Down Your System

Shutting down a Linux system is simple but not as simple as powering down the computer. You should never turn off a computer running Linux without shutting down Linux itself. In this section I show you how to shut down properly.

### Shutting down by using the shutdown command

The shutdown command is the most typical method of shutting down a system. shutdown broadcasts a warning message to all logged-in users that the system is changing run level. The shutdown command instructs init to change the current run level of the system to either halt (run level 0) or reboot (run level 6). For example, the following command tells init to switch the system to run level 0 (halt) immediately:

```
shutdown -h now
```

![](img/9eb7e89292d2f85707b4d49102c865b7_97_0.png)

shutdown can also be used to reboot the system by substituting the -r option for the -h option in the preceding command. The -r option is discussed in the "Rebooting Your System" section later in this chapter.

The shutdown command also provides you with an option to schedule the shutdown event for a later time. For example, the following command halts the system in 10 minutes:

```
shutdown -h +10
```

All logged-in users receive a message saying that the system is going to halt shortly, allowing them to finish up and save their work.

![](img/9eb7e89292d2f85707b4d49102c865b7_97_1.png)

When you use a delayed shutdown command, as described in this section, users who are logged in see a message warning them that the system will shut down soon. However, shutdown does not prevent anyone from logging in during the shutdown countdown period, and anyone who does log in during this period will not receive the warning. In order to prevent new logins when the shutdown command is pending, you can create a text file called /etc/nologin with an appropriate message stating that a system shutdown has already been scheduled and that people should try to log in at a later time. Do not forget to rename or delete the /etc/nologin file after you reboot. If you are rebooting a server remotely, be absolutely sure to remove or rename this file prior to the actual shutdown. No user accounts except root are allowed to log in when this file is present. In fact, you may want to add the rm -f /etc/nologin at the end of the /etc/rc.local script and make sure that init runs it at the end of run level 3.

### Shutting down your system with init

You can run init to manually halt your system. For example, the following command halts the system immediately:

```
init 0
```

If you are running in a multiuser mode (run level 3), this command is not the best approach, because it does not inform the users on the system that the system is going to halt. Instead, you can use the shutdown command to halt the server, as described in the “Shutting down with the shutdown command” section earlier in this chapter.

### Canceling a shutdown

The shutdown command enables you to schedule a shutdown event at a later time (as discussed in the “Shutting down with the shutdown command” section earlier in this chapter). However, before the system actually shuts down, a need might arise to cancel the shutdown event; in such a case you issue another shutdown command with a -c option to cancel any scheduled shutdown event as follows:

```
shutdown -c
```

### Automatic shutdown on power failure

If you use a UPS (uninterruptible power supply) to provide backup power for your system and it uses a serial port-based UPS monitoring software (usually supplied by the UPS vendor), you can use init to shut down the system gracefully when your UPS power is nearly drained. The default /etc/inittab includes the following line:

```
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"
```

This line tells init to run shutdown in case of a power failure. The powerfail action is activated when a UPS program or powerd (a power monitoring daemon) sends the SIGPWR signal to init. The default setting allows the system to run on UPS power for two minutes before it halts. If your UPS is capable of sustaining power for a greater or lesser amount of time, you should modify this value by changing +2 to a desired number of minutes. For example, to change it to five minutes, change +2 to +5.

If you restore your primary power source before your UPS power is totally drained, you can call init to cancel a previously scheduled shutdown event. You can do this by adding the following line in /etc/inittab:

```
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"
```

When init receives a SIGPWR signal and a file called /etc/powerstatus contains an “OK” string in it, the powerokwait action is activated and the shutdown is aborted.

## Rebooting Your System

In addition to running the init command to halt your system (init 0), you can also run init manually to reboot your system with the following command:

```
init 6
```

Just as with using the init command to reboot, if you are running in a multiuser mode (run level 3), this command is not the best approach, because it does not inform the users on the system that the system is going to reboot. Instead, you can use the shutdown command to reboot the server. For example, to reboot immediately, you can run the following command:

```
shutdown -r now
```

Or, you can schedule a reboot for some time in the future. For example, the following command reboots the server in 10 minutes:

```
shutdown -r +10
```

All logged-in users receive a message saying that the system is going to reboot shortly. This allows them time to finish up and save their work.

![](img/9eb7e89292d2f85707b4d49102c865b7_100_0.png)

The shutdown command does not prevent new users from logging into the system while a reboot is pending. See the section “Shutting down with the shutdown command” earlier in this chapter for more information on how to (very carefully) use the /etc/nologin file to prevent users from logging in during this time.

### Rebooting with Ctrl+Alt+Delete

If you are on the system console, you can use the traditional Ctrl+Alt+Del key combination to reboot your system. This is possible because of the following line in /etc/inittab:

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now
```

This line allows init to trap the Ctrl+Alt+Del key combination and call the shutdown script to reboot immediately.

![](img/9eb7e89292d2f85707b4d49102c865b7_100_1.png)

Anyone who has physical access to your system console can shut down the system by pressing the Ctrl+Alt+Delete keys. To protect yourself from such a shutdown, you can create a file called /etc/shutdown.allow that will contain a list of users (one username per line) who are allowed to shut down the system. The root account does not need to be listed in this file.

## Configuring init

As mentioned earlier in the chapter, init is the very first program that the kernel runs at the end of the boot sequence. There are two main versions of the init program: a UNIX System V-like init and a BSD-like init. The difference between the two flavors of init is that System V-ish init uses run levels and the BSD-ish init does not.

![](img/9eb7e89292d2f85707b4d49102c865b7_101_0.png)

Red Hat Linux comes with the UNIX System V version of init, and so all discussion about init in this chapter is limited to this version.

### /etc/inittab: The init configuration file

Because init is the first program that is run by the kernel at boot time, its process ID (PID) is 1. When init starts up, it reads a configuration file called /etc/inittab. Listing 4-1 shows the /etc/inittab file in a typical Red Hat Linux system.

### Listing 4-1 A typical /etc/inittab file

```
#
# inittab - This file describes how the INIT
#           process should set up the system in
#           a certain runlevel.
#
# Author: Miquel van Smoorenburg,
#         <miquels@drink...>
#
# Modified for RHS Linux by Marc Ewing and
# Donnie Barnes
#
# Default runlevel. The runlevels used by RHS are:
#   0 - halt (Do NOT set initdefault to this)
#   1 - Single-user mode
#   2 - Multi-user, without NFS (The same as 3, if you
#       do not have networking)
#   3 - Full multi-user mode
#   4 - unused
#   5 - X11
#   6 - reboot (Do NOT set initdefault to this)
#
id:3:initdefault:
```
