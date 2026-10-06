
$ su -c /sbin/shutdown -h now

```

您也可以使用：

```

$ su -c /sbin/shutdown -h 0

```

您也可以使用 `shutdown` 命令立即重启计算机，如下：

```bash

$ su -c /sbin/shutdown -r now

```

或者，您可以使用：

```bash

$ su -c /sbin/shutdown -r 0

```

| 相关 Fedora 和 Linux 命令 |
您在安装 Fedora 时可能会使用以下命令：
- dd—转换并复制数据
- fdisk—Linux 磁盘分区工具
- grub—用于 Linux 和其他系统的 GNU 引导加载程序
- LOADLIN—用于 DOS 的 Linux 引导加载程序
- mkbootdisk—Red Hat 的 Linux 磁盘创建工具
- RAWWRITE—用于 DOS 的磁盘镜像工具 |

## 参考资料

- http://fedora.redhat.com—查找有关 Fedora 安装、配置和使用的新闻、信息和文档时，从这里开始。

- http://www.powerquest.com/partitionmagic/—Powerquest 的 PartitionMagic 实用包含 BootMagic，它可以用于支持 Linux 的启动，遗憾的是，也支持其他能力较弱的操作系统，例如 Windows XP。

- http://www.v-v.com/product/sc7_ind.html—V Communications, Inc. 的 System Commander 是一个 4.2MB 的商业化下载程序，可用于支持任何可以在当今 PC 上运行的操作系统的启动。它包含了一个智能分区工具 Partition Commander。

- http://www.nwc.com/columnists/10/toIron.html—如何使用 Intel 的预执行执行环境 (PXE) 协议远程启动工作站。

- http://www.gnu.org/software/grub/—GRUB 引导加载程序的首页。

- http://www.elserv.ffm.fgan/lermen/HOME.html—LOADLIN Linux 加载器主页。

- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/BootPrompt-HOWTO.html—获取 BootPrompt-HOWTO 的链接，这是一份关于使用启动提示符传递内核参数的指南。

- http://www.tldp.org/HOWTO/Installation-HOWTO/index.html—获取 Linux Installation-HOWTO 的链接，这是一由 Eric S. Raymond 编写的 Linux 安装指南。

# 第 4 章

## 本章内容

## 安装后问题

- 排除安装后配置问题的故障
- 你的硬件与 kudzu（自动检测）
- 指针和键盘配置
- 配置显示图形
- 配置音频设备
- 检测和配置调制调器
- 在 Fedora 中配置电源管理
- 重置日期和时间
- 管理 PCMCIA
- 配置和使用 CD、DVD 和 CD-RW 驱动器
- 参考资料

如第 3 章“安装 Fedora”所示，在大多数情况下，安装 Fedora 是一项简单的任务。安装过程包括硬件探测，安装程序会调查你的系统硬件并据此配置系统设置。此过程确保了系统启动时，几乎所有的硬件都被识别并准备好运行。

然而，如果你是系统管理员（即使你在独立工作站上使用 Linux 也是），你可以预期对系统进行安装后配置。本章从有关故障排除的一些通用建议开始，然后对 Fedora 如何设置以跟踪你的硬件提供见解。随后你将看到如何启动并使用命令行来显示和诊断 Linux 内核关于几个常用 PC 硬件组件的输出。你还将看到几个图形配置客户端的操作。

## 排除安装后配置问题的故障

随着 Linux 的不断开发，它变得越来越具有容错性，这意味着如果在启动过程中遇到错误，错误不会导致内核或启动的完全失败。通常，你的计算机可能看起来运行良好，即使某些设备或进程没有正常工作。此类问题的来源可能包括未加载的模块、未启动的服务，或者以次优水平使用的设备（例如硬盘传输速度）。

你可以在 `dmesg` 输出或 `/var/log/messages` 文件中找到许多问题的线索，后者是一个简单的文本文件，包含了不断更新的内核和系统信息，你可以用任何编辑器查看它。在安装或配置新硬件后，请花时间查看此文件或 `dmesg` 输出；你会发现它们显示了系统启动和启动服务的进度。

这些信息是由内核、由 `/etc/rc.d/rc.sysinit` 运行的其他软件以及 Fedora 的运行级别脚本生成的。你可能一眼看到看起来像错误，但某些并不是真正的问题（例如，某项硬件被配置了但你的系统中并不存在）。

在排除错误信息的故障时，记住“Google 是你的朋友”。只需复制错误信息的部分或全部，并将信息粘贴到 http://www.google.com/linux/ 和 http://marc.theaimimsgroup.com/ 的搜索框中。你可能会找到帮助你解决问题的页面链接。你可能不是第一个遇到该问题的人。阅读 `modprobe.conf` 的手册页并使用 `/usr/src/linux-2.6/Documentation/devices.txt`（以及其他文件）将对帮助你排除问题大有帮助。

记住一次只解决一个问题，并在修改系统文件之前务必为其创建一个备份副本。不要使用带有 `.bak` 扩展名的常用文件，因为该扩展有时会被覆盖。这里有一个复制文件的好方法：

```
# cp filename filename.original
```

从备份恢复时，不要重命名文件，只需复制它，如下所示：

```
# cp filename.original filename
```

（当这些技巧为你节省了数小时的沮丧时，请通过购买书籍作为礼物送给朋友来感谢我们。）

## 你的硬件与 kudzu

当你添加或更换硬件时，例如，你需要配置系统以能够正常工作。如果你启用了 kudzu 服务，Fedora 将开机时自动检测硬件；如果你没有使用 kudzu，可能需要手动进行配置。

> 注意
> kudzu 服务在 `/etc/sysconfig` 目录下维护着系统硬件数据库。可以通过 `/etc/rc.d/init` 目录下的脚本从命令行启动、停止或重启 kudzu（如其他系统服务）。通过编辑 kudzu 脚本中的 `KUDZU_ARGS` 条目，可以启用 kudzu 的各种功能，例如超时（请查看 kudzu 手册页）。你还可以使用命令行或图形化的 system-config 客户端来控制 kudzu。参阅第 7 章“管理服务”获取更多关于这些命令的信息。

你可以在不重启的情况下执行许多安装后任务。在本章中，你将学习如何配置通用总线 (USB) 和 FireWire (IEEE-1394) 设备，以及键盘、调制调器和笔记本 PCMCIA。通过适当规划，你还可以创建一个允许热插存储和其他组件的配置，无需重启。

关于系统已安装硬件的信息位于 Fedora 目录下的许多文件中。除了 `/dev` 目录下为了方便实用程序的一个符号链接外，几乎所有的硬件设置都在 `/etc` 目录下的文本文件中。这些文件的内容被各种软件服务用于管理你的系统硬件、保存更改、确保重启后保存设置并在启动时正确配置你的系统。若干文件在 Linux 时会被 `/etc/sysconfig` 使用。例如，这些包括

- `/etc/sysconfig/hwconf`—列出完全配置硬件（由 kudzu 使用）
- `/etc/sysconfig/apmd`—系统电源管理设置（由 apmd 守护进程使用）
- `/etc/sysconfig/clock`—包含时区、时钟和硬件钟设置（由 clock 命令使用）
- `/etc/sysconfig/harddisks`—硬盘调优参数（使用 hdparam 命令的选项）
- `/etc/sysconfig/arda`—提供有关红外数据关联 (IrDA) 硬件的配置数据
- `/etc/sysconfig/keyboard`—列出当前的键盘映射（并提供语言设置）
- `/etc/sysconfig/mouse`—详细说明系统指针设备（例如是否使用 PS2 或 USB 鼠标）
- `/etc/modprobe.conf`—定义设备名称、要加载的内核硬件模块以及任何可选参数（有关 Linux 内内核模块的更多信息请参见第 24 章“内核与模块管理”）
- `/etc/pcmcia`—包含个人电脑内存卡国际协会 (PCMIA) 硬件数据库和设备设置的目录（参见本章后面的“管理 PCMCIA”部分）

关于 `/etc/sysconfig` 中文件的更多信息可以在 `/usr/share/doc/initscripts` 目录下的 `sysconfig.txt` 文件中找到。

# 第 4 章 安装后问题

> 注意
不要编辑 kudzu 的已安装硬件文本文件数据库；这些文件由 kudzu 动态更新。然而，如果你在使用设备时遇到问题，可以在排除故障时检查这些文件中的信息，以查看设备是否被正确识别以及其定义是否与实际硬件匹配。

## 指针和键盘配置

Fedora 包含了图形化工具，可以快速、方便地更改鼠标和键盘配置设置。你还可以使用这些工具为系统添加对新键盘或鼠标的支持。这些工具包括

- `mouseconfig`—一个用于纯文本控制台的基于对话框的鼠标配置工具
- `system-config-mouse`—用于红帽桌面面的图形化鼠标配置工具
- `system-config-keyboard`—用于 Fedora 桌面或使用文本控制台配置键盘的图形键盘配置工具

接下来的章节将解释如何使用这些工具在 Fedora 中配置键盘和指针设备。

## 使用 Linux 配置键盘

> 注意
Linux 支持许多不同类型的键盘。直到几年前，大多数键盘仍使用 PS/2 协议（最初由 IBM 开发），并通过 6 针微连接器连接到 PC。今天，几乎所有计算机都使用 USB 接口作为用户输入设备。虽然现在的许多 PC（以及笔记本电脑）继续提供 PS/2 端口，但大多数制造商现在正在引入不再直接支持 PS/2 的“无遗留”计算机。

你可以在 Fedora 中进行许多键盘配置选择。你可以选择一种键盘语言，该语言会提供你在控制台或图形会话中输入时所需的键盘字母、变音符号和布局。其他选项包括更改键盘的翻译表以重新映射键盘上的按键顺序、交换特定键（如 Caps Lock 和 Ctrl），或更改按键到屏幕上出现字符之间的延迟。（此配置可以帮助你将字符输入与你的打字速度同步。）

你可以通过基于文本（控制台）的键盘命令或图形用户界面进行键盘配置更改。

如果你不使用 X，请使用红帽的 `system-config-keyboard` 命令更改你的键盘类型和语言。此命令可以在没有活动 X 会话的情况下（或如果你正在使用 X，则在终端窗口内部）如下所示使用：

```bash
# system-config-keyboard
```

按下回车键后，你将看到“配置键盘”对话框，如图 4.1 所示。

![](img/7e0718570ccf16ae88870f5f49b7faed_122_0.png)

**图 4.1** `system-config-keyboard` 命令可为 Fedora 选择键盘映射（语言）。

此对话框允许你选择新的键盘类型。

滚动列表以突出显示所需的键盘类型，然后使用 Tab 键突出 OK 按钮并按回车键。列表代表 `/lib/kbd/maps/i386` 目录下的项目，用于将你的键盘布局和按键与某种语言关联。键盘配置存储在 `/etc/config/keyboard` 文件中，内容可能如下：

```
KEYBOARDTYPE="pc"
KEYTABLE="us"
```

如果你在 X 会话下使用 Fedora 桌面，可以使用图形界面选择键盘语言。要打开键盘配置对话框，请点击桌面面板上的“设置-键盘”菜单项，或在终端窗口的命令行中使用 `system-config-keyboard` 客户端，如下：

```bash
$ system-config-keyboard
```

按下回车键后，系统会提示输入 root 密码。输入密码并点击 OK。你将看到如图 4.2 所示的键盘对话框。该对话框与 `system-config-keyboard` 显示的类似。

![](img/7e0718570ccf16ae88870f5f49b7faed_123_0.png) 图 4.2 `system-config-keyboard` 客户端在 X 会话期间用于选择你在桌面会话中使用的语言。

滚动语言列表，突出显示一种语言，然后点击 OK 保存你的更改。

表 4.1 列出了你可以用于操作或获取键盘信息的文本和图形命令。

### 表 4.1 Linux 和 X 键盘相关命令

| 命令 | 说明 |
|---|---|
| dumpkeys | 显示翻译表 |
| kbd_mode | 修改当前键盘模式 |
| kbdrate | 更改按键延迟、重复 |
| loadkeys | 加载新键盘表 |
| showkey | 打印字符、代码和其他按键信息 |
| setled | 显示、更改键盘发光管 (LED) 设置 |
| xkbcomp | 显示、设置 X 字符翻译 |
| xkbprint | 显示或保存 X 映射 |
| xset | 修改 X 键盘设置 |
| xmodmap | 更改 X 映射 |

X11 键盘和其他客户端可用于向运行的 X 服务器输入键盘描述、字符翻译以及更改键盘（指针）偏好。X11 设置通常包含系统的 `xorg.conf` 文件中（更多信息请参见第 6 章“X Window 系统”）。

作为一个简单的示例，下面的短脚本（有关如何使用 shell 脚本请参见第 22 章“Shell 脚本”）可以在控制台期间每秒闪烁一次键盘 LED（按 Ctrl+C 停止）：

```bash
#!/bin/sh
while :
  do
    setleds -L +caps; sleep 1 ; setleds -L -caps; sleep 1;
done
```

也许更有用的示例是交换键盘上的 Caps Lock 和 Ctrl 键。某些用户可能会发现交换后的键盘会话更舒服。交换键的方法有很多。对于控制台会话，使用 `loadkeys` 命令加载包含键值的文件：

```
keymaps 0-15
keycode 58 = Control
keycode 29 = Caps_Lock
```

你可以立即使用 `loadkeys` 加载文件（可能交换的键）：

```bash
# loadkeys <swapskeys>
```

相同的交换也可用于你的红帽桌面，只需编辑 `/etc/X11/xorg.conf` 文件的 `InputDevice` 部分并添加：

```
Option "XkbOptions" "swapscaps"
```

另一种获得相同结果的方法是在家目录下创建一个名为 `.xmodmap` 的文件，包含：

```
remove Lock = Caps_Lock
remove Control = Control_L
keysym Control_L = Caps_Lock
keysym Caps_Lock = Control_L
add Lock = Caps_Lock
add Control = Control_L
```

或者你可以将设置保存在文件中（例如 `mykeyswap`），并使用 `xmodmap` 客户端直接加载新键：

```bash
$ xmodmap mykeyswap
```

注意，只有当你使用 `xterm` 或 `rxvt` 终端时这才会有效。关于红帽桌面的更多信息请参见第 6 章。

![](img/7e0718570ccf16ae88870f5f49b7faed_124_0.png)

## 在 Fedora 中配置指针设备

> 提示
如果在从图形桌面会话（即使用 X Window 系统）期间命令行启动 `system-config-keyboard` 命令将呈现图形界面。然而，你可以在命令行中包含 `--text` 选项来强制 `system-config-keyboard` 使用文本界面：

```bash
# system-config-keyboard --text
```
