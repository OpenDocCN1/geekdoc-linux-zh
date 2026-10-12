
最糟糕的情况是文件系统损坏，通常在重启宕机系统时被发现。系统尝试对 `/etc/fstab` 中记录的文件系统运行快速的 `fsck` 会话，从第六列包含 1 的文件系统开始，按数字顺序继续直到完成。`fsck` 程序会跳过第六列包含 0（零）的文件系统。

> **注意**
>
> 所有第六列包含 1 的文件系统首先并行检查，然后并行检查第六列包含 2 的文件系统，以此类推。

如果损坏严重到无法自动修复，系统会显示一条消息，提示 `按 Ctrl-d 继续`，否则请输入 root 密码以执行文件系统检查。输入 root 密码会显示 shell 提示符并打印一条有用的消息，告诉你需要检查哪个文件系统。

可以帮助忙碌的系统管理员的 `fsck` 选项包括：

- `-A` — 遍历 `/etc/fstab`，在单次长流程中检查所有文件系统
- `-C` — 为支持其显示的操作提供百分比或井号进度条
- `-N` — 执行试运行（不做任何更改），显示将会执行的操作；不要更改任何内容（适合查看情况有多糟糕）
- `-v` — 为所有操作产生详细输出，包括由 `fsck` 执行的命令
- `-a` — 不提问，非交互式地修复文件系统

`fsck` 对文件系统执行五次通过或五类更改，如下所示：

- 通过 1 — 检查 inode、块和大小
- 通过 2 — 检查目录结构
- 通过 3 — 检查目录连接性
- 通过 4 — 检查引用计数
- 通过 5 — 检查组汇总信息

当 `fsck` 发现严重错误（如多个文件声称的块（交叉链接）、文件系统外声称的块、链接计数过少（链接到 inode 的目录数量）或未记录的对应未分配 inode 的块或目录）时，它会显示错误消息并要求手动运行。

> **警示**
>
> 始终、务必在未挂载或以只读方式挂载的文件系统上运行 `fsck`。这是强制性的；否则，`fsck` 和用户写入可能会同时发生，导致损坏。如果是根文件系统，你应该在单用户模式下操作，或使用救援 CD-ROM 确保根文件系统是以只读方式挂载的。

以下是一个简单示例，检查挂载在 `/fun` 目录上且位于 `/dev/hdb1` 上的文件系统：

```bash
mount /fun
fsck.ext2 -v /dev/hdb1
```

以下是 `fsck` 的输出：

```bash
e2fsck 1.18, 11-Nov-1999 for EXT2 FS 0.5b, 95/08/09
/dev/hdb1: clean, 9692/1237888 files, 1754206/2474002 blocks
```

以下是对当前未挂载的同一文件系统执行详细（没有所有 yes 答案）强制检查的示例：

```bash
fsck.ext2 -v -f /dev/hdb1
```

以下是输出：

```bash
e2fsck 1.18, 11-Nov-1999 for EXT2 FS 0.5b, 95/08/09
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
9692 inodes used (0%)
157 non-contiguous inodes (1.6%)
# of inodes with ind/dind/tind blocks: 1194/205/0
1754206 blocks used (70%)
0 bad blocks
```

## 调整文件系统

`tune2fs` 命令用于在文件系统创建后设置参数，例如最大挂载次数。这个数字默认设置为 20，除非你在文件系统创建时设置或稍后使用 `tune2fs` 更改它。以下是一个将 ext3 日志文件系统的挂载计数设置为 0（零）的示例：

```bash
tune2fs -c 0 /dev/hda1
```

这会导致系统完全忽略挂载计数，并且永远不会例行启动文件系统检查。对于 ext3 文件系统而言，这是期望的行为，因为日志（journal）存储了文件系统的状态，所以 ext3 永远不会将文件系统标记为脏或损坏。

除了挂载计数，错误检查可以调整，以便当内核检测到文件系统的错误时，系统执行以下三种操作之一：

- `continue` — 正常继续
- `remount` — 将文件系统重新挂载为只读模式，准备进行 `fsck`
- `panic` — 导致内核恐慌，从而停止系统（除非您是系统测试人员，否则不推荐）

与 root 用户关联的保留百分比（仅 root 用户可用的空间）也可以通过 `-g` 选项与系统组关联，例如：

```bash
tune2fs -g admins /dev/sdb5
```

## 调试文件系统

`debugfs` 命令对于调试和修改机器上的文件系统非常有用。它极易删除或损坏文件系统的部分或全部内容，因此建议极度谨慎。

> **注意**
>
> 事实上，您必须阅读 `debugfs` 的 man 手册页才能看到如何损坏文件系统。它默认不以读写模式挂载，这可能是因为用户可以找到该命令。您已被警告过。

`debugfs` 工具是交互式的，拥有一个命令行 shell 环境，您只需输入 `?` 并按下 `Enter` 键即可获取帮助。

例如，您只需输入以下命令即可进入该工具：

```bash
debugfs /dev/sdb5
```

然后输入 `?` 并按下 `Enter` 键，即可查看可用的命令菜单。一些有趣且信息丰富的命令包括：

- `open` — 打开一个文件系统用于调试
- `features` — 显示文件系统的功能集
- `stats` — 显示文件系统的统计信息，类似于 `dumefs -h` 的输出
- `ls` — 显示目录，默认为根目录 `/`
- `pwd` — 显示当前工作目录
- `undelete` — 撤销文件删除（在删除后立即使用通常有效）
- `logdump` — 显示日志内容（如果位于日志引导文件系统中）
- `quit` — 退出该工具

## 挂载与卸载

在本章的最后部分，我们将讨论文件系统的挂载和卸载、可用选项，以及该主题在考试中的应用。

## 文件系统表

为了使普通用户能够使用文件系统，该文件系统必须由 root 用户挂载，或者以允许该权限用户的正确选项放入 `/etc/fstab` 文件中。当 `/etc/fstab` 中存在正确的条目时，用户只需发出 `mount` 命令并提供挂载点或设备的完整路径即可完成挂载。

文件系统应设置在 `/etc/fstab` 中，每个文件系统占一行。已挂载的条目反映在 `/etc/mtab` 中，该系统文件作为已挂载文件系统的描述由系统维护。这些信息（或其中大部分）也位于 `/proc/mounts` 文件中。

输入 `mount` 命令以查看当前文件系统列表。以下是一个示例：

```bash
mount
/dev/sda2 on / type ext3 (rw)
none on /proc type proc (rw)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
/dev/sda1 on /boot type ext3 (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
/dev/sdb8 on /home/data type ext3 (rw)
```

此输出可以与 `/proc/mounts` 文件的输出进行比较：

```bash
cat /proc/mounts
rootfs / rootfs rw 0 0
/dev/root / ext3 rw 0 0 /
/proc /proc proc rw 0 0
usbdevfs /proc/bus/usb usbdevfs rw 0 0
/dev/sda1 /boot ext3 rw 0 0
none /dev/pts devpts rw 0 0
none /dev/shm tmpfs rw 0 0
/dev/sdc8 /home/data ext3 rw 0 0
```

这两个命令都可以使用，但 `mount` 命令包含选项和其他有用信息。

文件系统表（`/etc/fstab`）应包含每个文件系统一行，包括设备、挂载点、文件系统类型、选项以及 dump/check 顺序。此文件（WHR）应仅可由 root 用户修改；否则，任何用户都可以将可移动设备或磁盘放入系统中并挂载它，可能会将数据复制到流氓设备上。

以下是一个活动的 `/etc/fstab` 文件示例：
