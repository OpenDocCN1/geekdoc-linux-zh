
某些字体文件包含该字体的多个高度（或大小）。如果字体包含不同高度的多种编码，请将要使用的高度作为 `-H` 选项的参数给出。（如果尝试在不使用高度选项的情况下指定此类字体，`consolechars` 将输出可用尺寸列表。）

常见的控制台字体高度包括 8（用于 8x8 字体）、14（用于 8x14 字体）和 16（用于 8x16 字体）。

⇒ 要将控制台字体设置为 sc 字体的 8x8 大小，输入：

```
$ consolechars -H 8 -f sc [RET]
```

### 16.3.2 显示控制台字体的字符

使用 `showfont` 显示当前控制台字体中的所有字符。

⇒ 要列出当前控制台字体中的所有字符，输入：

```
$ showfont [RET]
```

## 16.4 使用文本字体

*Text fonts* 是由屏幕上 ASCII 字符的排列创建的字体；它们常出现在 Usenet 文章和电子邮件消息中，作为文本文件中的装饰或标题元素出现，并用于在打印机上打印简单的横幅或海报。

从 ASCII 字符的排列制作“字体”（甚至图片）被称为 ascii art。以下配方描述了在这些字体中输出文本的方法。

### 16.4.1 输出水平文本字体

Figlet

DEB: figlet

RPM: figlet

WWW: http://www.figlet.org/

`figlet` 过滤器以给定的文本字体输出文本。将要输出的文本作为参数给出，对包含 shell 元字符的文本进行引用（参见 Recipe 3.1.3 [Quoting Reserved Characters]，第 56 页）。

⇒ 要以默认 figlet 字体输出文本“news alert”，输入：

```
$ figlet news alert [RET]
```

该命令以 ASCII 文本字体输出文本，如图 16-2 所示。

![](img/be7f02611e5cefde1a18c788fede22f7_434_0.png)

图 16-2. `figlet` 的输出。

`figlet` 的字体保存在 `/usr/lib/figlet` 目录中；使用 `-f` 选项后跟字体文件的基本名称（不含路径或扩展名）来使用该字体。

要以 `figlet` 字体输出文本文件的内容，请使用 `cat` 输出文件内容并将输出通过管道传递给 `figlet`。

⇒ 要以 `figlet` bubble 字体输出文件 `poster` 的文本，输入：

```
$ cat poster | figlet -f bubble [RET]
```

NOTES: `bubble` 字体安装在 `/usr/lib/figlet/bubble.flf`。

### 16.4.2 输出文本横幅

Bsd-games

DEB: bsdmainutils

RPM: bsd-games

WWW: ftp://metalab.unc.edu/pub/Linux/games/

在 Linux 系统上打印长垂直文本横幅的最简单方法是使用旧的 UNIX `banner` 工具。

将文本消息作为参数引用，`banner` 会将该消息的大型垂直“横幅”发送到标准输出。消息本身以由 ASCII 文本字符组成的“字体”输出，与 `figlet` 使用的类似，只是消息是垂直输出以便打印，并且你不能更改字体。要将 `banner` 的输出发送到打印机，请将其通过管道传递给 `lpr`。

⇒ 以下是两种使用方法。

- 要制作横幅“Happy Birthday Susan”，输入：

  `$ banner 'Happy Birthday Susan' RET`

- 要将横幅“Happy Birthday Susan”打印到默认打印机，输入：

  `$ banner 'Happy Birthday Susan' | lpr RET`

不幸的是，`banner` 理解的字符范围有点有限——以下字符不能在横幅消息中使用：

< > [ ] \ _ ~ { } | ^

要制作文本文件内容的横幅，请通过重定向标准输入将其内容发送到 `banner`（参见 Recipe 3.2.1 [Redirecting Input to a File]，第 67 页）。

要制作文件 `/etc/hostname` 内容的横幅，输入：

```
$ banner < /etc/hostname RET
```

横幅的默认宽度为 132 文本列；你可以通过将要使用的宽度作为 `-w` 选项的参数来指定不同的宽度。如果在不带数字的情况下给出 `-w` 选项，`banner` 将以 80 文本列输出。

⇒ 以下是两种使用方法。

- 要制作包含文本“Happy Birthday Susan”且宽度为 23 文本列的横幅，输入：

  `$ banner -w 23 'Happy Birthday Susan' RET`

+   • 要制作一个宽度为 80 个文本列、包含文字 “Happy Birthday Susan” 的横幅，输入：

+   

+       `$ banner -w 'Happy Birthday Susan' [RET]`

NOTES: 在 Recipe 15.2.7 [Outputting Text in Landscape Orientation]，第 369 页中描述了一种使用 `figlet` 制作水平文本横幅的方法。

## 16.5 使用其他字体工具

下表描述了 Linux 可用的一些其他字体工具。

Console Font Editor    Linux 控制台字体编辑器（cse），一种较旧的用于在屏幕上编辑字体字符的控制台字体工具。

DEB: cfe

RPM: cfe

WWW: http://lrn.ru/~osgene/

Debian Font Manager    用于在 Debian 系统上配置字体的工具。

DEB: defoma

    defoma-doc

    psfontmgr

Fonter    一个控制台字体编辑器。

DEB: fonter

WWW: ftp://metalab.unc.edu/pub/Linux/apps/misc/

FontForge    一个字体编辑器，可识别多种格式，包括 PostScript、TrueType 和 OpenType。

DEB: fontforge

RPM: fontforge

WWW: http://fontforge.sourceforge.net/

Font Viewer    用于查看 Adobe Type 1 和 TrueType 字体的工具。

DEB: gfontview

RPM: gfontview

WWW: http://gfontview.sourceforge.net/

Gozer

一个将作为参数给出的文本渲染为抗锯齿 TrueType 字体的工具。

DEB: gozer

WWW: http://www.linuxbrit.co.uk/gozer/

Metafont

Donald E. Knuth 设计字体和标志的语言（随 TeX 分发）。

DEB: tetex-base

    tetex-bin

    tetex-doc

    tetex-extra

RPM: tetex

WWW: http://www.tug.org/teTeX/

PkTrace

一个将使用 Metafont 制作的字体转换为 Type 1 字体的工具。

DEB: pktrace

RPM: mftrace

## IV. 图像

## 17. 查看图像

有许多用于查看图像的工具，与文本一样，既有查看工具也有编辑图像的工具。本章描述了一些查看图像的最佳方法；图像编辑将在下一章讨论。虽然你可以用图像编辑器查看图像，但如果你不打算编辑它，使用查看器更安全（也更快！）。

### 17.1 在 X 中查看图像

ImageMagick

DEB: imagemagick

RPM: ImageMagick

WWW: http://www.imagemagick.org/

要在 X 中查看图像，请使用 `display`，它是 ImageMagick 工具套件的一部分。它可以识别许多图像格式，包括 FlashPix、GIF/GIF87、Group 3 传真、JPEG、PBM/PNM/PPM、PhotoCD、TGA、TIFF、TransFig 和 XBM。它还可以查看使用 `gzip` 或 `bzip2` 压缩的图像，而无需你先解压缩，并且还提供基本的编辑功能。

`display` 工具以要查看的图像文件名作为参数，并在其自己的新窗口中显示图像。

⇒ 要查看文件 `sailboat.jpeg`，输入：

```
$ display sailboat.jpeg [RET]
```

该命令在新窗口中显示图像文件，如图 17-1 所示。

![](img/be7f02611e5cefde1a18c788fede22f7_440_0.png)

图 17-1. `display` 中的图像。

鼠标按钮在 `display` 中具有特殊含义。左键单击图像窗口以在新窗口中打开 `display` 命令菜单。`display` 命令菜单看起来像图 17-2。

![](img/be7f02611e5cefde1a18c788fede22f7_441_0.png)
