# 164 Chapter 6 + The /Proc System

```
------ 1 root root 0 2008-04-09 16:59 clear_refs
-rw-r--r-- 1 root root 0 2008-04-09 16:59 coredump_filter
-r-xr--x-- 1 root root 0 2008-04-09 16:59 cpuset
-r--rr-- 1 root root 0 2008-04-09 16:59 environ
dr------- 2 root root 0 2008-04-09 16:59 fdinfo
-r--r--r-- 1 root root 0 2008-04-09 16:59 io
-rw-r--r-- 1 root root 0 2008-04-09 16:59 loginuid
-rw-r--r-- 1 root root 0 2008-04-09 16:59 mem
-r--r--r-- 1 root root 0 2008-04-09 16:59 mounts
-r--r--r-- 1 root root 0 2008-04-09 16:59 mountstats
-rw-r--r-- 1 root root 0 2008-04-09 16:59 oom_adj
-r-xr--r-- 1 root root 0 2008-04-09 16:59 oom_score
-rw-xr-x-- 1 root root 0 2008-04-09 16:59 sched
-r--xr--r-- 1 root root 0 2008-04-09 16:59 schedstat
-r--r--r-- 1 root root 0 2008-04-09 16:59 smaps
-r--r--r-- 1 root root 10 2008-04-09 16:59 statm
dr-xr-xr-x 3 root root 0 2008-04-09 16:59 task
-r--xr--r-- 1 root root 0 2008-04-09 16:59 wchan
-r--r--r-- 1 root root 0 2008-04-08 16:58 cmdline
-r--r--r-- 1 root root 0 2008-04-08 16:58 status
lrwx-xr-x 1 root root 0 2008-04-07 16:57 cwd -> /tmp
lrwx-xr-x 1 root root 0 2008-04-07 16:57 exe -> /tmp/.x1-lock (deleted)
dx------ 2 root root 0 2008-04-07 16:59 maps
-r--xr--r-- 1 root root 0 2008-04-07 16:59 fd
lrwx-xr-x 1 root root 0 2008-04-07 16:57 root -> /
-r--xr--r-- 1 root root 0 2008-04-07 16:57 stat
dr-xr-xr-x 6 root root 140 2008-04-09 16:57 ..
dr-xr-xr-x 140 root root 0 2008-04-09 16:20
```

The “exe” entry for this PID tells that the file in question is not hidden, it's been deleted! If you weren't already aware, on UNIX systems you can delete a file that's being used by a running process with no consequence to the process. Even though file is not listed in the /tmp directory, can still be recovered thanks to the symbolic link, as long as the process remains running. If Adam had shut the box down and taken a forensic image immediately, he may have had a much harder time to get to this point, alone where he wanted to go.

```
[root@localhost 8912]# cat exe > /tmp/mystery-binary
```

Adam was able to dump of the executable from the process memory. Now he can do some quick and dirty analysis on the file to see what its purpose is.

![](bbox=[0.045, 0.945, 0.265, 0.965])