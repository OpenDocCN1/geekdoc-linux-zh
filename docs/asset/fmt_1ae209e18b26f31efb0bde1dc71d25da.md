
这将原始的 `phoenix.jpeg` 转换为：

![](img/939a59ecb60c25a97f69cbde1a0d6a2f_290_1.png)

## 19.1.6 创建图像拼图

要制作其他图像的拼图，使用 `montage`。它接受图像名称作为参数，最后是输出文件的名称。该拼图是通过将所有输入图像缩放到最大尺寸（120x120 像素），并按 5 行 4 列排列这些图像制作的。

- 若从 `owl.jpeg`、`thrush.jpeg` 和 `warbler.jpeg` 创建拼图，并写入 `end-birds.png`，输入：

```
$ montage owl.jpeg thrush.jpeg warbler.jpeg end-birds.png
```

**注意：** 在此示例中，读取了三个 JPEG 并输出为 PNG 文件；要指定使用的格式，请为输出文件名提供相应的扩展名。

## 19.1.7 合并图像

使用 `combine` 将两个图像合并为一个——将两个源图像文件名和要写入的新文件名作为参数。在没有任何选项的情况下，它通过将较小的图像叠加在较大的图像左上角来制作新图像；如果两个图像大小相同，则只显示第二幅图像。

- 若将 `ashes.jpeg` 和 `phoenix.jpeg` 合并为新文件 `picture.jpeg`，输入：

```
$ combine ashes.jpeg phoenix.jpeg picture.jpeg
```

你可以通过 `-blend` 选项指定混合两个图像的百分比。将第二幅图像混合到第一幅图像中的量（百分比）作为选项的参数。

- 若合并 `phoenix.jpeg` 和 `ashes.jpeg`，使得混合图像包含第二幅图像的 70%，输入：

```
$ combine -blend 70 ashes.jpeg phoenix.jpeg picture.jpeg
```

这结合了两幅图像并写入一个新的图像文件 `picture.jpeg`，其内容包含第一张图像的 70%。

注意：使用 `-blend 50` 可均匀混合源文件。

[< ] [ > ] [ << ] [上] [ >> ] [顶] [目录] [索引] [?]

## 19.1.8 图像的渐变（Morphing）

渐变（Morphing）是一种计算机成像方法，用于寻找两幅图像形状之间的差异；它被用于特效中变换两种生物的特征，例如人类和某种其他动物的面部。

你可以通过向 `-compose` 传递差异参数来组合以获得渐变效果。当指定了两个图像和一个输出文件时，此命令会取两个图像之间对应像素的差异；其效果类似于“渐变图像”。

- 要为文件 `ashes.jpeg` 和 `phoenix.jpeg` 创建渐变图像并写入 `picture.jpeg`，请输入：

```
$ combine -compose difference ashes.jpeg phoenix.jpeg picture.jpeg RET
```

文件 `picture.jpeg` 中的结果为：

![](img/939a59ecb60c25a97f69cbde1a0d6a2f_292_0.png)

注意：`xmorph` 是一个用于图像渐变的工具；请参见交互式图像编辑器与工具。

[<.] [>.] [<<.] [上] [>>.] [顶] [目录] [索引] [?]

## 19. 图像编辑

## 19.2 格式间的转换

@sf(Debian): `imagemagick`
@sf(WWW): `http://ftp.wizards.dupont.com/pub/ImageMagick/`

使用 `convert` 转换图像的文件格式。将要转换的文件名作为第一个参数，目标文件作为第二个参数。转换文件时，原始文件不会被修改。

要指定要转换的文件类型，可以在转换后的文件名中使用该类型的标准扩展名。

- 要将 JPEG 文件 `phoenix.jpeg` 转换为 PNG 图像，请输入：

```
$ convert phoenix.jpeg phoenix.png RET
```

此命令将 JPEG 图像 `phoenix.jpeg` 转换为 PNG 格式并写入新文件 `phoenix.png`。

下表列出了使用的文件扩展名并描述了它们的格式。（习惯上使用全小写扩展名。）

| 文件扩展名 | 图像格式 |
| :--- | :--- |
| bmp | Microsoft Windows 位图图像。 |
| cgm | 计算机图形元文件格式（Computer Graphics Metafile）。 |
| cmyk | 原始青、洋红、黄色和黑色字节。 |
| eps | Adobe 封装 PostScript（Encapsulated PostScript）。 |
| fax | Group 3 传真格式。 |
| fig | TransFig 图像格式。 |
| fpx | FlashPix 格式。 |
| gif | 图形交换格式 GIF89a 版本（通常读作 "gif"，与 "biff" 押韵）。 |
| gray | 原始灰色字节。 |
| jpegandjpg | 联合图像专家小组 JFIF 格式（通常读作 "jay-peg"）。 |
| pbm | 黑白位图格式。 |
| pcd | Kodak PhotoCD 格式，最大分辨率为 512x768 像素。 |
| pcl | 页面控制语言（Page Control Language）格式。 |
| pcx | ZSoft IBM PC Paintbrush。 |
| pdf | Adobe 便携式文档格式。 |
| pict | Apple Macintosh QuickDraw 格式。 |
| png | 便携式网络图形格式（通常读作 "ping"）。 |
| pnm | 便携式“任意映射”格式。 |

## 19. 图像编辑

# Linux 菜谱：日常使用的技巧与技术：

- ppm 颜色便携式像素图格式。
- ps AdobePostScript 格式。
- rgb 原始红、绿、蓝字节。
- tga TrueVision Targa 格式。
- tiffandtif 标记图像格式 Tagged Image Format（通常读作 "tiff"）[等待，原文写的是 "tiffandtif"]
*注：修正为 "tiff Tagged Image Format（通常读作 "tiff")"*
- xbm X Window 系统位图格式。
- xpm 颜色 X Window 系统像素图格式。
- xwd 颜色 X 系统“转储”文件格式。

在将文件转换为 JPEG 时，务必使用 `~interlace` 选项以确保生成的 JPEG 是非交织的——除非你确实想要一个交织图像；交织图像通过多次绘制完成，通常用于 Web 端，让读者在图像下载完成之前查看由早期像素组成的低分辨率图像。非交织图像则在单页中绘制。

例如，使用 `convert` 将 PNM 文件转换为非交织 JPEG，同时进行锐化、添加边框并添加注释语句。

- 要将 PNM 文件 `pike.pnm` 转换为非交织 JPEG，同时将图像锐化 50% 并添加 2x2 的边框和注释，请输入：

```
$ convert -interlace NONE -sharpen 50 -border 2x2 -comment 'copyright 1999 MS' pike.pnm pike.jpeg RET
```

此命令将其输出写入文件 `pike.jpeg`。注意 `-border` 和 `-comment` 选项之前在 `mogr` 工具中描述过。某些 ImageMagick 工具共享这些选项，如果你对图像文件进行多次更改，这将非常有用的。

在将文件转换为 JPEG 时，务必使用 `~interlace` 选项以确保生成的 JPEG 是非交织的——除非你确实想要一个交织图像；交织图像通过多次绘制完成，通常用于 Web 端，让读者在图像下载完成之前查看由早期像素组成的低分辨率图像。非交织图像则在单页中绘制。

例如，使用 `convert` 将 PNM 文件转换为非交织 JPEG，同时进行锐化、添加边框并添加注释语句。

- 要将 PNM 文件 `pike.pnm` 转换为非交织 JPEG，同时将图像锐化 50% 并添加 2x2 的边框和注释，请输入：

```
$ convert -interlace NONE -sharpen 50 -border 2x2 -comment 'copyright 1999 MS' pike.pnm pike.jpeg RET
```
