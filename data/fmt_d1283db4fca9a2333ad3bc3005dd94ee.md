
如果你想查看你的显卡支持哪些模式，可以编译并运行列表 2.2 中演示的快速脚本。此外，如果你不知道 `144` 是最后一个屏幕模式，你可以使用另一个函数 `vga_lastmodenumber()` 来推导出来。另外，`GLASTMODE` 在 `vga.h` 中定义为 `vga_lastmodenumber()` 的输出。

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

注意这里使用了我们第一个 SVGAlib 函数 `vga_hasmode()`。使用该函数，你可以确定显卡支持哪些模式，并据此进行编程。此外，如果你不知道 `144` 是最后一个屏幕模式，你可以使用另一个函数 `vga_lastmodenumber()` 来推导出来。

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

通过输入一个数字（例如 `5`），你将看到一个展示所选模式颜色范围的显示屏。如果显示效果正常，如图 2.6 所示，你就知道你的显卡支持该模式。如果显示变形或环绕屏幕，你就知道对于该特定显卡应避免使用此模式。

最后，你将获得所选模式的摘要。模式 `5` 的结果显示在列表 2.5 中。

## 列表 2.5 模式 5 的摘要。

```text
Width: 320 Height: 200 Colors: 256
DisplayStartRange: 0h Maxpixels: 65536 BIt: N0
```

## 编译

让我们花点时间讨论如何使用 `gcc`（标准 Linux C 编译器）编译 SVGAlib 程序。基本流程如下：

```bash
gcc -o <output> <input>
```

![](img/2e475714ef8969ed272622c46473d334_60_0.png)

**图 2.6**

`vgatest` 渲染的屏幕模式 5。

例如，如果你的源代码在一个名为 `source.c` 的文件中，并希望编译后的程序命名为 `george`，你需要输入以下内容：

```
gcc -o george source.c
```

现在，为了引入 SVGAlib 的功能，你需要在命令行末尾添加 `-lvgal`，如下所示：

```
gcc -o george source.c -lvgal
```

这告诉 `gcc` 它需要将你的编译程序与 `libvgal.so.1` 链接（参见第 1 章）。如果你还需要 SVGAlib 扩展库中的函数，即 `libvgagl.so.1`（关于 SVGAlib 的这一扩展将在后文详细介绍；如果你现在对此一无所知也不要紧），你需要在命令行中再添加一个标志。但请注意，在链接多个库时，最重要的库必须放在最后。由于 `libvgal.so.1` 比 `libvgagl.so.1` 更重要，你的命令行应该如下所示：

```
gcc -o george source.c -lvgagl -lvgal
```

> **注意**
>
> 当使用 `vgagl` (`libvgagl.so.1`) 进行编译时，必须在 `libvgal.so.1` 之前引用它，例如：`-lvgagl -lvgal`

担心代码中有错误吗？添加 `-Wall`（警告，全部）标志将显示 `gcc` 在你的代码中发现的所有可能问题。

最后，你可以优化编译以使生成的可执行文件运行得更快。你可以通过添加 `-O` 标志来实现这一点。使用 `-O2` 可以获得更好的优化（同时也意味着更大的程序和更长的编译时间）。事实上，你可以一直使用到 `-O3`。

这是我们现在使用所有标志后的结果：

```
gcc -Wall -O3 -o george source.c -lvgagl -lvgal
```

使用这种方法，你可以编译本书中的所有示例。

## VESA
