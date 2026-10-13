
该命令根据 `-b` 选项自动创建一个目录，然后下载并将 PDA 的内容保存到指定目录中。Red Hat 为这些命令提供了 GNOME 图形界面，可以在“辅助工具”菜单下的 Pilot/Handspring 进入。我们推荐这两个应用程序中的任意一个，它们提供了更多功能。

### GUI PDA 客户端软件

要使用图形界面与 PDA 交互，你可以使用 Organizer 客户端。你可以使用此应用程序安装和检索文本文档，并备份 PDA 内容。你需要通过选择正确的串口、设置和默认文件位置来正确配置软件。通过打开“辅助工具”菜单并选择“Pilot”来打开 Organizer。

![](img/446debe023486a07fde575245cf7a3ff_863_0.png)

图 25.10 Organizer 客户端可以与 PDA 同步数据。

另一个图形 PDA 客户端如图 25.11 所示，是全面的 Pilot 。你可以使用 Pilot 程序为你的 Palm 相关的 PDA 管理、检索、安装、备份和同步任何信息。你可以点击“日历”、“待办事项”、“地址录”和“备忘录”按钮来执行相关任务。使用“同步”和“备份”按钮来更新或保留 PDA 数据的副本。你通过从“辅助工具”菜单选择“Pilot”来打开此客户端。

> 注意：Red Hat 提供了几个邮件客户端供你使用，并提供 Evolution（类似于 Microsoft Outlook）作为默认。所有邮件客户端将在第 19 章中详细介绍。图形应用程序（包括 GIMP）将在第 26 章中讨论。

![](img/446debe023486a07fde575245cf7a3ff_864_0.png)

图 25.11 Pilot PDA 客户端支持 PalmOS 设备。

### Red Linux 扫描仪应用程序

使用扫描仪为提高生产力提供了丰富的选择。你可以在 GIMP、OpenDraw 和 Contour 等图形应用程序中处理扫描图像，然后将其打印或嵌入文字文档中。你可以扫描纸质文档用于存档，或使用光学字符识别（OCR）软件处理它们，将其转换为可以在编辑器或文字处理器中编辑的文字。Red Hat 有 `Xsane`（见图 25.12）和 `Kooka`（见图 25.13）应用程序协助扫描。

扫描支持由 Scanner Access Easy（SANE）提供。如果你的扫描仪受支持，它将列在 SANE 支持页面上：http://www.linux.org/sane/backends.html。

SANE 的开发版本支持普通版本不支持的扫描仪。如果你的扫描仪仅受开发版本支持，你需要下载并编译 CVS 版本 版本。这是一项复杂的操作，仅适用于高级 Linux 用户，并且超出了本书的范围。有关该过程的信息，请参阅 Linux 源码控制系统 CVS HOWTO：http://www.linux.org/howto/CVS-RCS-HOWTO.html。

如图 25.12 所示，`Xsane` 应用程序是 SANE 的图形前端。它允许你获取和处理扫描图像。它可以作为 GIMP 的插件运行。GIMP 在第 26 章中详细讨论。

![](img/446debe023486a07fde575245cf7a3ff_865_0.png)

图 25.12 启动后，`Xsane` 在你的桌面上显示几个相关屏幕：控制界面、直方图、预览屏幕和选项对话框。

`Kooka` 是一个与 `Xsane` 功能类似的 KDE 应用程序，但它还提供了 OCR（光学字符识别）能力和图像库功能。由于 `Kooka` 是 KDE 应用程序，当其他 KDE 应用程序（如 KOffice 和 KView）编写为使用它时，它可以提供扫描服务。`Kooka` 使用 `gocr` (http://jocr.sourceforge.net/) 作为字符识别应用程序，但计划在未来支持 Clara OCR (http://www.claraocr.org/)。

# Red Hat Linux 扫描仪应用程序

![](img/446debe023486a07fde575245cf7a3ff_866_0.png)

**图 25.13** VueScan 界面提供了大量的选项。这里，扫描了一份报纸剪报和一个照片。

你可以下载 VueScan 进行评估。该程序不受限制，但在你购买序列号（当前价格为 40 美元）之前，它会在任何扫描件上添加水印。该网站提供了我见过的关于扫描仪使用的最出色的文档和支持。

下载软件后，如要安装它，请在 `/usr/local` 中创建一个名为 `vuescan` 的目录，将 tar 文件复制到那里，并使用 `tar` 进行解压：

```bash
# mkdir /usr/local/vuescan
# cp xvzf vuesca75.tgz /usr/local/vuescan/
# cd /usr/local/vuescan/
# tar xvzf vuesca75.tgz
```

这会在根目录下留下一个二进制文件，路径为 `/usr/bin/vuescan/vuescan.html`。

为了让应用程序在 Red Hat 8.0 上正常运行，必须在启动程序时设置语言环境变量；否则字体将无法正常显示。以下是设置方法：

```bash
# env LANG=C /usr/local/vuescan/vuescan &
```
