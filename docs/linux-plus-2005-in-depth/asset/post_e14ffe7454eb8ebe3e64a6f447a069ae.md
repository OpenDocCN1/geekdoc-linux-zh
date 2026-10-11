
The absence of a device driver also prevents the operating system from using the associated hardware device. Normally, the **kudzu program** runs at each boot time, detects new hardware devices, and configures the device driver for them automatically. For example, if you add an Ethernet NIC card to the system, simply boot the computer, and the screen depicted in Figure 13–3 is displayed. Pressing Enter at this screen allows you to configure the new hardware, as shown in Figure 13–4.

If a hardware device is not detected by kudzu, the device driver for it must be configured manually. Device drivers can be inserted into the kernel as modules or can be compiled directly into the kernel. These topics are discussed later in this chapter.

![](img/09bf13b782f71165e17bb3839040c96a_513_0.png)

FIGURE 13–3 *The kudzu welcome screen*

![](img/09bf13b782f71165e17bb3839040c96a_513_1.png)

FIGURE 13–4 *Configuring new hardware using kudzu*

Although less common than other hardware problems, hardware failure can also render a device unusable. In this case, you must replace the hardware and allow `kudzu` to detect it, or configure the device driver for it manually. Because hard disks are used frequently and consist of moving parts, they are the most common hardware component to fail on Linux systems. If the Linux system uses hardware RAID level 1 or 5, the data on the hard disk can be regenerated using the configuration utility for the RAID controller. Most SCSI RAID controllers allow you to enter this utility by pressing a key combination such as `Ctrl+a` when prompted during system startup.

If, however, the Linux system does not use hardware RAID and the hard disk that failed contained partitions that were mounted on noncritical directories, such as `/home` or `/var`, then you can perform the following steps:

- 1. Power down the computer and replace the failed hard disk.
- 2. Boot the Linux system.
- 3. Use `fdisk` to create partitions on the replaced hard disk.
- 4. Use `mkfs` to create filesystems on those partitions.
- 5. Restore the original data using a back-up utility.
- 6. Ensure that `/etc/fstab` has the appropriate entries to mount the filesystems at system startup.

Alternatively, if the hard disk that contains the `/` filesystem fails, you can perform the following steps:

- 1. Power down the computer and replace the failed hard disk.
- 2. Reinstall Linux on the new hard disk (you can choose to leave partitions on other hard disks intact and mount them to the appropriate directory).
- 3. Restore the original configuration and data files using a back-up utility.

## Software-Related Problems

Software-related problems are typically more difficult to identify and resolve than hardware-related problems. As a result, you should identify whether the software-related problem is related to application software or operating system software.

## Application-Related Problems

Applications can fail during execution for a number of reasons, including missing program libraries and files, process restrictions, or conflicting applications.

As discussed in Chapter 12, “Compression, System Backup, and Software Installation,” when software is installed using the Red Hat Package Manager, it does a preliminary check to ensure that all shared program libraries and prerequisite packages (package dependencies) required for the application to work properly have been installed. If these are missing, the Red Hat Package Manager prints an error message to the screen and quits the installation. Similarly, uninstalling software using the Red Hat Package Manager fails if the software being uninstalled is a package dependency for another package. Also, when compiling source code, the configure script checks for the presence of any required shared program libraries and programs and fails to create the Makefile if they are absent. Thus, you must download and install the necessary shared libraries and/or packages before installing most software packages.

Some programs, however, might fail to check for dependencies during installation, or files that belong to a package dependency might be accidentally removed from the system over time. If this is the case, certain programs fail to execute properly.

To identify any missing files in a package or package dependency, recall that you can use the `-V` option to the `rpm` command, followed by the name of the package. The following output indicates that there are two missing files in the `bash` package:

```text
[root@server1 root]# rpm -V bash
missing /usr/share/doc/bash-2.05b/NEWS
missing /usr/share/doc/bash-2.05b/NOTES
[root@server1 root]#
```

To identify which shared libraries are required by a certain program, you can use the `ldd` command. For example, the following output displays the shared libraries required by the /bin/bash program:

```text
[root@server1 root]# ldd /bin/bash
    linux-gate.so.1 => (0x004c8000)
    libtermcap.so.2 => /lib/libtermcap.so.2 (0x00c23000)
    libdl.so.2 => /lib/libdl.so.2 (0x00a07000)
    libc.so.6 => /lib/tls/libc.so.6 (0x00805000)
    /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00a80000)
[root@server1 root]#
```

If any shared libraries listed by the `ldd` command are missing, you can download the appropriate library from the Internet and install it at the correct location, which is typically underneath the `/lib` or `/usr/lib` directories. After downloading and installing any shared libraries, it is good practice to run the `ldconfig` command to ensure that the list of shared library directories (`/etc/ld.so.conf`) and the list of shared libraries (`/etc/ld.so.cache`) are updated.

Recently, multimedia applications that play sound and video have been popular on the Linux platform. Many different formats are used to store and retrieve multimedia information; thus, multimedia programs often work with several different types of multimedia data. In addition, because multimedia data is usually large in size, it is often compressed using a format such as MP3 or DivX. For a multimedia program to decompress multimedia files, it requires the appropriate `compressor`/`decompressor` (codec), which is typically a shared library file. Codecs for most multimedia programs are available in tarball format from the Internet. After download, most codecs contain the shared library files as well as a script (`install.sh`) that, when executed, copies the shared libraries to the appropriate directory and runs the `ldconfig` command to update the /etc/ld.so.conf and /etc/ld.so.cache files. If no script is available, you must manually copy the shared library files to the appropriate location and update the /etc/ld.so.conf and /etc/ld.so.cache files.

## RESOLVING COMMON SYSTEM PROBLEMS

Processes are restricted by a number of constraints that can also prevent them from executing properly. Recall that all processes require a PID from the system process table. Too many processes running on the system can use all available PIDs in the process table; this is typically the result of a large number of zombie processes. Killing the parent process of the zombie processes then frees several entries in the process table.

In addition, processes can initiate numerous connections to files on the filesystem in addition to Standard Input, Standard Output, and Standard Error. These connections are called **filehandles**. The shell restricts the number of filehandles that programs can open to 1024 by default; to increase the maximum number of filehandles to 5000, you can run the command `ulimit -n 5000`. The **ulimit command** can also be used to increase the number of processes that users can start in a shell; this might be required for programs that start a great deal of child processes. For example, to increase the maximum number of user processes to 8000, you can use the command `ulimit -u 8000`.

To isolate application problems that are not related to missing dependencies or restrictions, you should first check the log file produced by the application. Most application log files are stored in the /var/log directory or subdirectories of the /var/log directory named for the application. For example, to view the errors for the Apache Web Server daemon, you can view the file /var/log/httpd/error_log.

Applications might run into difficulties gaining resources during execution and stop functioning. Often, restarting the process using a SIGHUP solves this problem. This condition might also be caused by another process on the system that attempts to use the same resources. To determine this, attempt to start the application when fewer processes are loaded, such as in Single User Mode. If resource conflict seems to be the cause of the problem, check the Internet for a newer version of the application or an application fix.

## Operating System-Related Problems

Many software-related problems are related to the operating system itself. These typically include problems with boot loaders, filesystems, and serial devices.

As discussed in Chapter 9, “System Initialization and X Windows,” boot loaders can encounter problems while attempting to load the operating system kernel. For the LILO boot loader, placing the word “linear” and removing the word “compact” from the /etc/lilo.conf file usually remedies the problem. For the GRUB boot loader, errors are typically the result of a missing file in the /boot directory. Also, ensuring that the Linux kernel resides before the 1024th cylinder of the hard disk and that 32-bit large block addressing (LBA32) is specified in the boot loader configuration file eliminates BIOS problems with large hard disks.

It is safe practice to create a boot disk after installation; if the boot loader fails to load the kernel, you can then use the bootloader and kernel on the boot disk to mount the root filesystem
