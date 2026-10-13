
You can also create unbuffered character devices and pipes with mknod. The devices.txt file listed previously will tell you when you need to use u in place of c with mknod. Named pipes, created with the p, are usually created by programs (and do not take major and minor numbers), but you can create one and use it with scripts. However, that is beyond the scope of this text.

## The /devfs Directory

Now that you’ve learned all about the historical devices in /dev, when you look there you might see something totally different (or not). Assuming Caldera OpenLinux uses /devfs, it might implement it using the old names. It might choose instead to use either the kernel names or the even newer (and changing) devfs names.

When you start to understand the /dev naming scheme, you’ll see that it matters little what devices are called, because the kernel knows them by their major and minor numbers. After you find out what a particular device is called, you can have a program reference and use it. If you create a block device in your home directory called foo1 with major number 3 and minor number 1 and look at it (you can do this with the command: less -f foo1), you will be looking at your IDE 0 (drive C:) hard drive’s first partition. This is why ordinary users cannot create device files—this would nullify any permissions you might have.

## The /proc Directory

As was previously mentioned, the /proc directory is actually a unique filesystem. Listing the files in this directory doesn’t really give you any clues that there is anything unusual about this directory—until you take a closer look at the file sizes. All the files and directories have a file size of 0, with two exceptions: kcore and self. A directory listing looks similar to the following:

```text
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 1
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 2
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 21
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 22
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 23
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 24
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 3
dr-xr-xr-x   3 bin     root        0 Dec  6 01:13 360
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 362
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 373
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 376
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 387
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 4
dr-xr-xr-x   3 daemon  root        0 Dec  6 01:13 425
dr-xr-xr-x   3 nobody  65535      0 Dec  6 01:13 465
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 5
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 525
dr-xr-xr-x   3 root    root        0 Dec  6 01:13 56
dr-xr-xr-x   3 root    users       0 Dec  6 01:48 860
dr-xr-xr-x   3 root    users       0 Dec  6 01:48 861
dr-xr-xr-x   3 col     users       0 Dec  6 01:48 862
-r--r--r--   1 root    root        0 Dec  6 01:13 cmdline
-r--r--r--   1 root    root        0 Dec  6 01:13 cpuinfo
-r--r--r--   1 root    root        0 Dec  6 01:13 devices
-r--r--r--   1 root    root        0 Dec  6 01:13 dma
-r--r--r--   1 root    root        0 Dec  6 01:13 filesystems
-r--r--r--  1 root  root         0 Dec 6 01:13 interrupts
-r--r--r--  1 root  root         0 Dec 6 01:13 ioports
-r--r--r--  1 root  root  33558528 Dec 6 01:13 kcore
-r--r--r--  1 root  root         0 Dec 3 18:12 kmsg
-r--r--r--  1 root  root         0 Dec 6 01:13 ksyms
-r--r--r--  1 root  root         0 Dec 6 01:13 loadavg
-r--r--r--  1 root  root         0 Dec 6 01:13 locks
-r--r--r--  1 root  root         0 Dec 6 01:13 mdstat
-r--r--r--  1 root  root         0 Dec 6 01:13 meminfo
-r--r--r--  1 root  root         0 Dec 6 01:13 modules
-r--r--r--  1 root  root         0 Dec 6 01:13 mounts
dr-xr-xr-x  2 root  root         0 Dec 6 01:13 net
-r--r--r--  1 root  root         0 Dec 6 01:13 pci
dr-xr-xr-x  2 root  root         0 Dec 6 01:13 scsi
lrwxrwxrwx  1 root  root        64 Dec 6 01:13 self -> 889
-r--r--r--  1 root  root         0 Dec 6 01:13 stat
dr-xr-xr-x  5 root  root         0 Dec 6 01:13 sys
-r--r--r--  1 root  root         0 Dec 6 01:13 uptime
-r--r--r--  1 root  root         0 Dec 6 01:13 version
```

Each of the numbered directories corresponds to an actual process ID. Looking at the process table, you can match processes with the associated process ID. For example, the process table might indicate the following for the Web server:

```text
# ps ax | grep httpd
460     ?   S     0:00 httpd -f /etc/httpd/apache/conf/httpd.conf
```

Details of this process can be examined by looking at the associated files in the directory for this process, /proc/460. You might wonder how you can see details of a process that has a file size of 0. It makes more sense if you think of it as a window into the kernel. The file doesn’t actually contain any data; it just acts as a pointer to where the actual process information resides. A listing of the files in the /proc/460 directory looks similar to the following:

```text
-r--r--r--  1 root  root   0 Dec 6 21:21 cmdline
lrwx------  1 root  root  64 Dec 6 21:21 cwd -> [0303]:2
-r--r--r--  1 root  root   0 Dec 6 21:21 environ
lrwx------  1 root  root  64 Dec 6 21:21 exe -> [0303]:43066
dr-x------  1 root  root   0 Dec 6 21:21 fd
-r--r--r--  1 root  root   0 Dec 6 21:21 maps
-rw-------  1 root  root   0 Dec 6 21:21 mem
lrwx------  1 root  root  64 Dec 6 21:21 root -> [0303]:2
-r--r--r--  1 root  root   0 Dec 6 21:21 stat
-r--r--r--  1 root  root   0 Dec 6 21:21 statm
-r--r--r--  1 root  root   0 Dec 6 21:21 status
```

Even though the files appear to be of size 0, examining their contents reveals otherwise:

```text
# cat status
Name:     httpd.apache
State:    S (sleeping)
Pid:      460
PPid:     1
Uid:      0       0       0       0
Gid:      0       0       0       0
VmSize:   1332 kB
VmLck:       0 kB
VmRSS:      688 kB
VmData:      300 kB
VmStk:        20 kB
VmExe:       376 kB
VmLib:       592 kB
SigPnd: 00000000
SigBlk: 00000000
SigIgn: 80000000
SigCgt: 0000466b
```

The man page for proc describes each of the files associated with a running process ID in detail.

The files in the /proc directory act very similar to the process ID subdirectory files. For example, examining the contents of the /proc/interrupts file displays something like the following:

```text
# cat interrupts
 0:   27222899   timer
 1:       3152   keyboard
 2:          0   cascade
 9:     450448   eth0
12:       4477   PS/2 Mouse
13:          1   math error
14:      15198 + ide0
15:          0 + ide1
```

Each number down the left-hand column represents an interrupt that is in use. Examining the contents of the file dynamically gathers the associated data and displays it to the screen. Most of the /proc filesystem is read-only; however, some files enable kernel variables to be changed. This provides a mechanism to actually tune the kernel without recompiling and rebooting.

The procinfo utility (which may not be included with OpenLinux) summarizes /proc file-system information into a display similar to the following:

```text
# /usr/bin/procinfo

Linux 2.0.35 (root@buildmeister.caldera.com) (gcc 2.7.2.3) #1 [train2]

Memory:       Total       Used       Free      Shared    Buffers     Cached
Mem:          30884      20332      10552      10840       8900       5292
Swap:         66492          0      66492

Bootup: Thu Dec 03 18:12:23 1998   Load average: 0.00 0.00 0.00 3/38 895

user :     0:00:19.69   0.0%  page in :  10886  disk 1:  6791r 3742w
nice :     0:00:00.00   0.0%  page out:   6089
system:    0:00:34.14   0.0%  swap in :      1
idle :     2d  7:42:19.82 100.0% swap out:     0
uptime:    2d  7:43:13.61          context : 1083993

irq  0:  20059365 timer                irq  8:          0
irq  1:         4 keyboard             irq  9:     326636 eth0
irq  2:         0 cascade [4]          irq 10:          0
irq  3:         0                      irq 11:          0
irq  4:         0                      irq 12:          0
irq  5:         0                      irq 13:          1 math error
irq  6:         2                      irq 14:      10515 ide0+
irq  7:         0                      irq 15:          0 ide1++
```
