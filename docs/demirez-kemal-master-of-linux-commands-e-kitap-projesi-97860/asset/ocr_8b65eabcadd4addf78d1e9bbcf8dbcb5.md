# 44 | Master of Linux Commands

# Fdisk -l

Actually, if you use disks to partition with fdisk command with -l parameters as fdisk you can see disk partitions on your system.

```
root@kemal:~# fdisk -l
Disk /dev/sda: 37,3 GiB, 40007761920 bytes, 78140160 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/o size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x85a4e5a1
Device Boot Start End Sectors Size Id Type
/dev/sda * 2048 74219519 74217472 35,4G 8 Linux
/dev/sda2 7422156 78139921 3917826 1,9G 5 Extended
/dev/sda3 7422568 78139921 3917824 1,9G 8 Linux sw
Disk /dev/sdb: 955,5 MiB, 100194368 bytes, 1956864 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/o size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
```

# Df

We can learn detailed information about disk usage with df command.

```
root@kemal:~# df
Dosyasistemi 1k-block Dolu Boş Use% Bağlanan yer
udev 10240 0 10240 0% /dev
tmpfs 100564 9148 94116 10% /run
/dev/sda 36394704 9062024 25460860 27% /
tmpfs 251404 256 251148 1% /dev/shm
tmpfs 5120 0 5120 0% /run/lock
tmpfs 251404 0 251404 0% /sys/fs/cgroup
tmpfs 50284 8 50276 1% /run/user/132
tmpfs 50284 32 50252 1% /run/user/0
```

To get an organized output (MB, GB basis) df -h command is used.

§