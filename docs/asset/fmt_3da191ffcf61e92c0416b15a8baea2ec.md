
2TB 起

- `$999 Netdisk 6000 2TB 4x500G`

- `$1,550 Netdisk 6000 3TB 4x500G`

## 1U 存储服务器

2TB 起

- [费曼学习法](https://wiki.example.org/feynmans_learning_method)的灵感源于诺贝尔物理奖获得者**理查德·费曼**。

1.  运用费曼技巧，你只需花上`20 min`就能深入理解知识点，而且记忆深刻，*难以遗忘*。

```
if (condVar > someVal) {console.log("xxx")}
```

![](img/465f773ec3a6747b5eef398f28f808b8_62_0.png)

![](img/465f773ec3a6747b5eef398f28f808b8_62_1.png)

图 3. 软阴影后的灰色背景按钮

图 4. 意在软阴影后具有灰色背景的按钮。通过单位 `alpha` 掩码导出并叠加在不同的颜色背景上。

脚本。虽然使用许多较小的脚本速度较慢，因为有额外的图像保存/加载周期影响，但这对于批量处理图像来说并不那么重要。优点是，一旦熟悉了这些小脚本，就可以从命令行和 `Makefile` 快速将它们组合在一起。通用实用函数已移动到 `MonkeyQGIMP` 模块中，以便快速创建小型图像编辑脚本。

# 列表 3. `MonkeyQGimp` 保存函数

```perl
#/usr/bin/perl

@layers = Gimp->image_get_layers($img);
print "layers size: " . scalar @layers . "\n";

package MonkeyQGIMP;

use Gimp 'auto';
use Gimp::Fu;
require Exporter;

sub imageOutput(
    my ($img, $outfilename) = @_;

    if ($outfilename =~ /\.xcf/) {
        print "Save to xcf file $outfilename\n";
        Gimp->save(0, $img, $outfilename);
    }
    else {
        $layer = Gimp->image_get_active_layer($img);
        $layer = Gimp->image_merge_visible_layers($img, $GIMP_CLIP_MERGE_EVERYTHING);
    }
    Gimp->image_delete($img);
}

sub mergedLayer(
    my ($img) = @_;

    my $existinglayer = Gimp->image_get_active_layer($img);
    $newlayer = Gimp->image_add_layer($img, $existinglayer, GIMP_LAYER_NORMAL, GIMP_LAYER_BEFORE, -1);
    Gimp->edit_fill($newlayer, GIMP_EDIT_FILL_WHITE);
    return Gimp->image_merge_visible_layers($img, 1);
}
```

## 通过调整每个图层的亮度或对比度，可以实现鼠标事件预亮图像的自动化。

## 带有 1 位 `Alpha` 通道的图像

作为第一个示例，假设我们有一个具有 8 位透明度的图像文件，并且想将其导入为仅包含 1 位 `alpha` 掩码的 `GIF`。为了获得最佳效果，我们应该对不完全透明或完全透明的像素进行一些处理。半透明像素可以与设计的背景颜色混合，以便在不进行任何特殊处理的情况下呈现视觉效果。

图像所示（图 3），软阴影被模糊为单位 `alpha` 掩码，导致导出的图像看起来很差。与灰色背景的锯齿现象将合并到导入的图像中，产生锯齿边缘，如图 4 所示，这种效果并不美观。选择灰色作为背景是最佳选择，否则边缘极其锯齿，且软阴影效果会丢失。

在下一个代码列表 2 中，我们通过处理 `GIMP` 您的图像文件来转换输出路径，并创建一个适用于 1 位 `alpha` 掩码的图像。`GIMP` 的输入和输出图像可以读可写。此脚本可能读取一个 `xcf` 文件并写入 `PNG` 文件。`PNG` 图像稍后用 `webgif` 脚本进行处理以获得最终图像。

列表 5. 最后，转换为用于互联网的 6 位 `GIF`。

```bash
$ gimp-monkeyq-webgif \
--inputimage Button-bunicely-merged-with-green.png \
--outputimage Button.gif -dither 64
$ identify Button.gif
Button.gif 317x213 317x213jX+i+h=0 PseudoClass
```

列表 6. 导出带有其他选项的 `GIF` 图像。对于此图像我们需要这 8 位吗？

```perl
$ sub_to_web {
  my($imagename, $filename);
  (num_cols, $use_dither) = @;
  $palette_type = @;
  $image = GIMP-file_load($imagename, $filename);
  ($image);
  GIMP-convert_indexed($image, $use_dither);
  ($palette_type, $num_cols, 1);
  GIMP-output($image, $filename);
}

{PF_STRING, "inputimage",
"Name of image to export", "",
PF_STRING, "outputimage",
"Name of image to save to", ""
PF_INT, "depth", "depth", "255"
PF_INT, "dither", "dither", "1"
PF_INT, "alpha", "1"}
```

列表 4. 将背景与糟糕的灰色合并。

```bash
$ gimp-monkeyq \
--inputimage Button-with-8Bit-alpha.xcf \
--outputimage Button-bunicely-merged-with-green.png \
--alphascolor #08ff00
```

![](img/465f773ec3a6747b5eef398f28f808b8_63_0.png)

让我们来看代码列表 2。导入 `GIMP API`，然后声明脚本的主函数，并将参数清晰地声明为变量。跳过函数后，脚本底部的结果给出了 `GIMP` 的元数据，以及应该显示菜单的选项以及它实际处理的参数数量和类型（这些通过对上面函数的引用）。在处理 `GIMP` 控制之前，只有少量的参数检查。

在处理完元数据处理器后，脚本加载转换函数文件，并创建一个与图像本身尺寸相同的新图层（`layer`），并将用指定的背景颜色填充。然后将此新图层置于按钮上，并合并可见图层。这使得背景中的所有透明度都经过了评估。在我们背景作为背景的情况下，输入的 `xcf` 文件隐藏了灰色背景图层，如果使用指定的亮绿色背景颜色运行脚本，软阴影将按照规定与绿色混合。

# 你是否将

“电脑做不到这一点”视为一种个人的挑战？

# 深度解析

# 我们也是如此。

## 列表 9. 为鼠标悬停事件创建一个快速的预点亮图像。
