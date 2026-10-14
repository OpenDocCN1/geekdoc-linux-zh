OOM killer does kick in, you will see lines like the following in your /var/log/syslog:

```
1228419127.32453_1704.hostname:2;5:Out of Memory: Killed process
21389 (java).
1228419127.32453_1710.hostname:2;5:Out of Memory: Killed process
21389 (java).
```

# Diagnose High I/O Wait

When I see high I/O wait, one of the first things I check is whether the machine is using a lot of swap. Since a hard drive is much slower than RAM, when a system runs out of RAM and starts using swap, the performance of almost any machine suffers. Anything that wants to access the disk has to compete with swap for disk I/O. So first diagnose whether you are out of memory and, if so, manage the problem there. If you do have plenty of RAM, you will need to figure out which program is consuming the most I/O.

It can sometimes be difficult to figure out exactly which process is using the I/O, but if you have multiple partitions on your system, you can narrow it down by figuring out which partition most of the I/O is on. To do this you will need the iostat program, which is provided by the sysstat Ubuntu package, so type

```
$ sudo apt-get install sysstat
```

Preferably you will have this program installed before you need to diagnose an issue. Once the program is installed, you can run iostat without any arguments to see an overall glimpse of your system:

```
$ sudo iostat
Linux 2.6.24-19-server (hostname) 01/31/2009

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
          5.73    0.07    2.03    0.53    0.00   91.64

Device:         tps   Blk_read/s   Blk_wrtn/s   Blk_read    Blk_wrtn
sda            9.82      417.96       27.53    30227262    1990625
sda1           6.55      219.10        7.12    15845129     515216
sda2           0.04        0.74        3.31       53506     239328
sda3           3.24      198.12       17.09    14328233    1236081
```