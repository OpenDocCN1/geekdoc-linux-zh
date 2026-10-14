
## System Shutdown

One of the most important factors in the health of a system is ensuring that the data and configuration it contains are protected from corruption. It is therefore important to ensure that all applications have terminated successfully and that all their respective files are properly closed. All this must happen before the system umounts the associated drives and powers off.

Most device input/output is handled in a similar manner across the server. Improperly closed files will not contain the information expected. This could lead to the improper functioning of applications dependent on said files.

One of the most common mistakes on Linux/Unix systems is to manually eject removable media before it is dismounted (umount). When this is done, data still stored in the buffers of the device driver cannot be written to the device. Even immediately reinserting the media might not maintain the proper machine state, and the data is therefore lost. To make matters worse, in many cases, the directory structure itself is memory resident. Not writing this structure back to the device properly could mean compromising the directory's contents as well.

The same phenomenon happens with nonremovable media if the system is shut down abruptly. Great strides have been made with new file systems to protect from such losses. Consistency checks at boot time can also repair some of the damage. It is best, however, to perform an orderly shutdown at all times.

Two methods can be used to properly shut down a server. The first method is to use the init command with a parameter of zero, as shown in Table 3.1. Though this method stops all processes, it should be used only in extreme circumstances because the shutdown is rather abrupt.

A more graceful way to bring down the system is to use the shutdown command. This command brings down the system in a more orderly fashion, gives end users a proper notification of the shutdown, and forewarns other running applications to close open files. Once shutdown has been invoked, new login sessions are refused. A simplified format of the shutdown command is

```
shutdown [-h or -r] time [shutdown message]
```

In this example, the -h implies that the system will be halted after the shutdown and -r indicates that you would like to reboot. The time parameter in the command is a required field and can be the keyword now, a time specified in hh:mm format, or a specific number of minutes from now in +format. When a delay is specified in the command, shutdown will create an /etc/nologin file. Users will also be reminded of the shutdown every time half of the remaining uptime has expired. As an example, a time period of 10 minutes will see a message broadcast to interactive sessions at one-minute intervals. If the keyword now is used on the command line, no warnings, other than the first, are issued.

The last parameter is an optional message that will be sent to all currently logged-on users informing them of the shutdown. The content of the message is at your discretion.

Listing 3.4 shows a comment entered at the console by the root user as well as a notification received by all logged-on users.

```
LISTING 3.4
Comment Entered at the Console

Athena:/etc # shutdown -h +10 “Memory upgrade. Please log off”

Broadcast message from root (pts/1) (Mon Mar 21 10:38:58 2005):

Memory upgrade. Please log off
The system is going DOWN for system halt in 10 minutes!
```

The proper shutdown of a system is necessary to minimize difficulties when you restart it. Using init 0 to shut down the system does not allow other running processes sufficient time to apply any pending changes and close their files properly. This can lead to file corruption and data loss. The preferred method would be to use the shutdown command.

The interpretation of keystroke sequences is dependent on physical access to the server as well as which version of Linux is being run. In SUSE LINUX, it is possible to use YaST to configure a response to the Ctrl+Alt+Del sequence. This should be disabled as it is preferred, in almost all cases, to control the shutdown through software instead of hardware.

## Emergency Boot and Recovery

The events that orchestrate a proper, clean boot sequence are numerous. Proper daily care of your server prevents many of the potential pitfalls. Murphy’s Law, which states that if anything can go wrong, it will at the most inopportune time, certainly applies to the computing environment. Before this happens, you should have a plan.

Backups and disaster recovery will be covered in depth in Chapter 10. Before recovery can happen, you will need a bootable system and access to the devices. In most cases, you will need to get access to the system to investigate the cause of the outage before you worry about possible recovery.

The simplest cases are usually self-inflicted. For example, a kernel name was mistyped in the Grub configuration file (see Figure 3.2). Because you can edit this information at boot time, you can correct the information, boot the system, and edit the proper files to ensure the correction is made permanent. Though GRUB is gaining in popularity, LILO is not subject to this type of misconfiguration. With LILO, the kernel file must be accessible in order for it to be added to the map file. This eliminates the chance an invalid kernel will be presented at boot time.

### FIGURE 3.2
Mistyped kernel name in the GRUB configuration file.

![](img/ae8469257d2662b469f2360b3bbbe322_95_0.png)

In more difficult cases, something has happened to impede the normal boot process, and the server cannot invoke the normal boot loader. More commonly, the boot process does not complete successfully. In these instances, a separate boot environment is required. The YaST configuration tool can be used to create a rescue floppy, module floppies for nonstandard drivers, as well as a set of standard SUSE boot floppies.

It is strongly suggested that once a system is properly configured, a rescue floppy is created. The recovery process for your server will depend on it. Every time a significant change is made to your system configuration, it is important to create a new rescue floppy. It is a good idea to retain the original should your new configuration prove problematic.

Similarly, if your configuration requires specialized drivers or additional modules to function properly, you will need to make floppy versions of them as well.

### NOTE

Because you can boot your system directly from DVD or the first install CD should your boot floppies become inoperable, you will still be able to access your drives.

In such circumstances, you will have bypassed your normal boot routine. Configuration settings such as TCP/IP address and services to start at boot time will have been ignored.

Having an additional set of rescue floppies will allow you to start your system properly.

In the event of a disaster, booting from the distribution DVD/CD or the YaST boot floppies should be possible. During the boot process, you are prompted for the type of installation you would like to perform. One of the options presented is to rescue the system. Once initiated, the rescue system prompts for the rescue disk and additional module disks as required.

At the conclusion of this phase, access to the disk subsystem of the server should be accessible. Investigating the cause of the failure can now begin. In the simplest case, you can get into the appropriate configuration file and fix your error. In most cases, however, things tend not to be so simple.

Boot failures on static, stable systems are caused by hardware failures. It is beyond the scope of this chapter, and possibly this book, to explore the various causes of a system outage. Chapter 10 will explore in more detail the recovery process.

## Summary

In this chapter, we examined the processes involved in booting up an SLES server. The major steps are the POST, BIOS, initrd, the boot loader, the kernel load, and the init process. A proper understanding of the role of each process will facilitate the diagnostic phase should a failure occur.

When a system shutdown is required, it is important to ensure that the shutdown is performed in a controlled manner to avoid file corruption and data loss. There are several options available for halting a system. The preferred method is to use the shutdown command. This utility provides for the proper notification of the shutdown to system users.

We also introduced the steps necessary to provide alternate access to the system should a problem arise in the startup process. Additional techniques for recovery are discussed in Chapter 10.
