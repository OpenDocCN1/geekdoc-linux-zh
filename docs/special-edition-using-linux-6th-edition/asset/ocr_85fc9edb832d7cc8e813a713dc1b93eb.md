```
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

```
# ps ax | grep httpd
460     ?   S     0:00 httpd -f /etc/httpd/apache/conf/httpd.conf
```

Details of this process can be examined by looking at the associated files in the directory for this process, /proc/460. You might wonder how you can see details of a process that has a file size of 0. It makes more sense if you think of it as a window into the kernel. The file doesn’t actually contain any data; it just acts as a pointer to where the actual process information resides. A listing of the files in the /proc/460 directory looks similar to the following:

```
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

```
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
```