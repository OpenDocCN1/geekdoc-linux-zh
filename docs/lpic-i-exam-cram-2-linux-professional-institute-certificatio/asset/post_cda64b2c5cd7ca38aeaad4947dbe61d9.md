
# EXAM CRAM 2

Exam 101

Exam 102

# LPIC 1

- Linux
- Professional
- Institute
- Certification

Join The Crammers Club!
See details Inside

CD features
Linux Version
Test Engine!

LPIC

Ross Brunson

Edited by Ed Tittel

# Win Free Books and Merchandise!

It's our goal to meet your needs, so please take a moment to send us your feedback at feedback@quepublishing.com. You'll not only help shape the future of Exam Cram 2 books, you'll be entered in a drawing for free books and merchandise!

> *The Network+ Exam Cram* is a brilliant book, just like the A+ Exam Cram I just used. I just passed my Network+ exam and this book helped more than anything."
> —Mike Jonas

> "Your A+ Exam Cram 2 book is excellent! The book and CD is well planned and easy to follow. I would advise anybody taking the A+ exams to purchase this asset to become certified and even just to use as a reference guide to personal computing. It's a bargain not to be missed!"
> —John Gill

> "I'm using your 70-214 Exam Cram 2 and I've got to tell you that I'm humbled. Great book, great material, great writing. My classes love it!"
> —Roger A. Grimes, Instructor, The Training Camp

> "The 70-216 Exam Cram 2 book is a great book—concise and simplified! Beats the Microsoft Press book, that's for sure. Keep up the good work!"
> —Shaun Pillay, MCP

> "I am highly recommending your Network+ Exam Cram 2 book to all of my friends. It was right on the money as far as what to expect on the exam."
> —Johnny Hughes

> "The 70-218 Exam Cram 2 is better than ever! Your books are the best summary books out there to study from."
> —Gerald Tapani

> "Why are you the only people to understand how beneficial it is to provide us with explanations to both correct and incorrect sample test questions? Beats me, but that's why I held out for your book! Now I have it and feel a bit more confident about being able to pass my next exam."
> —Fernando Arias

> "I'm recommending your A+ Exam Cram 2 book to everyone I know who is considering A+ certification!"
> —Jack Bolsen

> "I cannot put down the 70-291 Exam Cram 2 book! Please tell the entire Que Certification team that they have set a new standard in excellence!"
> —Tcat Houser

> "I have been reading your books and articles for several years now, and I want you to know that they are very well written and your efforts to educate are truly appreciated."
> —Francis B. MacMillan

> "Thank you for the best books I've had in this genre!"
> —Lars Kjaes

> "Thanks to Exam Cram, I went from being a secretary to becoming a network specialist trainee in six months! Thanks for the way up and out."
> —Jeavonna L. Chapman

> "I love Exam Crams! I plan on using these books for all my tests! Thank you again!"

![](img/49f4f38f3aec011238fa50f89e643db3_2_0.png)

# The LPIC I Cram Sheet

This Cram Sheet contains the key facts about the LPI Level 1 Exams. Review this information before entering the test room, paying attention to those areas where you feel you need the most review. You can transfer any of these facts from your memory onto a blank piece of paper before beginning the exam.

## EXAM 101

### Hardware and Architecture

1. To view IRQ, DMA, and I/O information on a running machine, use:
   - `cat /proc/interrupts`
   - `cat /proc/ioports`
   - `cat /proc/dma`
   - `cat /proc/pci`

2. Commands to view configuration information:
   - `lsdev`—Shows the most about IRQ, DMA, and I/O port usage
   - `lspci`—Shows the PCI bus information

3. To configure sound, use sndconfig.

4. If a system with two printer ports and a sound card has an error, check the IRQs for conflicts, particularly IRQ 5.

5. Modems must not be Winmodems; they must have the correct IRQs and UART to function as high-speed modems.

6. Serial ports:

| Port | IRQ | I/O Address |
| :--- | :--- | :--- |
| /dev/ttyS0 | 4 | 03f8 |
| /dev/ttyS1 | 3 | 02f8 |
| /dev/ttyS2 | 4 | 03e8 |
| /dev/ttyS3 | 3 | 02e8 |

7. Configure serial ports with the setserial command:
   - `setserial -a /dev/ttyS0`—Shows a port's configuration
   - `setserial /dev/ttyS0 baud_base 57600`—Sets the baud rate for a serial port

8. Printer ports:

| Port | IRQ | I/O Address |
| :--- | :--- | :--- |
| /dev/lp0 | 7 | 0378 |
| /dev/lp1 | 5 | 0278 |

9. Plug and Play uses the isapnp program to configure and troubleshoot PNP devices, the pnpdump program to show the PNP information, and the /etc/isapnp.conf file to set individual device configuration for PNP devices.

10. SCSI cards come in either 8-bit or 16-bit. 8-bit SCSI cards provide 8 IDs for devices (ID 7 is usually the card), and 16-bit cards provide 16 IDs for devices (ID 7 is usually the card).

11. The SCSI ID priority order is 7, 6, 5, 4, 3, 2, 1, 0, 15, 14, 13, 12, 11, 10, 9, 8.

12. The hwclock command is used to read and transfer time on the system:
   - `hwclock -r`—Reads hardware clock time
   - `hwclock --sysctok`—Sets the hardware clock with the system clock's time
   - `hwclock --hctosys`—Sets the system time with the hardware clock time

### Linux Installation and Package Management

13. Use a small /boot partition to avoid problems with the 1,024th cylinder, or enable the LBA options in the boot manager.

14. General rules for swap:
   - Can have up to eight swap files or partitions.
   - Swap space should ideally be 1 to 1.5 times the size of the physical RAM.

15. LILO reads its configuration file (/etc/lilo.conf) only when the /sbin/lilo program is run and can write the LILO configuration code to either the master boot record (MBR) or the first sector of the Linux system partition.

16. GRUB is a newer boot loader that reads its configuration file (/boot/grub/grub.conf) during the boot process and contains enough file system code to use pathnames and filenames to refer to boot files. If a system can't boot, or shows only the grub> prompt, run the grub-install program with the boot disk as the argument.

17. Steps for making and installing software from source include:
   - `./configure`—This script updates the Makefile with the system configuration.
   - `make`—This creates the software, compiling the components.
   - `make install`—This installs the compiled binaries and associated files into the system directories and is the one step that normally requires root access.

18. Shared libraries are located in /lib, /usr/lib, and /usr/X11/lib by default. When a library error occurs, run the ldconfig program, which reads the /etc/ld.so.conf file for library locations and writes a common cache of library locations in /etc/ld.so.cache. The ld program reads a binary and reports back its library dependencies. If a user needs to reference a library, she uses the LD_LIBRARY_PATH variable.

19. Debian Package Management uses the dpkg program to install, delete, and query packages. The dselect program is a front end for the dpkg program, providing a menu for all options. The apt-get program is for automated updates and reads the sources from /etc/apt/sources.list file. The Debian package database is kept in /var/lib/dpkg.

20. Red Hat Package Management uses the RPM program to install, remove, and query packages. The RPM database is kept in /var/lib/rpm and is rebuilt with rpm -rebuild. RPM packages come in precompiled and source packages.

### GNU and Unix Commands

21. Commands take the following format: `command -options arguments`, and some options can be placed at the end of the command.

22. Commands use `<` redirection for input and `>` redirection to write standard output to a file.

23. sed can search and replace words and phrases, but tr can only do individual characters.

24. grep uses `-i` for case insensitivity, `-r` for recursive searches, `-n` for line numbering, and `-v` for reversing the output.

25. stdin is Stream 0, stdout is stream 1, and stderr is stream 2. You can redirect any and all with `1>` and `2>`, but to send both stdout and stderr to the same place, you use `2>&1`.

26. Use `&` after a command to send it to the background, `Ctrl+z` to suspend a running program, and `bg` to send it to the background. A job in the `jobs` command output with a `+` symbol is the current job (the one with the `-` symbol is the previous job). Any `fg` or `bg` command acts on the current job by default. `kill %j` ends a job, where `$j` is the job number.

27. Start a job with a lowered priority with the `nice` command, and alter a running command's priority with the `renice` command. By default, nice drops the priority by a value of 10 and renice sets a priority and doesn't take a default. Programs are started by default with a priority of 10, and priorities range from -20 (highest) to 19 (lowest).

28. vi uses hjkl for cursor movement. Remember h = left, j = down, k = up, and l = right. vi offers three modes: command, insert, and lastline or ex mode.

### Devices, Linux File Systems, and FHS

29. mkefs is a front end for the mkfs—file system-specific tools. Use mke2fs /dev/hda1 to create a default ext2 file system on device /dev/hda1. Use the -m option to reserve space for the root user. Use the -j option to create an ext3 journal for the file system.

30. fsck checks file systems when they are mounted read-only or unmounted. fsck has five passes and can ask for manual intervention.

31. The /etc/fstab file has six columns (device, mount point, file system type, options, dump time, and fsck order) and is used by the root user to set options for file systems, and to allow users to mount and unmount file systems.

32. The user keyword in the /etc/fstab options column allows only the user who mounted a file system to unmount it, whereas the users (plural) keyword allows any valid user with the right permissions to mount and unmount the file system.

33. The /etc/mtab file is a table of mounted file systems. The mount command by itself, the cat /proc/mounts command, and cat /etc/mtab show the mounted file systems for the machine.

34. Quotas are on a file system-by-file system basis. The quota.user and quota.group files must be created in the root of the file system. Edit the /etc/fstab and put usrquota and grpquota in the options column for the file system, and then remount the file system. Then run the quotacheck program to populate quota.user/quota.group. Run edquota -u username to set the user's quota limits, use the -o option for a grace period, and then run quotactl -a or quotactl -f filesystem to start the quota subsystem. Users can check their own quotas with quota, and the root user can check all quotas with repquota.

35. File permissions are arranged in three trios: user, group, and other. Permissions are read from left to right, and the first match of your UID or group ID is the set of permissions you are locked into.

36. There must be a user owner and group owner for any file object. Change the ownership with the chown command, which can act on user or group ownership, or change both. Change the group owner with the chgrp command. If a SGID special bit is set on a directory, the group ownership of the directory cascades to all created objects.

37. Hard links are multiple names for the same inode and file; soft or symbolic links are a separate object with its own inode that points to another file. Hard links cannot span file systems, whereas symbolic links can span file systems and enable you to move data without disrupting users' access.

38. The find command is a real-time command and relatively slow but very accurate. The locate command is database-driven and very fast but returns a hit for every instance of the search term, wherever it occurs. find uses many options and can execute commands on the items it finds with the -exec option. locate can be configured to not show files or directory trees by configuring the /etc/updatedb.conf file.
