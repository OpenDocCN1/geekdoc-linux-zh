# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

dc3dd 7.2.641 started at 2017-05-05 23:39:47 -0400
compiled options:
command line: dc3dd ofs=nc.dc3dd.000 ofsz=2G log=nc.dc3dd.log
sector size: 512 bytes (assumed)
0 bytes ( ) copied (%%), 3 s, 0 K/s

The dc3dd output will start immediately, but stay at 0 bytes until it receives input
through the pipe. As soon as you start the imaging process on the subject matter, you'll see
the dcdd command on the listening machine start to process the incoming data. Again
notice we are using plain dd on the subject box to stream bytes over the pipe. dc3dd
takes over on the collection machine to implement dc3dd options and logging.

```
root@bootdisk:~# dd if=/dev/sda | nc 192.168.0.1 2525
```

When the transfer is complete, we can look at the results and the dc3dd log on
ourour machine.

```
root@forensic:~# ls -l /mnt/evid/nc.dc3dd.*
-rw-r--r 1 root 0 May 5 23:40 nc.dc3dd.000
-rw-r--r 1 root 2147483648 May 5 23:16 nc.dc3dd.001
-rw-r--r 1 root 2147483648 May 5 23:17 nc.dc3dd.002
-rw-r--r 1 root 2147483648 May 5 23:18 nc.dc3dd.003
-rw-r--r 1 root 2147483648 May 5 23:19 nc.dc3dd.004
-rw-r--r 1 root 2147483648 May 5 23:20 nc.dc3dd.005
-rw-r--r 1 root 2147483648 May 5 23:20 nc.dc3dd.006
```

```
root@forensic:~# cat /mnt/evid/nc.dc3dd.log
dc3dd 7.2.641 started at 2017-05-05 23:11:40 -0400
compiled options:
command line: dc3dd ofs=nc.dc3dd.000 ofsz=2G log=nc.dc3dd.log
sector size: 512 bytes (assumed)
1288401888 (12 G ) copied (%%), 747.491 s, 16 M/s
```

input results for file 'stdin:
21658284 sectors in

output results for files `nc.dc3dd.000`:
21658284 sectors out

dc3dd aborted at 2017-05-05 23:24:08 -0400

We can see that the dc3dd log ended with an "aborted" message because we had to
ually stop the listening process (with ctrl-c) in this case dc3dd is not handling the

137