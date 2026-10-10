
## 配置文件

此文件通常称为 `config-VERSION`（见上文示例），存储 Linux 内核的配置参数。此文件在新内核编译或安装时自动生成，用户*不应直接*修改此文件。

## 系统映射文件

此文件是一个查找表，将符号名称（如变量或函数）与其在内存中的相应位置相匹配。当调试一种称为*内核恐慌*的系统故障时，这非常有用，因为它允许用户知道发生故障时正在调用哪个变量或函数。与配置文件一样，其名称通常为 `System.map-VERSION`（例如 `System.map-4.15.0-65-generic`）。

## Linux 内核

这是真正的操作系统内核。其名称通常为 `vmlinux-VERSION`（例如 `vmlinux-4.15.0-65-generic`）。你也许还会发现使用 `vmlinuz` 代替 `vmlinux`，末尾的 z 表示文件已被压缩。

## 初始内存盘

这通常称为 `initrd.img-VERSION`，包含加载到 RAM 盘中的一个最小根文件系统，其中包含内核挂载真实根文件系统所需的实用程序和内核模块。

## 引导加载程序相关文件

在安装了 GRUB 的系统上，这些文件通常位于 `/boot/grub`，包括 GRUB 配置文件（GRUB 2 为 `/boot/grub/grub.cfg`，或 GRUB Legacy 为 `/boot/grub/menu.lst`）、模块（在 `/boot/grub/i386-pc` 中）、翻译文件（在 `/boot/grub/locale` 中）和字体（在 `/boot/grub/fonts` 中）。

# GRUB 2

## 安装 GRUB 2

可以使用 `grub-install` 实用工具安装 GRUB 2。如果您的系统无法启动，您需要使用 Live CD 或救援盘启动，查明系统的引导分区，挂载它，然后运行该实用工具。

以下命令假设您已以 root 身份登录。如果不是，请先运行 `sudo su -` 以“成为”root。完成后，输入 `exit` 注销并返回普通用户。

**注意**

系统中的第一块磁盘通常是*引导设备*，您可能需要知道该磁盘上是否有*引导分区*。这可以使用 `fdisk` 实用工具完成。要列出机器第一块磁盘上的所有分区，请使用：

```bash
# fdisk -l /dev/sda
Disk /dev/sda: 111.8 GiB, 120034123776 bytes, 234441648 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x97f8fef5

Device     Boot     Start       End  Sectors   Size Id Type
/dev/sda1  *         2048   2000895  1998848  976M 83 Linux
/dev/sda2       2002942  234440703  232437762  110.9G  5 Extended
/dev/sda5       2002944   18008063   16005120    7.6G 82 Linux swap / Solaris
/dev/sda6       18010112  234440703  216430592   103.2G 83 Linux
```

引导分区在 boot 列下用 `*` 标识。在上面的示例中，它是 `/dev/sda1`。

现在，在 `/mnt` 下创建一个临时目录，并挂载该分区：

```bash
# mkdir /mnt/tmp
# mount /dev/sda1 /mnt/tmp
```

然后运行 `grub-install`，将其指向*引导设备*（不是分区）和挂载引导分区的目录。如果系统有专用的引导分区，命令为：

```bash
# grub-install --boot-directory=/mnt/tmp /dev/sda
```

如果您正在安装到没有引导分区、但根文件系统上有 `/boot` 目录的系统，请将 `grub-install` 指向该目录。因此，命令为：

```bash
# grub-install --boot-directory=/boot /dev/sda
```

## 配置 GRUB 2

GRUB 2 的默认配置文件是 `/boot/grub/grub.cfg`。此文件是自动生成的，不推荐手动编辑。要对 GRUB 配置进行更改，您需要编辑 `/etc/default/grub` 文件，然后运行 `update-grub` 实用工具以生成符合规范的文件。

> **注意**
> `update-grub` 通常是 `grub-mkconfig -o /boot/grub/grub.cfg` 的快捷方式，因此它们产生相同的结果。

文件 `/etc/default/grub` 中有一些选项可以控制 GRUB 2 的行为，例如默认启动的内核、超时时间、额外的命令行参数等。最重要的选项包括：

- **GRUB_DEFAULT=**
  默认启动的菜单项。这可以是一个数值（如 `0`、`1` 等），也可以是菜单项的名称（如 `debian` 或 `saved`，后者与下文解释的 `GRUB_SAVEDDEFAULT=` 配合使用）。请记住菜单项从零开始编号，因此第一个菜单项是 `0`，第二个是 `1`，等等。

- **GRUB_SAVEDDEFAULT=**
  如果此选项设置为 `true`，且 `GRUB_DEFAULT=` 设置为 `saved`，则默认启动选项将是引导菜单中最后一次选择的选项。

- **GRUB_TIMEOUT=**
  在默认菜单项被选择之前的超时秒数。如果设置为 `0`，系统将直接启动默认项而不显示菜单。如果设置为 `-1`，系统将等待直到用户选择一个选项，无论花费多长时间。

- **GRUB_CMDLINE_LINUX=**
  这将列出将添加到 Linux 内核条目的命令行选项。

- **GRUB_CMDLINE_LINUX_DEFAULT=**
  默认情况下，每个 Linux 内核会生成两个菜单项，一个带有默认选项，另一个用于恢复模式。使用此选项，您可以添加仅添加到默认条目的额外参数。

- **GRUB_ENABLE_CRYPTODISK=**
  如果设置为 `y`，像 `grub-mkconfig`、`update-grub` 和 `grub-install` 这样的命令将查找加密磁盘，并添加启动时访问它们所需的命令。这会禁用自动启动（`GRUB_TIMEOUT=` 除 `-1` 以外的任何值），因为需要在访问磁盘之前输入口令来解密磁盘。

### 管理菜单项

当运行 `update-grub` 时，GRUB 2 将扫描机器上的内核和操作系统，并在 `/boot/grub/grub.cfg` 文件中生成相应的菜单项。可以手动向 `/etc/grub.d` 目录内的脚本文件添加新条目。

这些文件应该是可执行的，并由 `update-grub` 按数值顺序处理。因此，`05_debian_theme` 在 `10_linux` 之前被处理，依此类推。自定义菜单项通常添加到 `40_custom` 文件中。

菜单项的基本语法如下所示：

```text
menuentry "Default OS" {
    set root=(hd0,1)
    linux /vmlinuz root=/dev/sda1 ro quiet splash
    initrd /initrd.img
}
```

第一行始终以 `menuentry` 开始，并以 `{` 结束。引号中的文本将作为 GRUB 2 引导菜单上的条目标签显示。

`set root` 参数定义了操作系统根文件系统所在的磁盘和分区。请注意，在 GRUB 2 中磁盘从零开始编号，因此 `hd0` 是第一块磁盘（Linux 下的 `sda`），`hd1` 是第二块，等等。然而，分区从一开始编号。在上方的示例中，根文件系统位于第一块磁盘（`hd0`）、第一个分区 `(,1)`，即 `sda1`。

除了直接指定设备和分区外，您还可以让 GRUB 2 搜索具有特定标签或 UUID（*通用唯一标识符*）的文件系统。为此，请使用参数 `search --set=root`，后跟要搜索的 `--label` 参数和文件系统标签，或后跟文件系统的 UUID 的 `--fs-uuid`。

您可以使用以下命令找到文件系统的 UUID：

```bash
$ ls -l /dev/disk/by-uuid/
total 0
lrwxrwxrwx 1 root root 10 nov 4 08:40 3e0b34e2-94c9-43f2-90b0-2545ac1595d -> ../../sda5
lrwxrwxrwx 1 root root 10 nov 4 08:40 428e35ee-5ad5-4dcb-adca-539aba6c2d84 -> ../../sda6
lrwxrwxrwx 1 root root 10 nov 5 19:10 56C11DCDC5D2E1334 -> ../../sdb1
lrwxrwxrwx 1 root root 10 nov 4 08:40 ae71b214-0aec-48e8-80b2-090b6986b625 -> ../../sda1
```

在上方的示例中，`/dev/sda1` 的 UUID 是 `ae71b214-0aec-48e8-80b2-090b6986b625`。如果您希望将其设置为 GRUB 2 的根设备，命令将是 `search --set=root --fs-uuid ae71b214-0aec-48e8-80b2-090b6986b625`。

使用 `search` 命令时，通常添加 `--no-floppy` 参数，以免 GRUB 在软盘上浪费时间搜索。

`linux` 行指示操作系统内核的位置（在本例中，是文件系统根目录下的 `vmlinuz` 文件）。之后，您可以向内核传递命令行参数。

在上方的示例中，我们指定了根分区（`root=/dev/sda1`）并传递了三个内核参数：根分区应以只读方式挂载（`ro`），大多数日志消息应被禁用（`quiet`），并且应显示开屏画面（`splash`）。

`initrd` 行指示初始内存盘的位置。在上方的示例中，文件是 `initrd.img`，位于文件系统根目录下。

大多数 Linux 发行版实际上并不将内核和 initrd 放在根文件系统的根目录中。相反，这些是 `/boot` 目录或分区内实际文件的链接。

菜单项的最后一行应只包含字符 `}`。

## 与 GRUB 2 交互

使用 GRUB 2 启动系统时，您会看到一个选项菜单。使用箭头键选择选项，并按 `Enter` 确认并启动所选条目。

如果您只看到倒计时，而没有菜单，请按 `Shift` 调出菜单。

要编辑选项，使用箭头键选择该选项并按 `E`。这将显示一个编辑器窗口，其中包含与该选项相关的 `menuentry` 内容，如在 `/boot/grub/grub.cfg` 中定义的那样。

编辑选项后，输入 `ctrl` + `X` 或 `F10` 以启动，或按 `Esc` 返回菜单。

要进入 GRUB 2 shell，请在菜单屏幕上按 `c`（或在编辑窗口中按 `ctrl` + `C`）。您会看到这样的命令提示符： `grub >`

输入 `help` 以查看所有可用命令的列表，或按 `Esc` 退出 shell 并返回菜单屏幕。

