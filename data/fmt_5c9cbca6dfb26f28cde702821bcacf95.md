
从 Windows XP CD 启动，并在安装过程中按 `(R)` 键启动恢复控制台（Recovery Console）。从列表中选择您的 Windows XP 安装并输入管理员密码。在输入提示符处输入命令 `FIXMBR` 并用 `y` 确认安全查询。然后输入 `exit` 重启计算机。

# 恢复 Windows 2000 MBR

从 Windows 2000 CD 启动。在安装过程中，在下一个菜单中按 `(R)` 然后按 `(C)` 以启动恢复控制台（Restore Console）。从列表中选择您的 Windows 2000 安装并输入管理员密码。在输入提示符处输入命令 `FIXMBR` 并用 `y` 确认安全查询。然后输入 `exit` 重启计算机。

## 创建引导 CD

这涉及到尝试启动使用 YaST2 配置的 LILO 引导管理器的系统时出现的问题。在较新的 SuSE Linux 版本中，创建系统引导盘会失败，因为软磁盘上的可用空间已不再足以启动文件。

### 步骤

如果您的系统安装了 CD 驱动程序，就可以创建一个包含 Linux 文件的可引导 CD-ROM。此解决方案只是临时权宜之。通常可以正确配置 LILO。请参考 `/usr/share/doc/packages/lilo/README` 中关于此主题的、`lilo.conf` 的 man page (`man lilo.conf`) 以及 `lilo` 的 man page (`man lilo`)。

# 使用 ISOLINUX 的引导 CD

使用 ISOLINUX 引导管理器创建可引导 CD 最简单。SuSE 安装 CD 也是通过 isolinux 实现可引导的。

- 先使用以下替代程序启动已安装的系统：
  - 从用于安装的安装 CD 或 DVD 启动。
  - 在引导序列中选择预选选项 `installation`（安装）。
  - 接下来选择语言和键盘布局。
  - 在后续菜单中，选择 `Boot installed system`（启动已安装的系统）。
  - 系统会自动检测根分区并从中启动。

- 使用 YaST2 安装软件包 `syslinux`。

- 打开 root shell。以下命令创建一个临时目录，并将启动 Linux 系统所需的文件（Linux 引导加载程序以及内核和 initrd）复制到其中：

```
earth: # mkdir /tmp/CDroot
earth: # cp /usr/share/syslinux/isolinux.bin /tmp/CDroot/
earth: # cp /boot/vmlinux /tmp/CDroot/linux
earth: # cp /boot/initrd /tmp/CDroot
```

- 使用您喜欢的编辑器创建引导加载配置文件 `/tmp/CDroot/isolinux.cfg`。

```
DEFAULT linux
LABEL linux
KERNEL linux
APPEND initrd=initrd root=/dev/hdXY [boot parameter]
```

为参数 `root=/dev/hdXY` 输入您的根分区。它列在文件 `/etc/fstab` 中。为设置 `[boot parameter]` 输入额外选项，这些选项应在启动期间使用。配置文件例如所示：

```
DEFAULT linux 
LABEL linux 
KERNEL linux 
APPEND initrd=initrd 
root=/dev/hda7 hd-ide-scsi
```

随后（在命令提示符处输入）将为 CD 创建 ISO-9660 文件系统。

```
mkisofs -o /tmp/bootcd.iso -b isolinux.bin -c boot.cat
-no-emul-boot -boot-load-size 4
-boot-info-table /tmp/CDroot
```

整个命令必须作为一行输入。

- 之后，文件 `/tmp/bootcd.iso` 可以通过图形 CD 写入应用程序（如 KonCD 或 XCDrost）或直接在命令提示符下写入 CD：

```
cdrecord -v speed=2 dev=0,0,0 /tmp/bootcd.iso -eject
```

参数 `dev=0,0,0` 必须根据刻录机的 SCSI ID 进行更改。可以使用 `cdrecord-scanbus` 命令来确定。此外，请参考 `cdrecord` 的 man page (`man cdrecord`)。

- 测试引导 CD。重启计算机以验证 Linux 系统是否从 CD 正确启动。

# 启动与引导管理器

## X Window System

X Window System 是 UNIX 事实上的 GUI 标准。然而，X Window System 远不止于此——X11 是一个基于网络的系统。在机器 `earth` 上运行的应用程序可以在机器 `sun` 上显示其结果，前提是两台机器通过网络连接。网络可以是局域网（LAN），也可以是通过互联网连接数千英外的计算机。

其他外，以下章节特别关注了程序 `xf86config`，它可以代替 `xf86config` 来配置显示器、键盘和鼠标。

| 特性 | 描述 |
| :--- | :--- |
| 历史背景 | 92 |
| XFree86 4.x 版本 | 92 |
| 使用 xf86config | 94 |
| 优化安装 | 103 |
| 历史背景 | 111 |

## XFree86 4.x 版本

新的 X server 不再是一个单体程序，而只是一个相对的脚手架，在以后需要时可以在其中添加必要的程序。例如，它不再像以前版本那样为不同的显卡提供许多不同的服务器，而只有一个名为 `XFree86` 的可执行文件，该文件可以在 `/usr/X11/bin` 中找到。这才是真正的 X server。而负责控制显卡的图形驱动程序是一个可加载模块。

错误日志记录也得到了改进。X 服务器会创建一个非常详细的日志文件，在 X 服务器启动后，你始终可以在 `/var/log/XFree86.0.log` 文件中找到它。该版本的另一个进阶功能是支持特殊的 Type 字体。其他功能还包括 3D 协议扩展 `glx`、屏幕伽马校正以及用于多线程配置的多显卡支持。关于此点的更多信息可以参见第 103 页的《优化 X 窗口系统的安装》。

## 使用 x86config 进行配置

在大多数情况下，对于 X 窗口系统的简单配置，SaX 优于 x86config。然而，如果 SaX 配置无法工作，请直接使用 x86config，它几乎总是能起作用的。

XFree86 4.x 包含一个类似的文本界面程序 `x86config`。在某些点上，它包含了经过某种修改的对话框。它会将配置文件写入 `/etc/X11/XFree86Config`。通常情况下，XFree86 4.x 不需要使用 `x86config`，因为“问题”显卡也可以通过 framebuffer 或 vga 模块进行配置。

确保你已准备好以下信息：

- 鼠标类型、鼠标连接端口以及波特率（波特率通常可选）
- 显卡规格
- 显示器数据（频率等）

如果已知这些设置，或者你手头有说明书，即可开始配置。只有 root 用户可以执行此操作。启动配置的命令为：

```
earth:/root # x86config
```

### 鼠标

从欢迎界面之后选择鼠标类型：

- 1. 微软兼容 (2键协议)
- 2. Mouse Systems (3键协议)
- 3. 总线鼠标 (Bus Mouse)
- 4. PS/2 鼠标
- 5. 罗技鼠标 (串口，旧型号，罗技协议)
- 6. 罗技 MouseMan (微软兼容)
- 7. MM 系列
- 8. MM HitTablet

输出 5: X 鼠标选择

在选择鼠标时，请记住许多新款罗技鼠标兼容微软系统或使用 MouseMan 协议。选择 Bus Mouse 指任何总线鼠标，包括罗技鼠标。

通过输入相应的数字进行选择。系统可能会询问是否激活 `ChordMiddle`。这对于某些罗技鼠标或滚球鼠标激活中键功能是必要的。

请用 `y` 或 `n` 回答以下问题：

你是否要启用 ChordMiddle?

如果你使用的是双键鼠标，请在下一个问题上回答 `y` 以模拟第三按键。

请用 `y` 或 `n` 回答以下问题：

你是否要启用 Emulate3Buttons?

通过同时按下两个鼠标键可以启用中键。

接下来，指定鼠标的接口：

现在给出鼠标连接的完整设备名称，例如

`/dev/tty00`。直接按回车键将使用默认的 `/dev/mouse`。

鼠标设备：

如果你在系统安装期间已为鼠标输入了端口，直接输入 `/dev/mouse` 即可。

### 键盘

接下来，确定是否将 Meta (ESC) 分配给左 (Alt) 键，以及将 ModeShift (AltGr) 分配给右 (Alt) 键。

请用 `y` 或 `n` 回答以下问题：

你是否要为这些 Alt 键启用这些绑定？

如果你回答 `y`，左 (Alt) 键可以作为 Emacs 的 meta 键，并且需要 ModeShift (AltGr) 的按键也可以输入。
