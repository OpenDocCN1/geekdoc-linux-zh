
Although system calls occur at a relatively low level of abstraction, you can usually tell quite a bit about a process’s activity from the output. For example, the following log was produced by **strace** run against an active copy of **top**:

```
redhat$ sudo strace -p 5810
gettimeofday({1161913814, 213881}, [300, 0])          = 0
open("/proc", O_RDONLY|O_NONBLOCK|O_LARGEFILE|O_DIRECTORY) = 7
fstat64(7, {st_mode=S_IFDIR|0555, st_size=0, ...})      = 0
fcntl64(7, F_SETFL, FD_CLOEXEC)                         = 0
getdents64(7, /* 36 entries */ 1024)                    = 1016
getdents64(7, /* 39 entries */ 1024)                    = 1016
stat64("/proc/1", {st_mode=S_IFDIR|0555, st_size=0, ...}) = 0
open("/proc/1/stat", O_RDONLY|O_NONBLOCK) = 8
read(8, "1 (init) S 0 0 0 1 41945060 73"..., 1023)     = 191
close(8)                                                = 0
...
```

Not only does **strace** show you the name of every system call made by the process, but it also decodes the arguments and shows the result code the kernel returns.

**strace** is packed with goodies, most of which are documented in the man page. For example, the **-f** flag follows forked processes, which is useful for tracing daemons such as **httpd** that spawn many children. The **-e file** option displays only file operations, a feature that’s especially handy for discovering the location of evasive configuration files.

In this example, **top** starts by checking the current time. It then opens and stats the **/proc** directory and reads the directory’s contents, thereby obtaining a list of running processes. **top** goes on to stat the directory representing the **init** process and then opens **/proc/1/stat** to read the init’s status information.

Here’s an even simpler example (the **date** command) using **truss** on Solaris:

```
solaris$ truss date
...
time()                                                   = 1242507670
brk(0x00024D30)                                           = 0
brk(0x00026D30)                                           = 0
open("/usr/share/lib/zoneinfo/US/Mountain", O_RDONLY)    = 3
fstat64(3, 0xFFBFFAF0)                                    = 0
read(3, "T Z i f\0\0\0\0\0\0\0\0", 877)             = 877
close(3)                                                   = 0
ioctl(1, TCGETA, 0xFFBFFA94)                              = 0
fstat64(1, 0xFFBFF9B0)                                    = 0
write(1, " Sat May 1 14:56:46 MDT 2009\n", 29)           = 29
Sat May 1 14:56:46 MDT 2009
exit(0)
```

Here, after allocating memory and opening library dependencies (not shown), **date** uses the **time** system call to read the system time, opens the appropriate time zone file to determine the appropriate offset, and prints the date and time stamp by calling the **write** system call.

## 5.11 RUNAWAY PROCESSES

> See page 1131 for more information about runaway processes.

Runaway processes come in two flavors: user processes that consume excessive amounts of a system resource, such as CPU time or disk space, and system processes that suddenly go berserk and exhibit wild behavior. The first type of runaway is not necessarily malfunctioning; it might simply be a resource hog. System processes are always supposed to behave reasonably.

You can identify processes that use excessive CPU time by looking at the output of ps or top. If it’s obvious that a user process is consuming more CPU than is reasonable, investigate the process. It can also be useful to look at the number of processes waiting to run. Use the uptime command to show the load averages (average numbers of runnable processes) over 1, 5, and 15-minute intervals.

There are two reasons to find out what a process is trying to do before tampering with it. First, the process may be both legitimate and important. It’s unreasonable to kill processes at random just because they happen to use a lot of CPU. Second, the process may be malicious or destructive. In this case, you’ve got to know what the process was doing (e.g., cracking passwords) so that you can fix the damage.

Processes that make excessive use of memory relative to the system’s physical RAM can cause serious performance problems. You can check the memory size of processes by using top. The VIRT column shows the total amount of virtual memory allocated by each process, and the RES column shows the portion of that memory that is currently mapped to specific memory pages (the “resident set”). On Linux systems, applications that use the video card (such as the X server) get a bad rap because video memory is included in the memory usage computations.

Both of these numbers can include shared resources such as libraries, and that makes them potentially misleading. A more direct measure of process-specific memory consumption is found in the DATA column, which is not shown by default. To add this column to top’s display, type the f key once top is running and select DATA from the list. The DATA value indicates the amount of memory in each process’s data and stack segments, so it’s relatively specific to individual processes (modulo shared memory segments). Look for growth over time as well as absolute size.

Runaway processes that produce output can fill up an entire filesystem, causing numerous problems. When a filesystem fills up, lots of messages will be logged to the console and attempts to write to the filesystem will produce error messages.

The first thing to do in this situation is to determine which filesystem is full and which file is filling it up. The df -k command shows filesystem use. Look for a filesystem that’s 100% or more full. Use the du command on the identified filesystem to find which directory is using the most space. Rinse and repeat with du.

10. Most filesystem implementations reserve a portion (about 5%) of the storage space for “breathing room,” but processes running as root can encroach on this space, resulting in a reported usage that is greater than 100%.
