
“More kernel arguments” 字段中应包含条目 `adb_buttons=103,111`，以便在引导 Linux 后的 X11 会话期间将 F11 和 F12 映射到鼠标中键和右击。

引导完成后，如果你没有直接引导到 X11，可以使用 `Ctrl+Command+2` 到 `Ctrl+Command+6` 在仅文本模式的 Linux 控制台之间切换。不幸的是，你无法使用基于 Intel 的 X11 `Ctrl+Alt+F2` 到 `Ctrl+Alt+F6` 以及 `Alt+F7` 键盘命令从 X 会话跳转到仅文本控制台再跳回。

### PCMCIA 和 Card Services

David Hinds 的 Card Services 是移动 Linux 用户除了 Linux 内核和基本安装之外最重要的软件包。几乎所有基于 Intel 的笔记本都配备了一个或两个 PCMCIA 卡槽。（注意 Apple iBook 不支持 PCMCIA。）

对 PCMCIA 卡（现在更常被称为 PC 卡）的支持由 `cardmgr` 守护进程提供。该守护进程通过 `/etc/rc.d/init.d/pcmcia` 脚本启动。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_173_0.png)

图 6.1 `ntsysv` 命令用于设置特定服务，以便在 Linux 在你的笔记本上引导时启动。

如果你已配置 Linux 在引导时使用 `cardmgrd`。确保 Card Services 可用的一种方法是使用 Red Hat 的 `ntsysv` 命令。在控制台或 X11 终端窗口命令行中输入 `ntsysv` 并按 Enter。你将看到图 6.1 中显示的对话框。

使用上下箭头键滚动服务列表以选择 `pcmcia`，然后按空格键以确保出现星号 (*)。按 Tab 键突出显示 `OK` 按钮，然后按 Enter。这将确保在 Linux 重启时存在 PCMCIA 支持。你也可以使用 `pcmcia` 脚本立即启动该服务，如下所示：

```
$ /etc/rc.d/init.d/pcmcia start
```

如果你正考虑为 Linux 购买一张 PC 卡，请帮自己一个忙，务必阅读 `SUPPORTED.CARDS` 文件中最新的受支持卡列表。如果你在你的笔记本上安装了 Linux 内核源代码，你可以在 `/usr/src/linux/pcmcia*` 目录下找到一份副本。你还可以通过浏览到以下网址阅读最新版本：

```
http://pcmcia.sourceforge.org/
```

#### 构建和安装 Card Services

如果你有一张在 Linux 上不起作用的卡，请振作起来；对新卡的支持通常会在每个新的 Card Services 软件版本中添加。如果你的 Linux 发行版包含的 Card Services 版本无法与你的 PC 卡配合工作，你可以尝试下载最新的驱动程序。要安装新驱动程序，请在 `/usr/src/linux` 目录中解压源代码。注意你需要已安装 Linux 内核源代码。

导航到新的 `pcmcia` 目录，然后使用 `Configure` 脚本设置并创建一个 `makefile`，如下所示：

```
# ./Configure
```

按 Enter 后，你可能會看到以下内容：

------ Linux PCMCIA 配置脚本 ------

每个问题的默认回答对大多数用户都是正确的。

请参考 `PCMCIA-HOWTO` 获取有关每个选项的更多信息。

Linux 源目录 [/home2/rpn/BUILD/linux]: `/usr/src/linux`

输入 `/usr/src/linux` 以指定 Linux 内核源目录（这在 Red Hat 和 Mandrake Linux 上有效），然后按 Enter。你将看到以下内容：

内核源树版本为 2.2.14-15mdk。

当前内核构建日期为 2000 年 1 月 4 日 星期二 22:24:20。

备用目标安装目录 [/var/tmp/kernel-2.2.14-15mdk-root]:

Configure 脚本将识别当前的 Linux 内核并提供备用安装目录。如果你不担心覆盖原始模块，可以使用默认设置并按 Enter。然后你会被询问：

模块安装目录 [/lib/modules/2.2.14-15mdk]:

如果你希望新的 Card Services PCMCIA 内核模块在你的系统中工作，这一步至关重要。如果你接受默认设置，新模块将覆盖现有模块。如果你只是想查看模块是否构建成功，请指定备用目录并按 Enter。

构建 'trusting' 版本的卡工具 (y/n) [y]:

此选项用于创建可在笔记本上的任何人（而不仅是 root 操作员）使用的模块。输入 y 或 n，然后按 Enter。

包含 32 位 (CardBus) 卡支持 (y/n) [n]:

如果你使用较新的 CardBus PC 卡，请按 Enter。注意，支持的 CardBus 卡比旧的 16 位 PC 卡少。

包含 PnP BIOS 资源检查 (y/n) [n]:

除非你需要笔记本的 BIOS 帮助配置你的卡，否则使用默认选项 n 并按 Enter。

*PCMCIA* *drivers* 需要编译以匹配它们将使用的内核，否则部分或所有模块可能无法加载。

如果不确定该怎么做，请咨询 *PCMCIA-HOWTO*。

你希望如何设置内核特定选项？

1. 从当前运行的内核读取

2. 从 Linux 源树读取

输入选项 (1-2) [2]:

虽然默认选项是使用安装的 Linux 源代码，但此代码（特别是带有 *Mandrake Linux* 时）可能与你笔记本上运行的内核不匹配！更安全的方法是选择 1，使用当前运行内核的驱动程序选项。按 *Enter* 后，你将看到以下内容：

```
Kernel configuration options:

	Static in-kernel PCMCIA support is disabled.
	Symmetric multiprocessing support is disabled.
	PCI BIOS support is enabled.
	Advanced Power Management (APM) support is enabled.
	SCSI support is enabled.
	Networking support is enabled.
	Radio network interface support is enabled.
	Token Ring device support is enabled.
	Pasta switching is disabled.
	Module version checking is enabled.
	/proc filesystem support is enabled.
	Maximum physical memory: 1GB
```

System V init 脚本布局 (y/n) [y]:

你将获得关于你的 Linux 内核的简短报告。（你可能会惊讶于你拥有的已安装支持种类！）然后你会被询问你的系统是否使用 *System V* init 脚本布局。如果你使用的是 *Red Hat* 或 *Mandrake Linux*，请按 *Enter*（或 *y*）。

RC 脚本的顶层目录 [ /etc/rc.d ]:

*Red Hat 和 Mandrake Linux 都在 /etc/rc.d 目录下使用 init 脚本，因此你只需按 Enter。*

```
X Windows include files found.
/usr/X11R6/lib/libforms.so and /usr/X11R6/include/forms.h found.
Configuration successful.
```

Configure 脚本还将搜索 XForms 库和头文件。如果找到，你还可以构建、安装和使用 X11 的 `cardinfo` 客户端！现在你可以像这样构建 Card Services：

```
# make
```

要安装新的 PCMCIA 模块（通常位于 `/lib/modules/2.X.XX` 目录下的 `misc` 目录中，其中 X.XX 是你的内核版本），请使用 `make` 命令如下：

```
# make install
```

安装后，你可以使用以下命令启动 Card Services：

```
# /etc/rc.d/init.d/pcmcia start
```

或此命令：

```
# /etc/rc.d/init.d/pcmcia restart
```

`cardinfo` 客户端可以从 X11 终端窗口的命令行像这样启动：

```
# cardinfo &
```

按 Enter 后，你将看到图 6.2 中显示的窗口。

此客户端列出当前插入的任何卡，并提供有关状态、设备、IRQ 和正在使用的 I/O 端口的详细信息。通过点击插槽按钮（如图 6.2 所示），你可以重置、挂起、恢复、弹出或插入 PC 卡。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_176_0.png)
