
### 列表 6.3（续）

```c
for (j = 0; j < COLORS; j++)
{
    gl_setpalettecolor(j, &r, &g, &b);
    r = (r - 1) >= 0 ? (r - 1) : r;
    g = (g - 1) >= 0 ? (g - 1) : g;
    b = (b - 1) >= 0 ? (b - 1) : b;
    gl_setpalettecolor(i, r, g, b);
}
usleep(75000);
```

如果你决定在一个示例程序中测试列表 6.3，请注意，如果你决定使用 256 色模式，记得声明 `gl_setrgbpalette()`。此外，绘制屏幕的方式也要小心。为了测试目的，请尝试以下代码：

```c
gl_setpalettecolor(color, r, g, b);
gl_fillbox(0, 0, xmax, ymax, color);
```

然而，类似以下的代码将不起作用：

```c
color = gl_rgbcolor(r, g, b);
gl_fillbox(0, 0, xmax, ymax, color);
```

你能想明白这是为什么吗？

最后，经过所有这些工作，你可能会失望地发现，你的淡入淡出效果伴随着一定量的屏幕闪烁。通过与屏幕的垂直消隐同步来修正调色板更改，可以解决此问题（更多详情请参阅第 10 章）。

## 渐变的更多乐趣

在第 4 章中，你学会了如何绘制一个实心圆，这是 SVGAlib 尚未提供的功能。在第 5 章中，我向你展示了如何绘制一个简单的渐变屏幕。将这两者结合，你可以纯粹使用 2D 技术创造出 3D 图像的错觉。

你也许会像我感觉到的那样，觉得纯色圆圈有点无聊。它们是扁平的、枯燥的，完全无法激发我的兴趣。事实上，SVGAlib 的圆圈让我想起一首乔治·哈里森的老歌：“他们的生活中缺少些什么/他们需要一次彻底的教训。”

为了解决这个问题，你可以施加大量的阴影效果，使你的圆圈更加生动和吸引人。如果你做得正确，最终的效果看起来相当清晰。因此，列表 6.4 演示了制作渐变圆的一种方法，其概念类似于第 5 章中的渐变屏幕。然而，与从上到下移动不同，圆圈的色调会随着从外缘向中心推进而逐渐变亮。我通过一系列 `gl_setpalettecolor()` 和 `book_fillcircle()` 语句实现了这种效果。

更具体地说，我在一个圆圈上叠加了另一个圆圈，使序列中的每个圆圈都比前一个更小、更亮。这听起来可能很原始，但错觉确实有效——它实际上看起来相当无缝。你当然可以假设向该函数传递额外的参数，以便让任意一种颜色变成另一种颜色，但我已经满足于白色和红色。请注意，我还包括了第 4 章中的 `book_fillcircle()` 函数。

### 列表 6.4 红到白的渐变圆。

```c
void red_gradient_circle(int xc, int yc, int radius)
{
    int a,
        b,
        i,
        j = 0,
        color = 1;

    if (radius < 64)
    {
        a = 64 / radius;

        for (i = 0; i <= 63; i += a)
        {
            gl_setpalettecolor(color, 63, i, i);
            book_fillcircle(xc, yc, (radius - i), color);
            color = (color + 1 < 64) ? color + 1 : color;
        }
    } else if (radius > 64) {
        a = radius / 55;
        b = radius % 55;

        if (((b > 5) && (b < 11)) || (b > 50))
        {
            a++;
        }

        for (i = 0; i < radius; i += a)
        {
            gl_setpalettecolor(color, 63, j, j);
            book_fillcircle(xc, yc, (radius - i), color);
            color = (color + 1 < 64) ? color + 1 : color;
            j = (j + 1 < 64) ? j + 1 : j;
        }
    } else {
        for (i = 0; i <= 63; i++)
        {
            j = (i < 63) ? 1 : 63;
            gl_setpalettecolor(color, 63, j, j);
            book_fillcircle(xc, yc, (radius - i), color);
            color = (color + 1 < 64) ? color + 1 : color;
        }
    }
}

void book_fillcircle(int sx, int sy, int r, int c)
/* 来自列表 4.6 */
{
    int x = 0,
        y = r,
        d = 1 - r;

    if (r < 1) {
        gl_setpixel(sx, sy, c);
        return;
    }

    gl_hline(sx - x, sy + y, sx + x, c);
    gl_hline(sx - x, sy - y, sx + x, c);
    gl_hline(sx - y, sy + x, sx + y, c);
    gl_hline(sx - y, sy - x, sx + y, c);
    while (x < y)
    {
        if (d < 0)
        {
            d = x * 2 + 3;
        } else {
            d = x * 2 - y * 2 + 5;
            y--;
        }
        x++;
        gl_hline(sx - x, sy + y, sx + x, c);
        gl_hline(sx - x, sy - y, sx + x, c);
        gl_hline(sx - y, sy + x, sx + y, c);
        gl_hline(sx - y, sy - x, sx + y, c);
    }
}
```

这提供了一种有趣的效果，但它看起来并不完全真实。光线似乎从不直接落在中心，不是吗？为了创造球体（或 3D 圆圈）的错觉，有必要偏移亮点。这可能很棘手，因为“照亮”区域需要足够大以便可见，但它不能延伸到圆圈的边缘之外。

列表 6.5 展示了我用于红色伪球体的代码。它没有什么特别之处，但看起来很逼真。请记住，这个效果也需要 `book_fillcircle()`。你可以在图 6.1 中看到成品效果的示例。

### 列表 6.5 廉价的 3D 效果。

```c
void threed_circle(int xc, int yc, int radius)
{
    int a,
        b,
        i,
        j = 0,
        color = 1;

    if (radius < 56)
    {
        gl_setpalettecolor(color, 63, j, j);
        book_fillcircle(xc, yc, radius, color);
        xc += (radius / 4);
        yc -= (radius / 4);
        radius *= .60;

        a = 64 / radius;
        color++;
        if (radius < 16)
        {
            j = 20;
        } else if (radius < 37) {
            j = 15;
        }

        for (i = 0; i <= 63; i += a)
        {
            gl_setpalettecolor(color, 63, j, j);
            book_fillcircle(xc, yc, (radius - i), color);
            color = (color + 1 < 64) ? color + 1 : color;
            j = (j + 3 <= 63) ? j + 3 : 63;
        }
    } else if (radius > 110) {
        gl_setpalettecolor(color, 63, j, j);
        book_fillcircle(xc, yc, radius, color);
        xc += (radius / 4);
        yc -= (radius / 4);
        radius *= .60;

        a = radius / 55;
        b = radius % 55;

        if (((b > 5) && (b < 11)) || (b >= 50))
        {
            a++;
        }

        for (i = 0; i < radius; i += a)
        {
            gl_setpalettecolor(color, 63, j, j);
            book_fillcircle(xc, yc, (radius - i), color);
            color = (color + 1 < 64) ? color + 1 : color;
            j = (j + 1 <= 63) ? j + 1 : 63;
        }
    } else {
        gl_setpalettecolor(color, 63, j, j);
        book_fillcircle(xc, yc, radius, color);
        xc += (radius / 4);
        yc -= (radius / 4);
        radius *= .65;

        for (i = 0; i <= 63; i++)
        {
            gl_setpalettecolor(color, 63, j, j);
            book_fillcircle(xc, yc, (radius - i), color);
            color = (color + 1 < 64) ? color + 1 : color;
            j = (j + 1 <= 63) ? j + 1 : 63;
        }
    }
}
```

## 抗锯齿

尽管名字很长，*抗锯齿*（antialiasing）却相当简单。简而言之，它指的是“平滑”斜线粗糙边缘的过程。

![](img/2e475714ef8969ed272622c46473d334_129_0.png)

**图 6.1** 伪球体。

到了这个时候，我相信你肯定会痛苦地意识到，虽然 SVGAlib 中的垂直和水平线看起来很好，但斜线却让人难以满意。这是屏幕矩阵系统的一个不幸事实，在低分辨率模式下尤其令人痛苦。问题在于，在大多数矩阵中，根本没有足够的像素来准确表示斜线。因此，你只能得到一个粗糙的近似值，伴随着锯齿状的边缘（或*锯齿*）。这种缺陷在许多其他系统中也很常见（也就是说，它不是 Linux 或 SVGAlib 固有的，而是实际上发生在任何拥有屏幕矩阵的地方），通常也被称为*阶梯效应*。请参阅图 6.2 查看示例。

但是，*抗锯齿*这个名字是怎么回事呢？具有粗糙边缘的线条或形状被称为*别名的*（aliased）。因此，补偿这种缺陷的线条或形状被称为*去别名的*（antialiased）。

我们将使用的技术是将锯齿状物体周围的一些像素渲染为介于物体颜色和背景颜色之间的色调。这提供了一种临时混合效果，在高分辨率下（即在 640×480 屏幕模式或更高）相当有效。即使在低分辨率下，它通常也比没有好，尽管结果图像可能看起来模糊。请查看图 6.3 以获得更好的“描述”。

### 朴素方法

实现“去别名”线条（或其他形状）的最简单方法只是并行绘制三条线，其中两条边界线比中心线着色更浅。例如，假设你想使用颜色 *a* 来绘制线条，而背景是颜色 *c*。你会先绘制两条着色为 *b* 的“缓冲”线，*b* 是 *a* 和 *c* 色调之间的中间色。然后，在放置中心线之后，你就拥有了去别名的效果。你还可以绘制

![](img/2e475714ef8969ed272622c46473d334_130_0.png)

![](img/2e475714ef8969ed272622c46473d334_130_1.png)

