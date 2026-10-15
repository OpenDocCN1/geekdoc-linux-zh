
## 分区操作示例

```
Command (m for help): n
Command action
t 扩展
p 主分区 (1-4)
p
分区号 (1-4): 2
起始柱道 (201-1029): 201
结束柱道或 +size 或 +sizeM 或 sizeK (101-259): 250M
```

## 创建 LINUX 分区 41

```
Command (m for help): n
Command action
e 扩展
p 主分区 (1-4)
p
分区号 (1-4): 3
起始柱道 (452-1029): 452
结束柱道或 +size 或 +sizeM +sizeK (452-1029): +150M
```

```
Command (m for help): n
Command action
e 扩展
p 主分区 (1-4)
e
分区号 (1-4): 4
起始柱道 (603-1029): 603
结束柱道或 +size 或 +sizeM +sizeK (603-1029): 1029
```

```
Command (m for help): n
起始柱道 (603-1029): 603
结束柱道或 +size 或 +sizeM +sizeK (603-1029): +16M
```

```
Command (m for help): p

Disk /dev/sdc 64 heads, 32 sectors, 1029 cylinders
Units = cylinders of 2048 * 512 bytes

| Device Boot Begin End Blocks Id System |
| /dev/sd1 1 1 200 204784 6 DOS Linux>=32M |
| /dev/sd2 201 201 451 250724 83 Linux native |
| /dev/sd3 452 452 602 154624 83 Linux native |
| /dev/sd4 603 603 1029 372748 5 Extended |

Partition 4 has different physical/logical endings:
phys=(1023, 63, 32) logical=(1028, 63, 32)
/dev/sd5 603 603 619 17392 83 Linux native
```

```
Command (m for help): t
Partition number (1-5): 5
Hex code (type L to list codes): 82
Changed system type of partition 5 to 82 (Linux swap)
```

```
Command (m for help): v
83712 unallocated sectors
```

```
Command (m for help): w
The partition table has been altered!
Calling ioctl() to re-read partition table.
Syncing disks.
```

因此，我们在 SCSI 磁盘上有三个主分区、一个扩展分区和一个逻辑分区，标记为交换分区。

在你使用 `W`（write）开始分区磁盘之前，执行 `V`（verify）：`fdisk` 会检查其内部信息是否与磁盘匹配。这是一个额外的安全检查。通常对 `V` 的响应是显示未包含在任何分区中的 512 字节扇区数量。在上面的示例中，有 400 Megabytes 是空闲的（未使用）。在 Linux (`fdisk`) 和 DOS (`FDISK`) 下，可以在此区域创建更多逻辑分区。

## 安装

只要你不通过 `W` 终止 `fdisk`，程序就不会对你的硬盘执行任何修改。你的输入被存储了但没有执行。如果你不确定自己在做什么，可以随时通过 `Q`（quit）或 `Ctrl+C` 退出 `fdisk`——磁盘将保持原样。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_0.png)

使用 `fdisk` 永远不要修改正在使用的分区（即在 Linux 下已加载）。你可以在运行期间添加新分区，但当你想要删除分区时，应该重启系统。如果在 `W` 之后，`fdisk` 显示“Reread table failed with error: Device or resource busy.”，你应该重视这个警告；无法读取修改后的分区数据在这种情况下，你必须用 `Ctrl+Alt+Del` 重启！然后再次运行 `fdisk`，确保分区已按预期创建。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_1.png)

如第 33 页所述，关于柱道数大于 1024 的警告通常可以忽略。它们只涉及 `LILO` 启动（取决于使用的软件）。使用 `fdisk` 创建的分区仍然是空的，没有安装文件系统。与 DOS 下在 `FDISK` 后必须执行 `FORMAT` 命令一样，在 Linux 下必须使用 `mkfs` 命令创建文件系统。然而，你不需要手动执行此命令，安装程序会自动调用它。

![](img/dbea4db79a2d1f2183ab7081a3efe_2.png)

## 如何使用 cfdisk

`cfdisk` 命令是 `fdisk` 的早期变体。它通过光标键和菜单控制。一旦启动，程序会显示所有分区及其大小。你可以通过一个命令选择分区。此外，以下是键盘命令：

| 按键 | 功能 |
| :--- | :--- |
| | 显示在线帮助 |
| `N` | 新分区 |
| `D` | 删除所选分区 |
| `T` | 更改分区类型（用于交换分区） |
| `Q` | 退出程序（不更改分区表） |
| `Shift+W` | 修改分区表（写入） |

![](img/dbea4db79a2d1f2183ab7081a3efe_3.png)

`cfdisk` 是一个独立程序（不是 `fdisk` 的接口）。它不像 `fdisk` 那样开发得完全。`cfdisk` 可能会因错误消息“Cannot seek on disk drive.”突然退出。在这种情况下，你必须重启。`cfdisk` 程序需要 `ncurses` 库，在旧的 Linux 发行版中通常没有安装。

## 手动创建交换分区

在 RAM 非常小的计算机上，通常必须手动创建交换分区。（如果有足够的 RAM，可以在没有交换分区的情况下启动安装程序。它会自动创建并放置正确的交换分区。）

要手动创建交换分区，输入以下命令：

```
# mkswap -c /dev/sdc5 17392
# swapon /dev/sdc5
```

显然，代替 `/dev/sdc5` 的输入名称，代替 `17392` 的输入你交换分区的大小。`17392` 标识块的数量。此值由 `f` 显示。

# 现在怎么办？

现在剩下的就是安装 LINUX 程序。取决于发行版，这由一个用户友好、基于菜单的安装程序执行，通常不会产生任何问题。可能很难决定安装哪些程序，哪些不安装。（疑问时，装少的比装多的。你以后可以随时添加软件包。）某些重要发行版的信息可以在附录中找到。

安装程序配置计算机的方式在某些情况下可能会令人困惑。你可能会被要求提供你可能的细节。规则：延迟任何安装，直到你完全理解（尤其是 `LILO`）。安装程序（或至少类似的工具）在正常的 LINUX 操作期间也可以再次调用。

在开始时，配置 LINUX 到可以从启动盘启动而没有任何问题的程度是非常重要的。如果一切顺利，终止安装程序并使用安装期间创建的启动盘重启计算机。

## 2.6 通过 NFS 安装 LINUX

NFS 代表网络文件系统，允许通过网络向多个计算机提供整个文件系统。如果你想在已有的网络中安装 LINUX，且所有安装数据都通过 NFS 可用，那么这个

# 44 安装

安装是最简单、最优雅的方法之一。其主要优势在于，安装 LINUX 的计算机不需要自带的 CD-ROM 光驱驱动器。

通过 NFS 安装假设你的计算机配备了网卡，且该网卡在启动时能被安装盘片识别；计算机必须正确连接线缆；主机计算机必须配置为 NFS 服务器（详阅第 156 页）；存储安装数据的目录（通常是 NFS 服务器的 CD-ROM 驱动器路径）必须可以通过 NFS 访问；最后，你还需要主机的 IP 地址。

在安装过程中（且在很大程度上独立于具体的发行版），你必须指定以下内容：

- 计算机的网络名称（即以 `hostname.domain` 形式表示的主机名和域名）；原则上，你可以输入任何你选择的名称，因为该名称仅在安装期间使用。（如果你的计算机已经确定了最终的网络名称，显然应使用该名称。）主机名必须与 NFS 服务器的设置相对应。（例如，服务器可能被配置为只有通过系统管理员定义的特定名称才能访问安装数据目录。）

- 使用的网络设备：通常为 `eth0`（第一块以太网网卡）；理论上，也可以通过 PPP 或 SLIP 进行安装。

- 计算机的 IP 数字（格式如 `192.168.55.37` 的数字）；此指示也仅在安装期间有效。尽管如此，你必须输入一个有意义的数字：IP 必须符合本地网络且是唯一的。通常，IP 数字仅最后一位与 NFS 服务器的 IP 不同。

- NFS 服务器的 IP 数字（例如 `192.168.55.1`）。
