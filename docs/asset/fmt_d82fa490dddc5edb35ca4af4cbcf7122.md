
访问`siliconmechanics.com`或拨打我们的免付费电话。Silicon Mechanics 和 Silicon 标志是 Silicon Mechanics, Inc. 的注册商标。AMD 和 AMD 标志是 Advanced Micro Devices. 的商标，经许可使用。

## Python 2.5

在编写过程中。

# 使用 Qccpack 和 Python 进行图像处理

# 如何使用 QccPack 通过 Python 提示符和代码操纵图像。SUHAS A. DESAI

带宽和存储空间始终是有限的。数据压缩通常是最佳解决方案。在涉及图像处理时，压缩技术分为两类：无损压缩和有损压缩。

`Qccpack` 由 James Fowler 开发，是一个开源库集合，它使用基于小波的量化来实现常用压缩技术的可靠实现。

库正在不断开发中。目前，可以在不修改应用程序代码的情况下使用库。你可以链接到静态库 `libccpack.a`，并通过 `libccpack` 支持动态链接。

`Qccpack` 提供了小波编码、基于小波的带编码、误差编码、图像压缩以及通用算法实现。可以通过库例函数进行操作，`Qccpack` 库中还提供了你可以添加的额外模块。

`QccpackSHIFT` 是用于图像压缩分层树集划分（SPHT）算法的一个可选模块。`QccpackSHIFT` 模块包含两个工具：`splinterencoder` 和 `splinterdecoder`，用于对灰度图像执行 SPHT 编码和解码。

可以从 Sourceforge `Qccpack` 网页下载 `Qccpack` 和 `QccpackSHIFT`。Red 用户可以随时找到源码和二进制 RPM 包。其他用户需要编译源码。`Qccpack` 可以在 Solaris/ARC、HP-UX、Digital Unix Alpha 和 Digital RS/UX 上成功编译。

# 从 Python 提示符使用 Qccpack

你可以使用 `Qccpack` 训练 VQ 码本，并使用算术编码通过全搜索 VQ 解码图像。以一张 512x512 的灰度图像为例，以下示例步骤假设你处于 Python 解释器提示符下。

第 1 ：通过提取像素的四维（二维）向量将 PGM 文件转换为 DAT 格式：

```
>>> imgodat-ts 4 lenna.pgm lenna.40.dat
```

第 2 ：在 DAT 文件上使用 `gla` 训练一个 256 字的 VQ 码本（停止阈值 = 0）；

```
>>> gla -s 256 -t 0.81 lenna.40.dat lenna.256.ckb
```

第 3 ：将 DAT 文件向量化以产生 VQ 索引通道：

```
>>> vencode -d4 lenna.40.dat lenna.40256.ckb lenna.40256.chn
```

第 4 ：计算 VQ 索引的一阶熵（单位为比特/像素）：

```
>>> cherotropy -4 lenna.40256.chn First-order entropy of channel lenna.40256.chn is: 1.82585 (bits/symbol)
```

第 5 ：VQ 索引的算术熵通道：

```
>>> charmeticencode -d 4 lenna.40256.chn
enna.40256.chn
```

通道 `lenna.40256.chn` 算术编码后为: 1.83022

```
>>> rm lenna.40256.chn
```

第 6 ：解码编码通道：

```
>>> charmeticdecode lenna.40256.chn lenna.40256.dat
```

第 7 ：反 VQ 通道以产生数据：

```
>>> vdecode lenna.40256.chn lenna.40256.ckb
enna.40256.dat
```

第 8 ：将 DAT 转换为 PGM 格式：

```
>>> imgist lenna.pgm lenna.402_56.ppm
```

第 9 ：计算原始索引与编码索引之间的距离：

文件 `lenna.pgm.dat` 和 `lenna.40256.image` 之间的失真为：

- 13.841091 (MSE)
- 22.186606 (SNR)

# 广告索引

广告事宜请联系我们的销售部门：1-713-344-1956 分机 2 或发送 `ads@linuxjournal.com`。`www.linuxjournal.com/advertising`

### 列表 1. 将文件转换为 JPEG

```python
import sys
import Image
for infile in sys.argv[1:]:
    outfile = os.path.splitext(infile)[0] + ".jpg"
    if infile != outfile:
        try:
            Image.open(infile).save(outfile)
        except IOError:
            print("cannot convert", infile)
```

### 列表 2. 简单变换

```python
out = im.resize((120, 128))
out = im.rotate(45)
```

36.7190 dB (PSNR)

# Python Imaging Library (PIL)

Python Imaging Library 为 Python 解释器提供了图像处理功能。该库提供了广泛的格式支持，旨在快速访问数据。该库包含许多基本功能，包括使用内置内核进行去滤波和颜色转换。Python Imaging Library 是图像处理和批量处理的理想选择。你可以使用该库创建缩略图、在文件格式和图像之间转换。该库还支持缩放和其他仿变换。此模型允许你添加自己的解码器。这些插件的名称类似于：

## 核心包

Pillow 和 PIL 库对于图像编程至关重要。在 Linux 中运行这些命令进行构建：

```bash
python setup.py build_ext
```

# 使用 Python Imaging Library

Python Imaging Library 中最重要的类是 `Image` 类，它定义在模块中。我们通过从文件加载图像、处理其他图像或从零创建图像来创建其实例。要从文件加载图像，请使用模块中的函数在

| 广告商 | 页码 |
| :--- | :--- |
| ABERNSON, LLC | 93 |
| APHO Solutions | C2 |
| MICROSOFT, INC. | C4, 89 |
| ASA Computers | 63, 67 |
| Max Tech | 53 |
| AVGO CONSULT | 57 |
| Black Heart (Partners) | 77 |
| CARNET | 43 |
| PARASY SYSTEMS | 5 |
| CORAD, INC. | 25 |
| BEYONDSOFT MANAGEMENT | C3 |
| CONTOUR POINT | 15 |
| RIB COLOR TECHNOLOGIES | |
| EMAAC, INC. | 47 |
| SERVICE DIRECT | 69 |
| EMPERORIUM | 21 |
| SILICON MECHANICS | 78, 83 |
| FAXCOR | 29 |
| SUPERMARKET | 13 |
| IRON SYSTEMS | 56 |
| UNITED TECHNOLOGIES | 11 |
| LINUX JOURNAL | 6, 31, 59, 64 |
| USENIX SECURITY SYMPOSIUM | 95 |
| LINUX WORLD SAN FRANCISCO | 73 |
| TECHNOLOGIC SYSTEMS | 35 |
| HURRICANE ELECTRIC | 7 |
| TOTAL VIEW TECHNOLOGIES | |

# Image 模块

```python
>>> import Image
>>> im = Image.open('lena.ppm')
```

Python Imaging Library 支持多种图像格式。该库根据文件内容或扩展名自动确定格式。下一个示例（列表2）显示了 `Image` 类如何包含缩放和旋转图像的方法。

# 颜色转换

Python Imaging Library 允许使用 `convert` 函数在不同的像素表示之间转换图像——例如

```python
im = Image.open('lena.ppm').convert('L')
```

该库支持每个支持的模式与 RGB 模式之间的转换。要在其他模式之间转换，你可能需要使用中间图像。

# 过滤器
