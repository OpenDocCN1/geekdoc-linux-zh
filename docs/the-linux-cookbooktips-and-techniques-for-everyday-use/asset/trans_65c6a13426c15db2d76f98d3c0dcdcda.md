

• 要制作一个包含文本 `Happy Birthday Susan` 且宽度为 23 个文本列的横幅，输入：

```
banner -w 23 'Happy Birthday Susan' RET
```

• 要制作一个包含文本 `Happy Birthday Susan` 且宽度为 80 个文本列的横幅，输入：

```
banner -w 'Happy Birthday Susan' RET
```

**注意：** 使用 `figlet` 制作水平文本横幅的方法在 [以横向方式输出文本](#) 中有描述。

## 17.4 其他字体工具

下表描述了 Linux 可用的一些其他字体工具。

| 工具 | 描述 |
|---|---|
| `cse` | Linux 控制台字体编辑器 cse 是一个较旧的控制台字体编辑器。 { @sf{WWW} }: `http://www.ibiblio.org/pub/Linux/system/keyboards/` |
| `dtm` | Definitive Type Manager 是一个用于向系统添加和删除 Adobe Type 1 字体的工具。 { @sf{Debian} }: `dtm` |
| `fonter` | Fonter 是一个控制台字体编辑器；用它来制作和编辑控制台字体。 { @sf{Debian} }: `fonter` |
| `gfont` | gfont 工具创建 TeX 字体渲染的文本 GIF 图像。 { @sf{Debian} }: `gfont`; { @sf{WWW} }: http://www.engelschall.com/sw/gfont/ |
| `gfontview` | 这是一个用于查看 Adobe Type 1 和 TrueType 字体的工具。 { @sf{Debian} }: `gfontview` |

## 第四部分：图像

+   - [18. 查看图像](18. Viewing Images) 查看图像。
+   - [19. 编辑图像](19. Editing Images) 编辑图像。
+   - [20. 导入图像](20. Importing Images) 将图像导入 Linux。
+   - [21. PostScript](21. PostScript) 关于 PostScript 及相关内容。

[<](<) [>](>) [<<](<<) [Up](Up) [>>](>>)

[Top](Top) [Contents](Contents) [Index](Index) [?](?)

## 18. 查看图像

与文本一样，也有用于查看和编辑图像的工具。本章描述了各种查看图像的方法；图像编辑将在下一章讨论。虽然你可以用图像编辑器查看图像，但如果你不打算编辑它，使用查看器更安全（也更快！）。

+   18.1 预览打印文件 — 预览打印图像文件。
+   18.2 在 X 中查看图像 — 在 X 中显示图像。
+   18.3 在控制台中浏览图像 — 在控制台中显示图像。
+   18.4 在 Web 浏览器中查看图像 — 在 Web 浏览器中查看图像。
+   18.5 浏览 PhotoCD 档案 — 浏览 Kodak PhotoCD。
+   18.6 其他图像查看器 — 用于查看图像的其他工具。

## 18.1 预览打印文件

DVI（“设备无关”）、PostScript 和 PDF（“便携式文档格式”）文件格式可由许多应用程序生成。它们是常用的图形图像格式，用于打印；以下各节讨论了在显示屏上预览这些文件的方法。

+   18.1.1 预览 DVI 文件 — 预览 DVI 文件。
+   18.1.2 预览 PostScript 文件 — 预览 PostScript 文件。
+   18.1.3 预览 PDF 文件 — 预览 PDF 文件。

## 18.1.1 预览 DVI 文件

使用 xdvi 工具在 X 中预览 DVI 文件。将要预览的文件名作为参数给出。xdvi 会显示文档打印时的外观，并允许你以不同放大倍率查看。

+   • 要预览文件 `gentle.dvi`，输入：

## 18.1.3 预览 PDF 文件

@sf(Debian): `xpdf`
@sf(WWW): http://www.foolabs.com/xpdf/
@sf(Debian): `gv`
@sf(WWW): http://wwwthep.physik.uni-mainz.de/~plass/gv/
使用 xpdf 预览 PDF 文件。将要预览的 PDF 文件名作为参数给出。

+   - 要预览 PDF 文件 `flyer.pdf`，输入：

```
$ xpdf flyer.pdf RET
```

要退出 xpdf，按 Q；使用两个放大镜按钮将视图放大（+）或缩小（−），并使用左右箭头按钮在上一页和下一页之间移动（如果有）。

*注意：* 你也可以使用 gv 来预览 PDF 文件。

[ < ] [ > ] [ << ] [ Up ] [ >> ] [Top] [Contents] [Index] [ ? ]

## 18.2 在 X 中查看图像

@sf(Debian): `imagemagick`
@sf(WWW): ftp://ftp.wizards.dupont.com/pub/ImageMagick/
要在 X 中查看图像，请使用 display，它是 ImageMagick 工具套件的一部分。它可以识别许多图像格式，包括 FlashPix、GIF/GIF87、Group 3 传真、JPEG、PBM/PNM/PPM、PhotoCD、TGA、TIFF、TransFig 和 XBM。

display 以要查看的图像文件名作为参数，并在新窗口中显示图像。

+   - 要查看文件 `sailboat.jpeg`，输入：

```
$ display sailboat.jpeg RET
```

此命令在新窗口中显示图像文件：

