
# Joliet CD-ROM

关于微软特定的文件系统：即使对于 CD-ROM，如果没有新标准也无法工作。微软支持 ISO 但不支持 Unix 常用的 Rockridge 扩展。Windows 95/NT 引入了 Joliet 扩展。与 Rockridge 扩展的主要优势是，长文件名可以使用 Unicode 字符（所有语言的 65000 个字符）。遗憾的是，Windows 下无法使用带 Rockridge 扩展的 CD（受 8 字符限制）；Linux 下的 Joliet CD 也是如此。

# XFree86 3.2

3.2 版本是 XFree86 驱动的最新版本。与之前的 3.1.2 版本相比，最重要的改进是：

- 支持多种新型显卡（如 Matrox Millennium, S3 Virge, Tseng ET6000 和 Number Image 128）。
- 支持。
- 更简单的配置，新的配置程序 `XF86Setup`。
- `XF86Config` 中的新关键字。

对于其他发行版，只有当你使用 XFree86 当前充分支持的显卡时，XFree86 3.2 才有价值。在后面的子章节中，你将找到关于 3.1.2 版本的更改或改进信息，第 190 页有详细说明。

# XF86Setup

对于大多数用户来说，3.2 版本最令人满意的变化可能是设置程序。`XF86Setup` 在图形模式下运行（640x480 像素的标准 VGA）。理想情况下，程序会在第一次尝试时识别连接的鼠标；否则，应在第一个配置步骤中指定。不过，仅使用 `Tab` 键和方向键也可以操作程序。

# XFREE86 3.2

| MDisplay: 1024 | VDisplay: 768 |
| :--- | :--- |
| HSyncStart: 1048 | VSyncStart: 771 |
| HSyncEnd: 1184 | VSyncEnd: 777 |
| Htotal: 1328 | Vtotal: 896 |
| Left Right Wider Marrower | Up Down Shorter Taller |
| Flags (hex): 300a | Pixel Clock (MHz): 75.00 |
| Quit Auto Test Restore | Horizontal Sync (kHz): 56.48 |
| Fetch Next Prev | Vertical Sync (kHz): 70.07 |

图 E.1 `xvidtune`，用于微调位置。

你可以通过几个步骤配置键盘、显卡和屏幕。即使操作程序相当简单，但良好的硬件知识对于理解所有设置备选项仍然很有用。在设置显卡时，通过 `CARDLIST`，你可以从一个综合列表中选择一个显卡。然后你可以通过 `DETAILED SETUP` 为显卡设置各种参数和选项。（在许多情况下，程序会自动识别必要的设置。如果你不确定，请不要设置任何内容！）对于显示器，你可以选择几种标准显示器类型。从这些设置开始，你可以设置行频率和帧频率的允许值。你可以阅读 `README` 文件（`HELP`）。

当新的 X 服务启动时（仍在设置程序的上上下文中），会启动新工具 `xvidtune`。通过该程序你可以更改所有模式的大小和位置（`PREV` 和 `Next`）。你可以通过 `TEST` 测试图像位置，或通过 `APPLY` 存储这些设置。一旦退出程序，所有更改都存储在 `XF86Config` 中。

请注意，配置文件不在 `/etc/X11` 目录下（像 RedHat 那样），而是在 `/usr/X11R6/lib/X11/`！

虚拟屏幕的默认大小取决于有效模式的最大分辨率：当虚拟屏幕需要更大时，则需要显式设置。

## 650 附录 E：更新

如果 `XF86Setup` 不起作用，可以使用以前版本中已知（但也经过改进）的 `xf86config` 程序。该程序在文本模式运行。

## 手动配置

`XF86Config` 的结构没有发生显著变化——第 196 页的信息在很大程度上仍然有效。然而，还有一些扩展，下文将描述。

XFree86 3.2 支持 X11R6.1 的 XKeyboard 扩展。该扩展便于了外语言键盘的配置。配置通过新关键词进行。默认设置如下所示：

```
Section "Keyboard"

Protocol "Standard"

XkbRules "xfree86"

XkbModel "pc101"

XkbLayout "us"

EndSection
```

例如，对于德国键盘，需要以下设置：

```
Section "Keyboard"

Protocol "Standard"

XkbRules "xfree86"

XkbModel "pc102"

XkbLayout "de"

EndSection
```

对于 Screen（屏幕）部分，有一个新关键字 `DefaultColorDepth` 用于设置颜色深度（8、15、16、24 或 32 位；取决于显卡，通常并不支持所有选项）。当不带 `-bpp` 选项启动 X 服务器时，会使用此设置。

## 附录 F：附带 CD-ROM

随附的 CD-ROM 主要包含以下项目：

- RedHat 发行版 4.1，用于在 Intel 处理器的 PC 上安装 LINUX。有关 LINUX 安装的通用信息可以在第 2 章从第 15 页开始找到；RedHat 特有的细节请见附录 A 从第 603 页开始。
- 刻录光盘时（1997 年 2 月）已知的所有修正均位于 `updates` 目录。在 CD 到达书店时，RedHat 服务器可能已经提供了更多更新——您应该定期查看以下 WWW 页面：

```
http://www.redhat.com/support/docs/errata.html
```
