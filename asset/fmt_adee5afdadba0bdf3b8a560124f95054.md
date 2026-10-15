
opus: `mkdir /usr/x386`

opus: `cd /usr/x386`

opus#: `cp -r /cdrom/slack/x1 .`

```
这些命令还将从挂载在 `/cdrom` 的 CD-ROM 将所有文件复制到当前目录。
```

# 表 6.1 XFree86 主要分发文件

| 文件名 | 描述 |
| --- | --- |
| x3270.tgz | IBM 3270 终端仿真 |
| x_8514.tgz | IBM 8514 服务器 |
| x_mach32.tgz | 基于 Mach32 芯片的服务器 |
| x_mach8.tgz | 基于 Mach8 芯片的服务器 |
| x_mono.tgz | 单色显示器服务器 |
| x_s3.tgz | 基于 S3 芯片的服务器 |
| x_svga.tgz | 多数 SVGA 卡的服务器（良好的基础设置） |
| _vga16.tgz | EGA/VGA |
| xconfig.tgz | 示例配置 |
| xf_bin.tgz | 二进制文件 |
| xf_cfg.tgz | X 配置 |
| xf_doc.tgz | 文档 |
| xf_kit.tgz | 工具包 (1/2) |
| xf_kit2.tgz | 链接包 (2/2) |
| xf_lib.tgz | 动态库 |
| xf_pex.tgz | PEX |
| xffileman.tgz | 文件管理器 |
| xfm.tgz | Xfm 管理 |
| xfnt.tgz | 字体 |
| xf75.tgz | 75 点 |
| xgames.tgz | 游戏 |
| xgrabsc.tgz | Xgrab |
| include.tgz | 头文件 |
| xlock.tgz | 屏幕锁定 |
| xman1.tgz | 手册 (1/2) |
| xman3.tgz | 手册 (3/2) |
| xpaint.tgz | Xpaint |

# 安装 XFree86 系统

| 文件名 | 描述 |
|---|---|
| xpm.tgz | Xpm 库，共享和静态 |
| xspread.tgz | Xspread 程序 |
| xstatic.tgz | X 的静态库 |
| xvtg.tgz | XV 查看 |
| xxgdb.tgz | GNU 调试器的 X 前端 |

提取这些文件，请使用以下命令：

```
opus: `gzip -d filename.tgz`

opus: `tar -xvf filename`
```

注意：随本书附带的 CD-ROM 已经是尽可能新的。尽管如此，互联网上可能提供更新版本的 XFree86，因此必要的存档可能会节省一些麻烦。

- 参见“使用 FTP 进行远程文件传输”，第 xxx 页（第27章）

# 确保硬件支持 XFree86

确保你有运行 X 的适当硬件、足够的内存以及必要的磁盘空间。

你需要大约 21M 的磁盘空间来安装 XFree86 系统和提供的 X 应用程序。运行 X Windows 需要至少 16M 的虚拟内存。虚拟内存是系统物理内存与 Linux 分配的交换空间的组合。在 Linux 下运行 XFree86 需要至少 4M 的物理内存，对应 12M 的交换文件。物理内存越多，XFree86 系统的性能越好。

- 参见“创建分区”，第 60 和 97 页

接下来，你需要带有 XFree86 支持的视频驱动程序的显卡。根据 Matt Welsh 在 1995 年 3 月 15 日发布的 XFree86 HOWTO，表 6.2 和 6.3 列出的芯片组的显卡受 XFree86 支持。

# 表 6.2 XFree86 支持的非加速芯片组

| 制造商 | 芯片组 |
|---|---|
| ATI | 28800-4, 28800-5, 28800-6, 28800-a |
| Advance Logic | AL2101 |
| Cirrus Logic | CLGD6205, CLGD6215, CLGD6225, CLGD6235 |
| Compaq | AVGA |

# 表 6.2 续

| 制造商 | 芯片组 |
| --- | --- |
| Genoa | MX68000, MX680010 |
| MX | 77C22, 77C2E, 77C22E+ |
| NCR | OTI067, OTI067 |
| OAK | TVGA8800CS, TVGA8900B, TVGA8900C, TVGA8900CL, TVGA9000, TVGA9000, TVGA9100B, TVGA9200CX, TVGA9320, TVGA9400CX, TVGA9420 |
| Tseng | ET3000, ET4000AX, ET4000/W32 |
| Western Digital/ Paradise | PVGA1 |
| Western Digital | WD90C00, WD90C10, WD90C11, WD90C24, WD90C30 |

# 表 6.3 XFree86 支持的加速芯片组

| 制造商 | 芯片组 |
|---|---|
| Cirrus | GLD5420, GLD5420, GLD5422, GLD5424, GLD5426, GLD5428 |
| Western Digital | WD90C31 |
| ATI | Mach8, Mach32 |
| S3 | 86C911, 86C924, 86C801, 86C805, 86C8051, 86C928 |

# 使用 pkgtool 为 Slackware 安装 X Windows

要安装 X Windows，你需要以超级用户（即 root）身份登录。然后，你应该记录下想要安装的 X Windows 软件包的位置。这些文件位于附带的 Slackware CD-ROM 的 `/slackware` 目录下。要从随附 CD-ROM 访问 X Windows 软件包，请查看以下目录：`/cdrom/slackware/x1`、`/cdrom/slackware/x2` 等。请确保你记得这些文件的位置。

> 注意：由于 Linux 将 CD-ROM 挂载到目录中，因此文件是相对于该挂载点的路径。典型的 Linux 安装通常会将 CD-ROM 放置或挂载在根目录下名为 `cdrom` 的目录中。

- 参见“文件系统的挂载与卸载”，第 265 页

接下来，从命令行提示符输入 `pkgtool`。此命令会激活 Slackware 软件包工具程序，允许你删除旧软件包或安装新软件包。对于 X Windows，这些软件包是 Slackware 发行版包含的 `x` 和 `xap` 软件包。会出现一个包含以下选项的菜单：

| 菜单项 | 说明 |
|---|---|
| Current | 从当前目录安装软件包 |
| Other | 从其他目录安装软件包 |
| Floppy | 从软磁盘安装软件包 |
| Remove | 移除已安装的软件包 |
| View | 查看软件包包含的文件列表 |
| Exit | 退出软件包工具 |

按下 `<Shift-o>` 或使用方向键选择 `Other` 菜单行并按 `<Return>`。`pkgtool` 会询问源目录。输入你之前为第一个软件包目录输入的目录，通常是 `x1`。在这里，你应该输入 `/cdrom/slack/x1`。

在提供初始目录后，`pkgtool` 首先为你的显卡寻找 X 服务器。你只能安装一个服务器，因此在切换屏幕时，请等待到达所需的 X 服务器之前再选择 `Yes`。

- 参见“使用 pkgtool”，第 253 页

请记住，你必须在安装 Linux 之后安装 XFree86，你应该仔细检查要安装软件包的完整细节。如果你有完整安装所需的 21M 空间，请继续继续安装每个软件包，但 X 服务器除外；仅为你的芯片组安装一个 X 服务器。

# 配置 XFree86

安装 XFree86 之后，你必须为你的系统对其进行配置。XFree86 期望在以下目录之一找到名为 `XFree86Config` 的文件：

- `/etc/XFree86Config`
- `/usr/X11R6/lib/X11/XFree86Config`
- `/usr/X11R6/lib/X11/XFree86Config`

> 注意：在大多数 Linux 发行版（包括 Red Hat、Slackware 和 Caldera）中，配置 XFree86 的方法是相同的。

你可以在 `/etc/X11/lib` 目录下找到配置文件信息。在配置系统之前，你应该检查标记为 `README.Config` 和 `README.Linux` 的文件。如果你有在“确保 XFree86 的硬件支持”部分列出的标准设备，你应该检查示例 `Xconfig` 文件。这些文件存储在 `/lib/X11/Sample-Xconfig-files`。检查 `Xconfig.Index` 查看你的显卡是否在列表中。你可以通过以下命令执行：

```
cd /lib/X11/Sample-Xconfig-files

less Xconfig.Index
```
