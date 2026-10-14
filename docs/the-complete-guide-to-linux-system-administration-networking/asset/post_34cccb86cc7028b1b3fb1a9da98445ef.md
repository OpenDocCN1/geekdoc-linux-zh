
When you restart your system, the new vmlinuz file is used. After restarting, execute the uname -v command to see the timestamp of the kernel you are running.

> NOTE
> Recompiling the kernel can be much more complicated than what is outlined here. For further study, refer to the README file in /usr/src/linux-2.6.5-1.358, the help screens within the configuration utilities, and the copious documentation provided in /usr/src/linux-2.6.5-1.358/Documentation and on www.linuxhq.com.

## Chapter Summary

- A backup plan helps a system administrator create an orderly system for backing up Linux data on a regular basis and restoring lost data as needed.
- A backup plan must address questions such as who is responsible for maintaining backups, which parts of each Linux file system are backed up at what intervals, and how often backups are performed.
- The dollar value and time sensitivity of the data stored on your Linux systems determines how much expense you can justify in creating a backup plan. The value of data includes several factors beyond the money paid to an employee to create the data.
- A three-level backup method is commonly used. All data is backed up monthly (level zero), and changed files are backed up weekly (level one) and daily (level two). A multilevel backup system provides a reasonable trade-off between convenience and low cost on one side, and protecting data on the other.
- Backing up the root file system and preparing to restore critical applications are parts of a backup plan that may require special attention.
- Backups should be verified regularly to be certain that data is recoverable from the backup media.
- File permissions must be part of a valid backup in order to avoid problems when files are restored.
- Compression is commonly used when backing up data, but does increase vulnerability in case of corrupted data.
- The command-line utilities tar, cpio, dump, and restore are commonly used for simple backups.
- Many free and commercial utilities are available to help system administrators manage their backup strategy. Most of these are graphical applications and include facilities for networkwide backup, managing large sets of backup media, and verifying or restoring files from backup media.
- Log files record the activities of Linux programs. The main system log used by the kernel and many daemons is /var/log/messages.

System and kernel messages are logged by the syslog and klogd daemons using the configuration in /etc/syslog.conf.

Each line in syslog.conf defines a set of messages and what action to take with those messages. Messages are defined using a selector, which is made up of a facility and a priority. The facility defines the type of program that generated the message; the priority defines the severity or type of message.

Special characters in syslog.conf let you define multiple facilities or priorities, use multiple selectors, or implement other special features.

The logger utility lets you send a message to the system logging daemon from any command line or script.

Log files must be maintained by rotating them. This is typically done using the logrotate command. Analyzing log files can help a system administrator spot problems with security or performance.

A system clock in the Linux kernel maintains a time and date for system events. This clock is initially set from the hardware clock, but can be more accurately maintained using a network time server that relies on the Network Time Protocol. The date and hwclock commands display the date and time from the system and hardware clocks, respectively.

The /proc file system lets you view details about the kernel, running processes, and other system information. You can view process information using /proc or using a number of other utilities, such as ps and top.

Kernel parameters in /proc/sys can be viewed and altered using the sysctl command. Parameter values stored in /etc/sysctl.conf are configured automatically at boot time.

The Linux kernel supports loadable modules, which are managed using the lsmod, insmod, rmmod, and modprobe commands. Module parameters define information to help modules load and operate correctly.

RAID systems let you improve speed, fault tolerance, or both, depending on the configuration you choose. Hardware-based RAID systems let you use RAID without configuring RAID as part of the Linux kernel, but they are expensive.

RAID levels include features such as mirroring and duplexing to make data redundant, striping to make data access faster, and parity information to reconstruct data when one disk in the array fails.

Using the Logical Volume Manager, you can combine multiple physical hard disks into a single logical volume group, which can then be split into partitions for separate file systems. These partitions can be expanded by adding physical storage to the system without destroying data on the existing file system.

The Linux kernel is sometimes updated by Linux vendors via a new rpm file. You can also modify the kernel source code by adding a patch file or downloading new versions of the kernel source code.

- You can modify the configuration of the Linux kernel (without changing its source code) in order to activate or deactivate features, including making features built-in instead of loadable modules.
- The kernel source code is available as an rpm package or as raw source code from www.linuxhq.com. This site also has patches to let you upgrade to a newer version of the kernel, though that is rarely necessary.
- Three kernel configuration utilities are supported: config, menuconfig, and xconfig (xconfig). Each uses the same help text and the same options, but each interface has its own advantages and disadvantages.
- Kernel configuration utilities are started using the make command, which is also used after configuration is completed to start the actual kernel compilation process. This process can take several hours on a slower machine.
- The new kernel is located in /usr/src/linux-2.6.5-1.358/arch/i386/boot. It must be copied to /boot to make it usable and may require that you update or modify your boot manager to use the new kernel. You can also create a boot floppy disk using make bzdisk, though the default kernel configuration cannot fit on a floppy.

## COMMAND SUMMARY

| Command | Description | Example |
|---|---|---|
| apropos | Displays any man pages with information on the specified term. | apropos lvm |
| ark | Graphical backup (archiving) utility; part of the KDE desktop. | ark |
| config | Option used to configure the Linux kernel using interactive command-line entries; must be used with the make command while in an appropriate Linux kernel source code directory (such as /usr/src/Linux-2.6.5-1.358). | make config |
| date | Displays the date and time stored by the system clock. | date |
| dd | Copies data from one device to another, without any processing by the command. | dd if=/mnt/cdrom/images/bootdisk.img of=/dev/fd0 |
| depmod | Creates a file listing dependencies between all kernel modules available on the system for use by the modprobe command. Normally executed only as part of system startup scripts. | /sbin/depmod -a |
| dump | Stores files for backup. | dump -0u -f /dev/st0 /home |
| hwclock | Displays the date and time stored by the hardware clock, or updates those values. | hwclock |
| insmod | Adds a kernel module to the running kernel. The *modprobe* command is normally used instead of this command because *modprobe* automatically adds modules that are prerequisite to the one requested. | insmod ne2000 |
| klogd | A daemon used to log kernel messages according to the configuration given in the syslog.conf configuration file; started by scripts at start-up. | klogd |
| logger | A program that lets you send a message to the syslog function; messages are written to the log files according to the configuration in syslog.conf. | logger -p mail.info -t compressor Mail folders compressed |
| logrotate | A program that manages the rotation of multiple log files at regular intervals according to the logrotate.conf configuration file. | logrotate /etc/logrotate.conf |
| lsmod | Lists all modules currently installed in the Linux kernel. | lsmod |
| lvm | The Logical Volume Manager utility; only used when logical volume groups have been configured. | lvm |
| make | Performs actions defined in a Makefile, usually compiling a collection of source code into a finished binary program and preparing or installing that program. | make xconfig |
| makewhatis | Creates an internal database of man page information for use by the *whatis* command. | makewhatis |
| menuconfig | Option used to configure the Linux kernel using a text-based menu system; must be used with the *make* command while in an appropriate Linux kernel source code directory (such as /usr/src/Linux-2.6.5-1.358). | make menuconfig |
| modinfo | Displays information about a named kernel module. | modinfo ext3 |
| modprobe | Adds a kernel module to the running kernel, including any prerequisite modules. | modprobe ne2000 |
| patch | Updates source code files using a patch file that contains modifications to one or more source code files. | patch -p0 < patch_file |
| restore | Restores files that have been archived using the *dump* command. | restore rf /dev/st0 |
| rmmod | Removes a kernel module from the kernel. | rmmod ne2000 |
| sysctl | Views or modifies a kernel parameter via the /proc file system. | sysctl -w net.ipv4.ip_forward=1 |
