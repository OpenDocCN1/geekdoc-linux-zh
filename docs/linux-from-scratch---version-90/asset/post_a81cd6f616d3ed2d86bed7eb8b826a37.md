
## Chapter 7. System Configuration

## 7.1. Introduction

Booting a Linux system involves several tasks. The process must mount virtual and real file systems, initialize devices, activate swap, check file systems for integrity, mount any partitions or files, set the system clock, boot up networking, start any daemons required by the system, and accomplish any other custom tasks needed by the user.
This process must be organized to ensure the tasks are performed in the correct order, but at the same time, executed as fast as possible.

### 7.1.1. System V

System V is the classic boot process that has been used in Unix and Unix-like systems such as Linux since about 1983.
It consists of a small program, **init**, that sets up basic tasks such as **login** (via getty) and runs a script. This script, usually named **rc**, controls the execution of a set of additional scripts that performs the tasks required to initialize the system.

The **init** program is controlled by the `/etc/inittab` file and is organized into run levels that can be run by the user:

```
0 — halt
1 — Single user mode
2 — Multiuser, without networking
3 — Full multiuser mode
4 — User definable
5 — Full multiuser mode with display manager
6 — reboot
```

The usual default run level is 3 or 5.

### Advantages

- Established, well understood system.
- Easy to customize.

### Disadvantages

- Slower to boot. A medium speed base LFS system takes 8-12 seconds where the boot time is measured from the kernel message to the login prompt. Network connectivity is typically established about 2 seconds after the login prompt.
- Serial processing of boot tasks. This is related to the previous point. A delay in any process such as a file system check, will delay the entire boot process.
- Does not directly support advanced features like control groups (cgroups), and per-user fair share scheduling.
- Adding scripts requires manual, static sequencing decisions.

## 7.2. LFS-Bootstraps-20190524

The LFS-Bootstraps package contains a set of scripts to start/stop the LFS system at bootup/shutdown. The configuration files and procedures needed to customize the boot process are described in the following sections.

Approximate build time: less than 0.1 SBU
Required disk space: 244 KB

### 7.2.1. Installation of LFS-Bootstraps

Install the package:

```
make install
```

### 7.2.2. Contents of LFS-Bootstraps

Installed scripts:

checkfs, cleansfs, console, functions, halt, ifdown, ifup, localnet, modules, mountfs, network, reboot, sendsignal, setclock, ipv4-static, swatic, syslog, system, template, update, and dev_retry

Installed directories:

/etc/rc.d, /etc/init.d (symbolic link), /etc/sysconfig, /lib/services, /lib/lsb (symbolic link)

### Short Descriptions

- checkfs: Checks the integrity of the files systems before they are mounted (with the exception of journal and network based file systems)
- cleansfs: Removes files that should not be preserved after reboots, such as those in /var/run/ and /var/lock/; re-creates /var/utmp and removes the possibly present /etc/nologin, /fastboot, and /forcefsck files
- console: Loads the correct keymap for the desired keyboard layout; it also sets the screen font
- functions: Contains common functions, as error and status checking, that are used by several bootstraps
- halt: Halts the system
- ifdown: Stops a network device
- ifup: Initializes a network device
- localnet: Sets up the system's hostname and local loopback device
- modules: Loads kernel modules in /etc/sysconfig/modules, using arguments that are also given there
- mountfs: Mount all file systems, except ones that are marked noauto or are network based
- mountvirtfs: Mount virtual kernel file systems, such as proc
- network: Sets up network interfaces, such as network cards, and sets up the default gateway (where applicable)
- rc: The master run-level control script; it is responsible for running all the other bootstraps one-by-one, in a sequence determined by the name of the system being linked
- reboot: Boots the system
- sendsignal: Makes every process is terminated before the system reboots or halts
- setclock: Resets the kernel clock to local time in case the hardware clock is not set to UTC time
- ipv4-static | Provides the functionality needed to assign a static Internet Protocol (IP) address to a network interface
- swap | Enables and disables swap files and partitions
- sysctl | Loads system configuration values from /etc/sysctl.conf, if that file exists, into the running kernel
- syslogd | Starts and stops the system and log daemons
- template | A template to create custom bootscripts for other daemons
- udev | Prepares the /dev directory and starts Udev
- udev_retry | Retries failed udev events, and copies generated rules files from /run/udev to /etc/udev/rules.d if required

## 7.3. Overview of Device and Module Handling

In Chapter 6, we installed the Udev package via eudev built. Before we go into the details regarding how this works, a brief history of previous methods of handling devices is order. Linux systems in general used a static device creation method, whereby many device nodes were created under /dev (sometimes thousands of nodes). This was typically done via MAKEDEV script, which contains a number of calls to the major and minor device numbers for every possible device that might exist in the world. Using udev, only those devices which are detected by the kernel get device nodes for them. Because these device nodes will be created each time the system boots, they will be stored on devtmpfs (a file system that resides entirely in memory). Device nodes do not require much space, so memory used is negligible.

### 7.3.1. History

In February 2000, a new filesystem called devfs was merged into the 2.2 kernel and was made available during the 2.4 series of stable kernels. Although it was present in the kernel, this method of creating devices never received overwhelming support from developers. The main problem with the approach adopted by devfs was the way it handled device detection and connection. The latter issue, device naming, was perhaps the most critical. It is generally accepted that if device names are allowed to be configurable, then the policy should be up to the system administrator. devfs also suffered from race conditions inherent in its design and could not be fixed without a substantial revision to the kernel. It was deprecated for a long period – due to lack of maintenance – and was finally removed from the kernel in June 2006.

With the development of the unstable 2.5 kernel, later released as the 2.6 series of stable kernels, a new filesystem called sysfs came to be. The job of sysfs is to export the view of the system's hardware configuration to userspace. With this userspace-visible representation, the possibility of developing a replacement for devfs became much more realistic.

### 7.3.2. Udev Implementation

#### 7.3.2.1. Sysfs

#### 7.3.2.2. Device Node Creation

Device files are created by the kernel by devtmpfs. Any driver that wishes to register a device node will go through sysfs (via the device core) to do it. A devtmpfs instance is mounted on /dev, the device node will initially be created with a fixed name, permissions, and other. A short time later, the kernel will send an event to udev. Based on the rules specified in the files within /etc/udev/rules., /lib/udev/rules.d, and /run/udev/rules.d, udev will create symlinks to the device node, or change its permissions, owner, or group, or modify the udev database entry (name) for that. The rules in these directories are all merged together. If udev can't find a rule for the device it is creating, it will leave the permissions and ownership at whatever devtmpfs used initially.

### 7.3.2. Module Loading

Device drivers as modules may have aliases built into them. Aliases are usually related to the bus-specific identifiers of devices supported by a module. For example, the snd-pcm driver supports PCI devices with vendor ID 0x1319 and device ID 0x0801, and has an alias of `pci:v0001319d00000801*=snd-pcm*`. For most devices, the bus driver exports the aliases of the driver which would handle the device. E.g., the `/sys/bus/pci/devices/0000:00:1d.0/modalias` file might contain the string "pci:v0001319d00000801s00001319d000001bc4c00*". The default rules provided by Udev will call udev to `/sbin/modprobe` with the contents of the MODALIAS environment variable for loading all modules whose aliases match this string after wildcard expansion.

In this example, in addition to snd-pcm, the obsolete (and unwanted) driver will be loaded if it is available. See below for ways in which the unloading of unwanted drivers can be prevented.

The kernel is also able to load network protocols, filesystems and NLS support on demand.

### 7.3.4. Handling Hotpluggable/Dynamic Devices

When you plug in a device, such as a Universal Bus (USB) MP3 player, the kernel recognizes the device is now connected and generates a uevent. This is then handled by udev as described.

### 7.3.3. Problems with Loading Modules and Creating Devices

There are a few possible problems when it comes to automatically creating device nodes.

### 7.3.3.1. A kernel module is not automatically loaded

Udev will only load a module if it has a bus-specific alias and the bus driver exports the necessary aliases to sysfs. In other cases, no other module loading will occur. With Linux-5.2.8, Udev is known to load well-written drivers for INPUT, PCI, USB, SCSI, SERIO, and FireWire.

To determine if the device you require the necessary support for Udev, run modinfo with the module name as your argument and check whether there is a modalias file.

If no modalias exists in sysfs, the driver supports the device and can talk to it directly, but doesn't have the alias, it is a bug. Load the driver without help from Udev and expect the issue to be fixed.

If there is no modalias file in the relevant directory under /sys/bus/, this means that the kernel developers have not added modalias to this bus type. Expect this issue to be fixed in later kernel versions.

Udev is not intended to load “wrapper” drivers such as snd-pcm-oss and non-hardware drivers as loop at all.
