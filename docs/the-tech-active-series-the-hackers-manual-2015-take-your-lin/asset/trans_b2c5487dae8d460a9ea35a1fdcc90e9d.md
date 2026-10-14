

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
if blur > 0:
pdb.gimp_plug_in_gauss_iir(timg, blur_layer, blur, blur)

## 轻柔地，轻柔地

最后，我们应用色相和亮度调整，并将 bokeh 图层设置为“柔光”模式，这样底层图层会在圆盘下方被照亮。为了防止有任何黑色在桶填充后残留，我们使用 Color-To-Alpha 插件将其去除。

```
pdb.gimp_hue_saturation(bookeh_layer, 0, 0, lightness, saturation)
pdb.gimp_layer_set_mode(bookeh_layer, SOFTLIGHT_MODE)
pdb.plug_in_colortoalpha(timg, bookeh_layer, '#000000')
```

这基本上概括了我们脚本的核心。你从随附代码中可以看到，还需要处理一些整理工作，即将整个

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_138_0.png)

操作序列合并为单个可撤销操作，并恢复脚本所更改的任何工具设置。总是收拾好自己的东西、物归原位总是好的。在 register() 函数中，我们将其 menupath 设置为 "<Image>/Filters/My Filters/PyBookeh..."，这样如果注册成功，你将在“滤镜”菜单中看到一个“我的滤镜”菜单。你可以把以后想出的任何其他脚本添加到此菜单，以免使本就拥挤的“滤镜”菜单更加杂乱。示例图片显示了几个 PyBookeh 应用的结果。

应用滤镜后，画面会变得有些模糊。更改图层的不透明度可以恢复一些细节。

> “最后，将操作合并为单个可撤销操作，并重置任何已更改的工具设置。”

批评者可能会对这个脚本的实用性提出多余的嘲讽，的确，完全可以用手工完成它所做的一切，甚至可能做得更好。至少在某种程度上，这对任何 GIMP 脚本来说都是如此。但手工操作将极其费力且容易出错——你必须记下每个圆盘中心的坐标和颜色，而且如果想保持颜色叠加的效果，你必须极其灵巧地进行圆盘叠加。

## 注册你的插件

为了让你的插件出现在 GIMP 菜单中，有必要将其定义为一个 Python 函数，然后使用 register() 函数。最整洁的方式是将所有代码保存在一个布局合理的 Python 脚本中。这种脚本的一般形式是：

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

指定你插件的输入：你可以在此使用特殊的 Python-Fu 类型，如 PF_COLOR 和 PF_SPINNER，以获得用于输入这些内容的友好界面。results 列表描述你的插件输出（如果有）。在我们的例子中，(PF_IMAGE, image, "LSImage") 就足够了。最后，function 只是你的函数在代码中出现的 Python 名称。

proc_name 参数指定你的插件在 PDB 中的名称；实际上会自动添加前缀 python_fu_，这样所有 Python 插件在分类中都有自己的分支。menupath 参数指定你注册的插件类型，以及你的插件将出现在 GIMP 菜单中的位置：在我们的例子中，使用 "<Images>/Filters/Artistic/LineSplodge..." 就足够了。imagetypes 指定插件处理的图像类型，例如 "RGB"，如果插件不操作任何图像（例如我们的示例），则可以简单地使用 "*"。params 列表

为了确保 GIMP 在下一次加载时找到并注册你的插件，请将此文件保存为（比如说）myplugin.py，并放到插件文件夹中：Linux 下为 ~/.gimp-2.8/plugins（确保使用 chmod +x myplugin.py 使其可执行），Windows 用户则放到 %USERPROFILE%\.gimp-2.8\plug-ins，并根据实际情况替换版本号。

