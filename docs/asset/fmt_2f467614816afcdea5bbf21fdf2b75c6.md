
DEB: `imagemagick`

RPM: `ImageMagick`

WWW: http://www.imagemagick.org/

许多 Linux 工具可以以各种方式变换或处理图像。这里描述的是 ImageMagick 图像工具套件，其中 `mogrify` 工具特别适用于执行快速命令行图像变换；使用它来更改图像大小、旋转图像或减少图像中的颜色。

`mogrify` 工具始终将要处理的文件名作为参数，并将它的更改写入该文件。使用连字符 (`-`) 来指定标准输入，在这种情况下，`mogrify` 将其输出写入标准输出。

我将在接后的示例中使用图 18-1 所示的图像 `phoenix.jpeg`，以便你理解如何使用 `mogrify`。注意：你也可以通过 GIMP 交互地执行后续章节中许多许多图像变换（参见第 434 页食谱 18.3 [编辑图像]）；另一个既能变换图像又能进行格式转换非常有用的包是工具套件（参见第 443 页食谱 19.2 [扫描图像]）。

## 18.1.1 更改图像大小

使用 `mogrify` 调整图像大小有三种很好的方法，如下。注意：放大到更大的图像将显得块状或模糊。

要在不修改文件的情况下按特定比例查看图像，请使用 `display`；当你调整窗口大小时，你只调整屏幕上的图像，除非你选择保存它（参见第 [此处] 页食谱 18.2 [调整窗口]）。

方法 #1：要调整图像大小但保持其纵宽比（即宽高比保持不变），使用 `mogrify` 配合 `-geometry` 选项，并提供理想的像素值作为参数。将 `phoenix.jpeg` 调整为 480x320 像素，输入：
```
$ mogrify -geometry 480x320 phoenix.jpeg
```

方法 #2：要将图像调整为特定大小而不一定保持纵宽比，使用 `mogrify` 配合 `-geometry` 选项，并在提供的几何值参数后加上感叹号 (`!`)。无论纵宽比如何，将 `phoenix.jpeg` 调整为精确 640x480 像素，输入：
```
$ mogrify -geometry 640x480! phoenix.jpeg
```

方法 #3：你还可以通过 `mogrify` 使用百分比指定宽度或高度来缩放图像。要缩小百分比，给出数值后加上百分比号 (`%`)。要增加百分比，给出数值加 100 后加上百分比号。例如，要增加 25%，给出 "125%"。将 `phoenix.jpeg` 的高度增加 25%，宽度缩小 50%，输入：
```
$ mogrify -geometry 125%x50% phoenix.jpeg
```
该命令将原始 `phoenix.jpeg` 转换为高度增加了 25% 宽度缩小了 50% 的图像，如图 18-4 所示。

## 18.2 旋转图像

将高度大于宽度的 `phoenix.jpeg` 旋转 90 度，输入：
```
$ mogrify -rotate '90<' phoenix.jpeg
```
该命令将原始 `phoenix.jpeg` 旋转 90 度，如图所示。注意：执行此命令后，`phoenix.jpeg` 的宽度超过了高度，因此再次旋转时使用 `>` 而不是 `<`。

## 18.1.3 调整图像颜色

你可以使用 `mogrify` 对图像颜色进行若干调整。要减少图像中的颜色数量，使用 `-colors` 选项，后跟要使用的颜色数量。

将 `phoenix.jpeg` 的颜色减少到两种，输入：
```
$ mogrify -colors 2 phoenix.jpeg
```
该命令将原始 `phoenix.jpeg` 转换为黑白图像，如图 18-6 所示。

使用 `-dither` 选项通过 Floyd-Steinberg 误差扩散减少颜色，这是一种提高色彩还原质量的流行算法。

将 `phoenix.jpeg` 的颜色减少到四种并应用 Floyd-Steinberg 误差扩散，输入：
```
$ mogrify -colors 4 -dither phoenix.jpeg
```
该命令将原始 `phoenix.jpeg` 转换为抖抖的黑白图像，如图 18-7 所示。

# 第 18 章：编辑图像

使用 `-map` 选项并将第二个文件名作为参数，从第二张图像中读取颜色映射板（颜色集合），并将其应用于第一张图像中。
⇒ 要将文件 `rainbow.jpeg` 中的颜色更改为文件 `prism.jpeg` 中使用的颜色，输入：
```
$ mogrify -map prism.jpeg rainbow.jpeg RET
```

使用 `-monochrome` 选项将彩色图像变为黑白。
⇒ 要将彩色图像 `rainbow.jpeg` 变为黑白，输入：
```
$ mogrify -monochrome rainbow.jpeg RET
```

如果你有一个 PPM 文件，可以使用 `ppmquant` 对图像中的颜色进行量化，或将其减少到指定的数量——详情请参见 `ppmquant` 的 man 手页（参见 Recipe 2.8.4 [从系统手册中读取页面]，第 46 页）。

由于显示硬件的差异，图像的亮度在不同的计算机系统之间可能会有所。例如，在 Macintosh 上创建的图像在其他系统中通常看起来更暗。当你调整图像的亮度时，这被称为伽马校正（gamma correction）。

要调整图像的亮度，请将数值校正级别作为 `-gamma` 选项的参数。大多数 PC 显示器的伽马值为 2.5，而 Macintosh 显示器的伽马值较低，为 1.4。

⇒ 将图像 `rainbow.jpeg` 的伽马校正设置为 .8，输入：
```
$ mogrify -gamma .8 rainbow.jpeg RET
```

## 18.1.4 为图像添加注释

Independent Group 的 JPEG 软件
DEB: `libjpeg-progs`
RPM: `libjpeg-progs`
WWW: http://www.ijg.org/

在图像文件中读取和写入注释的方法很少。这种做法对于为图像添加版权声明或用 URL 为图像文件添加注记 很有用。并不是所有的图像格式都支持注释；JPEG 是最流行的。

在查看图像时不会看到注释；它被添加到文件中的图像头中。然而，你可以使用显示图像信息的工具（如 `display` 或 GIMP）来读取图像注释。另一种输出注释的方法在下文中有所描述。

### 方法 #1

使用 `commentjpg` 在 JPEG 文件中写入注释。将引号括的注释作为 `-comment` 选项的参数，并将输入文件名作为参数。默认是将新的 JPEG 文件写入标准输出。
⇒ 为文件 `map.jpeg` 中的图像添加文本“Map not drawn to full scale”注释，并将其写入文件 `warnmap.jpeg`（所有内容在一行）：
```
$ commentjpg -comment "Map not drawn to full scale" map.jpeg > warnmap.jpeg
```

使用 Bash 循环在一组文件中进行相同的注释（更多信息请参阅 Bash 文档）。若要为当前目录下所有的 `.jpg` 文件添加注释“Image courtesy”，并将其写入到具有相同名称但扩展名为 `.jpeg` 的新文件中：
```bash
for i in *.jpg; do commentjpg -comment "Image courtesy" $i > $i.jpeg; done
```

前面的示例可以写在单行上，省略 for 循环，如下所示：
```bash
$ for i in *.jpg; { commentjpg -comment "Image courtesy" $(basename $i) .jpeg; }
```

### 方法 #2

使用带有 `-comment` 选项的 `mogrify` 为图像文件添加注释。将引号中的注释作为参数提供。
⇒ 为图像文件 `phoenix.jpeg` 添加注释，输入（所有内容在一行）：
```
$ mogrify -comment "If you can read this, you're too close!" phoenix.jpeg
```

### 方法 #3

要读取 JPEG 文件中的注释，使用 `comment` 工具——它会输出作为参数提供的 JPEG 文件中的任何注释。
⇒ 要读取图像文件 `phoenix.jpeg` 中生成的任何注释，输入：
```
$ comment phoenix.jpeg
```

## 18.1.5 为图像添加边框

要在图像周围绘制边框，使用带有 `-border` 选项的 `mogrify`，随后是边框的像素宽度和高度。
⇒ 为 `phoenix.jpeg` 添加一个两像素宽、四像素高的边框，输入：
```
$ mogrify -border 2x4 phoenix.jpeg
```
