
下一步是选择打印机支持的默认分辨率。该值以水平和垂直每英寸点数表示。如果您不确定打印机，请查阅随打印机附带的制造商手册。滚动浏览分辨率列表（见图 15.3），并选择与打印机功能相匹配的一项。

### 图 15.3

配置 OpenLinux 打印机时选择适当的分辨率。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_374_0.png)

完成后，按 Enter 键。作为最后一步，您现在会看到一个对话框，询问与打印机一起使用的默认纸张尺寸。这些功能都用于构建和配置打印机的正确打印过滤器。滚动浏览纸张尺寸列表（见图 15.4），选择正确的尺寸，然后按 Enter 键完成打印机配置。

### 图 15.4

配置 OpenLinux 打印机时，您还必须选择默认纸张尺寸。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_374_1.png)

## 为打印配置 WordPerfect

如果您从 http://www.linux.corel.com/linux8/index.htm 下载并安装了 Corel 的 WordPerfect 8 for Linux 的免费个人使用版，则需要执行以下几个步骤才能打印。这涉及添加并选择打印机驱动程序作为默认打印机。

- 1. 启动 WordPerfect，然后按 F5 键。在 WordPerfect 打印对话框中，单击 Select 按钮。
- 2. 会出现一个选择打印机对话框，如图 15.5 所示。单击打印机创建/编辑按钮。

### 图 15.5

WordPerfect 选择打印机对话框用于创建或编辑打印机。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_375_0.png)

- 3. 会出现一个打印机创建/编辑对话框。单击添加按钮。
- 4. 会出现一个添加打印机驱动程序对话框（见图 15.6），其中包含可滚动的打印机驱动程序列表。滚动浏览列表，单击 Passthru PostScript 驱动程序（wp60ps02.us.all），然后单击确定按钮。
- 5. 会出现一个很小的创建打印机对话框，使用名称 passpost.prs。单击确定按钮。
- 6. 打印机创建/编辑对话框重新出现，其中 Passthru PostScript 打印机处于突出显示状态。单击设置按钮。
- 7. 会出现一个打印机设置对话框，如图 15.7 所示。在对话框底部附近，单击目标按钮。

### 图 15.6

选择 Passthru PostScript WordPerfect 打印机驱动程序以创建 OpenLinux 打印机。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_376_0.png)

### 图 15.7

在打印机设置对话框中，单击当前目标部分中的目标按钮以选择文档目标。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_376_1.png)

- 8. 会出现一个选择目标对话框（如图 15.8 所示），列出 $PRINTER、Disk、lp 和 ps。单击 ps，然后单击确定按钮。
- 9. 在打印机设置对话框中，单击确定按钮。在打印机创建/编辑对话框中，单击确定按钮。在选择打印机对话框中，单击确定按钮。您现在位于主打印对话框。单击确定以打印当前文档，或单击取消以取消打印操作。（您不会丢失创建的新打印机。）

如果您在执行这些步骤之前已在 OpenLinux 下正确设置了打印，现在就可以将 WordPerfect 文档打印到打印机了！

### 图 15.8

在选择目标对话框中，您完成打印机设置。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_377_0.png)

## 摘要

本小时介绍了可用于格式化和准备文本文档以便打印的一些程序。您还了解了一些 OpenLinux 中包含的更复杂的排版系统。最后，您学习了如何从命令行启动、列出和控制打印作业。您还学习了如何创建和配置与 OpenLinux 一起使用的打印机。

## 问答

Q OpenLinux 包含哪些其他格式化实用程序？
A 有很多，尤其是将文本文件文档转换为 PostScript 的实用程序。尝试使用 enscript 命令转换文本文档，然后阅读有关 eqn 实用程序用于排版格式化方程、pic 命令用于从文本排版图片以及 makeindex 命令用于创建文档索引的内容。

Q OpenLinux 包含哪些其他排版系统？
A 阅读 amstex 系统的手册页，该系统使用宏扩展 TeX 系统的功能。另一个名为 latex 的系统也包含在 OpenLinux 中。
Q 使用这些宏语言排版似乎很繁琐！有没有更简单的方法来创建这些文档？
A 尝试使用 Lynx 编辑器。这是一种准所见即所得编辑器，可创建样式类似于 latex 的文档。

Q 我尝试打印，lpr 命令返回类似“connection to ps@localhost.localdomain failed—Network is unreachable”的错误！发生了什么？

A 请确保您的 /etc/hosts 文件包含回环设备和本地主机的定义。另外，请确保文件中没有错误的 hostname 定义。

## 练习

- 1. 尝试打印多个文件，然后从打印队列中删除剩余的作业。
- 2. 使用 lisa 尝试重新配置打印机以使用更高的分辨率。会发生什么？
- 3. 使用多个 man 宏创建自己的 man 页面。尝试使用 nroff 脚本和 groff 程序。哪个效果更好？

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_380_0.png)

## 第 16 小时

### 图形工具

本小时介绍 OpenLinux 的各种图形程序和实用程序。我将首先简要讨论 OpenLinux 中使用的不同图形格式，然后展示如何使用过滤器程序和其他图形实用程序转换图形。这些程序可用于创建、编辑和转换从其他计算机程序或操作系统导入的图形。

您可以在本书的 CD-ROM 上找到大量优秀的图形程序，您可能会对其用途和多功能性印象深刻。本小时结束时，您将能够转换几乎任何类型的图形文件并执行复杂的图形文件转换操作。

## 了解 Linux 图形文件格式

有许多不同类型的图形文件格式，您的系统中已安装了若干类型的示例。如果您使用过其他计算机操作系统，您可能已经熟悉几种不同的格式。然而，如果 OpenLinux 对您来说是新的，请预期会遇到以前从未见过的格式的图形文件。

许多图形文件格式可以通过文件名的扩展名或文件名前缀中的字母来识别。例如，您可能会认识 .GIF、.PCX、.TIF 或 .JPG 等常见扩展名。如果您进行 OpenLinux 的完整安装，您的计算机上将安装超过 5,000 个图形！

表 16.1 列出了众多图形格式以及系统包含的相关转换程序。继续阅读以了解如何将图形图像从一种格式转换为另一种格式。

表 16.1 Linux 图形格式及转换程序

| 格式 | 类型 | 转换程序 |
|---|---|---|
| .10x | Gemini 10X | pbmto10x |
| .3d | 红/蓝 3D 位图 | ppm3d |
| .asc | ASCII 文本 | pbmtoascii |
| .atk | Andrew Toolkit 光栅 | atktopbm |
|  |  | pbmtoatk |
| .avs | AVS X 图像 | convert |
| .bie | 双电平图像专家 | convert |
| .bg | BBN BitGraph 图像 | pbmtobnb |
| .bmp | Windows、OS/2 位图 | bmptoppm |
|  |  | cjpeg |
|  |  | convert |
|  |  | gimp |
|  |  | ppmtobmp |
|  |  | xv |
| .bmp24 | Windows 24 位位图 | convert |
|  |  | xv |
| .brush | Xerox doodle 画笔 | brushtopbm |
| .cgm | 计算机图形元文件 | convert |
| .cmu | CMU 窗口管理器位图 | cmuwtopbm |
| .dcx | ZSoft Paintbrush | convert |
| .ddif | DDIF 图像 | pnmtoddif |
| .dib | Windows 位图图像 | convert |
| .dxb | AutoCAD 数据库文件 | ppmtoacad<br>sldtoppm |
| .dvi | TeX 打印机文件 | dvips<br>dvij4<br>dvij4l<br>dvij2p<br>dvij |
| .eps2 | Encapsulated PostScript Level II | convert |
| .epsf | Encapsulated PostScript | convert |
| .epsi | PostScript 预览位图 | pbmtoepsi<br>convert |
| .epson | Epson 打印机图形 | pbmtoepson |
| .fax | Group 3 传真 | convert |
| .fig | TransFig 图像 | convert |
| .fits | Flexible Image Transport | fitstopnm<br>pnmtofits<br>convert<br>gimp<br>xv |
| .fpx | FlashPix | convert |
| .g3 | Group 3 传真文件 | g3topbm<br>g32pbm<br>g3cat<br>pbm2g3<br>pbmtog3 |
| .gif | Graphics Interchange | cjpeg |

