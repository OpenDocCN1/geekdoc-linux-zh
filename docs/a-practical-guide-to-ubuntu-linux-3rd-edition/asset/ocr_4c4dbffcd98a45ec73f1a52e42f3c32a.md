state, memory usage, CPU usage, terminal association, parent, and group. You can extract information directly from the files in `/proc`. An example follows:

```
```
$ sleep 1000 &
[1] 3104
$ cd /proc/3104
$ ls -l
dr-xr-xr-x 2 sam sam 0 2010-04-09 14:00 attr
-r-------- 1 sam sam 0 2010-04-09 14:00 auxv
-r--r-F--- 1 sam sam 0 2010-04-09 14:00 cgroup
--w------- 1 sam sam 0 2010-04-09 14:00 clear_refs
-r--r--- 1 sam sam 0 2010-04-09 14:00 cmdline
-rw-rw---- 1 sam sam 0 2010-04-09 14:00 coredump_filter
-r--r-F--- 1 sam sam 0 2010-04-09 14:00 cpu-set
lrwxrwxrwx 1 sam sam 0 2010-04-09 14:00 cwd -> /home/sam
-r-------- 1 sam sam 0 2010-04-09 14:00 environ
lrwxrwxrwx 1 sam sam 0 2010-04-09 14:00 exe -> /bin/sleep
dr-x----- 2 sam sam 0 2010-04-09 14:00 fd
...
$ cat status
Name: sleep
State: S (sleeping)
Tgid: 3104
Pid: 3104
PPid: 1503
TracerPid: 0
Uid: 1000 1000 1000 1000
Gid: 1000 1000 1000 1000
FDSize: 256
Groups: 4 20 24 46 105 119 122 1000
VmPeak: 3232 kB
VmSize: 3232 kB
VmLck: 0 kB
...
```
```

In this example, **bash** creates a background process (PID 3104) for **sleep**. Next the user changes directories to the directory in `/proc` that has the same name as the PID of the background process (**cd /proc/3104**). This directory holds information about the process it is named for—the **sleep** process in the example. The **ls -l** command shows that some entries in this directory are links (**cwd** is a link to the directory the process was started from, and **exe** is a link to the executable file that this process is running) and some appear to be ordinary files. All appear to be empty. However, when you use **cat** to display one of these pseudofiles (**status** in the example), cat displays output. Obviously it is not an ordinary file.

`/sbin/shutdown`  A utility that brings the system down (see page 450).

`swap`  Even though **swap** is not normally a file, swap space can be added and deleted from the system dynamically. Swap space is used by the virtual memory subsystem of the kernel. When it runs low on real memory (RAM), the kernel writes memory pages from RAM to the swap space on the disk. Which pages are written and when they