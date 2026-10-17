
`start` 脚本运行一个名为 `xinit` 的程序，该程序启动 X 服务器 `/usr/X11R6/bin/X`（你可能对大多数其他 UNIX 系统上的 `/usr/bin/X` 更熟悉），并在你的主目录下查找名为 `.xinitrc` 的文件（注意开头的点）。`.xinitrc` 文件是一个启动你想要的所有 X 应用程序的 shell 脚本。例如，我们的 `.xinitrc` 文件启动了多个 `xterm` 程序的实例（它提供了一个 shell 窗口）以及一个名为 `clock` 的圆形时钟，如图 3.4 所示。

![](img/fbc693f336ddb03484459053e27e3594_148_0.png)

```
PID TID STAT COMMAND
120 vdi S 0:00 -HOME=/home/yonson PATH=/usr/lib/bin:HOME=/home/yonson;PATH=/usr
121 vdi S 0:00 /usr/lib/bin/start +HOME=/home/yonson;PATH=/usr
122 vdi S 0:00 -n /HOME=/home/yonson/.xinitrc -DISPLAY=:0
123 vdi S 0:00
124 vdi S 0:00 -n
125 ppi S 0:01 -csh +HOSTNAME=yonson yonson LOGAME=yonson
126 ppi S 0:00 -csh +HOSTNAME=yonson yonson LOGAME=yonson MINCODE
127 ppi S 0:00 -csh +HOSTNAME=yonson yonson LOGAME=yonson-root
1 ps -ef +HOSTNAME=yonson yonson LOGAME=yonson-root
yonson:~/books/linux>
```

图 3.4 从 `.xinitrc` 文件启动的典型 X 环境。

然而，在启动这些任何程序之前，必须启动 X 服务器，这项任务也由 `xinit` 处理。

X 服务器会寻找 XFree86 配置文件——这是你系统上 X 最关键的文件。该文件通常命名为 `XF86Config`，存储在 `/usr/X11r/lib/X11`（符号链接到 `/var/X11r/lib`），是一个特殊格式的文件，用于告诉 XFree86 关于你系统硬件的信息。

在系统上安装 XFree86 最困难的部分是完善这个文件。虽然有一些工具可以帮助，但这个过程仍然危险且充满错误。

`XF86Config` 文件包含六个部分，每个部分都向 X 服务器描述系统的部分内容。我们在表 3.2 中列出了这些部分。

### 表 3.2 XF86Config 文件中的部分

| 部分 | 用途 |
| --- | --- |
| Files | 告诉字体和 RGB 文件的位置 |
| ServerFlags | 特殊 X 服务器标志，例如 `DontZap`，它会关闭终止 X 服务器的 `Ctrl-Alt-Backspace` 序列 |
| Keyboard | 你拥有的是种种键盘 |
| Pointer | 关于你鼠标的信息 |
| Monitor | 关于你显示器的极其详尽的细节 |
| Device | 显卡 |
| Screen | 显卡和显示器的组合 |

### 安装 XFree86

要安装并正确设置 XFree86（即使在理想情况下，这也是一项艰巨的任务），你需要执行以下步骤：

- 确定你的系统配置。
- 为你的显卡设置适当的 X 服务器。
- 填写 `XF86Config` 文件。
- 测试 X 是否可以运行。
- 调整你的 `XF86Config` 文件。

我们将在本章剩余部分介绍这些步骤。

几乎所有的 XFree86（包括附带 Slackware Linux 版本）都会安装到 `/usr/X11R6` 目录。注意，许多其他目录如 `/usr/bin/X11` 和 `/usr/lib/X11` 都是 `/usr/X11R6` 的符号链接。如果你从附带的光盘安装了 Linux 和 XFree86，所有文件都在正确的位置。

如果你从网上获取 XFree86 更新，你可能需要解包文件。检查与 XFree86 文件在同一目录下的 `README` 文件。大多数文件都是压缩的 tar 包。例如，如果你看到类似 `X312bin.tar.gz` 的文件，你应该知道它是用 `gzip` (`.gz`) 压缩的 tar 包 (`.tar`)。要提取此文件，使用以下命令：

```bash
mv X312bin.tar.gz /usr/X11R6
cd /usr/X11R6
gzip X312bin.gz
tar xv X312bin.tar
```

前两个命令将 XFree86 文件（以及你的工作目录）移动到 `/usr/X11R6`，这是 Linux 预期所在的地方。特别是如果你从网上获取 XFree86，必须以 root 用户身份解压 XFree86 归档。如果你从附带的光盘加载 XFree86 并使用，就不会有任何问题。

### 设置 XFree86

由于 PC 硬件的多样性，且操作错误可能会损坏你的硬件，这一事实让我们感到很困惑，但设置 X 可能是让 Linux 运行最困难的事情。跟踪关于你显示器和显卡的每份文档。你需要了解关于显示器的某些数值。即使失败了且找不到关于显卡的任何信息，如果你的显卡支持标准 VGA，你应该可以使用 XFree86 附带的示例 `XF86Config` 文件。我们在表 3.3 和 3.4 中列出了 XFree86 支持的显卡。

### 表 3.3 XFree86 支持的加速卡和芯片组

| 类型 | 芯片和显卡 |
| --- | --- |
| 8514/A | 8514/A 克隆版 |
| ATI | Mach32, Mach64 |
| Cirrus | CLGD5420, CLGD5422, CLGD5424, CLGD5426, CLGD5428, CLGD5429, CLGD5430, CLGD5434 |
| IBM | XGA-2 |
| IIT | AGX-014, AGX-015, AGX-018 |
| Oak Tech. | OTI087 |
| S3 | 86C911, 86C924, 86C801, 86C805, 86C801, 86C928, 86C864, 86C944, 86C732, 86C764, 86C768, 86C968 |
| Tsang | ET4000/W32, ET4000/W32 |
| Vertex | P9000 |
| Western Digital | WD90C31, WD90C33 |

Cirrus、Oak 和 Western Digital 显在 Super VGA 服务器 `XFree86_SVGA` 中支持。其他类型有自己的服务器。Super VGA 服务器 `XFree86_SVGA` 支持一系列显卡和芯片组，列如表 3.4 所示。

### 表 3.4 XFree86_SVGA 服务器支持的 Super VGA 芯片组

| 厂商 | 芯片组 |
| --- | --- |
| ARK Logic | ARK1000PV, ARK2000PV |
| ATI | 18800, 18800-1, 28800-2, 28800-4, 28800-5, 28800-6, 68800-3, 68800-6, 68800AX, 68801LX, 88800CX, 8800 |
| Advance Logic & Technology | ALG2101, ALG2228, ALG2301, ALG2302, ALG2308, ALG265520, 65530, 65540, 65545 |
| Cirrus Logic | CLGD5420, CLGD5422, CLGD5424, CLGD5426, CLGD5428, CLGD5429, CLGD5430, CLGD5434, CLGD6205, CLGD6215, CLGD6225, CLGD6410, CLGD6412, CLGD6420, CLGD6440 |
| Compaq | AVGA |
| Genoa | GVVA |
| MX | MX68000, MX68010 |
| NCR | 77C22, 77C2E, 77C2E+ |
| Oak | OT1067, OT1077, OT1087 |
| RealTek | RTG3106 |
| Syng | ET3000, ET4000AX, ET4000/W32 |
| Western Digital/Paradise | PVGA, WD90C00, WD90C10, WD90C11, WD90C24, WD90C24A, WD90C31, WD90C33 |
| Trident | TVGA8800CS, TVGA8900B, TVGA8900C, TVGA8900CL, TVGA9000, TVGA9000B, TVGA9100B, TVGA9200CX, TVGA9320, TVGA9400CX, TVGA9420 |
