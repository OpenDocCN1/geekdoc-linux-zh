
popular operating systems including FreeBSD, OpenBSD, and NetBSD. BSD code can also be found in proprietary operating systems created by Microsoft, Apple, and Sun Microsystems.

Commercial Unix systems began to appear in the early 1980s. These systems combined various amounts of Unix and BSD code along with vendor-specific enhancements to create new platforms such as AIX, HP-UX, and Sun Solaris. Today, commercial Unix systems can be found in data centers at many large companies running mission critical applications.

In 1991, a computer science student at the University of Helsinki in Finland named Linus Torvalds created the Linux operating system. While Linux shares much of the core concepts of Unix, it contains no Unix code. This means it can be freely distributed in the same manner as BSD (although under a different license). The first commercial Linux distributions hit the market in the mid 1990s. Since then hundreds of Linux variants have been developed. The open nature of the Linux operating system has contributed to its success and helped make it one of the most popular server operating systems in use today.

The Unix platform has been around since long before graphical user interfaces were invented. The fact that Unix-based systems are still a commanding force in modern computing is a testament to the industrial design of the platform. With Unix, Linux, and BSD popularity at an all time high, now is the perfect time to explore these platforms and join the movement.

## Conventions Used in This Book

`/path/to/file`
File and directory paths are displayed in a fixed width font

`command`
Commands are displayed in a bold fixed width font

`[FILE], [DIRECTORY], [ETC]`
Items enclosed in brackets represent a variable parameter to be specified by the user (such as a file or directory)

`$ ping 192.168.1.1`
Examples using the $ shell prompt are executed with a non-privileged user account

`# ping 192.168.1.1`
Examples using the # shell prompt are executed at the root user

`...`
Additional command output truncated (to save space)

`$ who<TAB>`
Items enclosed in <> indicate an action key such as <TAB>, <ESC>, <SPACE>, etc.

# Section 1: Overview of Unix, Linux and BSD Architecture

## The Kernel

At the heart of every Unix, Linux, and BSD system is the kernel. The kernel provides a layer between the computer hardware and user applications. When applications need to display output to a screen or write files to the disk, the kernel facilitates these actions. Think of the kernel as the conductor in a symphony; it directs all the actions of the operating system.

![](img/fa2f95b64a707c963dfa0445bd9281a7_9_0.png)

When you type a command on the keyboard, the computer hardware receives the signals and transfers them to the kernel. The kernel recognizes the key strokes and draws them on the display. Once the typed command is executed, the program will utilize the kernel to request processor, memory, and other resources in order to perform the requested task.

## Popular Versions of Unix, Linux, and BSD

There are many different Unix, Linux, and BSD distributions. The tables below list the most popular systems in use today.

### BSD Systems

| OS | Description |
| :--- | :--- |
| **Darwin** | BSD-based core of the Mac OS X operating system |
| **FreeBSD** | User friendly BSD-based operating system |
| **OpenBSD** | Security focused BSD-based operating system |
| **NetBSD** | Highly portable BSD-based operating system |

### Linux Systems

| OS | Description |
| :--- | :--- |
| **Red Hat Enterprise Linux** | Popular commercial Linux distribution created by Red Hat, Inc. |
| **Fedora** | Free community-based distribution that serves as a test bed for new technologies that feed into Red Hat Enterprise Linux |
| **CentOS** | Free binary-compatible clone of Red Hat Enterprise Linux |
| **Debian** | Popular non-commercial Linux distribution |
| **Ubuntu** | User-friendly Linux distribution based on Debian |
| **SuSE Enterprise Linux** | Commercial Linux distribution created by Novell, Inc. |
| **openSUSE** | Free community-based distribution based on SUSE Enterprise Linux |

### Unix Systems

| OS | Description |
| :--- | :--- |
| **AIX** | IBM’s proprietary Unix platform |
| **HP-UX** | Hewlett Packard’s proprietary Unix platform |
| **Solaris** | Sun Microsystems’ proprietary Unix platform |
| **OpenSolaris** | Open source version of the Solaris operating system |

> **Note** *Other notable Unix platforms include SGI IRIX, Compaq Tru64, and SCO UnixWare/OpenServer; however, these systems are no longer widely used or supported.*

## Unix, Linux, and BSD Directory Structure

Most Unix, Linux, and BSD systems share a similar directory structure. The table below lists the main directories commonly used across all platforms.

| Directory | Purpose |
| --- | --- |
| / | Root (top level) directory |
| /boot | Linux kernel and boot loader files |
| /stand | Unix kernel directories |
| /unix |  |
| /vmunix |  |
| /kernel |  |
| /bin | Core binary programs for normal users |
| /usr |  |
| /usr/bin |  |
| /sbin | Administrative programs primarily used by the root user |
| /usr/sbin |  |
| /opt | Optional add-on/third-party software |
| /etc | System configuration files |
| /home | User home directories |
| /root | Home directory of the root user |
| /lib | Shared libraries used by various programs |
| /media | Mounted local and remote file systems |
| /mnt |  |
| /var | Variable data (such as system logs) that changes often |
| /tmp | Temporary files used by various programs |
| /dev | Device files |
| /sys | Virtual device driver files used by the kernel |
| /proc | Virtual parameter and informational files used by the kernel |
| /lost+found | Files that have been recovered (after a system failure) |

These directories are organized in a manner which separates various components of the operating system in an easy to manage file structure. The /home directory is where users spend most of their time. Files outside of this directory are usually secured so that only the root user can edit or delete them. This protects vital programs and configuration files and prevents users from accidentally damaging the core operating system. It also helps secure the system by preventing malicious programs from being able to compromise critical files and settings.

## Important Files

In addition to sharing a similar directory structure, most systems will also have the important files listed in following table.

| File | Purpose |
| --- | --- |
| /etc/passwd | User account settings |
| /etc/shadow | Encrypted passwords for user accounts |
| /etc/group | Group settings |
| /etc/fstab | Local file system settings |
| /etc/mtab | Mounted file systems |
| /etc/inittab | System startup settings |
| /etc/exports | NFS share settings |
| /etc/hosts | Static name resolution file |
| /etc/hostname | System host name setting |
| /etc/hosts.allow | Network hosts allowed to connect to the system |
| /etc/resolv.conf | DNS settings |
| /etc/hosts.deny | Network hosts not allowed to connect to the system |
| /etc/issue | Message displayed at shell login |
| /etc/issue.net | Remote login message |
| /etc/motd | Message displayed after logging in |
| /etc/profile | Shell environment settings |
| /etc/shells | Valid shells permitted to login |
| /etc/sudoers | Users allowed to use the `su` command (discussed on page 91) |
| /var/log/messages | Kernel messages log file |
| /var/log/wtmp | Current user login log file |
| /var/log/lastlog | User login history log file |
| /var/log/kern.log | Kernel log file |
| /var/log/syslog | Syslog messages log file |

![](img/fa2f95b64a707c963dfa0445bd9281a7_12_0.png)

This is just a brief list of the most commonly used files shared across most platforms. As a general rule, configuration files are located in the `/etc` directory and system logs are stored in `/var/log`. As you become more familiar with Unix, Linux, and BSD systems you will begin working with these files to manage system configuration and troubleshoot problems.
