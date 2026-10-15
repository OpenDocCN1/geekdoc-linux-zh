
13. 为了保持冗余，我们应该用另一块磁盘替换损坏的磁盘。如果你使用的是物理磁盘，可以使用 `zpool replace` 命令（`zpool` 手册页中有详细信息）。不过，在这个基于文件的示例中，我们只需从镜像中移除磁盘文件并重新创建它。
设备通过 `zpool detach` 命令分离：

```
root@solaris:~# zpool detach data2 /home/bob/disk1
```

14. 让我们检查一下存储池的状态：

```
root@solaris:~# zpool status data2
pool: data2
state: ONLINE
scrub: scrub completed with 0 errors on Thurs Mar 6
18:00:07 2014
config:
        NAME                STATE     READ WRITE CKSUM
        data2               ONLINE       0     0     0
          /home/bob/disk2   ONLINE       0     0     0
errors: No known data errors
```

15. 让我们移除磁盘以模拟故障，然后替换它：

```
root@solaris:~# rm /home/bob/disk1
root@solaris:~# mkfile 128m /home/bob/disk1
```

16. 为了在镜像中替换它，我们需要执行以下操作。要挂载另一个设备，我们需要指定镜像中已有的设备，并通过 `zpool attach` 命令将其挂载到该设备上：

```
root@solaris:~# zpool attach data2 /home/bob/disk2 /home/bob/disk1
```

17. 检查存储池的状态：

```
root@solaris:~# zpool status data2
pool: data2
state: ONLINE
scrub: resilver completed with 0 errors on Thurs Mar 6
18:08:16 2014
config:
        NAME                STATE     READ WRITE CKSUM
        data2               ONLINE       0     0     0
          mirror-0          ONLINE       0     0     0
            /home/bob/disk2 ONLINE       0     0     0
            /home/bob/disk1 ONLINE       0     0     0
errors: No known data errors
```

## 18. 向镜像存储池添加磁盘

ZFS 可以实现的一个非常关键的系统管理过程是无需将存储池离线即可向其添加磁盘。让我们将 data2 存储池的容量扩大一倍：

```
root@solaris:~# zpool list
NAME   SIZE  USED  AVAIL  CAP  DEDUP  HEALTH  ALTROOT
The default pools on the system...
data2   123M  64.5M  58.5M  52%  1.00X  ONLINE  -
```

19. 我们可以使用 `zpool add` 命令将磁盘添加到现有存储池。

```
root@solaris:~# zpool add data2 mirror /home/bob/disk3 /
                         /home/bob/disk4
root@solaris:~# zpool list
NAME   SIZE  USED  AVAIL  CAP  DEDUP  HEALTH  ALTROOT
The default pools on the system...
data2   246M  64.5M  181M  26%  1.00X  ONLINE  -
```

20. 存储池中的文件系统始终可用。如果现在查看状态，可以看到存储池由两个镜像组成：

```
root@solaris:~# zpool status data2
pool: data2
state: ONLINE
scrub: resilver completed with 0 errors on Wed Mar 6
17:58:17 2014
config:
        NAME                 STATE     READ WRITE CKSUM
        data2                ONLINE       0     0     0
          mirror-0          ONLINE       0     0     0
            /home/bob/disk2  ONLINE       0     0     0
            /home/bob/disk1  ONLINE       0     0     0
          mirror-1          ONLINE       0     0     0
            /home/bob/disk3  ONLINE       0     0     0
            /home/bob/disk4  ONLINE       0     0     0
errors: No known data errors
```

21. 我们可以使用 `zpool iostat -v` 查看数据当前写入存储池的位置：

```
root@solaris:~# zpool iostat -v data2

                              capacity     operations     bandwidth
pool                       alloc  free   read  write   read  write
-------------------------  -----  -----  -----  -----  -----  -----
data2                         64.5M  181M      0      0   14.7K    623
  mirror                      64.4M  58.6M      0      0   40.5K  1.51K
    /home/bob/disk2              -      -      0      2   22.4K  22.8K
    /home/bob/disk1              -      -      0      1     187  43.6K
  mirror                       102K   123M      0      0      0   2.32K
    /home/bob/disk3              -      -      0      0     213  22.9K
    /home/bob/disk4              -      -      0      0     213  22.9K
-------------------------  -----  -----  -----  -----  -----  -----
```
