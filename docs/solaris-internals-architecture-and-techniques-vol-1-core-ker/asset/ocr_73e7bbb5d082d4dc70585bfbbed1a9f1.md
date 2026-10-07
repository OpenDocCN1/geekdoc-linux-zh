# Table 2-2 UltraSPARC Software Traps

| Trap Definition | Trap Type Value | Priority |
|---|---|---|n| Trap instruction (SunOS 4.x syscalls) | 100 | 16 |
| Trap instruction (user breakpoints) | 101 | 16 |
| Trap instruction (divide by zero) | 102 | 16 |
| Trap instruction (flush windows) | 103 | 16 |
| Trap instruction (clean windows) | 104 | 16 |
| Trap instruction (do unaligned references) | 106 | 16 |
| Trap instruction (32-bit system call) | 108 | 16 |
| Trap instruction (set trap0) | 109 | 16 |
| Trap instructions (user traps) | 110–123 | 16 |
| Trap instructions (get hrtime) | 124 | 16 |
| Trap instructions (get xrtime) | 125 | 16 |
| Trap instructions (self xcall) | 126 | 16 |
| Trap instructions (get hrestime) | 127 | 16 |
| Trap instructions (trace) | 130-137 | 16 |
| Trap instructions (64-bit system call) | 140 | 16 |

#  2.2.3 A Utility for Trap Analysis

An unbundled tool, trapstat, dynamically monitors trap activity. The tool counts of each type of trap for each processor in the system during an interval specified as the argument. This is currently implemented on UltraSPARC and Intel x86 processor architectures, on Solaris 7 and later releases.

You can download trapstat from the website for this book: http://www.solarisinternals.com. Simply untar the archive and install the driver with the add_drv command.

> Note: trapstat is not supported by Sun. Do not use it on production machines because it loads code into the kernel.

```
# tar xvf trapstat28.tar
-xr-xr-x 0/2 52668 Jan 31 03:57 2000 /usr/bin/trapstat
-rxr-xr-x 0/1 33452 Feb 10 23:17 2000 /usr/bin/sparc7/trapstat
-rwxr-xr-x 0/1 40432 Feb 10 23:16 2000 /usr/bin/sparc9/trapstat
-rw-xr--r 0/1 21225 Sep 11 22:58 1999 /usr/kernel/drv/trapstat
-rw-r--r-- 0/1 188 Aug 31 10:06 1999 /usr/kernel/drv/trapstat.conf
-rw-rw--r-- 0/1 37328 Sep 08 17:28 1999 /usr/kernel/drv/sparc9/trapstat.conf
# add_drv trapstat
```