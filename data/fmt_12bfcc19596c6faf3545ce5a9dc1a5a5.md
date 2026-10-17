
```c
gl_fillbox(30, y, 20, 20, color[(l(* 2) + 1)]);
gl_hline(30, y, 49, color[18]);
gl_hline(31, (y + 1), 48, color[0]);
gl_hline(31, (y + 19), 49, color[7]);
gl_line(30, (y + 1), 30, (y + 19), color[18]);
gl_line(31, (y + 2), 31, (y + 18), color[0]);
gl_line(49, (y + 1), 49, (y + 18), color[7]);
}

gl_line(29, 250, 29, 417, color[15]);
gl_line(50, 250, 50, 417, color[15]);

/* 绘制当前颜色 */
y = 424;
gl_fillbox(16, 426, 28, 28, color[19]);
gl_hline(14, y, 44, color[18]);
gl_hline(15, (y + 1), 43, color[0]);
gl_hline(15, (y + 30), 44, color[7]);
gl_line(14, (y + 1), 14, (y + 30), color[18]);
gl_line(15, (y + 2), 15, (y + 29), color[0]);
gl_line(44, (y + 1), 44, (y + 29), color[7]);
gl_hline(14, (y + 31), 45, color[15]);
gl_line(45, y, 45, (y + 30), color[15]);

/* 绘制绘图区域 */
gl_fillbox(LEFT, TOP, BOX_WIDTH, BOX_HEIGHT, color[15]);
gl_hline(60, 25, 618, color[18]);
gl_hline(61, 26, 617, color[0]);
gl_hline(61, 458, 618, color[18]);
gl_hline(60, 459, 619, color[15]);
gl_line(60, 26, 60, 458, color[18]);
gl_line(61, 27, 61, 457, color[0]);
gl_line(618, 26, 618, 457, color[7]);
gl_line(619, 25, 619, 458, color[15]);
}

void move_cursor(int x, int y, int ox, int oy)
{
    vga_waitretrace();
    gl_putbox(ox, oy, 11, 19, box);
    gl_getbox(x, y, 11, 19, box);
    draw_cursor(x, y);
}

void draw_cursor(int x, int y)
{
    int w = vga_setegacolor(15);
    int b = vga_setegacolor(0);

    gl_setpixel(x, y, b);                /* 第 1 行 */
    gl_hline(x, (y + 1), (x + 1), b); /* 第 2 行 */
    gl_setpixel(x, (y + 2), b);    /* 第 3 行 */
    gl_setpixel((x + 1), (y + 2), w); 
    gl_setpixel((x + 2), (y + 2), b); 
    gl_setpixel(x, (y + 3), b);            /* 第 4 行 */
    gl_hline((x + 1), (y + 3), (x + 2), w); 
    gl_setpixel((x + 3), (y + 3), b); 
    gl_setpixel(x, (y + 4), b);    /* 第 5 行 */
    gl_hline((x + 1), (y + 4), (x + 3), w); 
    gl_setpixel((x + 4), (y + 4), b); 
    gl_setpixel(x, (y + 5), b);            /* 第 6 行 */
    gl_hline((x + 1), (y + 5), (x + 4), w); 
    gl_setpixel((x + 5), (y + 5), b); 
    gl_setpixel(x, (y + 6), b);            /* 第 7 行 */
    gl_hline((x + 1), (y + 6), (x + 5), w); 
    gl_setpixel((x + 6), (y + 6), b); 
    gl_setpixel(x, (y + 7), b);            /* 第 8 行 */
    gl_hline((x + 1), (y + 7), (x + 6), w); 
    gl_setpixel((x + 7), (y + 7), b); 
    gl_setpixel(x, (y + 8), b);            /* 第 9 行 */
    gl_hline((x + 1), (y + 8), (x + 7), w); 
    gl_setpixel((x + 8), (y + 8), b); 
    gl_setpixel(x, (y + 9), b);            /* 第 10 行 */
    gl_hline((x + 1), (y + 9), (x + 8), w); 
    gl_setpixel((x + 9), (y + 9), b); 
    gl_setpixel(x, (y + 10), b); /* 第 11 行 */
    gl_hline((x + 1), (y + 10), (x + 5), b); 
    gl_setpixel((x + 6), (y + 10), (x + 10), b); 
    gl_setpixel(x, (y + 11), b); /* 第 12 行 */
    gl_hline((x + 1), (y + 11), (x + 2), w); 
    gl_setpixel((x + 3), (y + 11), b); 
    gl_hline((x + 4), (y + 11), (x + 5), w); 
    gl_setpixel((x + 6), (y + 11), b); 
    gl_setpixel(x, (y + 12), b); /* 第 13 行 */
    gl_setpixel((x + 1), (y + 12), w); 
    gl_setpixel((x + 2), (y + 12), b); 
    gl_setpixel((x + 4), (y + 12), b); 
    gl_hline((x + 5), (y + 12), (x + 6), w); 
    gl_setpixel((x + 7), (y + 12), b); 
    gl_hline(x, (y + 13), (x + 1), b); /* 第 14 行 */
    gl_setpixel((x + 4), (y + 13), b); 
    gl_hline((x + 5), (y + 13), (x + 6), w); 
    gl_setpixel((x + 7), (y + 13), b);
    gl_setpixel(x, (y + 14), b); /* 第 15 行 */
    gl_setpixel((x + 5), (y + 14), b);
    gl_hline((x + 6), (y + 14), (x + 7), w);
    gl_setpixel((x + 8), (y + 14), b);
    gl_setpixel((x + 5), (y + 15), b); /* 第 16 行 */
    gl_hline((x + 6), (y + 15), (x + 7), w);
    gl_setpixel((x + 8), (y + 15), b);
    gl_setpixel((x + 6), (y + 16), b); /* 第 17 行 */
    gl_hline((x + 7), (y + 16), (x + 8), w);
    gl_setpixel((x + 9), (y + 16), b);
    gl_setpixel((x + 6), (y + 17), b); /* 第 18 行 */
    gl_hline((x + 7), (y + 17), (x + 8), w);
    gl_setpixel((x + 9), (y + 17), b);
    gl_hline((x + 7), (y + 18), (x + 8), b); /* 第 19 行 */
}

void tool0_up()
/* 自由手绘 */
{
int ybase = 75;
int w = vga_setegacolor(15); /* 白色 */
int b = vga_setegacolor(0); /* 黑色 */
int l = gl_rgbcolor(240, 240, 240); /* 浅灰色 */
int g = gl_rgbcolor(130, 130, 130); /* 深灰色 */

gl_hline(4, ybase, 28, w);
gl_line(4, (ybase + 1), 4, (ybase + 24), w);
gl_hline(5, (ybase + 1), 27, l);
gl_line(5, (ybase + 2), 5, (ybase + 23), l);
gl_hline(5, (ybase + 24), 28, g);
gl_line(28, (ybase + 1), 28, (ybase + 23), g);
gl_hline(4, (ybase + 25), 29, b);
gl_line(29, ybase, 29, (ybase + 24), b);
gl_fillbox(15, 86, 3, 3, b);
}

void tool0_down()
/* 自由手绘 */
{
int ybase = 75;
int w = vga_setegacolor(15); /* 白色 */
int b = vga_setegacolor(0); /* 黑色 */
int l = gl_rgbcolor(240, 240, 240); /* 浅灰色 */
int g = gl_rgbcolor(130, 130, 130); /* 深灰色 */

    gl_hline(4, ybase, 28, b);
    gl_line(4, (ybase + 1), 4, (ybase + 24), b);
    gl_hline(5, (ybase + 1), 27, g);
    gl_line(5, (ybase + 2), 5, (ybase + 23), g);
    gl_hline(5, (ybase + 24), 28, l);
    gl_line(28, (ybase + 1), 28, (ybase + 23), l);
    gl_hline(4, (ybase + 25), 29, w);
    gl_line(29, ybase, 29, (ybase + 24), w);
    gl_fillbox(15, 86, 3, 3, b);
    }

void tool1_up()
/* 直线 */
{
    int ybase = 75;
    int w = vga_setegacolor(15); /* 白色 */
    int b = vga_setegacolor(0); /* 黑色 */
    int l = gl_rgbcolor(240, 240, 240); /* 浅灰色 */
    int g = gl_rgbcolor(130, 130, 130); /* 深灰色 */

    gl_hline(30, ybase, 54, w);
    gl_line(30, (ybase + 1), 30, (ybase + 24), w);
    gl_hline(31, (ybase + 1), 53, l);
    gl_line(31, (ybase + 2), 31, (ybase + 23), l);
    gl_hline(31, (ybase + 24), 54, g);
    gl_line(54, (ybase + 1), 54, (ybase + 23), g);
    gl_hline(30, (ybase + 25), 55, b);
    gl_line(55, ybase, 55, (ybase + 24), b);
    gl_line(35, 95, 50, 80, b);
    }

void tool1_down()
/* 直线 */
{
    int ybase = 75;
    int w = vga_setegacolor(15); /* 白色 */
    int b = vga_setegacolor(0); /* 黑色 */
    int l = gl_rgbcolor(240, 240, 240); /* 浅灰色 */
    int g = gl_rgbcolor(130, 130, 130); /* 深灰色 */

    gl_hline(30, ybase, 54, b);
    gl_line(30, (ybase + 1), 30, (ybase + 24), b);
    gl_hline(31, (ybase + 1), 53, g);
    gl_line(31, (ybase + 2), 31, (ybase + 23), g);
    gl_hline(31, (ybase + 24), 54, l);
    gl_line(54, (ybase + 1), 54, (ybase + 23), l);
    gl_hline(30, (ybase + 25), 55, w);
    gl_line(55, ybase, 55, (ybase + 24), w);
    gl_line(35, 95, 50, 80, b);
}

void tool2_up()
/* 矩形 */
{
int ybase = 101;
int w = vga_setegacolor(15);         /* 白色 */
int b = vga_setegacolor(0);          /* 黑色 */
int l = gl_rgbcolor(240, 240, 240); /* 浅灰色 */
int g = gl_rgbcolor(130, 130, 130); /* 深灰色 */

gl_hline(4, ybase, 28, w);
gl_line(4, (ybase + 1), 4, (ybase + 24), w);
gl_hline(5, (ybase + 1), 27, l);
gl_line(5, (ybase + 2), 5, (ybase + 23), l);
gl_hline(5, (ybase + 24), 28, g);
gl_line(28, (ybase + 1), 28, (ybase + 23), g);
gl_hline(4, (ybase + 25), 29, b);
gl_line(29, ybase, 29, (ybase + 24), b);
gl_hline(9, 108, 24, b);
gl_line(9, 109, 9, 118, b);
gl_hline(9, 119, 24, b);
gl_line(24, 109, 24, 118, b);
}

void tool2_down()
/* 矩形 */
{
int ybase = 101;
int w = vga_setegacolor(15);         /* 白色 */
int b = vga_setegacolor(0);          /* 黑色 */
int l = gl_rgbcolor(240, 240, 240); /* 浅灰色 */
int g = gl_rgbcolor(130, 130, 130); /* 深灰色 */

gl_hline(4, ybase, 28, b);
gl_line(4, (ybase + 1), 4, (ybase + 24), b);
gl_hline(5, (ybase + 1), 27, g);
gl_line(5, (ybase + 2), 5, (ybase + 23), g);
gl_hline(5, (ybase + 24), 28, l);
gl_line(28, (ybase + 1), 28, (ybase + 23), l);
gl_hline(4, (ybase + 25), 29, w);
gl_line(29, ybase, 29, (ybase + 24), w);
gl_hline(9, 108, 24, b);
gl_line(9, 109, 9, 118, b);
gl_hline(9, 119, 24, b);
gl_line(24, 109, 24, 118, b);
}

void tool3_up()
/* 圆形 */
{
    int ybase = 101;
    int w = vga_setegacolor(15);      /* 白色 */
    int b = vga_setegacolor(0);       /* 黑色 */
    int l = gl_rgbcolor(240, 240, 240); /* 浅灰色 */
    int g = gl_rgbcolor(130, 130, 130); /* 深灰色 */

    gl_hline(30, ybase, 54, w);
    gl_line(30, (ybase + 1), 30, (ybase + 24), w);
    gl_hline(31, (ybase + 1), 53, l);
    gl_line(31, (ybase + 2), 31, (ybase + 23), l);
    gl_hline(31, (ybase + 24), 54, g);
    gl_line(54, (ybase + 1), 54, (ybase + 23), g);
    gl_hline(30, (ybase + 25), 55, b);
    gl_line(55, ybase, 55, (ybase + 24), b);
    gl_circle(42, 113, 8, b);
}

void tool3_down()
/* 圆形 */
{
    int ybase = 101;
    int w = vga_setegacolor(15);      /* 白色 */
    int b = vga_setegacolor(0);       /* 黑色 */
    int l = gl_rgbcolor(240, 240, 240); /* 浅灰色 */
    int g = gl_rgbcolor(130, 130, 130); /* 深灰色 */

    gl_hline(30, ybase, 54, b);
    gl_line(30, (ybase + 1), 30, (ybase + 24), b);
    gl_hline(31, (ybase + 1), 53, g);
    gl_line(31, (ybase + 2), 31, (ybase + 23), g);
    gl_hline(31, (ybase + 24), 54, l);
    gl_line(54, (ybase + 1), 54, (ybase + 23), l);
    gl_hline(30, (ybase + 25), 55, w);
    gl_line(55, ybase, 55, (ybase + 24), w);
    gl_circle(42, 113, 8, b);
}

void tool4_up()
/* 吸管 */
```
