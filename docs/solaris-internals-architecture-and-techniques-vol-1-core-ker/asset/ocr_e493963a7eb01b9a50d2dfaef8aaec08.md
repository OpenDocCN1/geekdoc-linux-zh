vent mapping of the stack pages with permissions on Solaris 2.6 and
Solaris 7. The entry in the /etc/system file will look like:

```
set no_exec_user_stack = 1
```

Note that Solaris 2.5.1 does not include this tunable parameter. Here is an
address space dump of process on Solaris 2.6.

```
/usr/proc/bin/pmap -x 25639
25639: tp
Address Kbytes Shared Private Permissions Mapped File
00010000 8 8 8 - read/exec dev:193,2 ino:1089162
00020000 8 8 8 - read/write/exec dev:193,2 ino:1089162
00022000 1032 1032 1032 read/write/exec [ heap ]
FE5E0000 1024 1024 1024 read/write/exec/shm/ [shmid:0x12d2]
FE6E0000 8 8 8 - read/exec [ anon ]
FE6F0000 16 16 16 - read/exec libc.so.1
FE700000 592 552 544 8 read/exec libc.so.1
FE710000 24 24 8 - read/write/exec libc.so.1
FE7A0000 8 8 8 read/exec [ anon ]
FE7B0000 8 8 8 - read/write/exec [ anon ]
FE7F0000 8 8 8 - read/exec ld.so.1
FE800000 104 104 104 - read/write/exec ld.so.1
FE810000 8 8 8 - read/write/exec ld.so.1
FE8E0000 4104 4104 4104 - read/write/exec [ stack ]
total kb 6994 6994 704 6200
```

Here's a pmap(1) dump of a 64-bit executable on a Solaris 7 system, complete\with 64-bit addresses. For 64 bits, the SPARC V9 Application Binary Interface
defines pages as read/write only, to block buffer overflows.

```
/usr/proc/bin/pmap -x 9964
9964: mem 1048576
Address Kbytes Shared Private Permissions Mapped File
0000000000000000 8 8 8 - read/exec mem
0000000000010000 8 8 8 - read/write/exec mem
0000001000100010 1040 1032 1032 read/write/exec [ heap ]
FFFFFFFF 696 576 416 160 read/exec libc.so.1
FFFFFFFF 64 64 64 read/write/exec libc.so.1
FFFFFFFF 8 8 8 - read/write/exec ld.so.1
FFFFFFFF 112 112 112 - read/exec ld.so.1
FFFFFFFF 16 16 16 - read/exec libc_par.so.1
FFFFFFFF 8 8 8 - read/exec [ anon ]
FFFFFFFF 8 8 8 - read/write/exec libbdl.so.1
FFFFFFFF 16 16 16 - read/write [ stack ]
total kb 2000 1864 552 1312
```

+   - p_lock — Lock structure pointer. the p_lock is a kernel mutex (mutual exclusion) that synchronizes access to specific fields in the process (see Chapter 2, Kernel Services). This level of granularity of kernel lock increases parallelism whereas there is not a single lock on the\entire process table. Instead, there is per-table locking, which that multiple
kernel threads can concurrently access different proc structures.