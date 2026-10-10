
`ACTION="add", KERNEL="sd[a-d] [0-9]*", RUN="/bin/miloader /dev/%k /media/usbdisk%n"`

`ACTION="remove", KERNEL="sd[a-d] [0-9]*", RUN="/bin/umount /media/usbdisk%n"`

`ACTION="remove", KERNEL="sd[a-d] [0-9]*", RUN="/bin/rmdir /media/usbdisk%n"`

在检测到设备时，`udev` 会创建一个指向实际 `devicedbisk` 的符号链接，其中 `n` 是设备号。例如，考虑 `udev0`：当你有一个名为 `/dev/usbdisk0` 的符号链接指向实际设备后。接下来，`RUN` 指令将在 `/media` 下创建一个同名的目录。注意，由于 `-p` 选项被传递给 `mkdir`，所有路径上的

如果这些新路径不存在，则会创建它们。添加操作的最终动作是将新发现的设备挂载在 `/media` 中创建的新挂载点上。当设备稍后移除时，将执行 `umount` 并删除该目录。

在位于 `/lib/udev/rules/99-usb-automount.rules` 配置了上述规则的 BeagleBoard 上插入 USB 闪存盘，将得到如下结果：

```
# ls /media

usbdisk/

# ls /media/usbdisk/

u-boot.bin

  UiName-beagle
```

# 19.7 持久化设备命名

持久化设备命名默认在 `udev` 中实现，使用了最初由 Hannes Reinecke 提出的方案。持久化命名规则位于包含字符串“persistent”的文件中。让我们检查一下这一切是如何运作的。

如果你查看你基于 `udev` 的系统中的 `/dev` 目录，你可以看到它在磁盘设备上的应用。

列表 19-14 显示了在将 USB 闪存盘插入连接到 BeagleBoard 端口的集线器后，我的 BeagleBoard 上 `/dev/` 目录中的文件。

```
LISTING 19-14 符号链接 by-id /dev/disk

# ls -l /dev/disk/by-id/

mc-SDG02_0x509c7de8- -> ../mmblk0

mc-SDG02_0x509c7de8-part1 -> ../mmblk0p1

mc-SDG02_0x509c7de8-part2 -> ../mmblk0p2

usb-Flash_Drive_SM_USB20_AA0401270000008398-0:0 -> ../sdb

usb-Flash_Drive_SM_USB20_AA0401270000008398-0:0-part1 -> ../sdb1

usb-SanDisk_Cuzer_Mini_SNDK86A0428636704-0:0 -> ../sda

usb-SanDisk_Cuzer_Mini_SNDK86A0428636704-0:0-part1 -> ../sda1
```

`ls -l` 的输出已经经过裁剪，以清除无趣数据的干扰。此目录中的符号链接按 `by-id` 列出。每个符号链接都指向 `udev` 为目标设备创建的设备节点。我们在这里从上到下看到：一张 SD 卡、一个通用 USB 闪存盘和一个 Cruzer Mini USB 闪存盘。在每种情况下，磁盘驱动器和设备上的每个分区都被列举在出来。你可以看到 SD 卡上有两个分区（`mmblk0` 是磁盘设备，`mmcblk0p1` 和 `mmcblk0p2` 是分区），并且，以类似的方式，在每个 USB 闪存盘上各有一个分区。

### 19.7.1 udev 辅助工具

等等，上文文本在逻辑流上有一个中断。让我根据提供的页面进行重新对齐：

符号链接就是持久化名称。你现在可以移除 USB 闪存盘并将其重新插入到不同的集线器端口。`udev` 通过其辅助工具 `usb_id` 为设备分配相同的名称（符号链接），使其指向正确的设备节点，这并不一定与你第一次插入它们时的原始设备节点相同。

列表 19-14 中显示的唯一 ID 字符串要么通过读取相关的原始设备，要么通过查询 `/sys` 中的属性数据产生。这是通过在 `udev` 树的 `extras` 目录找到一小组辅助工具完成的。有几个，包括 `scsi_id`、`cdrom_id`、`path_id` 和 `volume_id`。请查看 `udev` 树的 `extras` 子目录以获取所有工具。我们将使用 `udev` 工具来了解它们是如何运作的。

控制持久化名称（唯一 ID）的规则来自 `udev` 源码中的 `60-persistent-storage.rules`：

```
KERNEL=sd*[0-9]*|sr*, ENV(ID_SERIAL)!="%%", SUBSYSTEM==="usb",

IMPORT(program)=usb_id --export %p
```

该规则表示，对于任何 `ACTION` 为 `add` 或 `change` 的内核设备，如果内核设备名为 `sd*` 或 `sr*` 且不包含设备号（基础磁盘设备本身，而不是分区），则调用程序 `usb_id` 并将其从 `stdout` 的输出捕获为环境变量。`%p` 是一个 `udev` 字符串替换，指向 `DEVPATH`——即 `/sys` 中的路径。当我们在控制台上手动执行它时，看起来像这样：

```
# /lib/udev/usb_id --export /devices/platform/usb_hrdc/udev1/1-1/1-1-1.2/1-1.2:1.0

/host1/target:0:0:0:0:0/block/sda/sda

ID_VENDOR=SanDisk

ID_VENDOR_ENC=SanDiskx

ID_ID=07881

ID_MODEL=Cruzer_Mini

ID_MODEL_ENC=Cruzer\x20Mini\x20\x20\x20\x20

ID_MODEL_ID=5150

ID_REVISION=0.1
```

> 查看 `60-persistent-storage.rules` 文件以查看具体是如何操作的。`add|change` 子句位于规则文件的顶部，采用伪语句的形式，如果 `ACTION` 不是 `add` 或 `change`，则将跳过整个规则文件。

```
ID_SERIAL=SanDisk_Cruzer_Mini_SNDKBA0402863070
```

`mdev` 使用旧版的热插（hotplug）基础架构来接收内核事件（uevents）。回顾关于 `udev` 的列表 19-10，我们确保了用于热插代理名称的 `/proc` 文件被置（禁用），这样内核就不会将 uevent 传递给该代理。`busy-box mdev` 要求热插代理为其自身，通过 `/bin/mdev` 调用。启动脚本中的首要任务是将此 `/proc` 文件指向 `mdev`：

```
echo "/bin/mdev" > /proc/sys/kernel/hotplug
```

当然，这应该在启动脚本中挂载 `/proc` 之后完成。不那么明显的要求是还需要挂载 `/sys`。完成这些步骤后，你就可以使用该工具了。列表 19-16 是使用 busybox `mdev` 的示例启动脚本。

#### 列表 19-16 busybox mdev 示例启动脚本

```bash
#!/bin/sh

# 挂载虚拟文件系统

mount -t proc /proc /proc

mount -t sysfs /sys /sys

mount -t tmpfs /tmp /tmp

mount -t devpts /pts /dev/pts

# 将 /dev 挂载为 tmpfs

mount -n -t tmpfs -o mode=0755 udev /dev

# 复制默认静态设备，它们在这里被复制了

cp -a -f /lib/udev/dev/* /dev/

# 设置热插代理

echo "/bin/mdev" > /proc/sys/kernel/hotplug

# 启动 busybox mdev

/bin/mdev -s
```

`mdev` 的默认行为简单地在 `/dev` 中创建一个设备节点，其名称与 uevent 中的内核设备名相同。如果你不需要独立版 `udev` 的灵活性，这非常有用。它通常会为相关设备设备产生一个广为人知的名称。

在列表 19-16 中，调用 `mdev` 时传递的 `-s` 标志类似于 `udevadm trigger` 动作。它导致 `mdev` 扫描 `/sys` 并为发现的设备创建设备节点。通过这种方式，在 init 运行（或在 busybox 情况中是 busybox init）之前，为内核已经发现的初始设备创建设备节点。

## 19.8 在 busybox 中使用 udev

启动一个移除了 `udev` 且尚未启动 `mdev` 的 busybox 配置系统，我们得到如下结果：

```bash
# find /dev -type b -o -type c | wc -l

3
```
