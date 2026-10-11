
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

在目录中移除或安装字体后，必须使用此命令。你的系统 `XF86Config` 文件还包含一个指向已安装字体的条目。该条目（位于 Files 部分）可能如下所示：

```
FontPath	"/usr/X11R6/lib/X11/fonts/misc/"
FontPath	"/usr/X11R6/lib/X11/fonts/100dpi:unscaled"
FontPath	"/usr/X11R6/lib/X11/fonts/75dpi:unscaled"
FontPath	"/usr/X11R6/lib/X11/fonts/Type1/*"
FontPath	"/usr/X11R6/lib/X11/fonts/Speedo/*"
FontPath	"/usr/X11R6/lib/X11/fonts/75dpi/*"
FontPath	"/usr/X11R6/lib/X11/fonts/100dpi/*"
```

但是，如果你在 X11 会话期间运行了 `xfs` X11 字体服务器，这些条目可能会被替换为以下内容：

```
FontPath	"unix/:71"
```

这对应于 `xfs` 在基于 Red Hat Linux 的系统（如 Mandrake 或 Yellow Dog Linux）上通常的启动方式。`xfs` 服务器由位于 `/etc/rc.d/init.d` 目录下名为 `xfs` 的初始化脚本启动。你可以在 `/etc/X11/fs` 目录下找到 `xfs` 服务器的配置文件，该文件名为 `config`。如果你安装了许多不同的字体，该配置文件将包含一个广泛的字体“目录”条目，可能如下所示：

```
catalogue = /usr/X11R6/lib/X11/fonts/misc:unscaled,
/usr/X11R6/lib/X11/fonts/75dpi:unscaled,
/usr/X11R6/lib/X11/fonts/100dpi:unscaled,
/usr/X11R6/lib/X11/fonts/misc,
/usr/X11R6/lib/X11/fonts/Type1,
/usr/X11R6/lib/X11/fonts/Speedo,
/usr/share/fonts/ttf/japanese,
/usr/share/fonts/ttf/korean,
/usr/share/fonts/default/Type1,
/usr/X11R6/lib/X11/fonts/100dpi,
/usr/X11R6/lib/X11/fonts/75dpi,
/usr/X11R6/lib/X11/fonts/cyrillic,
/usr/share/fonts/ISO8859-2/misc,
/usr/share/fonts/ISO8859-2/100dpi,
/usr/share/fonts/ISO8859-2/75dpi,
/usr/share/fonts/ISO8859-2/Type1,
/usr/share/fonts/ISO8859-9/misc,
/usr/share/fonts/ISO8859-9/100dpi,
/usr/share/fonts/ISO8859-9/75dpi,
/usr/share/fonts/ttl/western,
/usr/share/fonts/ttf/decoratives
```

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_193_0.png)

图 6.8 `xfontsel` 客户端可用于查看 X11 已安装的字体。

你可以通过在 X11 会话中使用 `xfontsel` 客户端来查看系统已安装字体的示例字符集。请像下面这样从 X11 终端窗口的命令行启动该客户端：

```
$ xfontsel &
```

按下回车键后，你将看到图 6.8 中所示的窗口。它列出了字体数量，并提供了你可以用来查看不同字体族的下拉菜单。有一些方法可以提高桌面的显示分辨率和字体外观。请浏览 Doug Holland 的 Linux 字体去锯齿化迷你 HOWTO，网址为 http://www.linuxdoc.org/HOWTO/mini/FDU.html

你会发现，通过遵循以下几个简单步骤，你可能会改善 X11 会话的外观：

1. 重新排列 `XF86Config` 或 `xfs` 配置文件中的字体选择顺序。
2. 启动 X 服务器时使用 100dpi 选项，以使用更高的每英寸点数。
3. 添加 TrueType 字体。
4. 更改 KDE 控制中心中的桌面样式设置。
5. 更改 Netscape Communicator 的字体首选项。

### 资源信息

http://www.cs.utexas.edu/users/kharker/linux-laptop/

获取 Linux 和笔记本电脑信息的首选之地。

http://judi.greens.org/lilo/

非官方的 LILO 支持页面。它提供了最新版 LILO 的链接、初学者信息、常见问题解答（FAQs）以及故障排除文档。

http://pcmcia.sourceforge.org/

获取有关使用 Linux 和 PCMCIA 卡的信息和软件的起点。
