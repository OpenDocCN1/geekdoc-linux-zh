
```c
            gl_getpixelrgb(x, y, &r, &g, &b);

            draw_cursor(x, y);

            color[19] = gl_rgbcolor(r, g, b);

            gl_fillbox(16, 426, 28, 28, color[19]);

            break;

        case 5:

            flood_fill(x, y, color[19]);

            break;

        default:

            freehand(x, y, color[19]);

    }

}

}
```

六个工具中有五个是外部函数，而“吸管”（它可以将绘图窗口中的任何颜色设为当前颜色）比较简单，因此我直接在那里处理了。请确保在读取颜色值之前移除鼠标光标；否则，你读取到的将是鼠标的颜色而不是屏幕的颜色。

# 画直线

大多数工具的实现应该相当简单。然而，其中较难的一个是直线工具。它看起来可能很直接，但实际上颇具挑战性。任何优秀的绘图程序都会允许你单击鼠标以固定线条的一端，然后让你将另一端拖动到任意所需位置。这种技术比徒手“铅笔”让用户拥有更高的精确度。然而，问题在于，作为程序员的你，在鼠标移动时会绘制多条线条。你当然不希望它们同时出现——你希望一次只绘制一条。可移动的直线让用户能够自信地绘图，但也带来了一些麻烦。你需要能够放置和擦除旧版本的线条，而不干扰其下方的内容。

我对此问题的解决方案是，在绘制线条时存储每个像素。当鼠标移动时（假设左键仍处于按下状态），旧线条会被擦除（实际上，它是用线条最初绘制时读取的数值数组覆盖的），然后放置新线条，并保存一组新的数值。此过程持续进行，直到用户松开按钮。

我承认，我的解释可能让你更加困惑，因此请查看列表 18.7 以查看实际代码。

## 列表 18.7 可移动直线

```c
void line(int x, int y, int color)
{
    int origx = x,
         origy = y;
    int i;

    vga_waitretrace();
    gl_putbox(x, y, 11, 19, box);
    mouse_line(x, y, origx, origy, color);
    gl_getbox(x, y, 11, 19, box);
    draw_cursor(x, y);

    while (button & MOUSE_LEFTBUTTON)
    {
        mouse_update();
        x = mouse_getx();
        y = mouse_gety();
        if (x < LEFT)
        {
            x = LEFT;
            mouse_setposition(x, y);
        }
        if (y < TOP)
        {
            y = TOP;
            mouse_setposition(x, y);
        }
        if (x > RIGHT)
        {
            x = RIGHT;
            mouse_setposition(x, y);
        }
        if (y > BOTTOM)
        {
            y = BOTTOM;
            mouse_setposition(x, y);
        }
        button = mouse_getbutton();

        if ((x != ox) || (y != oy))
        {
            vga_waitretrace();

            gl_putbox(ox, oy, 11, 19, box);
            for (i = 0; i < mouse_oldline_length; i++)
            {
                gl_setpixelrgb(mouse_oldline[i][0],
                               mouse_oldline[i][1],
                               mouse_oldline[i][2],
                               mouse_oldline[i][3],
                               mouse_oldline[i][4]);
            }

            mouse_line(x, y, origx, origy, color);
            gl_getbox(x, y, 11, 19, box);
            draw_cursor(x, y);
            ox = x;
            oy = y;
        }
    }
}

int mouse_line(int x1, int y1, int x2, int y2, int c)
{
    int dx = x2 - x1;
    int dy = y2 - y1;
    int ax = ABS(dx) << 1;
    int ay = ABS(dy) << 1;
    int sx = (dx >= 0) ? 1 : -1;
    int sy = (dy >= 0) ? 1 : -1;

    int x = x1;
    int y = y1;

    mouse_oldline_length = 0;

    if (ax > ay) {
        int d = ay - (ax >> 1);
        while (x != x2) {
            mouse_oldline[mouse_oldline_length][0] = x;
            mouse_oldline[mouse_oldline_length][1] = y;
            gl_getpixelrgb(x, y,
                           &mouse_oldline[mouse_oldline_length][2],
                           &mouse_oldline[mouse_oldline_length][3],
                           &mouse_oldline[mouse_oldline_length][4]);
            mouse_oldline_length++;
            gl_setpixel(x, y, c);

            if (d > 0 || (d == 0 && sx == 1)) {
                y += sy;
                d -= ax;
            }
            x += sx;
            d += ay;
        }
    } else {
        int d = ax - (ay >> 1);
        while (y != y2) {
            mouse_oldline[mouse_oldline_length][0] = x;
            mouse_oldline[mouse_oldline_length][1] = y;
            gl_getpixelrgb(x, y,
                           &mouse_oldline[mouse_oldline_length][2],
                           &mouse_oldline[mouse_oldline_length][3],
                           &mouse_oldline[mouse_oldline_length][4]);
            mouse_oldline_length++;
            gl_setpixel(x, y, c);

            if (d > 0 || (d == 0 && sy == 1)) {
                x += sx;
                d -= ay;
            }
            y += sy;
            d += ax;
        }
    }
}
```

# 量化

将一个大组细分为较小集合的过程。在计算机图形学中，这指的是一种常见的颜色缩减方法，即通过数学方法选择少数几种颜色来代表更大的调色板。

# 读取文件
