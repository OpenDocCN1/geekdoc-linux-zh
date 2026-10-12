
```
chmod o+r /dev/cdrom
```

现在，任何可以访问你 Linux PC 的用户都可以播放音频 CD 并访问 CD-ROM 驱动器。

> **注意**
>
> 如果你使用 KDE 作为桌面，可以在 KDE 中找到类似的音频 CD 播放器。通过选择“Multimedia -> KDE CD Player”来启动 KDE CD 播放器。然后你可以选择播放音频 CD 中的某条轨道。

### 处理图形与图像

此类类别中的应用程序允许你准备、查看、修改和打印图形及图像。在本次课程的剩余时间内，你将尝试几个图形和图像处理应用程序。

### GIMP

GIMP（GNU 图像处理程序）是由 `Peter Mattis` 和 `Spencer Kimball` 编写的图像处理程序，并在 GNU 公共通用许可证（GPL）发布。如果你在从本书附带的 CD-ROM 安装 Red Hat Linux 时选择了“图形处理（Graphics Manipulation）”包，你就会安装它。

要尝试 GIMP，请从 GNOME 桌面选择“Main Menu -> Graphics -> The GIMP”（从 KDE 桌面选择“Graphics -> the GIMP”）。

## 第 19 节——多媒体应用程序

GIMP 启动并显示一个包含如何完成个人安装信息的窗口。该消息通知你，个人安装涉及在主目录下创建一个名为 `.gimp-1.1` 的目录，并在该目录放置若干文件。此目录本质上存储了你可能对 GIMP 进行的用户偏好更改。继续点击窗口底部的“Continue”按钮。GIMP 会创建必要的目录，将一些文件复制到这些目录，并引导你通过一系列对话框完成安装。

安装完成后，点击“Continue”按钮。从现在起，你将不再看到这两个安装窗口；你只有在第一次运行 GIMP 时才需要处理它们。

随后，GIMP 会加载任何插件——增强其功能的外部模块。启动窗口会在每个插件加载时显示关于该插件的消息。启动完成后，GIMP 在窗口中显示“今日提示（tip of the day）”。你可以浏览这些提示，然后点击“Close”按钮关闭提示窗口。在显示提示窗口的同时，GIMP 会显示工具箱（如图 19-2 所示）。

![](img/448aa2bd6846782b632c764b035753bc_260_0.png)

图 19-2
GIMP 工具箱

工具箱在菜单栏上有三个菜单：File（文件）、Xtns（扩展）和 Help（帮助）。File 菜单包括创建新图像、打开现有图像和退出 GIMP 的选项。Xtns 菜单允许你访问 GIMP 的许多扩展。Xtns 的具体内容取决于你的系统中安装了哪些扩展。Help 菜单允许你获取帮助。

要在 GIMP 中打开图像文件，选择“File -> Open”。这将弹出“Load Image（加载图像）”对话框，允许你选择图像文件。你可以更改目录并选择想要打开的图像文件。GIMP 可以读取大多数常见的图像格式，如 GIF、JPEG、TIFF、PCX、BMP、PNG 和 PostScript。选择文件并点击“OK”按钮后，GIMP 将图像加载到新窗口中。图 19-3 显示了 GIMP 打开的图像。

第四部分——周六晚上
第 19 节

![](img/448aa2bd6846782b632c7646782b632c764b035753bc_261_0.png)

# 图 19-3
使用 GIMP 显示图像

图 19-2 中的工具箱还有许多按钮，每个按钮都有一个图标，代表你用于编辑图像和应用特殊效果的工具。通过将鼠标指针悬停在每个工具按钮上，你可以获取弹出式帮助。你可以通过点击工具按钮来选择工具；然后你可以在图像上应用该工具的效果。

为了方便起见，当你对图像点击右键鼠标时，GIMP 会显示弹出菜单。弹出菜单包含了工具箱中 File 和 Xtns 菜单的大多数选项。你还可以选择一些额外选项，例如打印或邮件发送图像。然后你可以从这些弹出菜单中选择特定操作。

使用 GIMP 不仅可以加载和查看图像，但你必须花一些时间学习它的所有功能。要了解更多关于 GIMP 的信息，选择“Xtns -> Browser -> GIMP.ORG -> Documentation”。这将打开文档浏览器。

### Ghostscript

Ghostscript 是用于查看和打印 PostScript 文档的解释器。Ghostscript 的核心是 PostScript 语言几乎完整的实现。它根据 GNU GPL 分发。Ghostscript 是处理 PostScript 文件的命令行工具。

要运行 Ghostscript，在终端窗口输入 `gs`。该命令会产生窗口。窗口分为三个部分：

- 顶部有五个按钮，前六个是菜单按钮；点击其中任何一个都会出现菜单。
- 侧边有更多按钮、信息文本框和滚动条。
- 占据窗口大部分的区域是工作区域。

要在 Ghostview 中加载并查看 PostScript 文档，选择“File Open”或点击窗口左侧的“Open”按钮。此会导致 Ghostview 显示文件选择对话框。使用此对话框选择 PostScript 文件。你可以选择 Ghostscript 自带的 PostScript 文件。例如，选择 `/usr/share/ghostscript/5.50/examples` 下的 `tiger.ps` 文件。

> 如果你的系统版本高于 5.50，请用新的版本号替换 5.50。

点击对话对话框中的“Open”按钮打开选定文件。Ghostview 打开选定文件，处理内容并在窗口中显示输出（如图 19-4 所示）。

![](img/448aa2bd6846782b632c764b035753bc_262_0.png)

图 19-4
Ghostscript 显示文件

在这种情况下，输出是一个图片。显示输出后，Ghostscript 会产生以下消息：

```
showpage, press <return> to continue
```
