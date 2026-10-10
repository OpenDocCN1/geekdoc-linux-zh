
## 宽高比

显示器的宽度与高度之比。大多数监视器和电视的宽高比为 4:3。

## VGA 内存中像素的存储方式

在显存中，像素由一个或多个位表示。1 位像素只能容纳两个值（开和关），因此它只适用于黑白图像，例如之前展示的例子。通过增加每个像素的位数，即 *位深度*，可表示的颜色数量就会增加。彩色显示器需要每个像素 4 到 32 位不等。难怪 1600 万种颜色会占用大量内存。

表 2.3 展示了随着每像素位数增加，可表示的颜色数量如何变化。

| 位数 | 颜色数量 |
| :--- | :--- |
| 4 | 16 |
| 8 | 256 |
| 15 | 32,768 |
| 16 | 65,536 |
| 24 | 16,777,216 |
| 32 | 16,777,216 + Alpha 通道 |

## SVGAlib 屏幕模式

够理论示例了，让我们看看 SVGAlib 提供的 145 种屏幕模式。这些是 **/usr/include/vga.h** 中实际存在的所有模式，表 2.4 列出了其中所有模式，并包含颜色信息。如果你在疑惑，开头的 G 简单地指代 *图形模式*。当你使用 SVGAlib 编写程序时，需要使用这些模式之一。

> **注意**
>
> 16M32 表示使用每像素 32 位来表示 1600 万种颜色。

表 2.4 SVGAlib 下可用的屏幕模式。

| 模式编号 | 模式描述 |
| --- | --- |
| 0 | TEXT |
| 1 | G320x200x16 |
| 2 | G640x200x16 |
| 3 | G640x350x16 |
| 4 | G640x480x16 |
| 5 | G320x200x256 |
| 6 | G320x240x256 |
| 7 | G320x400x256 |
| 8 | G360x480x256 |
| 9 | G640x480x2 |
| 10 | G640x480x256 |
| 11 | G800x600x256 |
| 12 | G1,024x768x256 |
| 13 | G1,280x1,024x256 |
| 14 | G320x200x32K |
| 15 | G320x200x64K |
| 16 | G320x200x16M |
| 17 | G640x480x32K |
| 18 | G640x480x64K |
| 19 | G640x480x16M |
| 20 | G800x600x32K |
| 21 | G800x600x64K |
| 22 | G800x600x16M |
| 23 | G1,024x768x32K |
| 24 | G1,024x768x64K |
| 25 | G1,024x768x16M |
| 26 | G1,280x1,024x32K |
| 27 | G1,280x1,024x64K |
| 28 | G1,280x1,024x16M |
| 29 | G800x600x16 |
| 30 | G1,024x768x16 |
| 31 | G1,280x1,024x16 |
| 32 | G720x348x2 |
| 33 | G320x200x16M32 |
| 34 | G640x480x16M32 |
| 35 | G800x600x16M32 |
| 36 | G1,024x768x16M32 |
| 37 | G1,280x1,024x16M32 |
| 38 | G1,152x864x16 |
| 39 | G1,152x864x256 |
| 40 | G1,152x864x32K |
| 41 | G1,152x864x64K |
| 42 | G1,152x864x16M |
| 43 | G1,152x864x16M32 |
| 44 | G1,600x1,200x16 |
| 45 | G1,600x1,200x256 |
| 46 | G1,600x1,200x32K |
| 47 | G1,600x1,200x64K |
| 48 | G1,600x1,200x16M |
| 49 | G1,600x1,200x16M32 |
| 50 | G320x240x256V |
| 51 | G320x240x32K |
| 52 | G320x240x64K |
| 53 | G320x240x16M |
| 54 | G320x240x16M32 |
| 55 | G400x300x256 |
| 56 | G400x300x32K |
| 57 | G400x300x64K |
| 58 | G400x300x16M |
| 59 | G400x300x16M32 |
| 60 | G512x384x256 |
| 61 | G512x384x32K |
| 62 | G512x384x64K |
| 63 | G512x384x16M |
| 64 | G512x384x16M32 |
| 65 | G960x720x256 |
| 66 | G960x720x32K |
| 67 | G960x720x64K |
| 68 | G960x720x16M |
| 69 | G960x720x16M32 |
| 70 | G1,920x1,440x256 |
| 71 | G1,920x1,440x32K |
| 72 | G1,920x1,440x64K |
| 73 | G1,920x1,440x16M |
| 74 | G1,920x1,440x16M32 |
| 75 | G320x400x256V |
| 76 | G320x400x32K |
| 77 | G320x400x64K |
| 78 | G320x400x16M |
| 79 | G320x400x16M32 |
| 80 | G640x400x256 |
| 81 | G640x400x32K |
| 82 | G640x400x64K |
| 83 | G640x400x16M |
| 127 | G2,048x1,152x64K |
| 128 | G2,048x1,152x16M |
| 129 | G2,048x1,152x16M32 |
| 130 | G2,048x1,536x256 |
| 131 | G2,048x1,536x32K |
| 132 | G2,048x1,536x64K |
| 133 | G2,048x1,536x16M |
| 134 | G2,048x1,536x16M32 |
| 135 | G512x480x256 |
| 136 | G512x480x32K |
| 137 | G512x480x64K |
| 138 | G512x480x16M |
| 139 | G512x480x16M32 |
| 140 | G400x600x256 |
| 141 | G400x600x32K |
| 142 | G400x600x64K |
| 143 | G400x600x16M |
| 144 | G400x600x16M32 |

## Alpha 通道

1600 万色像素中额外的 8 位，用作单独图层以表示物体的透明度级别。

如果你想查看你的显卡支持哪些模式，可以编译并运行列表 2.2 中演示的快速脚本。此外，如果你不知道 144 是最后一个屏幕模式，你可以使用另一个函数 `vga_lastmodenumber()` 来推导出来。另外，`GLASTMODE` 在 `vga.h` 中定义为 `vga_lastmodenumber()` 的输出。

## 列表 2.2 我的显卡支持哪些屏幕模式？

```c
#include <stdio.h>
#include <stdlib.h>
#include <vga.h>

int main(void)
{
    int i;

    for (i = 0; i < 145; i++)
    {
        if (vga_hasmode(i) > 0)
        {
            printf("Mode %d is supported.\n", i);
        } else {
            printf("Mode %d is NOT supported.\n", i);
        }
    }

    return 0;
}
```

你可以将此代码命名为 `mode_tester.c` 或你喜欢的其他名称。要编译，请键入以下内容：

```bash
gcc -o mode_tester mode_tester.c -lsvga
```

我稍后解释 `-lsvga` 部分。运行 `mode_tester` 会产生类似列表 2.3 所示的输出。

## 列表 2.3 mode_tester 的示例输出。

```text
Mode 0 is supported.
Mode 1 is supported.
Mode 2 is supported.
Mode 3 is supported.
Mode 4 is supported.
Mode 5 is supported.
...
Mode 139 is NOT supported.
Mode 140 is NOT supported.
Mode 141 is NOT supported.
Mode 142 is NOT supported.
Mode 143 is NOT supported.
Mode 144 is NOT supported.
```

注意这里使用了我们第一个 SVGAlib 函数 `vga_hasmode()`。使用该函数，你可以确定显卡支持哪些模式，并据此进行编程。此外，如果你不知道 144 是最后一个屏幕模式，你可以使用另一个函数 `vga_lastmodenumber()` 来推导出来。

使用 `mode_tester` 程序的替代方法是运行 `vgatest`，它是随 SVGAlib 软件包提供的演示程序之一。列表 2.4 显示了启动 `vgatest` 时发生的情况。

## 列表 2.4 vgatest 的输出。

```text
Choose one of the following video modes:
1: 320x200, 16 colors (4 bitplanes)
2: 640x200, 16 colors (4 bitplanes)
3: 640x350, 16 colors (4 bitplanes)
4: 640x480, 16 colors (4 bitplanes)
5: 320x200, 256 colors (packed-pixel)
6: 320x240, 256 colors (Mode X)
7: 320x400, 256 colors (Mode X)
8: 360x480, 256 colors (Mode X)
9: 640x480, 2 colors (1 bitplane, monochrome)
10: 640x480, 256 colors (packed-pixel, banked)
11: 800x600, 256 colors (packed-pixel, banked)
12: 1024x768, 256 colors (packed-pixel, banked)
17: 640×480, 32K colors (5-5-5 RGB, blue at LSB, banked)
18: 640×480, 64K colors (5-6-5 RGB, blue at LSB, banked)
20: 800×600, 32K colors (5-5-5 RGB, blue at LSB, banked)
21: 800×600, 64K colors (5-6-5 RGB, blue at LSB, banked)
23: 1024×768, 32K colors (5-5-5 RGB, blue at LSB, banked)
24: 1024×768, 64K colors (5-6-5 RGB, blue at LSB, banked)
29: 800×600, 16 colors (4 bitplanes)
30: 1024×768, 16 colors (4 bitplanes)
32: 720×348, 2 colors (1 bitplane, monochrome)
34: 640×480, 16M colors (8-8-8 XRGB, 32-bit pixels, ...)
35: 800×600, 16M colors (8-8-8 XRGB, 32-bit pixels, ...)
36: 1024×768, 16M colors (8-8-8 XRGB, 32-bit pixels, ...)
Enter mode number (1–36): 5
```

通过输入一个数字（例如 5），你将看到一个展示所选模式颜色范围的显示屏。如果显示效果正常，如图 2.6 所示，你就知道你的显卡支持该模式。如果显示变形或环绕屏幕，你就知道对于该特定显卡应避免使用此模式。

最后，你将获得所选模式的摘要。模式 5 的结果显示在列表 2.5 中。

## 列表 2.5 模式 5 的摘要。

```text
Width: 320 Height: 200 Colors: 256
DisplayStartRange: 0h Maxpixels: 65536 BIt: N0
```

## 编译

让我们花点时间讨论如何使用 gcc（标准 Linux C 编译器）编译 SVGAlib 程序。基本流程如下：

```bash
gcc -o <output> <input>
```

![](img/2e475714ef8969ed272622c46473d334_60_0.png)

**图 2.6**
*vgatest* 渲染的屏幕模式 5。

