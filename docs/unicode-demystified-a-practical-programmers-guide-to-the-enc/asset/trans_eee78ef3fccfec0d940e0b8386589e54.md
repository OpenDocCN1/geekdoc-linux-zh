
在假设是非日志文件系统的情况下，分区越频繁，检查所需的时间就越长。这些检查通常是不必要的。`tune2fs` 工具可以帮助你在“每次重启系统时都检查文件系统”与“从不检查”之间找到平衡点。它通过调度 `fsck` 检查文件系统的时间来实现（这些检查仅在系统启动时发生）。你可以使用两种调度模式：自上次检查以来经过的时间和自上次检查以来的挂载次数。以下命令会导致 `/dev/hda6` 在 `fsck` 运行 8 次或自上次检查后 15 天后进行检查（以先到者为准）：

```
# tune2fs -c 8 -i 15 /dev/hda6
tune2fs 1.27, (8-Mar-2002)
Setting maximal mount count to 8
Setting interval between check 1296000 seconds
```

下一个 `tune2fs` 命令类似，不同之处它作用于不同的分区，并将当前挂载次数设置为 4。当你在上一个示例中没有指定当前挂载次数时，它假设为：

```
# tune2fs -c 8 -i 15 -C 4 /dev/hda10
tune2fs 1.27, (8-Mar-2002)
Setting maximal mount count to 4
Setting current mount count to 4
Setting interval between check 1296000 seconds
```

`-l` 选项显示分区的信息列表。你可以将此选项与其他结合使用。在“最大挂载次数”下方是 `-1`，这意味着 `fsck` 和内核将忽略挂载次数信息。挂载次数为 0 的原理相同：

```
# tune2fs -l /dev/hda5
tune2fs 1.27, (8-Mar-2002)
Filesystem volume name: /free
Last mounted: <not available>
Filesystem UUID: f59d69a8-a419-11d4-944c-e771d63cd639
Filesystem magic number: 0EF53
Filesystem revision: 1 (dynamic)
Filesystem features: has_journal filetype needs_recovery sparse_super
Filesystem state: clean
Errors behavior: Continue
Filesystem OS type: Linux
Inode count: 513024
Block count: 1024135
```

2. 对于那些生存目标是持续运行的系统，这种调度方式并不适用。你必须制定一个不基于系统重启而是基于时钟的调度。每个文件系统必须定期挂载、使用 `fsck`（见前节）进行检查并重新挂载。

## 第 17 章 红帽 Linux 管理

```
Last mount time: Thu Dec 20 20:59:51 2001
Last write time: Thu Dec 20 20:59:51 2001
Mount count: 6
Maximum mount count: -1
Last checked: Thu Dec 6 09:23:23 2001
Check interval: 0 (<none>)
```

设置你系统上的文件系统参数，使其适应你使用计算机的方式。使用 `-C` 选项错错执行检查，可以确保所有检查不会同时发生。务必检查并升级文件系统，以确保它们按照你的预期调度了检查。

要将 ext2 文件系统转换为 ext3 文件系统，你必须在文件系统上放置一个日志（第 145 页），并且内核必须支持 ext3 文件系统。使用 `-j` 选项在未挂载的文件系统上设置日志：

```
# tune2fs -j /dev/hdd3
tune2fs 1.27, (8-Mar-2002)
Creating journal: none
This filesystem will be automatically checked -1 mounts or 0 days, whichever comes first. Use tune2fs -c or -i to override.
```

（注：此处）在可以使用 `fstab`（第 959 页）挂载更改后的文件系统之前，你必须修改其在 `fstab` 文件中的条目以反映其新名称。将第三列改为 `ext3`。此命令将未挂载的 `ext3` 文件系统改回 `ext2` 文件系统：

```
# tune2fs -O ^has_journal /dev/hdd3
tune2fs 1.27, (8-Mar-2002)
```

更多详情请参考 `tune2fs` 手册。

## RAID 文件系统

RAID（廉价磁盘冗余阵）将信息分散在多个物理磁盘上，形成一个较大的虚拟设备。RAID 提高了性能并提供了冗余性。有六种以上的类型的 RAID 配置。使用红帽工具，你可以建立软件 RAID。硬件 RAID 需要专门设计用于实现 RAID 的硬件，本文未涵盖此内容。

## 不要用 RAID 替代备份

不要将 RAID 视作常规备份的替代品。如果你的系统遭遇了灾难性故障，RAID 将是无用之物。地震、火灾、盗窃等可能导致你的整个系统无法访问（如果你的硬盘被毁或丢失了）。RAID 无法处理诸如删除你需要的的文件这类简单的问题。在这些情况下，在可移动介质上（已移除的介质）上的备份是你能够恢复文件系统的唯一方法。

26. 随着磁盘价格下降，“廉价”部分已不再适用。

RAID 可以作为备份的有效补充。红帽拥有强大的 RAID 软件，你可以在安装红帽系统时安装它，也可以事后安装。Linux 内核可以在启动时自动检测 RAID 分区，如果分区 ID 是匹配的。

RAID 可以作为备份的有效补充。红帽拥有强大的 RAID 软件，你可以在安装红帽系统时安装它，也可以事后安装。Linux 内核可以在启动时自动检测 RAID 分区，如果分区 ID 是匹配的。

## GUI 系统管理工具

除了字符界面可用的系统管理工具外，你还有基于 GUI 的工具。

## GNOME 设置窗口/菜单

通过双击图标（第 216 页）或在 Nautilus 栏输入 `system-settings` 来显示 GNOME 设置窗口。这些工具在 GNOME 菜单中可用。

| GNOME 设置窗口 | 说明 |
| :--- | :--- |
| 身份验证 | 指定本地和远程登录使用 NIS 还是 Kerberos。 |
| 日期与时间 | 设置日期和时间。使用时间框手动设置。 |
| 显示 | 设置物理显示。参考第 922 页的 "redhat-config"。 |
| 扩展 | GNOME 菜单可用。添加工具。 |
| 键盘 | 设置你使用的语言和样式。 |
| 语言 | 设置 GNOME 用于标题、提示、标签等的语言。更多信息请参考第 1477 页的 "locale"。 |
| 登录屏幕 | 运行 gdm 显示 GDM（GNOME 显示管理器）设置窗口。参见 /etc/X11/gdm/gdm.conf。 |
| 通用 | 谨慎使用自动和定时登录选项，因为它们允许无人值的控制台自动登录。 |
| 欢迎界面 | 指定本地和远程登录使用标准或图形欢迎界面。参考后续标签页以设置这些欢迎界面。 |
| 网络时间协议 | 参考词表中 1482 页的 "NTP"。 |
| 启用网络时间协议 | 开启 NTP，以便你的计算机通过指定的服务器定期设置时。 |
| 服务器 | 指定你想用于系统时钟的时间服务器。 |
| 时区 | 有两种指定你想使用的时区的方法：地图或滚动列表。 |
| 查看 | 移动鼠标指针直到绿色箭头指向你所在的城市，然后点击。检查滚动列表中正确的城市是否被高亮。 |
| 系统时使用 UTC | 如果你想让系统时使用 UTC，请勾选此框（参考第 1143 页的 `date` --utc 选项）。 |
| (滚动列表) | 你可以手动使用滚动列表。滚动列表，并点击你所在的城市。 |
