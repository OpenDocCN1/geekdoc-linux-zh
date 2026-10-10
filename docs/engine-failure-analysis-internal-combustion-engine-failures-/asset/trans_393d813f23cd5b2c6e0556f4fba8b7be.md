

## 选项（续）

| 使用此选项 | 以执行此操作 |
| :--- | :--- |
| `--negate` | 将每个像素替换为其互补色。 |
| `--noise` *type* | 使用指定的滤波器类型添加或减少噪声。可选值有：均匀分布、高斯分布、乘性、脉冲、拉普拉斯、泊松。 |
| `--normalize` | 通过扩展完整的颜色值范围来转换图像并增强对比度。 |
| `-opaque` *color* | 为画笔使用指定的颜色（参见 `--pen`）。 |
| `-page` *宽 x 高* `[ % ] | !` | 设置图像画布的宽度和高度（像素）。附加 `%`（百分号）可按百分比调整宽度和高度。附加 `!`（感叹号）可强制设置确切尺寸。 |

Postscript 页面的选项为

| 页面尺寸 | 宽度 | 高度 |
| :--- | :--- | :--- |
| **11x17** | **792** | **1224** |
| A0 | 2380 | 3368 |
| A1 | 1684 | 2380 |
| A2 | 1190 | 1684 |
| A3 | 842 | 1190 |
| A4 | 595 | 842 |
| A4Small | 595 | 842 |
| A5 | 421 | 595 |
| A6 | 297 | 421 |
| A7 | 210 | 297 |
| A8 | 148 | 210 |
| A9 | 105 | 148 |
| A10 | 74 | 105 |
| ArchA | 648 | 864 |
| ArchB | 864 | 1296 |
| ArchC | 1296 | 1728 |
| ArchD | 1728 | 2592 |
| ArchE | 2592 | 3456 |
| B0 | 2836 | 4008 |
| B1 | 2004 | 2836 |
| B2 | 1418 | 2004 |
| B3 | 1002 | 1418 |
| B4 | 709 | 1002 |
| B5 | 501 | 709 |
| C0 | 2600 | 3677 |
| C1 | 1837 | 2600 |
| C2 | 1298 | 1837 |
| C3 | 918 | 1298 |
| C4 | 649 | 918 |
| C5 | 459 | 649 |
| C6 | 323 | 459 |
| Flsa | 612 | 936 |
| Flse | 612 | 936 |
| HalfLetter | 396 | 612 |
| Ledger | 1224 | 792 |
| Legal | 612 | 1008 |
| Letter | 612 | 792 |
| LetterSmall | 612 | 792 |

| 使用此选项 | 以执行此操作 |
| :--- | :--- |
| `+paint radius` | 使用指定半径的圆形笔触模拟油画效果。 |
| `+pen color` | 设置字体或不透明色的颜色。 |
| `+pointsize point` | 使用指定的点大小作为 PostScript 字体大小。 |
| `+quality n` | 设置 JPEG、MIFF 或 PNG 的压缩级别。对于 JPEG 图形，质量范围从 0（最差）到 100（最佳）。默认值为 75。 |
| `+raise width x height` | 使用指定的宽度和高度创建 3D 效果。 |
| `+region width x height[+ | - x 偏移量] [+ | - y 偏移量]` | 将选项应用于由宽度和高度指定的图像区域。 |
| `+roll x 偏移量 y 偏移量` | 按指定的 x 偏移量和 y 偏移量在垂直方向滚动图像。 |
| `+rotate 度数 < | >` | 按指定的度数向左 (`<`) 或向右 (`>`) 旋转图像。 |
| `+sample 宽 x 高 [ % | ! ]` | 使用像素采样将图像缩放到指定的最大宽度和高度，同时保持原始图像的宽高比。附加 `%`（百分号）可按百分比调整宽度和高度。要强制使用指定的尺寸，请附加 `!`（感叹号）。 |
| `–scene n` | 指定图像场景编号 *n*。 |
| `–seed value` | 使用指定的值作为伪随机数生成器的种子。 |
| `–segment 簇阈值 x 平滑阈值` | 使用指定的簇阈值和平滑阈值对图像进行分割。 |
| `–shade 方位角 x 仰角` | 使用指定方位角和仰角的远距离光源对图像进行着色。 |
| `–sharpen 系数` | 按指定的系数（0.0–99.9%）锐化图像。 |
| `–shear x 度数 x y 度数` | 沿 x 轴或 y 轴按指定的剪切角对图像进行剪切。 |
| `–solarize 系数` | 取反所有高于由系数（0–99.9%）指定的阈值水平的像素。 |
| `–spread n` | 将图像像素移动 *n* 个像素。 |
| `–swirl 度数` | 围绕中心按指定的度数旋涡图像像素。 |
| `–texture 文件名` | 使用指定*文件名*中找到的纹理作为图像背景。 |
| `–threshold n` | 创建二值图像，其中仅显示超过指定值的像素。 |
| `–transparency color` | 使指定的颜色透明。 |
| `–treedepth n` | 为颜色减少算法的最优树深度设置树深度 0 或 1。这是默认设置。指定 2 到 8 之间的整数以尝试计算量更大的树深度渲染。此选项需要 `–colors` 或 `–monochrome` 选项。 |
| `–units type` | 指定图像分辨率的类型。可选值有：未定义、PixelsPerInch（每英寸像素数）或 PixelsPerCentimeter（每厘米像素数）。 |
| `–verbose` | 显示所有消息。 |
| `–view string` | 使用由 *string* 指定的 FlashPix 查看参数。 |
| `–wave 振幅 波长` | 按指定的振幅和波长沿正弦波改变图像。 |

## 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| ``` <br> mogrify -format jpeg <br> image1.bmp image1.jpg <br> ``` | 将 *image1.bmp* 转换为 *image1.jpg*。 |
| ``` <br> mogrify 'vid:* .jpg' <br> catalog.jpg <br> ``` | 创建工作目录中所有 *.jpg* 文件的可视化目录，并将输出写入 *catalog.jpg*。 |

## montage（镶嵌组合）

```
montage [ 选项 ] 输入文件名 输出文件
```

将两个或多个输入文件名转换为合成图像，其中源图像在独立的瓦片中显示（对比 *combine*）。此实用程序是 ImageMagick 包的一部分，可从 [http://www.imagemagick.org](http://www.imagemagick.org) 下载。

> 另请参阅 *convert*、*identify*、*mogrify*。

### 选项

| 使用此选项 | 以执行此操作 |
| :--- | :--- |
| `-adjoin` | 将图像合并到单个多图像文件中。 |
| `-blur 系数` | 按指定的系数（0.0–99.9%）模糊图像。 |
| `-colorspace type` | 设置颜色空间类型。可选值有：CMYK、GRAY、OHTA、RGB、Transparent、XYZ、YCbCr、YIQ、YPbPr 和 YUV。 |
| `--colors n` | 将首选颜色深度设置为 *n*（8 或 16）。 |
| `--comment string` | 使用指定的 *string* 为图像添加注释。可以使用以下扩展符号： |
| `%b` | 文件大小。 |
| `%d` | 目录。 |
| `%e` | 文件扩展名。 |
| `%f` | 文件名。 |
| `%h` | 高度。 |
| `%m` | Magick。 |
| `%p` | 页码。 |
| `%s` | 场景编号。 |
| `%t` | 文件名顶部。 |
| `%w` | 宽度。 |
| `%x` | X 分辨率。 |
| `%y` | Y 分辨率。 |
| `\n` | 换行符。 |
| `\r` | 回车符。 |
| `--compress type` | 设置图像压缩类型。可选值有：BZip、Fax、Group4、JPEG、LZW、RunlengthEncoded、None、Zip。 |
| `--contrast`，`+contrast` | 增强 (`--contrast`) 或降低 (`+contrast`) 图像对比度。 |
| `--crop 宽 x 高` | 在指定的宽度和高度处裁剪图像。 |
| `--cycle n` | 按指定量（*n*）移动图像颜色映射。 |
| `--density <宽>x<高>` | 设置图像的垂直和水平分辨率（像素）。 |
| `--density 宽 x 高` | 将图像的垂直和水平分辨率设置为指定的宽度和高度（像素）。 |
| `--depth value` | 设置图像的颜色深度（8 或 16）。 |
| `--despeckle` | 减少图像中的斑点。 |
| `-dispose type` | 使用指定类型的 GIF 处置。可选值有：<br>0 无处置。<br>1 帧之间不处置。<br>2 用背景色覆盖帧。<br>3 用前一帧覆盖。 |
| `-draw string` | 用一个或多个图元为图像添加注释。图元包括以下项：circle、color、ellipse、fillCircle、fillEllipse、fillPolygon、fillRectangle、image、line、matte、point、polygon、rectangle 和 text。 |
| `-font 字体` | 设置普通文本的字体。 |
| `-frame 宽 × 高 + 外部斜边宽度 + 内部斜边宽度` | 使用带有指定宽度、高度、外部斜边宽度和内部斜边宽度的装饰性边框。 |
| `-gamma n` | 使用指定级别（*n*）的伽马校正，其中 *n* 是从 0.8 到 2.3 的级别。 |
| `-geometry 宽 × 高 [ % | ! | +− × 偏移量 | +− − y 偏移量 ]` | 按指定的最大宽度和高度创建图像，同时保持原始图像的宽高比。附加 `%`（百分号）可按百分比调整宽度和高度。要强制使用指定的尺寸，请附加 `!`（感叹号）。 |
| `-gravity type` | 设置图像引力朝向的方向。可选值有：NorthWest、North、NorthEast、West、Center、East、SouthWest、South 和 SouthEast。 |
| `-interlace type` | 设置交织方案类型。可选值有：None、Line、Plane 或 Partition。 |
| `-label string` | 使用 *string* 作为标签。 |
| `-matte` | 如果图像具有 matte 通道信息，则存储该信息。 |

