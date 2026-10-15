
## 使用 BootMagic 进行引导管理

BootMagic 是一个引导加载器工具，支持多种不同的操作系统。该程序基本上提供了一个图形界面，你可以使用鼠标或键盘选择并启动笔记本上已安装的操作系统。BootMagic 通常与 PowerQuest 的商业分区工具 PartitionMagic 一起安装。

不幸的是，BootMagic 必须使用 Windows 进行安装，并且配置是通过一个仅限 Windows 使用的工具完成的。另一个缺点是，BootMagic 必须安装在你的可启动设备的 MBR 中。如果你使用 LILO 来启动 Linux，那么 LILO 必须安装在根 Linux 引导分区中。

## 使用 System Commander 进行引导管理

System Command Deluxe 是 Linguist Software 的一款产品，是一种替代性的商业引导加载器，也可以用于启动 Linux。与 BootMagic 类似，System Commander 可以使用 Windows 安装，但也可以提供使用 DOS 安装的功能。根据 Linguist Software 的说法，System Commander 可以配置为禁止访问硬盘，并防止使用软盘驱动器启动系统。请注意，你也可以通过在硬盘上安装引导加载器、在笔记本 BIOS 中禁用可移动设备作为启动项，然后为 BIOS 设置密码来实现同样的效果。

## 使用 LILO 进行引导管理

LILO 是一个免费的、灵活的、功能强大的引导加载器，你可以使用 Linux 来安装它。LILO 几乎可以启动安装在笔记本上的任何操作系统，并且可以轻松配置以启动 DOS、Windows、FreeBSD、OpenBSD 和其他系统。如果你的 X11 出现问题，例如 Linux 系统被设置为直接启动到 X11 但 `XF86Config` 配置损坏时，LILO 也很有帮助。症状包括 X 服务器反复尝试运行并失败时，屏幕出现闪烁和重复显示。

通常你可以使用 `Ctrl+Alt+Delete` 重启你的机器。然后，在 `LILO` 引导提示符处，使用 `LILO` 通过 `linux single` 选项告知 Linux 以 root 管理模式启动：

```
boot: linux single
```

如果这不起作用，你还可以尝试以下命令：

```
boot: linux 0
```

这将启动 Linux，但禁用网络服务和 X11。最终你会到达 root 提示符，然后可以着手修复任何问题。你还可以使用 LILO 实施密码保护。这需要你编辑 `/etc/lilo.conf` 文件。

使用你喜欢的文本编辑器（例如 `pico` 编辑器），按如下方式打开该文件：

```
$ pico /etc/lilo.conf
```

然后你可以插入 `password=` 条目，并附带一个未加密的密码。（提示：不要使用与你登录 Linux 相同的密码！）例如：

```
image=/boot/vmlinux
  label=linux
  password=abcd
  initrd=/boot/initrd
```

进行你的更改并保存文件（如果使用 `pico`，请按 `Ctrl+X`）。你必须然后运行 `lilo` 来写入新的引导加载器，如下所示：

```
# /sbin/lilo
```

下次重启时，你会看到 `LILO` 提示符：

```
LILO boot:
```

按 `Enter` 键，你将看到：

```
Password:
```

输入你的密码并按 `Enter` 键以启动。（超级提示：你可以为在 `/etc/lilo.conf` 中配置的每个操作系统引导部分分配不同的密码！如果你已启用笔记本 BIOS 启动密码，这意味着可能需要三个密码才能使用 Linux！）

引导启动的一个潜在问题是，如果你安装 Linux 后又安装了另一个操作系统（如 Windows）。其他操作系统通常会抹去笔记本硬盘的 MBR，LILO 将会消失，这可能导致你无法启动到 Linux。最佳方法是在笔记本上安装完所有其他操作系统后再安装 LILO。这包括 BSDs、BeOS 和 OS/2。

LILO 还可以帮助你解决在具有麻烦 IDE 控制器的笔记本上安装 Red Hat Linux 的问题。LILO 引导提示符可用于向 Linux 内核传递消息或参数。例如，经验丰富的 IBM ThinkPad 600x（以及可能的 570）用户会使用以下命令：

```
linux hda=1558,240,63 hdc=cdrom
```

在 LILO 引导提示符处输入上述命令，以启用 Linux 识别内部硬盘驱动器和光盘驱动器（如果可用）。`hda=` 条目指定了硬盘驱动器的设备名称（`/dev/hda`）并提供刻录在驱动器上的设置。这些设置代表硬盘驱动器中的柱面数、扇区数和磁头数。这些选项也可以在 Red Hat 安装过程中使用。它们作为选项插入 LILO 配置对话框中，如下所示：

```
append = 'hda=1024,12,63'
```

此选项可以启用 Linux 在 ThinkPad 701 系列笔记本上启动。如果你在安装或启动 Linux 时因 LILO 错误遇到问题，请参阅第 3 章中的“引导加载器及陷阱”。你还应该查阅 Linux 笔记本页面，寻找针对你笔记本的解决方案。（如果你拥有知名厂商生产的主流笔记本，很可能在你之前已经有人安装过 Linux，并可能已解决了任何严重的技术问题。）

要卸载 LILO，你可以使用 DOS 的 `FDISK` 命令及其 `/MBR` 选项。将笔记本启动到 DOS，然后使用以下命令：

```
C:> FDISK /MBR
```

要在 Linux 下卸载 LILO，使用 `lilo` 命令及其 `-u`（卸载）选项：

```
# lilo -u
```

请确保你手头有启动盘，或者你确实想要卸载 LILO！

## Apple iBook 使用 BootX 进行引导管理

Apple iBook Linux 用户可以通过至少两种方式启动 Linux。第一种方式使用 iBook 中 Apple 的 OpenFirmware 引导 ROM，以及一个名为 Yaboot 的工具。第二种方式更简单、更常见，是使用 BootX 控制面板设备，该设备在 Mac 启动后启动。

Yaboot 工具在某种程度上类似于 LILO，并且在其配置文件中使用了相似的语法。使用 Apple 的 Open Firmware 提示符和 Yaboot 的一个好处是你将能够使用 iBook 的内部调制解调器。要使用 Yaboot 引导加载器（包含在 Yellow Dog Linux CD-ROM 上）启动 Linux，请在运行 MacOS 时将文件 `vmlinux`、`yaboot.tbxl` 和 `yaboot.conf` 复制到 iBook 的硬盘上。编辑 `yaboot.conf` 文件，使其看起来像这样：

```
timeout=5
default=linux

image=hd:8,/vmlinux
label=linux
root=/dev/hda10

novideo
```

保存并关闭该文件，然后重新启动你的 iBook。在重启过程中，按住 `Cmd+Option+o+f` 键，你会看到苹果的 Open Firmware 提示符。要引导 Linux，请使用 `boot` 关键字，并指向 Yaboot 引导加载程序，例如：

```
boot hd:8,/yaboot.tzh1
```

然后你将引导进入 Linux。请注意，至少在使用 Yellow Dog Linux 1.2 时，你的 X11 会话将限制为 256 色！你可以通过浏览 [http://www.yellowdoglinux.com/support/faq/bootloader.shtml](http://www.yellowdoglinux.com/support/faq/bootloader.shtml) 来了解有关 Yaboot 的更多信息。

引导 Linux 的更简单方法是使用 BootX。此程序允许你选择不同的 Linux 内核，引导使用 Yellow Dog Linux 1.2 光盘进行安装，并设置各种选项，例如延迟或视频设置。如果在 iBook 上使用 BootX，当前或新的 Linux 内核可以保存在 Mac 系统文件夹中名为 Linux Kernels 的文件夹内。这是测试新的 Linux PPC 内核的一种简便方法。

为了在 Apple iBook 上正确引导 Yellow Dog Linux，你应该使用以下 BootX 设置：

- 在 Kernel: 字段中应选择正确的 Linux 内核。
- 根设备（如果 Yellow Dog Linux 安装在同一硬盘上）应设置为 `/dev/hda10`。
- 应选择 “No video driver” 选项。
- 在 Options 对话框中，应选择 “Force video settings” 选项。
