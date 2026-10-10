

输入 `y` 并按下回车键。此时你可能会看到以下内容（如果通过 telnet 会话运行该脚本）：

> 已设置 $DISPLAY，这可能表明你正在 X 会话中运行此安装。建议在进行安装时不要运行 X。
>
> 是否继续？(y/n) [n]

输入 `y` 并按下回车键。安装脚本随后将执行一些初步检查，然后询问是否允许覆盖现有的 X11 配置：

> 正在检查你运行的操作系统...
> uname 报告 'Linux' 版本 '2.2.12-20'，架构为 'i586'。
> 目标格式为 'ELF'。libc 版本为 '5.1'。
>
> 正在检查所需文件 ...
>
> 你似乎已安装 X。继续操作将覆盖现有安装。不过，在大多数配置文件被覆盖之前，你将有机会选择是否被提示确认。
> 是否继续？(y/n) [y]

请注意，默认答案被括号包裹（ `[]` ）。如果默认答案可以接受，你只需按下回车键即可。按下回车键继续。

> 正在移除一些不再需要的旧目录...
>     移除旧目录 /usr/X11R6/lib/X11/objc/compiled
>
> XFree86 现在将大多数可自定义的配置文件安装在 /etc/X11 下，而不是 /usr/X11R6/lib/X11 下，并在 /usr/X11R6/lib/X11 下创建指向 /etc/X11 的符号链接。你目前在 /usr/X11R6/lib/X11 的以下子目录中存在文件：
>
>     app-defaults  lnxproxy  proxy/mgr  restart  xserver
>
> 你是否希望将它们移动到 /etc/X11 并创建必要的链接？(y/n) [y]

此步骤将保存你的原始系统默认设置，因此你只需按下回车键即可。随后脚本将列出被移动的文件。然后你会被问及以下问题：

> 你是否希望覆盖 app-defaults 配置文件？(y/n) [n]

如果你不担心现有的默认文件（其中包含各种 X11 客户端的默认资源设置），请输入 `y` 并按下回车键。如果你希望保留该文件，请输入 `n` 并按下回车键。（提示：对于 xdm 和 xinit 文件，你可能应该回答 `n` 以保留现有的图形登录设置。）脚本将继续询问每个原始默认文件。翻页查看回答。随后脚本将开始解压缩 tarball 文件。如果你包含了一些可选文件（见表 6.2），系统会询问你是否想要安装它们。在此之后，脚本将完成。

# 配置 XFree86 4.0

安装完成后，你可以尝试使用带有 `-configure` 选项的新 XFree86 命令来为笔记本配置 X11：

```
# XFree86 -configure
```

该命令将尝试自动检测你笔记本的图形芯片组：

```
...
(II) NEMAGIC: Neomagic 芯片组驱动程序: neo2070, neo2090, neo2093, neo2097, neo2160, neo2200
...
你的 XF86Config 文件是 /root/XF86Config.new
```

要测试服务器，请运行 `XF86x86 -xf86config /root/XF86Config.new`

在此示例中，新的 X 服务器检测到了 NeoMagic 芯片组。如果测试命令行成功，你可以将名为 `XF86Config.new` 的文件复制并重命名为 `/etc/X11` 目录下的 `XF86Config`，然后重启 X。但是，如果你遇到问题，仍然需要配置 X11！幸运的是，XFree86 4.0 包含一个更新版的 `xf86config` 命令。在控制台的命令行中，输入 `xf86config` 并按下回车键：

```
# xf86config
```

首先，系统会要求你选择鼠标类型、设备、键盘类型以及键盘语言。（提示：如果在安装新的 XFree86 4.0 之前你成功配置过 X11，请保留一份原始 `XF86Config` 的副本以回答这些问题。）然后，系统会要求你输入监视器设置，并通过查看新的 XFree86 4.0 数据库（位于 `/usr/X11R6/lib/X11` 目录下的名为 `Cards` 的文件）来选择你的图形芯片组：

```
你想查看显卡数据库吗？
```

输入 `y` 并按下回车键以查看显卡数据库。当初始的编号显卡列表出现时，你可以按下回车键翻页，直到找到你笔记本的图形芯片：

- 360 Miro Crystal 20SD 带有 ICD2061A (BIOS 2.xx) S3 864
- 361 Miro Crystal 20SD 带有 ICS2494 (BIOS 1.xx) S3 864
- 362 Miro Crystal 20SV S3 964
- 363 Miro Crystal 22SD S3 Trio64
- 364 Miro Crystal 40SV S3 964
- 365 Miro Crystal 80SV S3 968
- 366 Miro Crystal 8S S3 801/805
- 367 Miro Crystal DMD S3 6326
- 368 MiroMedia 3D S3 VI/RGE
- 369 Miro MiROvideo 20TD ET4000/W32(1/lp)
- 370 Miro Video 20SV S3 968
- 371 NeoMagic (笔记本/小型计算机) MagicGraph 128 系列
- 372 Number Nine FX Motion 331 S3 Trio64V+
- 373 Number Nine FX Motion 332 S3 964
- 374 Number Nine FX Motion 531 S3 868
- 375 Number Nine FX Motion 771 S3 968
- 376 Number Nine FX Vision 330 S3 Trio64
- 377 Number Nine GXE Level 10/11/12 S3 928

输入数字以选择对应的显卡定义。

按回车键翻到下一页，按 q 继续配置。

输入你的芯片组对应的数字（例如，按照我们的示例输入 `371`），并按下回车键：

```
371

你选择的显卡定义：

标识符: NeoMagic (笔记本/小型计算机)
芯片组: MagicGraph 128 系列
驱动程序: vga

此显卡基本上是不受支持的。它可能仅作为通用的
VGA 兼容显卡工作。如果你的 XFree86 版本比该
显卡定义所基于的版本更新，那么该显卡现在可能
已得到支持。

按回车键继续，或按 ctrl-c 中止。
```

在此示例中，数据库中包含 NeoMagic 显卡不受支持的信息，脚本自动为该显卡选择了此 `vga` X 服务器模块。使用此示例是因为存在一个修复方法。继续运行脚本以回答关于视频内存、默认色彩深度（如单色、256 色、数千色或数百万色）的问题。然后你将看到以下内容：

```
我现在将编写 XF86Config 文件。请确保不要意外覆盖之前配置好的文件。

是否将其写入 /etc/X11/XF86Config？
```

输入 `y` 并按下回车键。此时，大多数笔记本用户可以尝试使用 `startx` 命令启动 X 会话，如下所示：

```
# startx
```

但是，NeoMagic 芯片组用户应该编辑生成的 `/etc/X11/XF86Config` 文件，然后查找第一个 `Driver` 条目：

```
Driver    "vga"
```

这应该更改为

```
Driver    "neomagic"
```

接下来，查找 `Device` 部分中的 `Driver` 条目：

```
Driver    "vga"
```

此条目应更改为

```
Driver    "neomagic"
```

保存更改并退出编辑器。然后你可以尝试启动你的 X11 会话。此修复指定 X 服务器模块应加载 `neomagic.o` 服务器模块，而不是指定的 `vga.o` 模块，这应该适用于许多使用 NeoMagic 图形芯片组的不同类型笔记本。新的显卡服务器模块集合安装在 `/usr/X11R6/lib/modules/drivers` 目录下：

| aga_drv.o | fbdev_drv.o | neomagic_drv.o | tga_drv.o |
| :--- | :--- | :--- | :--- |
| ati_drv.o | glide_drv.o | nv_drv.o | trident_drv.o |
| chips_drv.o | glint_drv.o | r128_drv.o | tsecg_drv.o |
| cirrus_alpine.o | i740_drv.o | rendition_drv.o | vga_drv.o |
| cirrus_drv.o | i810_drv.o | svga_drv.o | |
| cirrus_laguna.o | linix | sis_drv.o | |
| cyrix_drv.o | mga_drv.o | tdfx_drv.o | |

安装 XFree86 4.0 时，你将在系统上发现新安装的手册页。要阅读关于 Trident 芯片组的信息，请使用 `man` 命令，如下所示：

```
$ man trident
```

请注意，初始 XFree86 4.0 发行版中的文档可能较为简略。这种情况将在后续版本中得到改善。

### 研究你的芯片组

如果你在使用新版或旧版 XFree86 配置 X11 时遇到问题，你可以做的第一件事是阅读适合你笔记本芯片组的相应 `README` 文件。请查看 `/usr/X11R6/lib/X11/doc` 目录。你将找到以下内容：

```
# ls README.*
```

- README
- README.3DLabs
- README.Config
- README.DBcTga
- README.DGA
- README.I128
- README.LinkRit
- README.Linux
- README.MGA
- README.Mach32
- README.Mach64
- README.NVIDIA
- README.Oak
- README.P5000
- README.S3
- README.S3V
- README.S1S
- README.Video7
- README.W32
- README.WestDg
- README.apx
- README.P5000
- README.ark
- README.ati
- README.chips
- README.cirrus
- README.rendition
- README.clikprog
- README.trident
- README.cyrix
- README.epson
- README.tseng
- README.1740
- README.mouse
- README.neo

例如，如果你的笔记本使用 NeoMagic 图形芯片组的变体，`README.neo` 文件包含关于你可以在系统的 `XF86Config` 文件中使用的选项的信息，这些选项有助于你：

- 解决显示闪烁问题
- 了解色彩深度支持
- 配置笔记本以使用外部显示器
- 查找使用类似芯片组的笔记本
- 如何具体设置视频内存参数
- 使用各种驱动程序选项来拉伸或缩小你的显示

### X11 字体配置

X11 字体存储在各种位于 `/usr/X11R6/lib/X11/fonts` 目录下的目录中。每个字体目录包含各种字体文件，以及一个名为 `fonts.dir` 的字体目录文件。该文件由 `mkfontdir` X11 客户端创建，并且

