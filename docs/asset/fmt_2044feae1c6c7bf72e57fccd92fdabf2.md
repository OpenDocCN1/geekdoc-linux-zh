
```
volassist -Ufsgen -g rootdg make cluster_varvol 8323280 nmirror=2 dsk6 dsk7 init=active

addvol /dev/vol/rootdg/cluster_varvol cluster_var

rmvol /dev/disk/dsk1h cluster_var

rmvol: Removing volume '/dev/disk/dsk1h' from domain 'cluster_var'

rmvol: Removed volume '/dev/disk/dsk1h' from domain 'cluster_var'
```

- 6. 验证迁移和镜像是否成功。

您可以使用`volprint`和`showfdmn`命令。此外，使用`disklabel`命令验证磁盘标签。当然，集群正在运行这一事实也是一个很好的迹象，表明一切按计划进行。

- 7. 从`cluster_usrvol`和`cluster_varvol`中移除日志 plex，因为它们位于包含卷数据的同一磁盘上。添加来自另一块磁盘的新日志 plex。

定位日志 plex。

```
# volprint | grep LOG

p1 cluster_usrvol-03 cluster_usrvol ENABLED LOGONLY - ACTIVE - -

sd dsk6-03 cluster_usrvol-03 ENABLED 195 LOG

p1 cluster_varvol-03 cluster_varvol ENABLED LOGONLY - ACTIVE - -

sd dsk6-05 cluster_varvol-03 ENABLED 195 LOG
```

```
# volplex -v cluster_usarvol dis cluster_usarvol-03
# voledit -rf rm cluster_usarvol-03
```

```
# volplex -v cluster_varvol dis cluster_varvol-03
# voledit -rf rm cluster_varvol-03
```

使用根磁盘组中的另一磁盘添加新的日志 plex。

```
# volassist addlog cluster_usarvol dsk5h
# volassist addlog cluster_varvol dsk5h
```

8. 验证一切是否成功完成。

```
# volprint cluster_rootvol cluster_usarvol cluster_varvol

Disk group: rootdg

TY NAME            ASSOC        KSTATE   LENGTH   PLOFFS   STATE   TUTIL0  PUTIL0

v  cluster_rootvol  cluroot      ENABLED  1048576  -        ACTIVE  -       -

pl cluster_rootvol-01 cluster_rootvol ENABLED 1048576 - ACTIVE - -

ad dsk6-01        cluster_rootvol-01 ENABLED 1048576 0 - - -

pl cluster_rootvol-02 cluster_rootvol ENABLED 1048576 - ACTIVE - -

ad dsk7-01        cluster_rootvol-02 ENABLED 1048576 0 - - -

v  cluster_usarvol  fagen       ENABLED  8389344  -        ACTIVE  -       -

pl cluster_usarvol-01 cluster_usarvol ENABLED 8389344 - ACTIVE - -

ad dsk6-02        cluster_usarvol-01 ENABLED 8389344 0 - - -

pl cluster_usarvol-02 cluster_usarvol ENABLED 8389344 - ACTIVE - -

ad dsk7-02        cluster_usarvol-02 ENABLED 8389344 0 - - -

pl cluster_usarvol-03 cluster_usarvol ENABLED LOGONLY - ACTIVE - -

ad dsk5h-01       cluster_usarvol-03 ENABLED 195 LOG - - -

v  cluster_varvol   fagen       ENABLED  8323280  -        ACTIVE  -       -

pl cluster_varvol-01 cluster_varvol ENABLED 8323280 - ACTIVE - -

ad dsk7-03        cluster_varvol-01 ENABLED 8323280 0 - - -

pl cluster_varvol-02 cluster_varvol ENABLED 8323280 - ACTIVE - -

ad dsk6-04        cluster_varvol-02 ENABLED 8323280 0 - - -

pl cluster_varvol-03 cluster_varvol ENABLED LOGONLY - ACTIVE - -

ad dsk5h-02       cluster_varvol-03 ENABLED 195 LOG - - -
```

## 14.7.2 使用 `volencap(8)` 命令封装

当您使用 `volencap` 命令封装 AdvFS 域、磁盘或磁盘分区时，设备上已有的数据将保持不变。这是一件好事，因为如果您决定移除 LSM，则无需重新创建或恢复数据。

`volencap` 命令接受分区、磁盘或域作为输入：

- 如果您选择封装单个磁盘分区，则将从该磁盘分区创建一个 nopriv 磁盘和一个 LSM 卷。
- 如果您选择封装整个磁盘，则将为磁盘上每个未标记为未使用的分区创建一个 nopriv 磁盘和一个 LSM 卷。
- 如果您选择封装 AdvFS 域，则域中所有 AdvFS 卷都将成为 LSM 卷。

`volencap` 命令会在 `/etc/vol/reconfig.d` 目录中创建文件，`volreconfig(8)` 命令会使用这些文件，根据输入给 `volencap` 命令的设备创建 LSM 卷、plex 和子磁盘。

### 14.7.2.1 封装 AdvFS 域

除 `cluster_root` 域之外，任何域都可以封装。要将 `cluster_root` 域置于 LSM 控制之下，必须使用 `volmigrate` 命令（参见本章前面的 14.7.1 节）。

只要域未被使用，封装就不需要重启。如果可能，请卸载要封装的域中的文件系统，以避免重启集群。

要封装域，请执行以下操作：

```
# volencap tcrhb

Setting up encapsulation for tcrhb.

For AdvFS domain tcrhb:

  - Creating nopriv disk dsk6c.

The following disks are queued up for encapsulation or use by LSM:

dsk6c

Please consult the Cluster Administration Guide for steps

that you will need to follow to complete the encapsulation.
```

您可以通过使用带有 `"-s"` 选项的 `volencap` 命令查看哪些设备已排队等待封装：

```
# volencap -s

The following disks are queued up for encapsulation or use by LSM:

dsk6c
```

为了完成封装过程，我们需要运行 `volreconfig` 命令。

### 注意：

如果您决定不完成封装过程，可以通过使用带有 `"-k <diskname|partition>"` 选项的 `volencap` 命令取消对一个设备的封装，或者使用 `"-k -a"` 选项取消所有排队中的封装请求：

```
# volencap -k dsk6c
```

-或-

```
# volencap -k -a
```

只要排队等待封装的设备未被使用，`volreconfig` 命令即可完成封装过程。

```
# volreconfig

Encapsulating dsk6c.

The following disks were encapsulated successfully:

    dsk6c
```
