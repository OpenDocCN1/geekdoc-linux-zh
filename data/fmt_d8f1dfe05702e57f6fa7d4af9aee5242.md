
![](img/b652b4dadd201d28c21028cece91d826_332.png)

> 而不是提供数字 `1` 单用户模式，你可以指定字母 `s` 或 `S`。可能是你的初始化程序（通常是 `/sbin/init`）损坏或配置错误。

## `boot:`

### 使用 `GRUB` 作为引导加载器

`GRUB` 已成为许多 Linux 发行版的引导加载器，因为它提供了许多 `LILO` 缺乏的功能。例如，在编辑配置后不需要重新安装引导加载器。`GRUB` 能够在启动时读取其配置文件，这意味着你不需要将其写入扇区。与 `LILO` 不同，你可以在启动过程中与 `GRUB` 交互，传递选项来控制系统启动。

### 配置 `GRUB` 引导加载器

`GRUB` 加载器的通常位置是 `/boot/grub/menu.lst`。某些发行版（如 Fedora、Red Hat 和 Gentoo）使用 `grub.conf` 而不是 `menu.lst`。像 `LILO` 一样，`GRUB` 配置文件分为全局和逐镜像段，每个段都有自己的选项。在进入细节之前，你应该了解一些 `GRUB` 的特性。

#### `GRUB` 术语与特性
列表 6.2 显示了一个示例 `GRUB` 配置。该文件大致相当于列表 6.1 中的 `LILO` 配置。特别是，它可以使用相同的内核启动操作系统——位于 `/dev/h5` 的 Fedora、位于 `/dev/h6` 的 Debian 以及位于 `/dev/h2` 的 DOS。Fedora 和 Debian 共享 `/boot` 分区（`/dev/h1`），`GRUB` 配置就位于那里。

#### 列表 6.2：示例 `GRUB` 配置文件

```
# grub.conf/menu.lst

#
# 全局选项:
#

default=0

timeout=15

splashimage=/grub/bootimage.xpm.gz

#
# 内核镜像选项:
#

title Fedora (2.6.9)

root (hd0,0)

kernel /mlinux-2.6.9 root=/dev/h5 mem=512M

initrd /initrd-2.6.9

title Debian (2.6.11.10-experimental)

root (hd0,0)

kernel (hd0,0)/bzImage-2.6.11.10-experimental ro root=/dev/h6

#
# 其他操作系统
#

title DOS

rootnoverify(hd0,1)

chainloader +1
```

### 配置引导程序

`GRUB` 引导程序并不使用 Linux 那种文件名来引用设备。`GRUB` 对设备进行编号，因此 `GRUB` 使用的是 `(hd0)` 而不是 `/dev/hda`。同样地，`/dev/hdb` 将变变为 `(hd1)`。`GRUB` 不区分 ATA 和 SCSI 设备，因此在仅支持 SCSI 的系统上，第一个设备将是 `(hd0)`。在 ATA 和 SCSI 混合的系统上，ATA 驱动器通常获得较小的数字编号，尽管情况并不总是如此。

此外，`GRUB` 对磁盘上分区的编号是从 0 开始的，而不是 Linux 使用的 1。`GRUB` 用逗号分隔分区编号，例如，`(hd0,0)` 表示第一块磁盘上的第一个分区（通常为 `/dev/hda1`），或 `(hd0,4)` 表示第一块磁盘上的第一个逻辑分区（通常为 Linux 的 `/dev/fd0`），或者如果你有多个软驱器，可能是 `(fd1)` 或更高。软磁盘是不分区的，因此它们不会获得分区。

`GRUB` 定义了自己的根分区，这可能与 `GRUB` 的根分区不同。`GRUB` 的根分区是存放 `GRUB` 文件（`menu.lst` 或 `grub.conf`）的分区。该文件通常位于 Linux 的 `/boot/grub/` 目录下；如果你没有使用独立的 `/boot` 或 `/boot/grub` 分区，则 `GRUB` 的根目录将与 Linux 的根目录相同。但是，如果你将 `/boot` 拆分为单独的分区（这是非常常见的），那么 `GRUB` 的根分区将与 Linux 的 `/boot` 分区相同。在引用 `GRUB` 配置目录下的文件时，你必须记住这一差异。

### 核心 `GRUB` 全局选项

`GRUB` 的全局部分包含了其预镜像配置。通常，你在全局部分找到的选项比在 `LILO` 配置中找到得多：

- **默认操作系统**：`default=option` 告诉 `GRUB` 启动哪个操作系统。列出列表 6.2 中的 `default=0` 会导致启动第一个操作系统（记住 `GRUB` 索引从 0 开始）。如果你想启动第二个操作系统，请使用 `default=1`，对你所有的操作系统以此此类推。
- **超时（Timeout）**：`timeout=option` 定义了在启动操作系统之前等待用户输入的时间（单位为秒）。注意，`GRUB` 以秒为单位测量超时时间，而 `LILO` 使用的是十分之一。
- **背景图形**：`splashimage=` 行指向一个图形文件，该文件将作为启动过程的背景显示。此行是可选的，但大多数 Linux 发行版都会指向一个镜像来美化启动菜单。文件名引用相对于 `GRUB` 根分区的，因此如果 `/boot` 在单独的分区上，则路径中的该部分将被省略。或者，路径也可能以 `GRUB` 设备规范开头，例如使用 `(hd0,5)` 来引用该分区上的一个文件。

### 核心 `GRUB` 镜像特定选项

`GRUB` 的镜像选项通常在第一行之后缩进，与 `LILO` 类似，但这是一种约定，而不是文件格式的要求。选项以标识符开始，并继续是告诉 `GRUB` 如何处理该镜像的选项：

- **标题（Title）**：标题行开始一个镜像段落（stanza），并指定引导加载程序运行时显示的标签。与 `LILO` 的 `label` 选项不同，`GRUB` 的 `title` 可以接受空格，并且按照惯例描述性得多，如列表 6.2 所示。
- **`GRUB` 根分区（`GRUB` root）**：`root` 选项指定 `GRUB` 根分区的位置。如果存在，这将是 `/boot` 分区；否则，它通常是 Linux 根（`/`）分区。（`GRUB` 可以存在于 FAT 分区、软磁盘或某些其他操作系统的分区上，尽管根目录下的 `GRUB` 可能位于任何奇异的地方。）
- **内核规范（Kernel specification）**：描述 Linux 内核位置以及任何传递给它的内核选项的内核设置。路径相对于 `GRUB` 的根分区。作为替代，你可以使用 `GRUB` 的语法指定设备，例如 `kernel(hd0,5)/linux root=/dev/hda5`。注意，你在这一行上传递内核选项。`LILO` 将内核选项分在单独的行，例如 `append=line`、`line=line` 和只读选项。在 `GRUB` 中，你将这些选项合并到内核行中。`root` 选项告诉内核以只读方式挂载根文件系统（稍后会重新挂载为读写），`root=` 指定 Linux 根文件系统。因为这些选项是传递给内核的，在需要时使用 Linux 风格的设备标识符，这与 `GRUB` 配置文件的其他选项不同。
- **初始内存磁盘（Initial RAM disk）**：使用 `initrd` 选项指定初始内存磁盘，类似于 `LILO` 中同名的选项。
- **非根（Non-root）**：`rootverify` 选项与 `root` 选项类似，区别是 `GRUB` 将不会尝试访问分区上的此文件。它用于为 `GRUB` 无法直接加载内核的操作系统指定分区，例如 DOS 和 Windows。
- **链式加载（Chain loading）**：`chainloader` 告诉 `GRUB` 将控制权交给另一个引导加载程序。通常，它是 `+1` 选项，用于加载根分区的第一个扇（通常用 `rootverify` 指定）并将执行权交给此次级引导加载程序。

要向 `GRUB` 添加内核，请遵循以下步骤：

1. 以 `root` 身份，将 `menu.lst` 或 `grub.conf` 文件加载到文本编辑器中。
2. 复制一个用于 Linux 内核引导分区的可用配置。
3. 修改标题行以指向你新配置的唯一名称。
4. 修改内核行以指向新内核。如果你需要更改任何内核选项，请进行修改。
5. 如果需要添加、删除或更改内存磁盘，请修改 `initrd` 行。
6. 根据需要修改内核行。
7. 保存更改并退出编辑器。
8. 此时 `GRUB` 已配置好启动。使用 `B` 键启动。

> 警告：在确定内核正常之前不要重启。

### 安装引导加载程序

安装 `GRUB` 与 `LILO` 有些不同。安装 `GRUB` 的命令如下：

```
grub-install /dev/hda
```

或者

```
grub-install '(hd0)'
```
