
```
该选项不可作为模块可用。
```

编译完成后，系统就准备好使用`/proc`文件系统。与 Linux 的所有事物一样，系统可以开启和关闭——在这种情况下，涉及到`/etc/fstab`。为了让系统创建并使用`/proc`文件系统，它必须像任何其他文件系统一样被“挂载”（`mounted`）。在这种情况下，挂载过程的作用是让`/proc`文件系统变得可用。就像其他文件系统点（目录条目）无论是否挂载都存在一样，`proc`文件系统在被“挂载”之前无法使用，因为必须存在指向文件系统的路径才能使用它。因此，如果你删除了根文件系统中的`/proc`目录条目，`/proc`就没有去处，你会得到错误而不是`/proc`文件系统。`/etc/fstab`中相应的行如下：

```
/proc /proc defaults 0 0
```

文件系统是`/proc`，并且没有为其分配相应的设备文件——因为它不是设备。挂载位置是`/proc`，文件系统类型是`proc`，默认挂载，且在任何检查（`fs`）或转储（`dump`）中都没有。检查或转储动态变量是没有意义的，因为你无法纠正或更改它们，下文讨论的`/proc/sys`中的文件除外。此外，也不会恢复`/proc`，因为在`/proc`之上强制执行恢复来更改此文件系统会导致系统不稳定。

`/proc`文件系统是非常动态的。许多条目几乎会随着系统活动而变化。如果你查看`/proc`文件系统，你看到的是一个时刻的快照。列表 6-1 显示了`/proc`根文件系统。

### 列表 6-1：proc 根文件系统

```
dr-xr-xr-x 58 root       0 Nov 15 19:01 .
dr-xr-xr-x 21 root       1024 Nov 15 12:02 ..
dr-xr-xr-x 3 root       0 Nov 16 07:46 1
dr-xr-xr-x 3 root       0 Nov 16 07:46 1076
dr-xr-xr-x 3 root       0 Nov 16 07:46 1079
dr-xr-xr-x 3 dns dns       0 Nov 16 07:46 1088
dr-xr-xr-x 3 root       0 Nov 16 07:46 1092
dr-xr-xr-x 3 bin        0 Nov 16 07:46 1094
dr-xr-xr-x 3 root       0 Nov 16 07:46 1176
dr-xr-xr-x 3 root       0 Nov 16 07:46 1181
dr-xr-xr-x 3 root       0 Nov 16 07:46 1190
dr-xr-xr-x 3 root       0 Nov 16 07:46 1202
dr-xr-xr-x 3 root       0 Nov 16 07:46 1263
dr-xr-xr-x 3 root       0 Nov 16 07:46 1270
dr-xr-xr-x 3 root       0 Nov 16 07:46 1271
dr-xr-xr-x 3 root       0 Nov 16 07:46 1284
dr-xr-xr-x 3 root       0 Nov 16 07:46 1286
dr-xr-xr-x 3 root       0 Nov 16 07:46 1287
dr-xr-xr-x 3 root       0 Nov 16 07:46 1288
dr-xr-xr-x 3 nobody   0 Nov 16 07:46 1317
dr-xr-xr-x 3 nobody   0 Nov 16 07:46 1318
dr-xr-xr-x 3 nobody   0 Nov 16 07:46 1319
dr-xr-xr-x 3 nobody   0 Nov 16 07:46 1320
dr-xr-xr-x 3 nobody   0 Nov 16 07:46 1321
dr-xr-xr-x 3 root       0 Nov 16 07:46 1363
dr-xr-xr-x 3 root       0 Nov 16 07:46 1371
dr-xr-xr-x 3 root       0 Nov 16 07:46 1372
dr-xr-xr-x 3 root       0 Nov 16 07:46 1373
dr-xr-xr-x 3 root       0 Nov 16 07:46 1374
dr-xr-xr-x 3 root       0 Nov 16 07:46 1375
dr-xr-xr-x 3 nobody   0 Nov 16 07:46 1618
dr-xr-xr-x 3 nobody   0 Nov 16 07:46 1619
dr-xr-xr-x 3 nobody   0 Nov 16 07:46 1620
dr-xr-xr-x 3 root       0 Nov 16 07:46 1741
dr-xr-xr-x 3 root       0 Nov 16 07:46 1800
dr-xr-xr-x 3 root       0 Nov 16 07:46 1892
dr-xr-xr-x 3 root       0 Nov 16 07:46 2
dr-xr-xr-x 3 root       0 Nov 16 07:46 4
dr-xr-xr-x 3 root       0 Nov 16 07:46 4856
dr-xr-xr-x 3 david     0 Nov 16 07:46 4858
dr-xr-xr-x 3 david     0 Nov 16 07:46 4914
dr-xr-xr-x 3 david     0 Nov 16 07:46 4915
dr-xr-xr-x 3 david     0 Nov 16 07:46 4917
dr-xr-xr-x 3 david     0 Nov 16 07:46 4964
dr-xr-xr-x 3 david     0 Nov 16 07:46 4965
dr-xr-xr-x 3 root       0 Nov 16 07:46 4967
dr-xr-xr-x 3 root       0 Nov 16 07:46 4968
dr-xr-xr-x 3 root       0 Nov 16 07:46 5038
-r-r--r- 1 root       0 Nov 16 07:46 apm
dr-xr-xr-x 4 root       0 Nov 16 07:46 bus
-r-r--r- 1 root       0 Nov 16 07:46 cmdline
-r-r--r- 1 root       0 Nov 16 07:46 cpuinfo
-r-r--r- 1 root       0 Nov 16 07:46 devices
-r-r--r- 1 root       0 Nov 16 07:46 dma
-r-r--r- 1 root       0 Nov 16 07:46 fb
-r-r--r- 1 root       0 Nov 16 07:46 filesystems
dr-xr-xr-x 2 root root       0 Nov 16 07:46 fs
dr-xr-xr-x 4 root root       0 Nov 16 07:46 ide
-r-r--r- 1 root root       0 Nov 16 07:46 interrupts
-r-r--r- 1 root root       0 Nov 16 07:46 ioports
-r-r--r- 1 root root 134221824 0 Nov 16 07:46 kcore
-r-r--r- 1 root root       0 Nov 15 19:01 kms
-r-r--r- 1 root root       0 Nov 16 07:46 uptime
-r-r--r- 1 root root       0 Nov 16 07:46 host
-r-r--r- 1 root root       0 Nov 16 07:46 host
-r-r--r- 1 root root       0 Nov 16 07:46 host
-r-r--r- 1 root root       0 Nov 16 07:46 locks
-r-r--r- 1 root root       0 Nov 16 07:46 modules
-r-r--r- 1 root root       0 Nov 16 07:46 mounts
-r-r--r- 1 root root       0 Nov 16 07:46 net
-r-r--r- 1 root root       0 Nov 16 07:46 partitions
-r-r--r- 1 root root       0 Nov 16 07:46 pci
```
