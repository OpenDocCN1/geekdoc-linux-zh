
# GRUB

`GRUB` 是一个 GNU 软件包（www.gnu.org/software/grub），它已经取代了 `LILO` 成为 Fedora 中唯一的可用引导程序。`GRUB` 提供了以下功能：

- 支持多种可执行格式。
- 支持多个操作系统（如 Fedora、FreeBSD、NetBSD、OpenBSD 以及其他 Linux 系统）。
- 通过链式加载（chain-loading）功能支持多启动操作系统（如 Windows 95、Windows 98、Windows NT、Windows ME、Windows XP 和 OS/2）。链式加载是从 `GRUB` 加载另一个引导程序（假设是特定于专用操作系统的引导程序）以启动所选操作系统的行为。
- 支持多种文件系统类型。
- 支持引导镜像的自动解压。
- 支持从网络下载引导镜像。

更多关于 `GRUB` 如何工作的信息，请输入 `man grub` 或 `info grub`。`info` 命令包含了关于 `GRUB` 的细节。或者，查看 `GRUB` Wiki：http://grub.enbug.org。

## 使用 GRUB 启动

当你安装 Fedora 或 RHEL 时，启动计算机（带有一个或多个操作系统）所需的信息会自动设置好并准备就绪。只需重启计算机。当你看到启动信息时，按下回车键（在超时之前前快速按下），就会出现 `GRUB` 启动屏幕（顶部显示 `GRUB`，下方列出各个分区）。然后你可以执行以下操作之一：

- 默认 — 如果你什么都不做，默认操作系统将在几秒后自动启动。
- 选择操作系统 — 使用上、下方向键选择屏幕上显示的任何操作系统。然后按回车键启动该操作系统。
- 编辑启动过程 — 如果你想更改启动过程中使用的任何任何选项，请使用方向键选择你想要的操作系统并输入 `e` 进行选择。按照接下来的步骤临时更改你的启动选项。

如果你想更改启动选项以便在每次启动计算机时生效，请查看“永久更改启动选项”章节。更改这些选项涉及编辑 `/boot/grub/grub.conf` 文件。

## 临时更改启动选项

通过 `GRUB` 启动屏幕，你可以选择为当前启动会话更改或添加启动选项。首先，在 `GRUB` 超时并启动默认系统之前，快速按下回车键。在出现的 `GRUB` 选择界面中，使用方向键选择你想要的操作系统并输入 `e`（如前所述）。你将看到一个包含如下信息的信息的图形化界面：

```
GNU GRUB version 0.97 (639K lower / 136048K upper memory)
root(hd0,0)
kernel /boot/vmlinuz-2.6.17-1.2647.fc6 root=LABEL==/1 rhgb quiet
initrd /boot/initrd-2.6.17-1.2647.fc6.img
Use the f and j keys to select which entry is highlighted.
Press 'b' to boot, 'e' to edit the selected command in the
boot sequence, 'c' for a command-line, 'o' to open a new line
after ('0') for before the selected line, 'd' to remove the
selected line, escape to go back to the main menu.
```

图 2-3：通过 `GRUB` 菜单从你的 Fedora 系统编辑启动项。

`GRUB` 编辑界面的示例中有三行用于标识你所选操作系统的启动。第一行（以 `root` 开头）显示 `GRUB` 引导程序的项位于第一块硬盘的第一分区（`hd0,0`）。无论硬盘是 SCSI、IDE 还是其他类型，`GRUB` 都将硬盘表示为 `hd0`。你只需要从零开始计算驱动号和分区号。

示例的第二行（以 `kernel` 开头）标识了引导镜像（`/boot/vmlinuz-2.6.17-1.2647.fc6`）和若干选项。这些选项标识了初始加载（只读）的分区，以及标签为 `LABEL=` 的分区上的根文件系统位置。第三行（以 `initrd` 开头）标识了初始 RAM 磁盘的位置，该磁盘包含了启动过程中所需的最小文件和目录。

如果你打算更改任何与启动过程相关的行，你可能只会更改第二行来添加或删除启动选项。以下是操作方法：

1. 将光标置于 `kernel` 行上并输入 `e`。
2. 在引导镜像名称后添加或删除选项。你可以使用极简的 bash 命令行编辑功能来编辑该行。你可以使用命令补全（输入文件名的一部分并按 Tab 键完成）。以下是一些你可能想要添加或删除的选项：
   - 进入 shell — 如果你忘记了 root 密码或启动过程挂起，可以通过添加 `init=/bin/sh` 直接进入 shell。
   - 关闭服务 — 如果启动过程挂起，添加 `acpi`、`npci`、`nodma` 或 `selinux`。
   - 选择运行级别 — 如果你想进入特定的模式，更改 linux 之后的数字。
3. 按 `b` 启动
4. 在 `grub.conf` 中保存新选项。

## 永久更改启动选项

如果你想更改启动选项以便在每次启动计算机时生效，请查看“永久更改启动选项”章节。更改这些选项涉及编辑 `/boot/grub/grub.conf` 文件。

以下是 `grub.conf` 的示例：

```
default=0
timeout=5
hidden
title Fedora Core
kernel /boot/vmlinuz-2.6.17-1.2647.fc6 root=LABEL==/1 rhgb quiet
initrd /boot/initrd-2.6.17-1.2647.fc6.img
splashimage /boot/grub/splash.xpm.gz
title Windows XP
chainloader=1
```

`default=0` 表示列表中的第一个分区是默认启动分区。`timeout=5` 允许 `GRUB` 在启动前暂停 5 秒。`splashimage` 行加载 `/boot/grub/splash.xpm.gz` 作为启动屏幕上的图像。

# 第 2 章：安装 Fedora 81

`/dev/hda2` 最终被挂载为 `/boot`。内核行上的其他选项会将该分区初始设置为只读 (`ro`)，并将根文件系统设置为 `LABEL=/`

对于 Windows XP 分区，`rootverify` 行表示 `GRUB` 不应尝试挂载该分区。在这种情况下，Windows XP 位于第一块硬盘的第一个分区 (`hd0,0`) 或 `/dev/hda1` 上。链式加载程序 `+1` 并不是挂载分区并向新操作系统传递选项，而是将系统的启动控制权交给另一个引导程序。`+1` 表示分区的第一个扇区被用作引导程序。

> 注意：微软操作系统要求您使用链式加载程序从 `GRUB` 启动。

如果您对 `/boot/grub.conf` 文件进行了任何更改，无需手动加载这些更改。这些更改在您重启电脑时会被 `GRUB` 自动读取。如果您习惯于使用 `LILO` 引导器，起初可能会让您感到困惑，因为 `LILO` 要求您重新运行 `lilo` 命令才能使更改生效。

## 添加新的 GRUB 启动镜像

对于包含不同特征的内核，您可能有不同的启动镜像。如今，当您获取 Fedora 或 RHEL 的更新内核时，您应该加载包含该内核的 RPM 包，该内核会被添加到 `grub.conf` 中作为默认启动内核。在启动时，您可以选择想要运行的内核。

> 注意：为了防止启动屏幕上出现几十个条目并堆积大量内核，当您在 Fedora 系统上安装新内核时，除了最近的内核外，所有旧内核都会被移除。同样，在您添加新内核时，不会获得大量的启动条目，您的 `grub.conf` 文件中只会维护最近的内核条目。

如果您自己构建了内核，或者从其他来源获取了内核，您需要手动修改 `grub.conf` 文件来告诉 Fedora 或 RHEL 启动该内核。以下是修改 `grub.conf` 文件的步骤：

- 1. 将新镜像从创建它的目录（例如 `/usr/src/kernels/linux-2.6.15-1/arch/i386/boot/`）复制到 `/boot` 目录。使用一个反映其内容的名称，例如 `bz-2.6.15-1`。例如：

  ```cp /usr/src/linux-2.6.15-1/arch/i386/boot/bzImage /boot/bz-2.6.11-5```
- 2. 在 `/boot/grub.conf` 文件中添加几行，以便在启动时如果选择了该镜像就可以启动：

```
title Fedora Core (My own IPv6 build)

root (hd0,1)

kernel bz-2.6.17-0 root=/dev/hda2

initrd /initrd-2.6.17-0.img
```
