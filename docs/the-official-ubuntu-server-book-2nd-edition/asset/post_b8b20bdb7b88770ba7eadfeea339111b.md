
OOM killer does kick in, you will see lines like the following in your /var/log/syslog:

```
1228419127.32453_1704.hostname:2;5:Out of Memory: Killed process 21389 (java).
1228419127.32453_1710.hostname:2;5:Out of Memory: Killed process 21389 (java).
```

## Diagnose High I/O Wait

When I see high I/O wait, one of the first things I check is whether the machine is using a lot of swap. Since a hard drive is much slower than RAM, when a system runs out of RAM and starts using swap, the performance of almost any machine suffers. Anything that wants to access the disk has to compete with swap for disk I/O. So first diagnose whether you are out of memory and, if so, manage the problem there. If you do have plenty of RAM, you will need to figure out which program is consuming the most I/O.

It can sometimes be difficult to figure out exactly which process is using the I/O, but if you have multiple partitions on your system, you can narrow it down by figuring out which partition most of the I/O is on. To do this you will need the iostat program, which is provided by the sysstat Ubuntu package, so type

```
$ sudo apt-get install sysstat
```

Preferably you will have this program installed before you need to diagnose an issue. Once the program is installed, you can run iostat without any arguments to see an overall glimpse of your system:

```
$ sudo iostat
Linux 2.6.24-19-server (hostname) 01/31/2009
```

| avg-cpu: | %user | %nice | %system | %iowait | %steal | %idle |
| --- | --- | --- | --- | --- | --- | --- |
|  | 5.73 | 0.07 | 2.03 | 0.53 | 0.00 | 91.64 |

| Device | tps | Blk_read/s | Blk_wrtn/s | Blk_read | Blk_wrtn |
| --- | --- | --- | --- | --- | --- |
| sda | 9.82 | 417.96 | 27.53 | 30227262 | 1990625 |
| sda1 | 6.55 | 219.10 | 7.12 | 15845129 | 515216 |
| sda2 | 0.04 | 0.74 | 3.31 | 53506 | 239328 |
| sda3 | 3.24 | 198.12 | 17.09 | 14328233 | 1236081 |

The first bit of output gives CPU information similar to what you would see in top. Below it are I/O stats on all of the disk devices on the system as well as their individual partitions. Here is what each of the columns represents:

- **tps**: This lists the transfers per second to the device. “Transfers” is another way to say I/O requests sent to the device.
- **Blk_read/s**: This is the number of blocks read from the device per second.
- **Blk_wrtn/s**: This is the number of blocks written to the device per second.
- **Blk_read**: In this column is the total number of blocks read from the device.
- **Blk_wrtn**: In this column is the total number of blocks written to the device.

When you have a system under heavy I/O load, the first step is to look at each of the partitions and identify which partition is getting the heaviest I/O load. Say, for instance, that I have a database server and the database itself is stored on /dev/sda3. If I see that the bulk of the I/O is coming from there, I have a good clue that the database is likely consuming the I/O. Once you figure that out, the next step is to identify whether the I/O is mostly from reads or writes. Let’s say that I suspect that a backup job is causing the increase in I/O. Since the backup job is mostly concerned with reading files from the file system and writing them over the network to the backup server, I could possibly rule that out if I see that the bulk of the I/O is due to writes, not reads.

> **NOTE** You will probably have to run iostat more than one time to get an accurate sense of the current I/O on your system. If you specify a number on the command line as an argument, iostat will continue to run and give you new output after that many seconds. For instance, if I wanted to see iostat output every two seconds, I could type sudo iostat 2. Another useful argument to iostat if you have any NFS shares is -n. When you specify -n, iostat will give you I/O statistics about all of your NFS shares.

In addition to iostat, these days we have a much simpler tool available in Ubuntu called iotop. In effect it is a blend of top and iostat in that it shows you all of the running processes on the system sorted by their I/O statistics. The program isn't installed by default but is provided by the iotop Ubuntu package, so type

```
$ sudo apt-get install iotop
```

Once the package is installed, you can run iotop as root and see output like the following:

```
$ sudo iotop
Total DISK READ: 189.52 K/s | Total DISK WRITE: 0.00 B/s
```

| TID | PRIO | USER | DISK READ | DISK WRITE | SWAPIN | IO> | COMMAND |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 8169 | be/4 | root | 189.52 K/s | 0.00 B/s | 0.00 % | 0.00 % | rsync --server --se |
| 4243 | be/4 | kyle | 0.00 B/s | 3.79 K/s | 0.00 % | 0.00 % | cli /usr/lib/gnome- |
| 4244 | be/4 | kyle | 0.00 B/s | 3.79 K/s | 0.00 % | 0.00 % | cli /usr/lib/gnome- |
| 1 | be/4 | root | 0.00 B/s | 0.00 B/s | 0.00 % | 0.00 % | init |

In this case, I can see that there is an rsync process tying up my read I/O.

## Out of Disk Space

Another common problem system administrators run into is a system that has run out of free disk space. If your monitoring is set up to catch such a thing, you might already know which file system is out of space, but if not, then you can use the df tool to check:

```
$ sudo df -h
```

| Filesystem | Size | Used | Avail | Use% | Mounted on |
| --- | --- | --- | --- | --- | --- |
| /dev/sda1 | 7.9G | 541M | 7.0G | 8% | / |
| varrun | 189M | 40K | 189M | 1% | /var/run |
| varlock | 189M | 0 | 189M | 0% | /var/lock |
