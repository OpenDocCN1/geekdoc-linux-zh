catch it and invoke a user-defined signal handler, or take the default action. See “Signals” on page 324.

The `/etc/crash` utility provides a function, shown below, for dumping a process’s uarea.

```
```text
# /etc/crash
dumpfile = /dev/mem, namelist = /dev/ksyms, outfile = stdout
> u 67
PER PROCESS USER AREA FOR PROCESS 67
PROCESS MISC:
        command: crash, psargs: /etc/crash
        start: Fri May  5 21:37:41 2000
        mem: 4cf9, type: exec
        vnode of current directory: f64769c0
OPEN FILES, OPEN FILE FLAGS, AND THREAD REFERENT:
        [0]: F 0x6407cd0, 0, 0 [1]: F 0x6407cd0, 0, 0
        [2]: F 0x6407cd0, 0, 0 [3]: F 0x65695a8, 0, 0
        [4]: F 0x6569300, 0, 0 [5]: F 0x6569300, 0, 0
        [6]: F 0x6569b98, 0, 0
cmask: 0022
RESOURCE LIMITS:
        cpu time: 18446744073709551613/18446744073709551613
        file size: 18446744073709551613/18446744073709551613
        swap size: 2147489552/2147489552
        stack size: 8388608/2147489552
        coredump size: 18446744073709551613/18446744073709551613
        file descriptor: 64/1024
        address space: 18446744073709551613/18446744073709551613
SIGNAL DISPOSITION:
        1: default  2: c#63914  3: default  4: default
        5: default  6: default  7: default  8: default
        9: default 10: default 11: default 12: default
       13: default 14: default 15: default 16: default
       17: default 18: default 19: default 20: default
       21: default 22: default 23: default 24: default
       25: default 26: default 27: ignore  28: default
       29: default 30: default 31: default 32: default
       33: default 34: default 35: default 36: default
       37: default 38: default 39: default 40: default
       41: default 42: default 43: default 44: default
       45: default
```
```

In the preceding example, we omitted the up-front dumping of the process table (the `p` function) to select a process’s uarea to dump. The `u` function takes a process table slot number as an argument, slot 19 in this case (the Xsession process, the same one used in the examples files example). Note the rather large values in the resource limits. This example was done on a Solaris 2.6 system, which included 64-bit data types for the rlimits.

# 8.2.3 The Lightweight Process (LWP)

The LWP structure is defined in `/usr/include/sys/klwp.h`. The kernel maintains resource utilization counters and microstate accounting information for every LWP. The sum of all LWPs resource usage is stored in the process when the LWP exits. See “The Kernel Process Table” on page 290.