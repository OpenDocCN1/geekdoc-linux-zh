
```
blur_layer = pdb.gimp_layer_copy(timg, timg[0],1)
pdb.gimp_image_insert_layer(timg, blur_layer, None, 0)
bokeh_layer = pdb.gimp_layer_new(timg, width, height, RGBA_IMAGE, "bokeh", 100, NORMAL_MODE)
pdb.gimp_image_insert_layer(timg, bokeh_layer, None, 0)
```

我们脚本接下来的任务是提取用户所选路径中的点列表。这有点不简单，因为一般的路径可能是一个非常复杂的对象，带有曲线、方向变化等种种情况。细节见下面的方框，但别担心——你只需要理解主 `for` 循环将按绘制顺序沿着路径前进，将每个组成点的坐标提取为两个变量`x`和`y`。

提取点信息后，下一个挑战是获取该处图像的局部颜色。执行此操作的 PDB 函数称为`gimp_image_pick_color()`。它有许多选项，类似于“颜色选择器”工具的对话框。我们的特定调用让程序在`x,y`点周围 10 像素半径内采样，并选择平均颜色。这比只选择该单个像素的颜色更可取，因为单个像素的颜色可能不代表其周围环境。

### 拿个油漆桶来

要在散景图层上绘制颜色适当的圆盘，我们一开始——有点反直觉——先绘制一个黑色圆盘。为了不依赖所有用户都有一致的画笔集，我们不使用画笔工具，而是通过桶式填充一个圆形选区来制作圆形。选区是这样实现的：

```
pdb.gimp_image_select_ellipse(timg, CHANNEL_OP_REPLACE, x - radius, y - radius, diameter, diameter)
```

有一些常量引用了各种 Gimp 特有的

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_137_0.png)

> 快速提示

> 想要更多、更多自制插件，请查看 Gimp 插件注册表：http://registry.gimp.org

这些就是我们的圆盘。如果你感觉很疯狂，可以添加混合或渐变，但统一颜色效果就很好。

### 路径、矢量、描边、点、图像和可绘制对象

路径存储在称为矢量的对象中。更具体地说，该对象包含一系列描边，每条描边描述路径的一部分。我们假设一条没有曲线的简单路径，因此只有一条描边，从中获取我们渴望的点。在代码中，我们将这条描边称为`gpoints`，它实际上是一个元组，其第三个条目是点列表。由于 Python 列表从 0 开始，因此通过`gpoints[2]`访问点列表。该列表的格式为`[x0,y0,x0,y0,x1,y1,x1,y1...]`。每个点被计算了两次，因为在其他设置中，列表需要保存曲率信息。为了避免重复，我们使用`range()`函数的`step`参数，每次迭代递增 4，这样我们在位置 0、4、8 获得`xs`，在位置 1、5、9 获得`ys`。点列表的长度由`gpoints`的第二个条目提供，即`for i in range(0,gpoints[1],4):`

你会看到对变量`timg`和`tdraw`的多次引用。它们表示调用我们函数时的活动图像和图层（更准确地说是图像和可绘制对象）。可以想象，它们是非常方便的东西，因为很多工具至少需要一个图像和一个图层才能工作。实际上，它们非常方便，以至于当我们在 Gimp 中注册脚本时，我们不需要提及它们——人们会假定你想将它们传递给函数。图层和通道共同构成了称为可绘制对象的类——这种抽象在这里是合理的，因为有很多操作同样适用于两者。

GIMP 模式及其他奥妙。它们很容易通过全大写的形式辨认出来。这里的第二个参数代表数字 2，同时也表示当前选区应被指定的椭圆选区替换。

尺寸的指定方式是给出包围椭圆的外框左上角以及该外框的宽度。我们将这个选区羽化两个像素，以缓和边缘，然后将前景色设置为黑色。接着，我们在“背后”模式下用桶填充这个新选区，以免干扰图层上的其他圆盘：

```
pdb.gimp_selection_feather(timg, 2)
pdb.gimp_context_set_foreground('#000000')
pdb.gimp_edit_bucket_fill_full(bookeh_layer, 0,BEHIND_MODE,100,0,False,True,0,0)
```

现在说明使用黑色的原因：我们将以加法颜色模式绘制圆盘。这意味着重叠的圆盘区域会变得更亮，这有点类似于摄影中的效果。问题是，加法颜色对透明度没什么实际作用，所以我们先把它涂成黑色，然后我们新增的加法圆盘会覆盖掉所有黑色。

```
pdb.gimp_context_set_foreground(color)
pdb.gimp_edit_bucket_fill_full(bookeh_layer, 0,ADDITION_MODE,100,0,False,True,0,0)
```

当我们以这种方式绘制完所有圆盘后，如果请求了高斯模糊，我们就对复制出的图层进行高斯模糊。我们说过，图像的一部分应保持清晰；你可能希望以后处理这个图层，使感兴趣区域的透明度更低。在进行填充之前，我们取消所有选区，否则我们只会模糊最近绘制的圆盘。

```
if blur > 0:
pdb.gimp_plug_in_gauss_iir(timg, blur_layer, blur, blur)
```

## 轻柔地，轻柔地

最后，我们应用色相和亮度调整，并将 bokeh 图层设置为“柔光”模式，这样底层图层会在圆盘下方被照亮。为了防止有任何黑色在桶填充后残留，我们使用 Color-To-Alpha 插件将其去除。

```
pdb.gimp_hue_saturation(bookeh_layer, 0, 0, lightness, saturation)
pdb.gimp_layer_set_mode(bookeh_layer, SOFTLIGHT_MODE)
pdb.plug_in_colortoalpha(timg, bookeh_layer, '#000000')
```

这基本上概括了我们脚本的核心。你从随附代码中可以看到，还需要处理一些整理工作，即将整个

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_138_0.png)

操作序列合并为单个可撤销操作，并恢复脚本所更改的任何工具设置。总是收拾好自己的东西、物归原位总是好的。在`register()`函数中，我们将其`menupath`设置为`"<Image>/Filters/My Filters/PyBookeh..."`，这样如果注册成功，你将在“滤镜”菜单中看到一个“我的滤镜”菜单。你可以把以后想出的任何其他脚本添加到此菜单，以免使本就拥挤的“滤镜”菜单更加杂乱。示例图片显示了几个`PyBookeh`应用的结果。

应用滤镜后，画面会变得有些模糊。更改图层的不透明度可以恢复一些细节。

> “最后，将操作合并为单个可撤销操作，并重置任何已更改的工具设置。”

批评者可能会对这个脚本的实用性提出多余的嘲讽，的确，完全可以用手工完成它所做的一切，甚至可能做得更好。至少在某种程度上，这对任何 GIMP 脚本来说都是如此。但手工操作将极其费力且容易出错——你必须记下每个圆盘中心的坐标和颜色，而且如果想保持颜色叠加的效果，你必须极其灵巧地进行圆盘叠加。

## 注册你的插件

为了让你的插件出现在 GIMP 菜单中，有必要将其定义为一个 Python 函数，然后使用`register()`函数。最整洁的方式是将所有代码保存在一个布局合理的 Python 脚本中。这种脚本的一般形式是：

```
#!/usr/bin/env python
from gimpfu import *
def myplugin(params):
# code goes here
register(
proc_name, e.g. "python_fu_linesplodge"
blurb, "# Draws a line and a splodge"
help, author, copyright, date,
menupath, imagetypes,

params, results,
function() # "myplugin"
main)
```

指定你插件的输入：你可以在此使用特殊的 Python-Fu 类型，如`PF_COLOR`和`PF_SPINNER`，以获得用于输入这些内容的友好界面。`results`列表描述你的插件输出（如果有）。在我们的例子中，`(PF_IMAGE, image, "LSImage")`就足够了。最后，`function`只是你的函数在代码中出现的 Python 名称。
