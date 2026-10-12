
你的打印机。lpc 命令专为管理员设计，因此可能不在你的默认 PATH 中。要启动 lpc 命令，请输入以下内容：

```
# /usr/sbin/lpc
lpc> status
Printer Printing Spooling Jobs Server Subserver Redirect Status
hp@localhost enabled disabled 4 none none
lp0@localhost enabled enabled 0 none none
lpc>
```

当命令返回 lpc> 提示符时，输入单词 status。此示例显示了两台打印机：hp 和 lp0 的状态。hp 打印机有四个任务正在等待。虽然队列和打印功能已启用，但它们并未打印，因为打印队列未启用。（打印机可能已被禁用。）lp0 打印机没有显示任何问题，没有打印任务正在等待。

## 使用 Ghostscript 和 Acrobat 显示文档

如果你每次想要更改文档内容或格式时，都将 Groff 或 LaTeX 文档发送到打印机，那么 Red Hat Linux 的出版工作可能会非常耗纸。为了节省纸张和来回奔波的时间，你可以使用一些打印预览程序，在屏幕上显示文档在打印页面上的外观。以下部分介绍了用于显示 PostScript 文件的 ghostscript 命令和用于显示便携式文档格式（PDF）文件的 Adobe Acrobat 阅读器。

### 使用 ghostscript 和 gv 命令

要在 Red Hat Linux 中显示 PostScript 或 PDF 文档，你可以使用 ghostscript 命令。ghostscript 命令是一个相当简陋的界面，旨在让你逐步浏览文档并逐行解释它们。（如果 ghostscript 命令未安装在你的系统上，你可以通过安装随本书附带光盘 CD-1 上的 ghostscript 包来获取它。）

你可以显示计算机上任何你碰巧拥有的 .ps 或 .pdf 文件。例如，如果安装了 vnc-doc 包，你可以输入以下内容来显示 PDF 文件（否则，你可以找到自己的 PDF 文件来尝试）：

```
$ ghostscript /usr/share/doc/vnc-doc-*/rfbprotoheader.pdf
>>showpage, press <return> to continue<<
```

在 GS> 提示符下，按 Enter 键（或 Return 键）即可逐页浏览文件。文件浏览完成后，你可以输入另一个 PostScript 或 PDF 文件的名称并逐页浏览该文件。完成后，输入 quit。

gv 命令（ghostview）是查看 PostScript 文件的另一种更友好的方式。（如果 gv 命令未安装在你的系统上，你可以通过安装随本书附带光盘 CD-2 上的 gv 包来获取它。）

若要用 gv 打开名为 `rbash.ps` 的文件，你会输入以下内容：

```
$ gv /usr/share/doc/bash-doc-*/bashref.ps
```

当 ghostview 窗口打开时，你可以看到文档。在页面上左键单击鼠标并上下移动以滚动文档。使用 Page Up 和 Page Down 键逐页浏览文档。你可以点击左侧列中的页码以跳转到特定页面，或点击 Print All 按钮打印整个文档。

## 使用 Adobe Acrobat Reader

便携式文档格式（PDF）提供了一种以打印外观存储文档的方式。使用 Adobe Acrobat Reader，你可以以非常友好的方式查看 PDF 文件。Adobe Acrobat 使得在 PDF 文件中导航变得非常容易。PDF 文件可能包含超链接、目录、图形和各种字体。

你还可以从 Adobe 网站 www.adobe.com/support/downloads 下载免费的 Acrobat Reader 副本。Acrobat Reader 是免费的，旨在鼓励人们购买用于创建 PDF 文档的 Acrobat 4 程序。使用 Acrobat 4，你可以将几乎任何类型的文档转换为 PDF，从扫描图像创建 PDF 文件，在 PDF 文档中添加电子注释和高亮，并应用数字签名（用于安全目的）。

安装 Adobe Acrobat Reader 后，输入以下命令以启动该程序：

```
$ acroread
```

点击 File → Open，然后选择你要显示的 PDF 文件的名称。图 6-12 显示了在 Adobe Acrobat Reader 中查看 PDF 文件的示例。

![](img/1744bde8c889adfab3fc911e1687fecf_268_0.png)

图 6-12：在 Adobe Acrobat Reader 中显示 PDF 文件。

Acrobat Reader 有很多很好的功能。例如，你可以在文档旁边显示书签列表，并点击书签跳转到特定页面。你还可以显示页面的缩略图以快速滚动并选择页面。

使用菜单栏或按钮，你可以逐页浏览 PDF 文档，放大和缩小，跳转到文档的开头或结尾，并显示文档的不同视图（以及显示书签和页面缩略图）。要打印副本，请点击 File → Print。

## 处理图形

在 Red Hat Linux 中，创建和操作图形的工具正变得更多且更强大。排在首位的是 GNU 图像操作程序（GIMP）。GIMP 让你能够组合和创作图像以及修饰照片。Red Hat Linux 附带用于创建图形的其他工具包括 xv（用于截取屏幕截图的程序）和 xpaint（用于处理位图图像）。

> **交叉引用：** 有关其他多媒体应用程序（如用于处理数码相机图像的 gphoto 窗口）的描述，请参见第 8 章。

### 操作照片和图像

GIMP 程序是随 Red Hat Linux 附带的免费软件，用于操作照片和图形图像。若要使用 GIMP 创建图像，你可以导入绘图、照片或 3D 图像，或者从零开始创建一个。你可以通过点击系统菜单中的 Programs → Graphics → The GIMP，或在终端窗口中输入 gimp& 来启动 GIMP。

> **注意：** 如果 GIMP 不在你的系统上或未正确安装，你可以通过安装随本书附带光盘 CD-1 来安装它。或者，你可以从 www.gimp.org 获取最新版本的 GIMP。

在许多方面，GIMP 类似于 Adobe Photoshop。有些人认为 GIMP 的脚本功能可与 Adobe Photoshop 中的操作相当，甚至更好。然而，GIMP 缺乏的一项功能是对 CMYK 分离的支持。

### 截取屏幕截图

如果你想要展示你在 Red Hat Linux 上工作的示例，可以使用 xv 工具来捕获屏幕图像。这个工具对我们这些写计算机书的人特别有用。（本书中的大多数图像都是使用 xv 工具捕获的。）由于 xv 是共享软件，若要将其用于商业用途，你应该向 xv 的创建者支付 25 美元的费用（点击 About XV 按钮以了解许可证及缴费方式）。

xv 工具不再是 Red Hat Linux 发行版的一部分。从存储 Linux 的 FTP 站点（如 ftp://ftp.redhat.com/pub/contrib/libos/1995/）获取 xv 的副本。要打开 xv 窗口，请输入：

当你第一次启动 xv 时，xv 图像显示窗口（你的屏幕截图将出现在这里）会显示出来。点击该窗口以查看 xv 控制窗口（其中包含抓取和保存屏幕的按钮）。图 6-13 显示了 xv 控制窗口。注意，Red Hat Linux 附带的 xv 版本（如图所示）未注册。如果你将其用于工作，我强烈建议你注册一份副本。

![](img/1744bde8c889adfab3fc911e1687fecf_270_0.png)

**图 6-13：** 使用 xv 捕获屏幕图像并保存为多种格式。

若要使用 xv 抓取图像，请点击 Grab。对话框让你选择 Grab（使用鼠标左键抓取窗口）或 AutoGrab（在设定的秒数后抓取光标定位其上的窗口）。对于 Grab，你既可以点击你想要抓取的窗口，也可以使用鼠标中键（在三键鼠标上）拖动打开一个矩形区域以抓取。

在使用 AutoGrab 之前，你必须输入 xv 在 AutoGrab 抓取光标指示的窗口前应等待的 Delay（秒数）。

抓取图像后，你可以对其进行一些操作。在图像窗口上选择一个矩形区域。然后，从控制窗口点击 Scissors（剪切该区域）、Crop（剪切区域外的部分）或任一箭头按钮（上下或左右翻转选定的区域）。点击旋转箭头以将图像向一个方向或另一个方向旋转。

若要保存图像，请点击 Save。从 15 种不同的图像输出类型中选择格式。选择 Full Color、B/W Dithered 或 Grayscale。为图像选择目录和文件名。然后点击 OK。如果你想查看计算机上的任何图像，点击 Load 并选择你需要的文件。

**注意：** 如果你只是想快速截图，**screenshotter** 是 Gnome 桌面附带的免费工具，正好可用于此目的。将其添加到你的 Gnome 面板中（Gnome 菜单 → Panel → Add to panel → Applet → Utility → Screenshotter）。然后点击 screenshotter 图标的左侧以选择窗口或滑动一个区域以捕获。点击 screenshotter 图标的右侧以抓取整个桌面。捕获的图像以 JPEG 文件形式保存在你的主目录中。

