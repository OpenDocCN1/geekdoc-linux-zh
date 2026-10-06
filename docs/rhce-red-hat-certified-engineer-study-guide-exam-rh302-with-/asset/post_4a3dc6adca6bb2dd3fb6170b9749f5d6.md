
# The /etc/rc.d/rc.sysinit Script

System initialization scripts may log error messages. If the system doesn't properly start up, you should examine /var/log/messages for relevant error messages.

The remaining sections of this chapter explain these scripts and their operation in more detail. They also explain how to configure what services run at a given runlevel.

As explained, the /etc/rc.d/rc.sysinit script initializes several systems and devices. It also performs several operations. Here is a guide to the operations performed by the script; it can

- Checks for an /etc/sysconfig/network script, which sets environment variables describing the network configuration. If the /etc/sysconfig/network script exists, it executes it; otherwise, it sets environment variables that turn off networking and sets the host name to localhost.

- Source the file /etc/rc.d/init.d/functions, which contains a group of shell functions. These functions are used by scripts in the /etc/rc.d/init.d directory. Included are functions that:

    - Start a program
    - Stop a program
    - Find the process ID of a program
    - Display the status of a program
    - Display success and failure messages that help track program start-up
    - Log start-ups, shutdowns, errors, and other messages
    - Request confirmation of sensitive actions

- Display a welcome banner that includes prompt for interactive start-up

- Set the logging level.

- Mount the /proc file system, configure kernel parameters by using sysctl, and set the system clock.

- Load the default keymap if /etc/sysconfig/console/default.kmap; others load the keymap specified in /etc/sysconfig/keyboard.

- Run /sbin/setsysfont script, which sets the default system font.

- Activate the swap partitions specified in /etc/fstab.
- Set the host name and the NIS domain name, if applicable.
- Remount the root file system in read-only mode and checks its status if there is a problem with the root file system. If a serious error is found, the script starts a shell that enables you to attempt to repair the damaged file.
- Set up configured ISA plug-and-play devices.
- Remount the root file system in read-write mode.
- Check disk quotas on the root file system.
- Set up /etc/mtab, which lists mounted file systems, and /etc/HOSTNAME, which identifies the host.
- Set up support for loadable kernel modules.
- Load the sound module, if a sound card is specified in /etc/conf.modules; load the MIDI module, if a MIDI interface is specified in /etc/conf.modules.
- Load the RAID devices specified in /etc/raidtab.
- Check the non-root file systems. If a serious error is found, the script starts a shell that enables you to repair the damaged file system. Otherwise, the script checks disk quotas on the non-root file systems and mounts those specified in /etc/fstab as automatically mountable. It turns on disk quota checking, if the disk quota package is installed.
- Remove unneeded temporary files of various sorts, such as lock files.
- Initialize serial ports by running the script /etc/rc.d/rc.serial, if it exists. The /etc/rc.d/rc.serial script contains setserial commands that configure serial devices. It is not generally needed to configure standard serial ports and is included mainly for compatibility with older Linux releases.
- Load the SCSI tape module if a SCSI tape drive is present.
- Create the header file /boot/kernel.h, under some circumstances.
- Create symbolic links for /boot/System.map-kernel_version.
- Copy the boot messages to /var/log/dmesg, so that they can be read by the dmesg command.

During system start-up, the init process invokes /etc/rc.d/sysinit and then invokes /etc/rc.d/rc. Chapter 15 describes this process in detail. In order to be prepared for the RHCE exam, you should generally be familiar with the steps performed by the /etc/rc.d/sysinit script. Now that you've had a tour of the /etc/rc.d/sysinit script, complete Exercise 14.1, which requires you to study the script in more detail.

# EXERCISE 14.1

# The /etc/rc.d/rc.sysinit Script

1. Understanding the /etc/rc.d/rc.sysinit script is helpful in resolving a variety of system start-up problems. To learn more about the script, examine it and find where it performs each of the operations identified in this section.

2. The script also performs several less significant operations. Find and identify these.

# The /etc/rc.d/rc Script

The /etc/rc.d/rc script sets a new runlevel and then runs a series of scripts associated with the specified runlevel. The scripts are contained in the directories

- /etc/rc.d/rc0.d
- /etc/rc.d/rc1.d
- /etc/rc.d/rc2.d
- /etc/rc.d/rc3.d
- /etc/rc.d/rc4.d
- /etc/rc.d/rc5.d
- /etc/rc.d/rc6.d

The /etc/rc.d/rc script sets a new runlevel and then runs a series of scripts associated with the specified runlevel. The scripts are contained in the directories

| Runlevel | Description |
| :--- | :--- |
| 0 | System halt |
| 1 | Single-user |
| 2 | Multiuser mode |
| 3 | Multiuser mode |
| 4 | Unused |
| 5 | Full multiuser mode |
| 6 | System reboot |

# Runlevel Scripts

Each /etc/rc.d/init.d directory contains a series of symbolic links that refer to runlevels. The most common runlevel scripts, which are used to start and stop services, are summarized in Table 14.2.

| Script | Description |
| :--- | :--- |
| atd | AT server, which processes commands |
| autofs | Automatically mounts file systems |
| crond | CRON server, which runs commands at specified intervals |
| gpm | Mouse support for text mode |
| halt | Reboots or halts the system |
| httpd | Apache Web Server |
| inet | A variety of basic TCP/IP services |
| keytable | Loads the keyboard map |
| killall | Kills running services |
| kudzu | Checks at boot time for hardware changes |
| linuxconf | A hook that allows linuxconf to perform specified actions on start-up and shutdown |
| local | The /etc/rc.d/rc.local script, which has locally specified contents |
| lpd | LP service, which provides access to remote printers |
| named | DNS server, which provides host name and IP address lookups |
| netfs | Mounts network file systems |
| network | Activates and deactivates network interfaces |
| nfs | Network File System (NFS) server, which provides file sharing |
| pcmia | Activates and deactivates PCMCIA support |

| Script | Description |
| :--- | :--- |
| portmap | Manages RPC connections, used, for example, by NFS and NIS |
| postgresql | Database management system |
| random | Saves and restores the status of the random number generator to yield better-quality random numbers |
| reboot | Symbolic link to halt script |
| routed | RIP client and server, which automatically updates routes |
| rstatd | RSTAT server, which provides performance metrics |
| rd | RUSERS server, which helps locate users |
| rwhod | RWHO server, which lists logged-in users |
| sendmail | Mail server
| single | Puts the system in single-user-mode |
| smb | Samba (SMB) server, which provides authentication and file and printer sharing |
| sound | Saves and restores sound mixer settings |
| sshd | SSH server, which provides secure logins and remote command execution |
| syslog | Starts and stops system logging |
| xfs | The X Window System font server |
