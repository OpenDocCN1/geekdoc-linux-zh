# gdb

We can use gdb to create a core dump. For creating a core dump of a particular process, we specify the problematic process PID as an debug parameter, and once it is in the debug mode, from gdb we can obtain a core dump. In Figure 3-11, gdb has created a core dump with the name core.1863 in the current directory.

```
lnx02:~ # gdb -p 1863
GNU gdb 6.3
Copyright 2004 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License,
and you are
welcome to change it and/or distribute copies of it under certain
conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB. Type "show warranty" for
details.
This GDB was configured as "s390x-suse-linux".
Attaching to process 1863
Reading symbols from /root/a.out...done.
Using host libthread_db library "/lib64/tls/libthread_db.so.1".
Reading symbols from /lib64/tls/libc.so.6...done.
Loaded symbols for /lib64/tls/libc.so.6
Reading symbols from /lib/ld64.so.1...done.
Loaded symbols for /lib/ld64.so.1
0x00000200000ccd4 in wait () from /lib64/tls/libc.so.6
(gdb) generate-core
Saved corefile core.1863
(gdb) quit
The program is running. Quit anyway (and detach it)? (y or n) y
Detaching from program: /root/a.out, process 1863
```

Figure 3-11 Example of obtaining core dump using gdb

# gcore

Like gdb, in Red Hat we have a gcore as an default command to creates a core image of the specified process, suitable for use with gdb. By default, the core is written to the file core.<pid> in the current directory. The process identifier, pid, must be given on the command line.

Example 3-32 Example creation of core using gcore

```
gcore <PID>
gcore 1863
```