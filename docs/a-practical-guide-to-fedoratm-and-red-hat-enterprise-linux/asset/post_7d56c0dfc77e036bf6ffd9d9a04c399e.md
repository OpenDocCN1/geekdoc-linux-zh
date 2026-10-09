
## 101.3 CHANGE RUNLEVELS AND SHUTDOWN OR REBOOT SYSTEM

Set the default runlevel
- Setting the Persistent Runlevel page 444
- `/etc/inittab` page 508

Change between runlevels including single-user mode
- Changing the Current Runlevel page 445
- `telinit` page 449
- Booting the System to Single-User/Rescue Mode page 450
- Going to Graphical Multiuser Mode page 452

Shutdown and reboot from the command line
- Bringing the System Down page 454

Alert users before switching runlevels or other major system events

Properly terminate processes
- `kill`: Aborting a Background Job page 164
- `kill`: Sends a Signal to a Process page 465
- `killall`: Kills a Command page 467
- `pkill`: Kills a Command page 468
- `kill`: Aborts a Process page 1050

### Partial List of Used Files, Terms, and Utilities

`/etc/inittab`
- `/etc/inittab` page 508

`shutdown`

Tailor the design to the intended use of the system
- Planning the Installation page 29

Ensure the /boot partition conforms to the hardware architecture requirements for booting
- Where to put the /boot partition page 41
- LBA addressing mode and the /boot partition page 590

### Partial List of Used Files, Terms, and Utilities

- / (root) filesystem
  - / (root) page 40
  - / (root) page 181
  - / page 189
  - root filesystem page 1271 (Glossary)
- /var filesystem
  - /var page 41
  - /var page 191
- /home filesystem
  - /home page 41
  - /home page 190
- swap space
  - (swap) page 40
  - swap page 513
  - swap space page 1276 (Glossary)
- mount points
  - Mount Points page 38
  - Mount point page 521
- partitions
  - Partitions page 36
  - Partition table page 36
  - Primary, Extended, and Logical Partitions page 37
  - Default Partitioning page 39
  - Manual Partitioning; Planning Partitions page 39
  - Example minimum partition sizes page 42
  - Manual/Custom Partitioning page 74
  - partition page 1265 (Glossary)

## 102.2 Install A Boot Manager

Providing alternative boot locations and backup boot options

Install and configure a boot loader such as GRUB
- GRUB: The Linux Boot Loader page 590

Interact with the boot loader
- Booting the System to Single-User/Rescue Mode page 450

### Partial List of Used Files, Terms, and Utilities

- /boot/grub/menu.lst
  - Configuring GRUB page 591
- **grub-install**
  - **grub2-install**: Installs the MBR and GRUB Files page 594
- **MBR**
  - Reinstalling the MBR page 456
  - MBR page 590
  - **grub2-install**: Installs the MBR and GRUB Files page 594
- **superblock**
  - superblock page 1276 (Glossary)

*/etc/lilo.conf*

*lilo*

## 102.3 Manage Shared Libraries

- Identify shared libraries
  - **lxd** page 487
- Identify the typical locations of system libraries
- Load shared libraries

### Partial List of Used Files, Terms, and Utilities

- **lxd**
  - **lxd** & **libwrap** page 486
  - **lxd** page 487
- **ldconfig**
- */etc/ld.so.conf*
- **LD_LIBRARY_PATH**

## 102.4 Use Debian Package Management

Install, upgrade, and uninstall Debian binary packages
- Using **apt-get** to Install, Remove, and Update Packages page 1184
- Find packages containing specific files or libraries which may or may not be installed
- Obtain package information like version, content, dependencies, package integrity, and installation status (whether or not the package is installed)

### Partial List of Used Files, Terms, and Utilities

- */etc/apt/sources.list*
  - **sources.list**: Specifies Repositories for apt-get to Search page 1187
- **dpkg**
  - **apt-get** and **dpkg** page 1184
- **dpkg-reconfigure**
- **apt-get**
  - Using **apt-get** to Install, Remove, and Update Packages page 1184
  - Using **apt-get** to Upgrade the System page 1185
  - Other **apt-get** Commands page 1186
- **apt-cache**
- **aptitude**

## 102.5 USE RPM AND YUM PACKAGE MANAGEMENT

> See Chapter 12: Finding, Downloading, and Installing Software page 531

Install, re-install, upgrade, and remove packages using RPM and YUM
- JumpStart: Installing and Removing Software Packages Using yum page 534
- Updating Packages page 538
- RPM: The RPM Package Manager page 546
- Installing, Upgrading, and Removing Packages page 548

Obtain information on RPM packages such as version, status, dependencies, integrity, and signatures
- Querying Packages and Files page 547

Determine what files a package provides, as well as find which package a specific file comes from
- Finding the Package That Holds an Application or File You Need page 536
- Querying Packages and Files page 547

### Partial List of Used Files, Terms, and Utilities

- **rpm**
  - RPM: The RPM Package Manager page 546
  - Querying Packages and Files page 547
- **rpm2cpio**
- **/etc/yum.conf**
  - yum.conf: Configures yum page 541
- **/etc/yum.repos.d/**
  - yum Repositories page 542
- **yum**
  - yum page 533
  - JumpStart: Installing and Removing Software Packages Using yum page 534
  - Finding the Package That Holds an Application or File You Need page 536
  - yum: Keeps the System Up-to-Date page 538
- **yumdownloader**
  - Downloading RPM Package Files with yumdownloader page 540
  - yumdownloader page 582

# 103 GNU AND UNIX COMMANDS

## 103.1 WORK ON THE COMMAND LINE

> See Chapter 5: The Shell page 141
> See Chapter 9: The Bourne Again Shell (bash) page 327
> See Chapter 7: The Linux Utilities page 215
> See Chapter 27: Programming the Bourne Again Shell (bash) page 981

Use single shell commands and one line command sequences to perform basic tasks on the command line
- Chapter 5: The Shell page 141
- Chapter 7: The Linux Utilities page 215
- Chapter 9: The Bourne Again Shell (*bash*) page 327

Use and modify the shell environment including defining, referencing, and exporting environment variables
- Parameters and Variables page 352
- Variables page 1031

Use and edit command history
- History page 376

Invoke commands inside and outside the defined path
- Absolute versus relative pathnames page 149
- **PATH**: Where the Shell Looks for Programs page 359

### Partial List of Used Files, Terms, and Utilities

- .(dot) or source: Runs a Startup File in the Current Shell page 332
- **exec** versus . (dot) page 1045

*bash*
- Chapter 5: The Shell page 141
- Chapter 9: The Bourne Again Shell (*bash*) page 327
- Chapter 27: Programming the Bourne Again Shell (*bash*) page 981

*echo*
- **echo**: Displays Arguments page 219
- **echo –c** page 1009

*env*
- **env**: Runs a Program in a Modified Environment page 1035

*exec*
- Opening a File Descriptor page 1017
- Duplication a File Descriptor page 1017
- **exec**: Executes a Command or Redirects File Descriptors page 1045

*export*
- **declare**: Lists and Assigns Attributes to Variables page 357
- **readonly** and **export** page 357
- **export**: Puts Variables in the Environment page 1032

*pwd*
- **pwd** page 143

*set*
- man: Displays the System Manual page 128
- uname: Displays System Information page 470
- History page 376

## 103.2 PROCESS TEXT STREAMS USING FILTERS

Send text files and output streams through text utility filters to modify the output using standard UNIX commands found in the GNU textutils package
- Redirection page 153
- Pipelines page 158
- Filters page 161

### Partial List of Used Files, Terms, and Utilities

- cat: Joins and Displays Files page 216
- cat page 152
- Redirection page 153
- cut: Selects Characters or Fields from Input Lines page 225
- head: Displays the Beginning of a File page 235
- sort: Sorts and/or Merges Files page 239
- tail: Displays the Last Part of a File page 241
- tr page 159
- tr page 260
- *man*
- *uname*
- *history*
- *cat*
- *cut*
- *expand*
- *fmt*
- *head*
- *od*
- *join*
- *nl*
- *paste*
- *pr*
- *sed*
- *sort*
- *split*
- *tail*
- *tr*
