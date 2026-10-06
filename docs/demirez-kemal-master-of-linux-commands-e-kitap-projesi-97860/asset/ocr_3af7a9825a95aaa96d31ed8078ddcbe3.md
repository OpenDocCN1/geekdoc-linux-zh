```
root@kemal:~# df -h
Dosyasistemi      Boy  Dolu  Boş Use%  Bağlanan yer
udev             10M   10M    0% /dev
tmpfs            99M  9,0M   90M 10% /run
/dev/sda         35M  8,7G   25G 27% /
tmpfs           246M  256K  246M 1% /dev/shm
tmpfs            5,0M     0   5,0M 0% /run/lock
tmpfs           246M     0   246M 0% /sys/fs/cgroup
tmpfs            50M  8,0K   50M 1% /run/user/132
tmpfs            50M   32K      1% /run/user/0
```

To get the list with the information in the file system df-T (ext4, vfat, etc.).

```
root@kemal:~# df -T
Dosyasistemi     Tür      1K-block    Dolu  Boş Use%  Bağlanan yer
udev             devtmpfs  10240       010240    0% /dev
tmpfs            tmpfs    100564 9148  9416 10% /run
/dev/sda         ext4     36394704 9068272 2546012 27% /
tmpfs            tmpfs     251404     256 251148 1% /dev/shm
tmpfs            tmpfs      5120       0  5120 0% /run/lock
tmpfs            tmpfs     251404       0 251404 0% /sys/fs/cgroup
tmpfs            tmpfs     50284       8 50276 1% /run/user/132
tmpfs            tmpfs     50284      32 50252 1% /run/user/0
```

# Du

To find out the size of the space the subdirectory occupies under a directory, or folder of files on the disk is utilized by du command. It can be used with various parameters to give the result we want the command output.

```
root@kemal:~# du -h --max-depth=1 /
367M    /home
52K     /tmp
11M     /bin
16K     /media
4,0K    /mnt
8,0K    /srv
```