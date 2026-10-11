System information appears as a file. For example, the /proc/kcore file is just a method for addressing your computer's memory. If you type ls -1 /proc/kcore you will see the amount of memory in your system as bytes. Only root can access the proc directory. A sample output from ls -1 /proc is

```
```
dr-xr-x  3 root root         0 Nov 10 16:24 1
dr-xr-x  3 root root         0 Nov 10 16:24 2
dr-xr-x  3 bin  root       212 Nov 10 16:24 212
-r--r-----  1 root root     0 Nov 10 16:24 cmdline
-r--r-----  1 root root     0 Nov 10 16:24 cpuinfo
-r--r-----  1 root root     0 Nov 10 16:24 devices
-r--r-----  1 root root     0 Nov 10 16:24 dma
-r--r-----  1 root root     0 Nov 10 16:24 filesystems
-r--r-----  1 root root     0 Nov 10 16:24 interrupts
-r--r-----  1 root root     0 Nov 10 16:24 ioparts
-r---------  1 root root 134156288 Nov 10 16:24 kcore
-r--------  1 root root     0 Nov 5 18:23 kmsg
-r--r-----  1 root root     0 Nov 10 16:24 ksyms
-r--r-----  1 root root     0 Nov 10 04:23 loadavg
-r--r-----  1 root root     0 Nov 10 16:24 locks
-r--r-----  1 root root     0 Nov 10 16:24 mddstat
-r--r-----  1 root root     0 Nov 10 16:24 meminfo
```
```

A directory is created for each of the processes that is running named with the process's ID. This system information is helpful when diagnosing system problems. Say you want to see the interrupts on your system. You could issue the command cat /proc/interrupts, which would result in an output similar to the following:

```
```
0: 42516998 timer
1: 539 keyboard
2: 0 cascado
5: 0 + es1370
6: 11 + floppy
8: 1 rtc
10: 69455 eth0
12: 132 PS/2 Mouse
13: 1 math error
14: 277135 + ide0
15: 0 + ide1
```
```

This file lists all your system's interrupts that are being used and what is using each one.