
also known as init, as configured through the newer Upstart system with related files in the /etc/init directory.

Linux services are controlled in part by runlevel. While RHEL 6 uses the Upstart system, the default runlevel is still configured in /etc/inittab, and the service scripts in the /etc/rcn.d directories, where n represents the runlevel, determine which services are started and stopped. The status of those scripts in each runlevel can be configured with the chkconfig command (along with other tools). Runlevel scripts are linked to real scripts in the /etc/init.d directory, which can be used to start, stop, restart, reload, even status a service, and more.

For most users, network configuration is also an important part of the boot process. Most related configuration files can be found in the /etc/sysconfig/network-scripts directory. While you can modify the network configuration with the ifup, ifdown, ifconfig, and route, and dhclient commands, you can detail the current status of the network with the ifconfig, route, netstat, and arp commands. If you prefer to configure with administrative tools, RHEL 6 includes Network Manager and system-config-network packages.

You may need to set up local systems as NTP clients. The Date/Time Properties tool can help configure key configuration files such as /etc/sysconfig/ntp and /etc/ntp.conf.

![](img/9139201cfcaf4292284a0eed074928e5_314_0.png)

## TWO-MINUTE DRILL

Here are some of the key points from the certification objectives in Chapter 5.

### The BIOS and the UEFI
- While not strictly a part of the exam, it's important to know the basics of the BIOS and the UEFI.
- You can change the boot sequence from the BIOS/UEFI menu.
- Once the BIOS/UEFI detects a designated boot drive(s), it hands control to GRUB via the master boot record (MBR) of the appropriate drive.

### Bootloaders and GRUB
- RHEL 6 uses the traditional version of GRUB, version 0.97.
- The GRUB configuration file is organized in stanzas.
- From the GRUB menu, you can boot into a runlevel other than the default. You can even boot into a runlevel that provides root administrative access without an account password.
- The GRUB menu, along with individual options, can be password-protected.
- The GRUB configuration file specifies a kernel, a root directory volume, and an initial RAM disk for each operating system.
- If the GRUB configuration file is missing, you may be able to boot from the grub> prompt with information on the /boot directory partition, the Linux kernel file, the top-level root directory, and the Initial RAM disk file.

### Between GRUB and Login
- You can analyze boot messages through /var/log/dmesg or the dmesg command.
- There are six different runlevels available; the default is configured in /etc/inittab.
- Upstart has replaced SysVInit, with configuration files in the /etc/init directory.
- Once the kernel boots, it hands control to init, also known as the First Process.
- Different services are started based on the default or chosen runlevel.

### Control by Runlevel
- The default runlevel configured in /etc/inittab runs scripts in the associated /etc/rcn.d directory, where n is the runlevel.
- Runlevel scripts in the /etc/rcn.d directories are links to actual scripts in the /etc/init.d directory.
- You can use runlevel scripts in the /etc/init.d directory to control a service with the start, stop, restart, reload, and other commands.
- The services that start in each runlevel can be controlled with the chkconfig command, as well as the tools associated with the ntsysv and system-config-services commands.

### Network Configuration
- Important network configuration commands include ifup, ifdown, ifconfig, route, netstat, and arp.
- Key network configuration files are located primarily in the /etc, /etc/sysconfig, and /etc/sysconfig/network-scripts directories.
- You can edit the network configuration files directly, or configure network connections with the tools available through the system-config-network-tui or nm-connection-editor commands
- Name resolution depends on appropriate settings in the /etc/resolv.conf, /etc/hosts, and /etc/nsswitch.conf files.

### Time Synchronization
- The NTP service can help keep systems in sync with servers configured in the /etc/ntp.conf file.
- NTP clients can be configured with the Date/Time Configuration tool.

![](img/9139201cfcaf4292284a0eed074928e5_316_0.png)

## SELF TEST

The following questions will help measure your understanding of the material presented in this chapter. As no multiple-choice questions appear on the Red Hat exams, no multiple-choice questions appear in this book. These questions exclusively test your understanding of the chapter. It is okay if you have another way of performing a task. Getting results, not memorizing trivia, is what counts on the Red Hat exams. There may be more than one answer for many of these questions.

### The BIOS and the UEFI
1. On what part of the boot hard drive is the first stage of the GRUB bootloader typically located?

### Bootloaders and GRUB
2. When you see the GRUB configuration menu, what command would you use to modify the kernel arguments? Assume that GRUB is not password-protected.
3. What command would you enter at the kernel command line to boot into single-user mode?
4. If you see the root(hd0,1) directive in the GRUB configuration file, on what partition is the /boot directory? Assume the GRUB configuration file is properly configured.

### Between GRUB and Login
5. What temporary file system is loaded directly from the GRUB menu?
6. What one-word command can you use to read the kernel initialization messages?
7. In what directory can you find the configuration files associated with the first process?
8. What is the name of the system that controls splash screens, configured in the /etc/init directory?

### Control by Runlevel
9. In what directory can you find the scripts that control services? Hint: scripts in specific run-levels are linked to the actual scripts in this directory.
10. Name three actions that can be typically run from scripts in the directory associated with question 9.

### Network Configuration
11. What command lists all network devices currently available on the local system, including those that are not active?
12. What command lists the current routing table of the local system?

### Time Synchronization
13. What command starts the GUI-based configuration tool for time synchronization?

## LAB QUESTIONS

Several of these labs involve installation exercises. You should do these exercises on test machines only. The second Lab of Chapter 1 sets up KVM for this purpose. However, some readers may not have hardware that supports KVM. Options to KVM include virtual machine solutions such as VMware, available from www.vmware.com, or Virtualbox, open-source edition, available from www.virtualbox.org. Red Hat presents its exams electronically. For that reason, most of the labs in this and future chapters are available from the CD that accompanies the book, in the Chapter5 subdirectory. It's available in .doc, .html, and .txt formats, in the filename starting with 56505-labs. In case you haven't yet set up RHEL 6 on a system, refer to the first lab of Chapter 2 for installation instructions. The answers for each lab follows the Self Test answers for the fill-in-the-blank questions.

## SELF TEST ANSWERS

### The BIOS and the UEFI
- 1. For the BIOS/UEFI to hand control over to Linux, it needs to identify the Master Boot Record (MBR) of the boot hard drive.

### Bootloaders and GRUB
- 2. From the GRUB menu, the command that modifies kernel arguments is e.
- 3. To boot into single-user mode from the GRUB kernel command line, you'd enter the 1 command; while not identical, single is also acceptable.
- 4. The root (hd0,1) directive documents the /boot directory on the second partition on the first hard drive.

### Between GRUB and Login
- 5. The temporary filesystem loaded from the GRUB menu is the initial RAM disk filesystem, also known by its filename, initramfs.
- 6. The one-word command that you can use to read the kernel initialization messages is dmesg.
- 7. The configuration files associated with the first process are located in the /etc/init directory.
- 8. The name of the system that controls splash screens on RHEL 6 is Plymouth.

### Control by Runlevel
- 9. Scripts that control services are located in the /etc/init.d directory. The /etc/rc.d/init.d directory is also an acceptable answer. While there are scripts that qualify in other directories, /etc/init.d is the location for the great majority of such scripts.
- 10. Typical actions that can be run from scripts in the /etc/init.d directory include start, stop, restart, reload, and more. Any of the actions listed near the end of a file in that /etc/init.d directory is an acceptable answer.

### Network Configuration
- 11. The ifconfig -a command lists all detected network devices, active and inactive.
