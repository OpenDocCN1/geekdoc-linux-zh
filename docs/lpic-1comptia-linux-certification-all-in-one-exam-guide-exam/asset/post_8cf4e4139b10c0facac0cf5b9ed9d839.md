
10. A. The ssh-keygen -t rsa command can be used at the SSH client to create an RSA private/public key pair for SSH public key authentication.

11. D. The ~/.ssh/id_dsa.pub file is the DSA public key that can be used for SSH public key authentication.

12. A. You need to add the public key to the ~/.ssh/authorized_keys file in the home directory of the user you want to authenticate as using public key authentication.

13. B. The gpg --gen-key command is used to create a GPG private/public key pair.

14. B. The gpg --import public_key_filename command can be used to import another user's GPG public key into your keyring so that you can decrypt files she sends you.

15. A. The gpg --output output_filename --symmetric encrypted_filename command can be used to decrypt a file sent to you by someone else (assuming you’ve already imported this person's GPG public key into your keyring).

## Appendix A
## Exam Objective Reference

To help you prepare for your Linux+/LPIC 1 exams, we've included a listing of each objective and where you can find the associated content in the book. The list of objectives is broken down by each exam in the certification:

- Exam LX0-101
- Exam LX0-102

### Exam LX0-101

The objectives for the LX0-101 exam and where you can find the relevant content in the book are listed in the table that follows.

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| **101 System Architecture** | | |
| **101.1 Determine and configure hardware settings** | | |
| Enable and disable integrated peripherals | 12 | 449 |
| Configure systems with or without external peripherals such as keyboards | 12 | 451 |
| Differentiate between the various types of mass storage devices | 12 | 430 |
| Set the correct hardware ID for different devices, especially the boot device | 12 | 434, 436, 437 |
| Know the differences between coldplug and hotplug devices | 12 | 462 |
| Determine hardware resources for devices | 12 | 444 |
| Tools and utilities to list various hardware information (e.g., lsusb, lspci, etc.) | 12 | 455 |
| Tools and utilities to manipulate USB devices | 12, 10 | 455, 429, 455 |
| The following is a partial list of the used files, terms, and utilities: | 12 | 455, 458 |
| • /sys | | |
| • /proc | | |
| • /dev | | |
| • modprobe | | |
| • lsmod | | |
| • lspci | | |
| • lsusb | | |

### 101.2 Boot the System

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Provide common commands to the boot loader and options to the kernel at boot time | 6 | 196 |
| Demonstrate knowledge of the boot sequence from BIOS to boot completion | 6 | 181 |
| Check boot events in the log file | 6 | 182 |
| The following is a partial list of the used files, terms, and utilities: | 17 | 684 |
| • /var/log/messages | 6 | 182 |
| • dmesg | | |
| • BIOS | | |
| • bootloader | | |
| • kernel | | |
| • init | | |

### 101.3 Change runlevels and shut down or reboot system

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Set the default runlevel | 6 | 204, 210 |
| Change between runlevels including single-user mode | 6 | 205, 210 |
| Shut down and reboot from the command line | 6 | 217 |
| Alert users before switching runlevels or other major system events | 6 | 217 |
| Properly terminate processes | 13 | 494 |
| The following is a partial list of the used files, terms, and utilities: | | |
| • /etc/inittab | 6 | 204 |
| • shutdown | 6 | 217 |
| • init | 6 | 186 |
| • /etc/init.d | 6 | 207 |
| • telinit | 6 | 212 |

## 102 Linux Installation and Package Management

### 102.1 Design hard disk layout

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Allocate filesystems and swap space to separate partitions or disks | 5, 10 | 142, 366 |
| Tailor the design to the intended use of the system | 5 | 128 |
| Ensure the /boot partition conforms to the hardware architecture requirements for booting | 5 | 146 |
| The following is a partial list of the used files, terms, and utilities: | 5 | 145 |
| * / (root) filesystem | 5 | 145 |
| * /var filesystem | 5 | 145 |
| * /home filesystem | 5 | 145 |
| * swap space | 5 | 145 |
| * mount points | 5 | 145 |
| * partitions | 5 | 145 |

### 102.2 Install a boot manager

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Providing alternative boot locations and backup boot options | 6 | 189–196 |
| Install and configure a boot loader such as GRUB | 6 | 187 |
| Interact with the boot loader | 6 | 196 |
| The following is a partial list of the used files, terms, and utilities: | 6 | 194–196 |
| * /boot/grub/menu.lst | 6 | 194 |
| * grub-install | 6 | 193 |
| * MBR | 6 | 184 |
| * superblock | 10 | 365 |
| * /etc/lilo.conf | 6 | 189 |
| * lilo | 6 | 188 |

### 102.3 Manage shared libraries

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Identify shared libraries | 8 | 314 |
| Identify the typical locations of system libraries | 8 | 316 |
| Load shared libraries | 8 | 314 |
| The following is a partial list of the used files, terms, and utilities: | 8 | 316–318 |
| * ldd | 8 | 318 |
| * ldconfig | 8 | 317 |
| * /etc/ld.so.conf | 8 | 317 |
| * LD_LIBRARY_PATH | 8 | 316 |

### 102.4 Use Debian package management

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Install, upgrade, and uninstall Debian binary packages | 8 | 304 |
| Find packages containing specific files or libraries which may or may not be installed | 8 | 306, 307, 309 |
| Obtain package information like version, content, dependencies, package integrity, and installation status (whether or not the package is installed) | 8 | 306 |
| The following is a partial list of the used files, terms, and utilities: | 8 | 305–312 |
| * /etc/apt/sources.list | 8 | 305 |
| * dpkg | 8 | 312 |
| * dpkg-reconfigure | 8 | 311 |
| * apt-get | 8 | 309 |
| * apt-cache | 8 | 308 |
| * aptitude | 8 | 310 |

### 102.5 Use RPM and YUM package management

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Install, re-install, upgrade and remove packages using RPM and YUM | 8 | 284–290 |
| Obtain information on RPM packages such as version, status, dependencies, integrity, and signatures | 8 | 285–292 |
| Determine what files a package provides, as well as find which package a specific file comes from | 8 | 291 |

The following is a partial list of the used files, terms, and utilities:

- rpm
- rpm2cpio
- /etc/yum.conf
- /etc/yum.repos.d/
- yum
- yumdownloader

## 103 GNU and Unix Commands

### 103.1 Work on the command line

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Use single shell commands and one-line command sequences to perform basic tasks on the command line | 2 | 24 |
| Use and modify the shell environment including defining, referencing, and exporting environment variables | 2 | 21 |
| Use and edit command history | 2 | 41 |
| Invoke commands inside and outside the defined path | 2 | 25 |

The following is a partial list of the used files, terms, and utilities:

- .
- bash
- echo
- env
- exec
- export
- pwd
- set
- unset
- man
- uname
- history

### 103.2 Process text streams using filters

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Send text files and output streams through text utility filters to modify the output using standard UNIX commands found in the GNU texutils package | 14 | 529 |

The following is a partial list of the used files, terms, and utilities:

| Utility | Chapter | Page |
| :--- | :---: | :---: |
| * cat | 4 | 113 |
| * cut | 14 | 530 |
| * expand | 14 | 530 |
| * fmt | 14 | 531 |
| * head | 4 | 113 |
| * od | 14 | 533 |
| * join | 14 | 532 |
| * nl | 14 | 533 |
| * paste | 14 | 532 |
| * pr | 14 | 535 |
| * sed | 14 | 535 |
| * sort | 14 | 533 |
| * split | 14 | 533 |
| * tail | 4 | 113 |
| * tr | 14 | 540 |
| * unexpand | 14 | 530 |
| * uniq | 14 | 540 |
| * wc | 14 | 541 |

### 103.3 Perform basic file management

| Official Objective | Chapter | Page |
| :--- | :---: | :---: |
| Copy, move, and remove files and directories individually | 4 | 111, 115 |
| Copy multiple files and directories recursively | 4 | 111 |
| Remove files and directories recursively | 4 | 111, 114 |
| Use simple and advanced wildcard specifications in commands | 4 | 120 |
| Using find to locate and act on files based on type, size, or time | 4, 17 | 101, 667 |
| Usage of tar, cpio, and dd | 10 | 389, 391, 392 |
