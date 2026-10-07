Some people automatically turns services on in run levels 2, 4, and 5, so if your output indicates that these levels are on, this is fine. These changes only start the daemon on reboot, so if you want to test whether turning on the NFS daemon allows your problem, run the NFS initialization script like this:

```
# /etc/rc.d/init.d/nfs
```

If you still get the 'Permission Denied' error, check the /etc/hosts.allow file for the mounting machine. The three lines below should be included. Change the IP as appropriate. any machine on the 192.168.1.0 subnet may export.

```
portmap: 192.168.1.0/255.255.255
rpc.mountd: 192.168.1.0/255.255.255
rpc.nfsd: 192.168.1.0/255.255.255
```

# The free Command Reports Less Memory Than the Machine Has

There are two common problems of interpretation of the output of the free command. To understand these, let's consider some sample output, created on a machine with 96MB of physical memory:

```
$ free
total used free shared cached
Mem: 95772 87968 51148 5572 28008
| +/- buffers/cache: 54388 41384 |
| Swap: 136512 12308 124204 |
```

The total column lists both RAM (on the Mem line) and swap space (on the Swap line). You can see, 95,772KB is less than 96MB (98,304KB). Most of this discrepancy is caused by the Linux kernel itself, which typically consumes about 2-4MB of RAM (The kernel image stored in /boot is usually compressed, and parts of it are discarded after being loaded, so its size isn't a good judge of how large the in-memory kernel is). You lose some RAM to shadowed ROMs, I/O space, and other artifacts of your computer's architecture.

The second problem many people have is that the amount of used is very high (or, alternatively, the amount free is very low), as reported by the (or free) column's entry on the Mem line. This is usually an illusion, however, because Linux dynamically assigns memory to disk cache duty. This speeds up disk access by temporarily storing information from disk in RAM. If the RAM is needed for other purposes, Linux ditches some of the disk cache. The -/+ buffers/cache line reports a true estimate of the amount of memory used. As you can see, it shows a much less extreme memory load