

## 方法 #3

要读取 JPEG 文件中的注释，请使用 `rdjpgcom` 工具——它会输出作为参数给出的 JPEG 文件中的任何注释。

+   ⇒ 要读取图像文件 `phoenix.jpeg` 中的任何注释，输入：

```
$ rdjpgcom phoenix.jpeg [RET]
If you can read this, you're too close!
$
```

## 18.1.5 为图像添加边框

要为图像绘制边框，请使用 `mogrify` 并使用 `-border` 选项，后跟边框的宽度和高度（以像素为单位）。

+   ⇒ 要为 `phoenix.jpeg` 添加宽两像素高四像素的边框，输入：

```
$ mogrify -border 2x4 phoenix.jpeg [RET]
```

此命令将原始的 `phoenix.jpeg` 转换为带有 2x4 像素边框的图像，如图 18-8 所示。

![](img/be7f02611e5cefde1a18c788fede22f7_462_0.png)

*图 18-8. 带边框的 phoenix.jpeg 图像。*

`-frame` 选项的工作方式与 `-border` 类似，但它为图像添加更装饰性的边框。

+   ⇒ 要为 `phoenix.jpeg` 添加宽八像素高八像素的装饰性边框，输入：

```
$ mogrify -frame 8x8 phoenix.jpeg [RET]
```

此命令将原始的 **phoenix.jpeg** 转换为带有 8x8 装饰性边框的图像，如图 18-9 所示。

![](img/be7f02611e5cefde1a18c788fede22f7_463_0.png)

*图 18-9. 带装饰性边框的 phoenix.jpeg 图像。*

**注释：** 边框或边框被添加到现有图像的外部；图像不会被裁剪或缩小以添加边框。

## 18.1.6 创建图像蒙太奇

要制作多个图像的蒙太奇，请使用 **montage**。它将要使用的图像名称作为参数，后跟要写入蒙太奇图像的输出文件名。

蒙太奇图像是通过将所有输入图像缩放以适应最大可能尺寸，最高为 120x120 像素，并将这些图像以每行五列、四列的方式平铺而成的。

⇒ 要从文件 **owl.jpeg**、**thrush.jpeg** 和 **warbler.jpeg** 创建蒙太奇并将其写入 **ohio-birds.png**，输入：

```
$ montage owl.jpeg thrush.jpeg warbler.jpeg ohio-birds.png [RET]
```

**注释：** 在此示例中，读取了三个 JPEG 并输出到 PNG 文件；要在输出中指定使用的格式，请在输出文件名中给出适当的扩展名。

## 18.1.7 合并图像

使用 **composite** 将两幅图像合并为一幅新图像——将两个源图像文件和要写入的新文件的名称作为参数给出。没有任何选项时，**composite** 通过将两幅图像中较小的那一幅叠加在较大的那一幅之上，从左上角开始，创建新的图像文件；如果两幅图像大小相同，则只有第二幅图像可见。

+   ⇒ 要将两幅图像 ashes.jpeg 和 phoenix.jpeg 合并到新文件 picture.jpeg 中，输入：

```
$ composite ashes.jpeg phoenix.jpeg picture.jpeg [RET]
```

您可以使用 -dissolve 选项指定将两幅图像混合的百分比。将要“溶解”第一幅图像进入第二幅图像的百分比作为该选项的参数给出。

+   ⇒ 要将图像文件 ashes.jpeg 和 phoenix.jpeg 合并，使新图像包含 70% 的第一幅图像溶解到第二幅图像中，输入：

```
$ composite -dissolve 70 ashes.jpeg phoenix.jpeg picture.jpeg [RET]
```

此命令合并两幅图像并写入新的图像文件 picture.jpeg，其内容包含第一幅图像的 70%。

注释：使用 -dissolve 50 可使两个源文件混合均匀。

## 18.1.8 将两幅图像变形融合

变形是一种计算机成像方法，用于查找两幅图像中形状之间的差异；它常用于特效中，将两个生物的特征结合起来，例如人类和动物的面部。

您可以使用 convert 通过使用 -morph 选项，使用两个文件获得类似变形的效果。将要在两个文件之间的转换中使用的中间序列帧数作为该选项的参数给出。

当指定两个输入图像和一个输出文件时，此命令会取两个图像中对应像素之间的差异。效果就像“变形”后的图像。

如果您指定支持动画的文件格式，例如 MIFF，输出将写入单个动画图像文件。否则，输出将写入一系列文件，每个文件在其名称后附加其在系列中的编号。

您还可以指定在显示动画图像的每一帧时使用的延迟；为此，请使用 -delay 选项并给出时间，以百分之一秒为单位。

+   ⇒ 要将文件 ashes.jpeg 和 phoenix.jpeg 变形，制作一个名称以 morph.png 开头的三幅图像序列，输入：

```
$ convert -morph 3 ashes.jpeg phoenix.jpeg morph.png [RET]
```

