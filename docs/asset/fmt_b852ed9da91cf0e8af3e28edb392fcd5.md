
列表 13-11：运行脚本 `-v` 以打印支持的声音，然后

## 破解脚本

对 `say -v` 输出的检查显示，至少有一个声音的语言编码是 Fiona。Fiona 被列为 en-scotland，而不是 en_scotland，后者会更一致（鉴于 Moira 被列为 en_IE，而不是 en-irish 或 en-ireland）。一个简单的破解方法是让脚本同时处理 en_ 和 en-。否则，你可以尝试一下它，并思考在什么时候让脚本——或守护进程——与你说话会有用。

# 14 IMAGAGAGICK 与图形文件处理

![](img/954a28cc04c09826495e330f44c0085b_344_0.png)

命令行在 Linux 世界中拥有极其广泛的能力，但由于它是基于文本的，你对图形做不了什么。或者其实可以？

事实证明，一套极其强大的命令行工具套件 ImageMagick 适用于几乎所有的命令行环境，从 OS X 到 Linux 再到许多其他。要使用本章中的脚本，你需要从 http://www.imagemagick.org/ 下载并安装该套件，或者从包管理器（如 `apt`、`yum` 或 `brew`）安装，如果你在第 304 页的脚本 #91 中执行过的话。

由于这些工具设计为在命令行中工作，它们所需的磁盘空间很小，约为 19MB（对于 Windows 版本）。如果你想深入研究强大且灵活的软件，你也可以获取源代码。开源再次获胜。

## 94 更智能的图像尺寸分析器

`file` 命令提供了确定文件类型以及在某些情况下确定图像尺寸的能力。但它经常失败：

```
$ file * | head -4

100.0399.png: PNG image data, 1024 x 768, 8-bit/color RGBA, non-interlaced

8t grade arti.jpeg: JPEG image data, JFIF standard 1.01

99.gif: GIF image data, version 89a, 143 x 163

Angel.jpg: JPEG image data, JFIF standard 1.01
```

PNG 和 GIF 文件可以用，但更常见的 JPEG 呢？`file` 命令无法确定图像的尺寸。真恼人！

### 代码

让我们用脚本修复这个问题，它使用 ImageMagick 的 `identify` 工具来更准确地确定图像尺寸（列表 14-1）。

```bash
#!/bin/bash

# identifies--使用 ImageMagick 的 

# identify 工具显示图像信息和尺寸

for name

do

  identify -format "%f: %G with %k colors.\n" "$name"

done

exit 0
```

列表 14-1：`identifies` 脚本

### 工作原理

当你使用 `-verbose` 标志时，`identify` 工具会提取关于每个图像的海量信息，正如其对一个文件的输出所示：

```
$ identify -verbose testimage.png

Image: testimage.png

Format: PNG (Portable Graphics)

Class: DirectClass

Geometry: 1172x158+0

Resolution: 72x72

Units: Undefined

Filesize: 80.9KB

Number pixels: 185176

Pixels per second: 18.5

User time: 0:000u

Elapsed time: 0:01.009

Version: ImageMagick 6.7.7-10
```

那是大量的数据。你可能会认为数据太多了。但如果没有 `-verbose` 标志，输出是非常晦涩的：

```
$ identify testimage.png

testimage.png 1172x158+0+0
```

我们想要一个折中方案，而获取该方案输出字符串非常有帮助。让我们仔细观察列表 14-1，关注脚本中唯一有意义的一行：`-format` 字符串有几乎 30 个选项，允许你按照所需的格式从一张或多张图像提取你需要的特定数据。我们利用 % 获取原始文件名，利用 % 作为宽=高的快捷方式，并利用 % 作为图像最大颜色的计算值。

你可以在 http://www.imagemagick.org/script/escape.php 了解更多关于 `-format` 选项。

### 运行脚本

ImageMagick 完成了所有工作，因此此脚本主要作为特定输出的方法。获取图像信息快速又方便，如列表 14-2 所示。

### 破解脚本

目前我们使用图像的像素尺寸和可用色彩，但一个非常有用的补充将文件大小。然而，如果不对输出进行一些重新格式化，任何更多信息都难以阅读。

## 95 图像水印

如果你想在网上发布时保护你的图像和其他内容，那么你注定会失望。任何内联内容都可以被复制，无论你是否设置了密码、强力的版权声明，甚至在网站上添加了试图阻止用户保存单个图像的脚本。事实是，计算机要渲染在线内容，就必须使用设备上的图像缓冲区，而该缓冲区可以被屏幕截屏或类似的工具复制。

但一切并非不可救。你可以做两件事来保护你的在线图像。一个是发布小尺寸图像样本。看看专业摄影师的网站你就会明白我们的意思。他们通常只分享缩略图，因为他们让你购买更大的图像文件。

水印是另一种解决方案，尽管有些艺术家反感直接在照片上添加水印或其他标识信息。但使用 ImageMagick，添加水印非常简单，即使是批量处理也是如列表 14-3 所示。

### 代码

```bash
#!/bin/bash

# watermark--将指定的文本作为水印添加到输入图像上，

# 将输出保存为 image=wm

wmfile=/tmp/watermark.$$                      # 应该是一个起始参数

fsize="44"

trap "\$(which rm) -f "$wmfile" 0 1 15      # 不留临时文件

if [ $# -ne 2 ]; then

    echo "Usage: $(basename $0) imagefile \"watermark text\"" >&2

    exit 1

fi

if [ ! -r "$1" ]; then

    echo "$(basename $0): Can't read input image $1" >&2

    exit 1

fi

# 首先，获取图像尺寸。

# dimensions=$(identify -format "%G" "$1")

# 让我们创建一个临时水印叠加层。

# convert -size $dimensions xc:none -pointsize $fsize -gravity south \

#     -draw "fill black text 1,1 '$2' text 0,0 '$2' fill white text 2,2 '$2'" \

#     $wmfile

# 现在将叠加层和原始文件进行合并。

# suffix="$(echo $1 | cut -d. -f1 | rev)"

prefix="$(echo $1 | cut -d. -f2- | rev)"

newfilename="$prefix*wm.$suffix"

composite -dissolve 75% -gravity $wmfile $1 "$newfilename"

echo "Created new watermarked image file $newfilename."
```
