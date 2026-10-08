
# Chapter 5. The proc File System

- btime — The boot time, measured in the number of seconds since January 1, 1970, otherwise known as the *epoch*.

## 5.2.28. /proc/swaps

This file measures swap space and its utilization. For a system with only one swap partition, the output of `/proc/swap` may look like this:

```
| Filename | Type | Size | Used | Priority |
| /dev/hda6 | partition | 136512 | 20024 | -1 |
```

While some of this information can be found in other files in the `/proc/` directory, /proc/swap provides a snapshot of every swap file, the type of swap space, the total size, and the amount of this space that is in use (in kilobytes). The priority column is useful when multiple swap files are in use. The lower the priority, the more likely the swap file is to be used.

## 5.2.29. /proc/uptime

This file contains information detailing how long the system has been on since its last restart. The output of `/proc/uptime` is quite minimal:

```
350735.47 234388.90
```

The first number is the total number of seconds the system has been up. The second number is how much of time the machine has spent idle, in seconds.

## 5.2.30. /proc/version

This file specifies the version of the Linux kernel and `gcc` in use, as well as the version of Red Hat installed on the system:

```
Linux version 2.4.20-0.40 (user@foo.redhat.com) (gcc version 3.2.1 20021125
(Red Hat Linux 8.0 3.2.1-1)) #1 Tue Dec 3 20:50:18 EST 2002
```

This information is used for a variety of purposes, including the version data presented when a user logs in.

## 5.3. Directories in /proc/

Common groups of information concerning the kernel are grouped into directories and subdirectories within the `/proc/` directory.

### 5.3.1. Process Directories

Every `/proc/` contains a number of directories with numerical names. A listing of the may begin things like this:

```
dr-xr-xr-x 3 root root      0 Feb 13 01:28 1
dr-xr-xr-x 3 root root      0 Feb 13 01:28 1010
dr-xr-xr-x 3 xfs xfs        0 Feb 13 01:28 1087
dr-xr-xr-x 3 daemon daemon  0 Feb 13 01:28 1123
dr-xr-xr-x 3 root root      0 Feb 13 01:28 11307
dr-xr-xr-x 3 apache apache 0 Feb 13 01:28 13660
dr-xr-xr-x 3 rpc rpc 0 Feb 13 01:28 637
dr-xr-xr-x 3 rpcuser rpcuser 0 Feb 13 01:28 666
```

These directories are called process directories, as they are named after a program's process ID and contain information specific to that process. The owner and group of each process directory is set to the user running the process. When the process is terminated, its /proc process directory vanishes. Each process directory contains the following:

- cmdline The command issued when starting the process.
- cpu Provides specific information about the utilization of each of the system's CPUs. A process running on a dual CPU system produces output similar to:
```
cpu 11 3
cpu0 0
cpu1 11 3
```
- cwd A symbolic link to the current working directory for the process.
- environ Gives a list of the environment variables for the process. The environment variable is given in upper-case, and the value is in lower-case.
- exe A symbolic link to the executable of this process.
- fd A directory containing all the file descriptors for a process. These are given in total:
```
lrwx------ 1 root root 64 May 08:31:00 -> /dev/null
lrwx------ 1 root root 64 May 08:31:01 -> /dev/null
lrwx------ 1 root root 64 May 08:31:02 -> /dev/null
lrwx------ 1 root root 64 May 08:31:03 -> /dev/ptmtx
lrwx------ 1 root root 64 May 08:31:04 -> socket:[7774817]
lrwx------ 1 root root 64 May 08:31:05 -> socket:[7774829]
lrwx------ 1 root root 64 May 08:31:07 -> /dev/ptmtx
```
- maps Contains maps to various variables and library files associated with this process. This file can be longer, depending on the complexity of the process, but sample output from the sshd process being:
```
04800480-08600880 r-x 00000000 03 03 394179 /usr/bin/sshd
08600880-08800880 rw-p 0003e00 03 03 394179 /usr/bin/sshd
08800880-08905000 rw 00000000 00 00 000000
40000000-40010000 r-x 00000000 03 03 239205 /lib/ld-2.2.so
40010000-40030000 rw-p 0001300 03 03 239205 /lib/ld-2.2.so
40030000-40038000 rw-p 0023282 03 03 239282 /lib/libpam.so
40038000-4003a000 rw-p 00000000 00 00 000000 /lib/libpam.so
4003a000-4003c000 r-x 00000000 03 03 239218 /lib/ld-2.2.so
4003c000-4003d000 rw-p 00010100 03 03 239218 /lib/ld-2.2.so
```
- mem The memory held by the process.
- root A link to the root directory of the process.
- stat The status of the process.
- statm The status of memory in this process. Below a sample /proc/stat file: 263 210 5 0.

The seven columns relate to memory statistics for the process. From left to right, report the following aspects of the memory used:
1. Total program size, in kilobytes
2. Size of memory portions, in kilobytes
3. Number of pages that are shared
4. Number of pages of code
5. Number of pages of data/stack
6. Number of library pages
7. Number of dirty pages

status — The status of the process in a more readable form than stat or statm. Sample output for sshd looks similar to:
```
Name: sshd
State: S (sleeping)
Tgid: 797
Pid: 797
PPid: 1
Uid: 0 0 0
Gid: 0 0 0
FD: 32
Groups:
VmSize: 3072 kB
VmL: 0 kB
VmRSS: 840 kB
VmData: 104 kB
VmStk: 12 kB
VmExec: 300 kB
VmLib: 2529 kB
Vmnd: 00000000000000
VmBlk: 00000000000000
VmIgn: 00000000000001
VmCgt: 00000000000005
CapIn: 00000000000000
CapPrm: 00000000000000
CapEff: 00000000000000
```
The information in this output includes the process name and ID, the state (such as S (sleeping) or R (running)), group ID, and detailed data regarding memory usage.

## 5.3.1. /proc/self

The /proc/self/ directory is a link to the currently running process. This allows a process to look at itself without having to know its ID. Within a shell environment, a listing of /proc/self/ produces the same contents as the directory for that process.

## 5.3.2. /proc/bus/

This directory contains information specific to the buses available on the system. So, for example, on a standard system containing ISA, PCI, and USB, current data on each of these buses is available in its directory under /proc/bus/. The contents of the subdirectories and files varies greatly on the precise configuration of the system. However, each of the directories for each bus type has at least one directory for each bus. These individual bus directories are signified with numbers, such as 00, contain binary files that refer to the various devices available on bus. So, for example, a system with a USB bus but no USB devices connected to it has a /proc/bus/usb/ directory containing several files:
```
total 0
dr-xr-xr-x 1 root root      0 May 3 16:25 001
--r--r--r-- 1 root root      0 May 3 16:25 devices
--r--r--r-- 1 root root      0 May 3 16:25 drivers
```

The /proc/bus/usb/ directory tracks the various devices on any USB buses, as well as the drivers required to use them. The /proc/bus/usb/001/ directory contains all devices on the first bus. By looking at the contents of the devices file, one can identify the USB root hub on the motherboard:
```
T: Bus=01 Lev=00 Rt=00 Cnt=00 DevB=1 Spd=12 MxCh=2
B: Alloc=0/900 us ( ) Int=0 Iso=0
D: Vendor=1.0 Cl=09(hub ) Sub=00 Prot=0 MxFS=8 Cfg=1
P: Vendor=0000 PID=0000 Rev=0
Product=USB Hub
SerialNumber=d400
C*: Ifs=1 Cfg=1 At=40 MxPwr=0Ma
I: Ifs=0 Alt=0 Efs=1 Cl=09(hub ) Sub=00 Prot=00 Driver=hub
E: Ad=81 (1) At=03 (Int.) MxFS=8 Ivl=255
```

## 5.3.3. /driver/

This directory contains information for specific drivers in the kernel. A common file found here is rtc, which provides output from the driver for the system's Real Time Clock (RTC), the device that keeps the time while the system is switched off. Sample output from /proc/driver/rtc looks like:
```
rtc_time : 01:38:43
rtc_date : 1998-02-13
rtc_epoch : 1900
alarm : 00:00:00
DST_enable : no
BCD : yes
24hr : no
square_wave : no
alarm_IRQ : no
update_IRQ : no
periodic_IRQ : no
periodic_freq : 1024
batt_status : okay
```

For more information about the RTC, /user/src/linux-2.4/Documentation/rtc.txt.
