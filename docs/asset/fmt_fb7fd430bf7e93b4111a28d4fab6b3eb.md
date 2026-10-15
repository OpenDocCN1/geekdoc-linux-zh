
`udevadm` 输出中的所有路径（如 `/devices/pci0000:00/...`）都是相对于 `/sys` 的相对路径，尽管它们看起来像绝对路径。输出经过了格式化，以便你可以在构建规则时将其回传给 udev。例如，如果 `ATTR(size)="1974271"` 子句是该设备独有的，你可以将该片段复制到规则中作为识别标准。请参阅 `udevadm` 的手册页获取更多选项和语法。

### 规则和持久化名称

`udev` 依赖一组规则来指导其对设备的管理。默认规则属于 `/lib/udev/rules.d` 目录，但那里的本地规则你可能永远不会编辑或删除。`udev` 的主配置文件是 `/etc/udev.conf`；然而，默认行为是合理的。我们示例中的 `udev.conf` 文件仅包含注释，除了用于启用日志的一行外。遗憾的是，由于发行版之间的政治斗争，它们之间几乎没有协同。默认目录中的许多文件名是相同的，但内容差异巨大。规则按照 `nn-description` 的模式命名，其中 `nn` 是数字。

# 第 11 章

```
ubuntu udev info -a /block/sdb/sdb1
```

```
looking at device '/devices/pci0000:00/0000:11.0/0002:03.0/
usb1/1-1/1-1:1.0/host30/target30:0:30:0:0/block/sdb/sdb1':
KERNEL=="sdb"
SUBSYSTEM=="block"
DRIVER=""
ATTR(partition)="1"
ATTR(start)="63"
ATTR(size)="1974208"
ATTR(state)="71 792 1857 808 0 0 0 0 0 512 808"
```

```
looking at device '/devices/pci0000:00/0000:11.0/0002:03.0/
usb1/1-1/1-1:1.0/host30/target30:0:30:0:0/block/sdb/sdb':
KERNELS="sdb"
SUBSYSTEM="block"
DRIVERS=""
ATTR(scsi_level)==="3"
ATTR(vendor)==="UT163"
ATTR(model)==="USB2FlashStorage"
...
```

`udevadm` 的输出显示了多种匹配机会。其中一种可能性是 `size` 字段，它很可能是该设备唯一的。如果分区的大小发生变化，设备将无法被识别。相反，我们可以使用两个值的组合：内核的命名属性、`sda` 的 `USB2FlashStorage`（这里指代一个额外的字母）以及 `model` 属性的内容。通过为这个特定的闪存盘创建特定的规则，另一个很好的选择是设备的序列号（我们在此处输出中省略了序列号）。

接下来，我们将该设备的规则放入文件 `/etc/udev/rules.d/10-local.rules` 中。由于我们有多个目标，因此需要一系列规则。

首先，我们处理在 `/dev` 中创建设备符号链接的问题。以下规则利用我们从 `udevadm` 中获得的关于 `ATTRS` 和 `KERNEL` 匹配键的知识来识别设备：

```
ATTR(model)==="USB2FlashStorage", KERNEL=="sd[a-z]1",
SYMLINK+="ate-flash%n"
```

（该规则为了适应页面宽度进行了折叠；在原始文件中，它在同一行上）。
当我们触发规则时，`udev` 将 `/dev/ate-flash%N` 设置为指向设备的符号链接（其中 N 是从 0 开始的顺序中的下一个整数）。我们并不预期系统中会出现多个此类设备。如果真的出现了多个副本，它们会在 `/dev` 中获得唯一的名称，但具体名称将取决于设备的插入顺序。

接下来，我们使用 `ACTION` 键在每当设备出现在 USB 总线上时运行某些命令。`RUN` 赋值键允许我们创建一个恰当的挂载目录并将设备挂载到那里。

# 设备及其驱动程序

```
ACTION==="add", ATTRS(model)==="USB2FlashStorage", KERNEL="sd[a-z1]"
RUN+="/bin/mkdir -p /mnt/ate-flash%n"
ACTION==="add", ATTRS(model)==="USB2FlashStorage", KERNEL="sd[a-z1]"
PROGRAM="/lib/udev/vol_id -t %n", RESULT="vfat"
RUN+="/bin/mount vfat /dev/%k /mnt/ate-flash%n"
```

`PROGRAM` 和 `RUN` 键看起来相似，但 `PROGRAM` 是规则选择阶段的一部分的匹配键，而 `RUN` 是在规则触发后作为规则动作一部分的赋值键。上面的第二条规则验证了闪存盘是否包含文件系统，然后带有 `-t vfat` 选项执行 `mount` 命令。

类似的规则在设备移除时进行清理：

```
ACTION==="remove", ATTRS(model)==="USB2FlashStorage"
KERNEL="sd[a-z1]" /bin/mount -d /mnt/ate-flash%n
ACTION==="remove", ATTRS(model)==="USB2FlashStorage"
KERNEL="sd[a-z1]" /bin/rmdir /mnt/ate-flash%n
```

规则设置完成后，我们必须通知 `udev` 更改。`udevadm` 命令是少数需要 root 权限的命令之一：

```
ubuntu sudo udevadm --reload-rules
```

拼写错误在之后会被静默忽略，即使使用了 `--debug` 标志，因此务必仔细检查规则。

这就完成了！现在当闪存盘插入 USB 端口时，`udev` 会创建一个符号链接 `/dev/ate-flash1` 并将其挂载到 `/mnt/ate-flash1`。

```
ubuntu ls -l /dev/ate*
1rwrwxrw- 1 root 4 2009-08-09 21:22 /dev/ate-flash1 -> sdb1
```

```
ubuntu mount | grep athe
/dev/sdb1 mount /mnt/ate-flash1 type vfat (rw)
```

# FreeBSD 设备管理

正如我们在 331 页的简述中所看到的，FreeBSD 自管理的 `/dev` 文件系统被称为 `devfs`，其用户级设备守护进程是 `devd`。

# Devfs: 自动设备

正如我们在 331 页的简述中所看到的，FreeBSD 自管理的 `/dev` 文件系统被称为 `devfs`，其用户级设备守护进程是 `devd`。

# Devfs: 自动设备管理

与 Linux 的 `udev` 不同，`devfs` 是某种程度上可配置的。`devfs` 的配置分为两个部分

# 第 11 章

## 驱动程序与内核

例如，使用命令

```
linux sysctl net.ipv4.ip_forward=0
```
