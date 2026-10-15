

```
newfilename="$prefix+wm.$suffix"
① composite -dissolve 75% -gravity south $wmfile "$1" "$newfilename"

echo "Created new watermarked image file $newfilename."

exit 0
```

Listing 14-3: 水印脚本

## How It Works

脚本中几乎所有令人困惑的代码都归功于 ImageMagick。是的，它在做复杂的事情，但即便如此，ImageMagick 的设计和文档方式仍然让使用它成为一项挑战。尽管如此，也不要因噎废食，因为各种 ImageMagick 工具的功能和特性非常出色，完全值得投入学习成本。

第一步是获取图像的尺寸 ①，以便水印覆盖层具有完全相同的尺寸。如果尺寸不匹配，就会出问题！

“%g” 生成宽度 × 高度，然后将其作为新画布的大小传递给 convert 程序。② 处的 convert 行是我们从 ImageMagick 文档中复制来的，因为说实话，从零开始很难做到完全正确。（要了解 convert -draw 参数语言的具体细节，我们建议你快速在线搜索一下。或者你也可以直接复制我们的代码！）

新文件名应为基本文件名加上 “+wm”，而 ③ 处的三行代码正是实现这一点。rev 命令会逐字符反转其输入，因此 cut -d . -f1 可以获取文件名后缀，因为我们不知道文件名中会出现多少个点。然后后缀被重新排到正确位置并加上 “+wm”。

最后，我们使用 composite 工具 ④ 将各部分组合起来并生成带水印的图像。你可以尝试不同的 -dissolve 值来使覆盖层更透明或更不透明。

## Running the Script

脚本接受两个参数：要加水印的图像名称以及水印序列本身的文本。如果水印包含多个单词，请确保整个短语用引号括起来以便正确传递，如 Listing 14-4 所示。

```
$ watermark test.png "(C) 2016 by Dave Taylor"
Created new watermarked image file test+wm.png.
```

Listing 14-4: 运行水印脚本

## The Results

结果如图 14-1 所示。

![](img/4ffb1cc24a1b24b49254839643abedb2_349_0.png)

Figure 14-1: Image with automatically applied watermark

图 14-1：自动应用水印的图像

如果遇到无法读取字体错误，则你很可能缺少 Ghostscript 软件套件（在 OS X 上很常见）。要解决此问题，请使用你的包管理器安装 Ghostscript。例如，使用以下命令在 OS X 上安装 brew 包管理器：

```
$ brew install ghostscript
```

## Hacking the Script

用于水印的字体大小应是图像尺寸的函数。如果图像宽 280 像素，44 点的水印就太大了，但如果图像宽 3800 像素，44 点可能又太小了。可以将合适的字体大小或文本位置选择留给用户，通过将其作为另一个参数添加到脚本中来实现。

ImageMagick 也知道你系统上的字体，因此允许用户按名称指定用作水印的字体会很有帮助。

## #96 Framing Images

能够为图像添加边框或精美框架通常很有用，而 ImageMagick 通过 convert 工具在这方面提供了大量功能。问题是，与套件的其他部分一样，很难从 ImageMagick 文档中弄清楚如何使用此工具。

例如，这里是 -frame 参数的说明：

几何参数中的尺寸部分表示添加到图像尺寸的额外宽度和高度。如果几何参数中未给出偏移量，则添加的边框为纯色。偏移量 x 和 y，如果存在，则指定边框的宽度和高度被分割以形成厚度为 x 像素的外斜面和厚度为 y 像素的内斜面。

明白了吗？

也许看一个例子会更容易。事实上，我们将在本脚本的 usage() 函数中正是这样做的，如 Listing 14-5 所示。

## The Code

```
#!/bin/bash
# frameit--Makes it easy to add a graphical frame around
# an image file, using ImageMagick
usage()
{
cat << EOF
Usage: $(basename $0) -b border -c color imagename
or $(basename $0) -f frame -m color imagename
EOF
exit 1
}
```

在第一种情况下，将边框参数指定为 size x size 或 percentage x percentage，后跟边框所需的颜色（RGB 或颜色名称）。

在第二种情况下，指定框架大小和偏移量，后跟底色。

```
EXAMPLE USAGE:
$(basename $0) -b 15x15 -c black imagename
$(basename $0) -b 10%x10% -c gray imagename

$(basename $0) -f 10x10+10+0 imagename
$(basename $0) -f 6x6+2+2 -m tomato imagename
```

```
#### MAIN CODE BLOCK
# Most of this is parsing starting arguments!
while getopts "b:c:f:m:" opt; do
case $opt in
```

