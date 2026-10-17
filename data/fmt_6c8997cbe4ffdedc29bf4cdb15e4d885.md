
| `–edge` _factor_ | 使用指定的增强因子（百分比）检测图像中的边缘。 |
| `–enhance` | 增强有噪声的图像。 |
| `–equalize` | 执行直方图均衡化。 |
| `-filter` _type_ | 使用 `-geometry` 调整图像大小时，使用指定的滤波器类型。可用的滤波器包括：Bessel、Blackman、Box、Catrom、Cubic、Gaussian、Hamming、Hanning、Hermite、Lanczos（默认值）、Mitchell、Point、Quadratic、Sinc、Triangle。 |
| `-flip` | 通过垂直反转扫描线创建镜像图像。 |
| `-flop` | 通过水平反转扫描线创建镜像图像。 |
| `-font` _font_ | 设置普通文本的字体。 |
| `-frame` _width x height + outer-bevel width + inner-bevel width_ | 使用指定的宽度、高度、外部斜面宽度和内部斜面宽度的装饰性边框。 |
| `-fuzz` _distance_ | 合并指定距离内的颜色。 |
| `-gamma` _n_ | 使用指定的伽马校正级别（n），其中 n 是 0.8 到 2.3 之间的级别。 |
| `-geometry` _width x height [% \| !]_ | 创建具有指定最大宽度和高度的图像，同时保持原始图像的宽高比。附加 `%`（百分号）可按百分比调整宽度和高度。要强制使用指定尺寸，请附加 `!`（感叹号）。 |
| `-gravity` _type_ | 设置图像的倾斜方向。选项包括 NorthWest（西北）、North（北）、NorthEast（东北）、West（西）、Center（中）、East（东）、SouthWest（西南）、South（南）、SouthEast（东南）。 |
| `-implode` _factor_ | 按指定因子使图像像素向中心收缩。选项包括收缩（0-99.9%）或膨胀（-99.9-0%）。 |
| `-interlace` _type_ | 设置交织方案类型。选项包括 None、Line、Plane 或 Partition。 |
| `--label` "string" | 使用指定的字符串作为标签。请务必用双引号将字符串括起来。 |
| `--layer` _type_ | 设置图层类型。选项包括 Red（红）、Green（绿）、Blue（蓝）或 Matte（遮罩）。 |
| `--linewidth` _n_ | 将线宽设置为 _n_ 像素。 |
| `--loop` _n_ | 重复 GIF 动画 _n_ 次。指定 0 表示无限循环。 |
| `--map` _filename_ | 从指定文件名获取颜色集。 |
| `--matte` | 如果图像包含 alpha 通道，则存储 alpha 通道信息。 |
| `--modulate` _brightness, saturation, hue_ | 通过指定百分比的增加或减少来改变亮度、饱和度和色调。省略百分号。 |
| `--monochrome` | 将图像转换为黑白。 |
| `--morph` _image sequence_ | 对图像序列进行变形。 |
| `--negate` | 将每个像素替换为其互补色。 |
| `--noise` _type_ | 使用指定的滤波器类型添加或减少噪声。选项包括 Uniform（均匀）、Gaussian（高斯）、Multiplicative（乘法）、Impulse（脉冲）、Laplacian（拉普拉斯）和 Poisson（泊松）。 |
| `--normalize` | 转换图像并通过跨越全色值范围来增强对比度。 |
| `--opaque` _color_ | 使用指定颜色作为画笔颜色（参见 `--pen`）。 |
| `--page` _width x height [% \| !]_ | 设置图像画布的宽度和高度（以像素为单位）。附加百分号可按百分比调整宽度和高度。附加感叹号可强制指定确切尺寸。对于 PostScript 页面，可用的宽度和高度对应以下页面大小： |

##### 页面大小（续）

| 页面大小 | 宽度 | 高度 |
| :--- | :--- | :--- |
| 11x17 | 792 | 1224 |
| A0 | 2380 | 3368 |
| A1 | 1684 | 2380 |
| A2 | 1190 | 1684 |

#### 选项（续）

| 使用此选项 | 用于执行此操作 |
|---|---|
| `-paint` *半径* | 使用指定半径的圆形笔触模拟油画效果。 |

#### 选项（续）

| 使用此选项 | 用于执行此操作 |
|---|---|
| `-pen` *颜色* | 设置字体颜色或不透明颜色。 |
| `-pointsize` *字号* | 对 PostScript 字体使用指定的字号。 |
| `-preview` *类型* | 使用以下图像预览类型：添加噪声、模糊、亮度、木炭画、去噪点、变暗、边缘检测、伽马值、灰度、色调、脉冲、JPEG（默认）、油画、量化、凸起、减少噪声、滚动、旋转、饱和度、分割、阴影、锐化、错切、增光、扩散、漩涡、阈值和波浪。 |
| `-profile` *字符串* | 通过指定的字符串为图像添加 ICC 颜色或 IPTC 新闻专线信息配置文件。 |
| `-quality` *值* | 设置 JPEG、MIFF 或 PNG 的压缩级别。 |
| `-raise` *宽度 x 高度* | 使用指定的宽度和高度创建 3D 效果。 |
| `-region` *宽度 x 高度* | 将选项应用于由宽度和高度指定的图像区域。 |
| `-roll` *x 偏移量 y 偏移量* | 通过指定的 x 偏移量和 y 偏移量垂直滚动图像。 |
| `-rotate` *度数* `<` 或 `>` | 将图像向左（`<`）或向右（`>`）旋转指定的度数。 |
| `-sample` *宽度 x 高度* `[%]` `![` ]` | 使用像素采样法将图像缩放到指定的最大宽度和高度，同时保持原始图像的宽高比。添加 `%`（百分号）可按百分比调整宽度和高度。添加 `!`（感叹号）可强制使用您指定的尺寸。 |
| `-scene` *n* | 指定图像场景编号 *n*。 |
| `-seed` *值* | 使用指定的值作为伪随机数生成器的种子。 |
| `-segment` *聚类阈值* *平滑阈值* | 使用指定的聚类阈值和平滑阈值对图像进行分割。 |
| `-shade` *方位角* *x* *仰角* | 使用位于指定方位角和仰角的远程光源为图像着色。 |
| `-sharpen` *因子* | 通过指定的因子（0.0 – 99.9%）锐化图像。 |
| `-shear` *x 度数* *x y 度数* | 沿 x 或 y 轴以指定的错切角度错切图像。 |
| `-solarize` *因子* | 取反所有高于指定因子（0–99.9%）所确定的阈值水平的像素。 |
| `-spread` *n* | 将图像像素偏移 *n* 个像素。 |
| `-swirl` *度数* | 围绕中心以指定的度数旋转图像像素。 |
| `-texture` *文件名* | 使用在指定 *文件名* 中找到的纹理作为图像背景。 |
| `-threshold` *值* | 创建二级图像，其中仅显示超过指定值的像素。 |
| `-transparent` *颜色* | 使指定颜色透明。 |
| `-treedepth` *0* | 设置树深度为 0 或 1。 |
| `-units` *类型* | 指定图像分辨率的类型。选项为：未定义、PixelsPerInch（每英寸像素数）或 PixelsPerCentimeter（每厘米像素数）。 |
| `-verbose` | 显示所有消息。 |
| `-view` *字符串* | 使用由 *字符串* 指定的 FlashPix 查看参数。 |
| `-wave` *振幅* *波长* | 沿正弦波改变图像，使用指定的振幅和波长。 |

| 示例 | 执行以下操作 |
|---|---|
| `convert mypicture.gif mypicture.jpg` | 将指定的输入文件（`mypicture.gif`）转换为 JPEG 图形。 |

#### identify

`identify` *文件名*

确定由 *文件名* 指定的图形文件的格式和特征，并检查图像是否不完整或损坏。您可以使用 shell 模式指定多个文件名（参见第 4 章中的“Shell 模式”部分）。使用 `--verbose` 选项可以查看有关每个图形文件的详细信息。此实用程序是 ImageMagick 包的一部分，可从 http://www.imagemagick.org 下载。

另请参阅 `combine`、`convert`、`mogrify`、`montage`。

##### 选项
