max locked memory    (kbytes, -l) unlimited
max memory size      (kbytes, -m) unlimited
open files              (-n) 1024
pipe size              (512 bytes, -p) 8
stack size            (kbytes, -s) unlimited
cpu time              (seconds, -t) unlimited
max user processes        (-u) 1024
virtual memory        (kbytes, -v) unlimited

Individual switches specify specific resources:

+   - `-c`—Maximum size of core files
+   - `-d`—Maximum size of a process’s data segment
+   - `-f`—Maximum size of shell-created files
+   - `-l`—Maximum amount of memory that can be locked
+   - `-m`—Maximum resident set size
+   - `-n`—Maximum number of open file descriptors
+   - `-p`—Pipe size (cannot be set)
+   - `-s`—Maximum stack size
+   - `-t`—Maximum CPU time
+   - `-u`—Maximum number of processes for a single user
+   - `-v`—Maximum amount of virtual memory available to the shell

Each resource has both a maximum hard limit, and a current soft limit, which can be any amount up to the maximum. For example, the stack size can have both a hard and soft limit. You can check these limits with the -H (hard limit) and -S (soft limit) switches.

```
$ ulimit -H -s
unlimited
$ ulimit -S -s
8192
```

The stack size here is limited to 8K, but it can be changed to any number of bytes. To change a limit, supply a new value to the ulimit command

```
$ ulimit -S -s 16384
$ ulimit -S -s
16384
```

The special values hard and soft, refer to the current hard or soft limit. Use them to copy one limit to the other limit.

```
$ ulimit -H -s soft
$ ulimit -H -s
16384
```