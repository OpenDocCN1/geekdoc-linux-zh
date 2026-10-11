
是否对文件系统执行同步或异步的 I/O 操作。`async` 通常是默认设置。`mount` 的手册页警告称，在具有有限写入次数的介质（如闪存驱动器或存储卡）上使用 `sync` 可能会缩短设备的使用寿命。

### 使用 UUID 和标签

指定包含要挂载的文件系统的设备名称可能会引起一些问题。有时，根据连接系统的时间或位置，相同的设备名称可能会被分配给另一个设备。例如，连接在另一个端口上或另一个闪存驱动器之后的 `/dev/sdb1` 上的 USB 闪存驱动器可能会被分配为 `/dev/sdc1`。

避免这种情况的一种方法是指定卷的标签或 `UUID`（*通用唯一识别码*）。两者都是在创建文件系统时指定的，除非文件系统被销毁或手动分配新的标签或 `UUID`，否则它们不会改变。

命令 `lsblk` 可用于查询文件系统信息并找出标签以及与其关联的 `UUID`。要做到这一点，请使用 `-f` 参数，后跟设备名称：

```
$ lsblk -f /dev/sda1
NAME FSTYPE LABEL UUID                       FSAVAIL FUSE% MOUNTPOINT
sda1 ext4      6e2c12e3-472d-4bac-a257-c49ac07f3761  64,9G 33% /
```

以下是每一列的含义：

- `NAME`
  - 包含文件系统设备的名称。
- `FSTYPE`
  - 文件系统类型。
- `LABEL`
  - 文件系统标签。
- `UUID`
  - 分配给文件系统的通用唯一标识符 (`UUID`)。
- `FSAVAIL`
  - 文件系统中可用的空间大小。
- `FUSE%`
  - 文件系统的已用空间百分比。
- `MOUNTPOINT`
  - 文件系统的挂载点。

在 `/etc/fstab` 中，可以使用 `UUID=` 选项后跟 `UUID`，或者使用 `LABEL=` 后跟标签来指定设备。因此，而不是使用：

```
/dev/sda1  /  ext4  noatime,errors
```

你应该使用：

```
UUID=6e2c12e3-472d-4bac-a257-c49ac07f3761  /  ext4  noatime,errors
```

或者，如果你有一个标记为 home disk 的磁盘：

```
LABEL=homdisk /home ext4 defaults
```

相同的语法也可以用于 `mount` 命令。代替设备名称，传入 `UUID` 或标签。例如，要在 `/mnt/external` 上挂载一个 `UUID` 为 `56C11DCC5D2E1334` 的外部 `NTFS` 磁盘，命令如下：

```
$ mount -t ntfs UUID=56C11DCC5D2E1334 /mnt/external
```

### 使用 Systemd 挂载磁盘

`Systemd` 是初始化进程，在许多 Linux 发行版中是第一个运行的进程。它负责生成其他进程、启动服务和引导系统。除了许多其他任务外，`systemd` 还可以用于管理文件系统的挂载（和自动挂载）。

要使用 `systemd` 的这个功能，你需要创建一个称为 *mount unit*（挂载单元）的配置文件。每个要挂载的卷都有其自己的挂载单元，它们需要放置在 `/etc/systemd/system/` 目录下。

挂载单元是具有 `.mount` 扩展名的简单文本文件。基本格式如下所示：

```ini
[Unit]
Description=

[Mount]
What=
Where=
Type=
Options=

[Install]
WantedBy=
```

`Description=`

挂载单元的简短描述，类似于“挂载备份磁盘”。

`What=`

应该挂载什么。卷必须指定为 `/dev/disk/by-uuid/VOL_UUID`，其中 `VOL_UUID` 是卷的 `UUID`。

`Where=`

应该是卷应挂载到的完整路径。

`Type=`

文件系统类型。

`Options=`

你可能希望传递的挂载选项，这些与 `mount` 命令或 `/etc/fstab` 中使用的选项相同。

`WantedBy=`

用于依赖项管理。在这种情况下，我们将使用 `multi-user.target`，这意味着每当系统启动到多用户环境（正常启动）时，该单元都会被挂载。

我们之前的外部磁盘示例可以写成如下形式：

```ini
[Unit]
Description=External data disk

[Mount]
What=/dev/disk/by-uuid/56C11DCC5D2E1334
Where=/mnt/external
Type=ntfs
Options=defaults

[Install]
WantedBy=multi-user.target
```

但我们还没有做完。为了正确工作，挂载单元的名称**必须**与挂载点相同。在这种情况下，挂载点是 `/mnt/external`，因此文件应命名为 `mnt-external.mount`。

之后，你需要使用 `systemctl` 命令重启 `systemd` 守护进程，并启动该单元：

```sh
# systemctl daemon-reload
# systemctl start mnt-external.mount
```

现在，外部磁盘的内容应该在 `/mnt/external` 上可用。你可以使用 `systemctl status mnt-external.mount` 命令检查挂载状态，如下所示：

```
# systemctl status mnt-external.mount
- mnt-external.mount - External data disk
  Loaded: loaded (/etc/systemd/system/mnt-external.mount; disabled; vendor preset: enabled)
  Active: active (mounted) since Mon 2019-08-19 22:27:02 -03; 14s ago
  Where: /mnt/external
  What: /dev/sdb1
  Tasks: 0 (limit: 4915)
  Memory: 128.0K
  CGroup: /system.slice/mnt-external.mount

Aug 19 22:27:02 pop-os systemd[1]: Mounting External data disk...
Aug 19 22:27:02 pop-os systemd[1]: Mounted External data disk.
```

`systemctl start mnt-external.mount` 命令只会为当前会话启用该单元。如果你希望每次启动时都启用它，请将 `start` 替换为 `enable`：

```
# systemctl enable mnt-external.mount
```

### 自动挂载挂载单元

当访问挂载点时，可以自动挂载挂载单元。要做到这一点，你需要一个 `.automount` 文件，与描述该单元的 `.mount` 文件一起存放。基本格式是：

```
[Unit]
Description=

[Automount]
Where=

[Install]
WantedBy=multi-user.target
```

与之前一样，`Description=` 是文件的简短描述，而 `Where=` 是挂载点。例如，我们之前示例的 `.automount` 文件如下：

```
[Unit]
Description=Automount for the external data disk

[Automount]
Where=/mnt/external

[Install]
WantedBy=multi-user.target
```

保存该文件时，请使用与挂载点相同的名称（在这种情况下为 `mnt-external.automount`），重新加载 `systemd` 并启动该单元：

```
# systemctl daemon-reload
# systemctl start mnt-external.automount
```

现在，每当访问 `/mnt/external` 目录时，磁盘将被挂载。与之前一样，要在每次启动时启用自动挂载，请使用：

```
# systemctl enable mnt-external.automount
```

### 指导练习

1. 使用 `mount`，如何以只读方式在 `/dev/sdc1` 上挂载 `ext4` 文件系统到 `/mnt/external`，并使用 `noatime` 和 `async` 选项？

2. 在卸载 `/dev/sdd2` 上的文件系统时，你收到“目标正忙”的错误消息。如何找出哪些文件正在打开该文件系统，以及哪些进程打开了它们？
