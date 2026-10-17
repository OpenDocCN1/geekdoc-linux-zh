
图 4.7 第二个圆弧，以庄严的黑白呈现。

请注意指定以下内容的代码行：

```c
for (degrees = 180; degrees < 270; degrees++)
```

这些代码行将圆弧置于左上角。如果数值范围是 0 到 90，而不是 180 到 270，那么圆弧将位于右下角。

## 椭圆

椭圆，或*椭圆*，可以被视为拉伸的圆。（作为参考，它们的几何布局如图 4.8 所示。）由于这一点，椭圆函数需要四个参数：`xc` 和 `yc` 用于中心点，`rx` 和 `ry` 用于*两个轴*（或半径）。这与圆形成对比，圆只有一个半径。圆的半径可以旋转并触及每一个点，很像自行车辐条。

我再次从图形大师 Michael Abrash 那里借鉴了创建椭圆的方法，如列表 4.9 所示。输出结果如图 4.9 所示。

![](img/2e475714ef8969ed272622c46473d334_97_1.png)

图 4.8 椭圆的机械原理。

### 列表 4.9 一个 Michael Abrash 椭圆。

```c
void book_ellipse(int xc, int yc, int rx, int ry)
{
    int x = 0,
        y = ry;

    long threshold,
        rxsquared = rx * rx,
        rysquared = ry * ry,
        xadjust,
        yadjust;

    vga_drawpixel(xc, yc + ry);
    vga_drawpixel(xc, yc - ry);

    xadjust = 0;
    yadjust = rxsquared * 2 * ry;
    threshold = rxsquared / 4 - rxsquared * ry;

    for (;;)
    {
        threshold += xadjust + rysquared;
        if (threshold >= 0)
        {
            yadjust -= rxsquared * 2;
            threshold -= yadjust;
            y--;
        }

        xadjust += rysquared * 2;
        x++;

        if (xadjust >= yadjust)
        {
            break;
        }

        vga_drawpixel(xc + x, yc - y);
        vga_drawpixel(xc - x, yc - y);
        vga_drawpixel(xc + x, yc + y);
        vga_drawpixel(xc - x, yc + y);
    }

    vga_drawpixel(xc + rx, yc);
    vga_drawpixel(xc - rx, yc);

    x = rx;
    y = 0;
    xadjust = rysquared * 2 * rx;
    yadjust = 0;
    threshold = rysquared / 4 - rysquared * rx;

    for (;;)
    {
        threshold += yadjust + rxsquared;
        if (threshold >= 0)
        {
            xadjust -= rysquared * 2;
            threshold -= xadjust;
            x--;
        }
        yadjust += rxsquared * 2;
        y++;
        if (yadjust >= xadjust)
        {
            break;
        }
        vga_drawpixel(xc + x, yc - y);
        vga_drawpixel(xc - x, yc - y);
        vga_drawpixel(xc + x, yc + y);
        vga_drawpixel(xc - x, yc + y);
    }
}
```

![](img/2e475714ef8969ed272622c46473d334_99_0.png)

图 4.9 正在运行的椭圆。

## Fastball.c

本节以一个我确信你会喜欢的程序结束。`Fastball.c`，如图 4.10 中的列表所示，会在屏幕上绘制旋转的几何图形，其中一些可能非常有趣。很难描述，所以最好自己启动并查看一下。随意玩玩；也许加上你的改进，它将成为 *de facto* SVGAlib 应用程序。通过自定义你的调色板，可以让它特别有趣，下一章将详细描述这个过程。示例输出如图 4.10 所示。

### 列表 4.10 Fastball.c。
