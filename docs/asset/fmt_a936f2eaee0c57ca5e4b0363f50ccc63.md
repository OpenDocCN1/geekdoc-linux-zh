
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

`List 6.5` 展示了我用于红色伪球体的代码。它没有什么特别之处，但看起来很逼真。请记住，这个效果也需要 `book_fillcircle()`。你可以在图 `6.1` 中看到成品效果的示例。

### 列表 6.5 廉价的 3D 效果。
