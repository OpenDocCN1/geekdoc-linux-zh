
For Solaris, the dispadmin command displays or changes process scheduler parameters while the system is running. Some useful examples using dispadmin are as follows.

Retrieves the current scheduler parameters for the real-time class from kernel memory and writes them to the standard output (time quantum values are in microseconds):

```
$ dispadmin -c RT -g -r 1000000
# Real Time Dispatcher Configuration
RES=1000000
# TIME QUANTUM                PRIORITY LEVEL
# (rt_quantum)
1000000        #                0
1000000        #                1
... [Output truncated]
```

Retrieves the current scheduler parameters for the time-sharing class from kernel memory and writes them to the standard output (time quantum values are in nanoseconds):

```
$ dispadmin -c TS -g -r 1000000000
# Time Sharing Dispatcher Information
RES=1000000000
#ts_quantum  ts_tqexp  ts_slpret  ts_maxwait
ts_lwait  PRIORITY  LEVEL
200000000  0        50       0        50    #    0
... [Output truncated]
```

## 23.8.2 Disk Usage and Management

The following are samples of the ZFS commands from Chapter 24, and the traditional UNIX du command, that allow a system administrator to monitor the disk usage and status of the system disks.

- zpool list: Lists existing or all or indicated pools, along with health status and space usage
- zpool status: Displays the detailed health status of all or indicated pools
- zpool iostat: Displays I/O statistics for all or indicated pools
- zpool upgrade -a: Upgrades all pools to the latest available version
- zpool set deduplication on/off: Sets the deduplication property of a pool
- zpool scrub: Examines all data in the named pool and verifies that the checksums are correct
- zfs upgrade: Upgrades file systems to a new on-disk version
- du: Displays the block usage for file systems and directories

For ZFS, PC-BSD is currently at version 5000, Solaris 11 at version 34.

The following set of commands show the output of the preceding commands executed on a PC-BSD system. The output for a Solaris system is very similar, using the default pool name of rpool instead of tank.

```
[bob@pcbsd-4976] /usr/home/bob# zpool list
NAME      SIZE  ALLOC   FREE   CAP  DEDUP  HEALTH  ALTROOT
sender    95.5M  374K  95.1M   0%  1.00x  ONLINE  -
tank      928G  10.5G  917G   1%  1.00x  ONLINE  -
[bob@pcbsd-4976] /usr/home/bob# zpool list tank
NAME      SIZE  ALLOC   FREE   CAP  DEDUP  HEALTH  ALTROOT
tank      928G  10.5G  917G   1%  1.00x  ONLINE  -
[bob@pcbsd-4976] /usr/home/bob# zpool iostat
capacity  operations  bandwidth
pool      alloc   free   read write   read write
--------  -----   ----   ---- -----   ---- -----
sender    374K   95.1M     0     0     15     2
tank      10.5G  917G      0    17   9.92K  120K
--------  -----   ----   ---- -----   ---- -----
[bob@pcbsd-4976] /usr/home/bob# zpool iostat tank
capacity  operations  bandwidth
pool      alloc   free   read write   read write
--------  -----   ----   ---- -----   ---- -----
tank      10.5G  917G      0    17   9.91K  120K
[bob@pcbsd-4976] /usr/home/bob# zpool status
pool: sender
state: ONLINE
scan: none requested
config:
NAME                     STATE     READ WRITE CKSUM
sender                   ONLINE       0     0     0
  /usr/home/bob/master   ONLINE       0     0     0
errors: No known data errors
pool: tank
state: ONLINE
scan: resilvered 9.09G in 0h5m with 0 errors on Fri May 2 20:55:14 2014
config:
NAME      STATE     READ WRITE CKSUM
tank      ONLINE       0     0     0
  ada0s1a  ONLINE       0     0     0
```

errors: No known data errors
```
[bob@pcbsd-4976] /usr/home/bob# zfs list
NAME                USED   AVAIL   REFER   MOUNTPOINT
sender              324K   63.2M   33K     /sender
sender/bacup        70K    63.2M   31.5K   /sender/bacup
sender/data         52K    63.2M   31.5K   /sender/data
tank                10.5G  903G    144K    legacy
tank/ROOT           9.18G  903G    144K    legacy
tank/ROOT/default   9.18G  903G    9.18G   /mnt
tank/tmp            396K   903G    396K    /tmp
tank/usr            1.34G  903G    144K    /mnt/usr
tank/usr/home       170M   903G    160K    /usr/home
tank/usr/home/bob   168M   903G    168M    /usr/home/bob
tank/usr/home/sarwar 1.84M  903G    1.84M   /usr/home/sarwar
tank/usr/jails      144K   903G    144K    /usr/jails
tank/usr/obj        144K   903G    144K    /usr/obj
tank/usr/pbi        1.18G  903G    1.18G   /usr/pbi
tank/usr/ports      296K   903G    152K    /usr/ports
tank/usr/ports/distfiles 144K 903G 144K /usr/ports/distfiles
tank/usr/src        144K   903G    144K    /usr/src
tank/var            5.36M  903G    144K    /mnt/var
tank/var/audit      160K   903G    160K    /var/audit
tank/var/log        580K   903G    580K    /var/log
tank/var/tmp        4.50M  903G    4.50M   /var/tmp
[bob@pcbsd-4976] /usr/home/bob# zpool upgrade
This system supports ZFS pool feature flags.
All pools are formatted using feature flags.
Every feature flags pool has all supported features enabled.
[bob@pcbsd-4976] /usr/home/bob# zfs upgrade
This system is currently running ZFS filesystem version 5.
All filesystems are formatted with the current version.
[bob@pcbsd-4976] /usr/home/bob# zpool status sender
  pool: sender
 state: ONLINE
scan: scrub repaired 0 in 0h0m with 0 errors on Thu Jun 19 19:44:29 2014
config:
        NAME                STATE     READ WRITE CKSUM
        sender              ONLINE       0     0     0
          /usr/home/bob/master  ONLINE   0     0     0
errors: No known data errors
[bob@pcbsd-4976] /usr/home/bob# du > dufile
[bob@pcbsd-4976] /usr/home/bob# more dufile
18      ./ .i3
54      ./ .gnome/apps
62      ./ .gnome
```
