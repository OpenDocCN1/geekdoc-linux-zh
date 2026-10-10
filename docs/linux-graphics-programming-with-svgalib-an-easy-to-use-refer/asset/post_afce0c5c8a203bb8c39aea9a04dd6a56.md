
## A Better Method

A more efficient and effective method for antialiasing a line would be to draw the “buffer” pixels at the same time that the main line (or shape) is being drawn. Listing 6.6 shows one way of doing this, using the basic formula found in `vga_drawline()` combined with the faster vgal drawing functions. As each primary pixel is painted, the surrounding pixels are then shaded accordingly. The buffer pixels are either placed to the left and right of the main pixel or else above and below, based on the slope of the line.

To improve overall quality, the color value of each buffer pixel is determined before it’s drawn, which allows for a multicolored background. This can get tricky, however, when you consider that `gl_getpalettecolor()` normally uses the 64-color scale, whereas `gl_getpixelrgb()` and `gl_setpixelrgb()` anticipate 256 colors. To compensate, I’ve multiplied each `gl_getpalettecolor()` value by four, which will work every time, unlike `vga_ext_set()`.

**Listing 6.6 A better way to antialias a line.**

```c
#define ABS(a) (((a)<0) ? -(a) : (a))

int book_aa_line(int x1, int y1, int x2, int y2, int color)
{
    int dx = x2 - x1;
    int dy = y2 - y1;
    int ax = ABS(dx) << 1;
    int ay = ABS(dy) << 1;
    int sx = (dx > 0) ? 1 : -1;
    int sy = (dy > 0) ? 1 : -1;

    int x = x1;
    int y = y1;

    int r1,
        g1,
        b1,
        r2,
        g2,
        b2;

    /* If the line is vertical or horizontal, no antialiasing
       is necessary.
    */
    if ((dx == 0) || (dy == 0))
    {
        gl_line(x1, y1, x2, y2, color);
        return 0;
    }

    gl_getpalettecolor(color, &r1, &g1, &b1);
    r1 *= 4;
    g1 *= 4;
    b1 *= 4;

    if (ax > ay)
    {
      int d = ay - (ax >> 1);
      while (x != x2)
      {
        gl_setpixel(x, y, color);
        gl_getpixelrgb(x, (y + 1), &r2, &g2, &b2);
        gl_setpixelrgb(x, (y + 1),
                       ((r1 + r2) / 2), ((g1 + g2) / 2), ((b1 + b2) / 2));
        gl_getpixelrgb(x, (y - 1), &r2, &g2, &b2);
        gl_setpixelrgb(x, (y - 1),
                       ((r1 + r2) / 2), ((g1 + g2) / 2), ((b1 + b2) / 2));
        if (d > 0 || (d == 0 && sx == 1))
        {
          y += sy;
          d -= ax;
        }
        x += sx;
        d += ay;
      }
    } else {
      int d = ax - (ay >> 1);
      while (y != y2)
      {
        gl_setpixel(x, y, color);
        gl_getpixelrgb((x + 1), y, &r2, &g2, &b2);
        gl_setpixelrgb((x + 1), y,
                       ((r1 + r2) / 2), ((g1 + g2) / 2), ((b1 + b2) / 2));
        gl_getpixelrgb((x - 1), y, &r2, &g2, &b2);
        gl_setpixelrgb((x - 1), y,
                       ((r1 + r2) / 2), ((g1 + g2) / 2), ((b1 + b2) / 2));
        if (d > 0 || (d == 0 && sy == 1))
        {
          x += sx;
          d -= ay;
        }
        y += sy;
        d += ax;
      }
    }

    return 0;
}
```

One pitfall that you might run into with this method is that the standard SVGAlib palette is rather dark (see Chapter 5 for a complete discussion). This, in turn, will make your buffer pixels not quite right, and your end result will appear to be nothing more than stupid-looking fat lines. To correct this, you may find it necessary to reset the palette to something brighter *before* doing any drawing. Alternatively, if you want to leave the standard palette intact, you can simply use `gl_rgbcolor()` like I've done in Listing 6.7.

**Listing 6.7 Adjusting colors with `gl_rgbcolor()`.**

```c
    int c[256],
        i = 0,
        r,
        g,
        b;

    for (r = 0; r < 256; r += 51)
    {
        for (g = 0; g < 256; g += 51)
        {
            for (b = 0; b < 256; b += 51)
            {
                c[i] = gl_rgbcolor(r, g, b);
                i++;
            }
        }
    }
```

## The Best Method

The next technique I'm about to show you was theorized and developed by Xiaolin Wu. It's interesting to note that Wu wasn't taken seriously at the time. His algorithm was seen as being too simple. Yet, today, it's taken for granted, thus becoming another irony in the world of computers. As for the professor who wouldn't listen to Wu, well, better luck next time.

You'll notice that this example also borrows heavily from `vga_drawline()`. The advantage here over the previous code is that the buffer pixels are shaded in a more intelligent manner. Rather than being all one color, their hues are based upon how far they lie from the “ideal” line. Have a look at Listing 6.8 to see what I mean.

**Listing 6.8 Along the lines of Xiaolin Wu.**

```c
void wu_line(int x1, int y1, int x2, int y2, int r, int g, int b)
{
    #define ABS(a) (((a)<0) ? -(a) : (a))

    int dx, dy, ax, ay, ax2, ay2, sx, sy, x, y;
    int r1, g1, b1, r2, g2, b2;
    int highr, lowr, highg, lowg, highb, lowb;
    int percent, complement;
    int color;

    dx = x2 - x1;
    dy = y2 - y1;
    ax = ABS(dx) << 1;
    ax2 = ax * 2;
    ay = ABS(dy) << 1;
    ay2 = ay * 2;
    sx = (dx >= 0) ? 1 : -1;
    sy = (dy >= 0) ? 1 : -1;

    if (x1 == x2)
    {
        color = gl_rgbcolor(r, g, b);
        gl_hline(x1, y1, x2, y2, color);
        return;
    } else if (y1 == y2) {
        color = gl_rgbcolor(r, g, b);
        gl_vline(x1, y1, x2, color);
        return;
    } else if (ax == ay) {
        color = gl_rgbcolor(r, g, b);
        gl_hline(x1, y1, x2, y2, color);
        return;
    }

    x = x1;
    y = y1;

    gl_setpixelrgb(x, y, r, g, b);

    if (ax > ay)
    {
        int d = ay - (ax >> 1);
        while (x != x2)
        {
            if (d > 0 || (d == 0 && sx == 1))
            {
                y += sy;
                d -= ax;
            }
            x += sx;
            d += ay;
            percent = ((ABS(d) * 100) / ax);
            complement = 100 - percent;

            gl_getpixelrgb(x, y, &r1, &g1, &b1);
            highr = (r > r1) ? r : r1;
            lowr = (r == highr) ? r1 : r;
            r2 = (((highr - lowr) * percent) / 100)
                 + lowr;
            r2 = (r > r1) ? r2 : (255 - r2);
            highg = (g > g1) ? g : g1;
            lowg = (g == highg) ? g1 : g;
            g2 = (((highg - lowg) * percent) / 100)
                 + lowg;
            g2 = (g > g1) ? g2 : (255 - g2);
            highb = (b > b1) ? b : b1;
            lowb = (b == highb) ? b1 : b;
            b2 = (((highb - lowb) * percent) / 100)
                 + lowb;
            b2 = (b > b1) ? b2 : (255 - b2);
            gl_setpixelrgb(x, y, r2, g2, b2);

            if (ay2 > ax)
            {
                gl_getpixelrgb(x, (y - sy), &r1, &g1, &b1);
                highr = (r > r1) ? r : r1;
                lowr = (r == highr) ? r1 : r;
                r2 = (((highr - lowr) * complement) / 100)
                     + lowr;
                r2 = (r > r1) ? r2 : (255 - r2);
                highg = (g > g1) ? g : g1;
                lowg = (g == highg) ? g1 : g;
                g2 = (((highg - lowg) * complement) / 100)
                     + lowg;
                g2 = (g > g1) ? g2 : (255 - g2);
                highb = (b > b1) ? b : b1;
                lowb = (b == highb) ? b1 : b;
                b2 = (((highb - lowb) * complement) / 100)
                     + lowb;
                b2 = (b > b1) ? b2 : (255 - b2);
                gl_setpixelrgb(x, (y - sy), r2, g2, b2);
            }
            else {
                gl_getpixelrgb(x, (y + sy), &r1, &g1, &b1);
                highr = (r > r1) ? r : r1;
                lowr = (r == highr) ? r1 : r;
                r2 = (((highr - lowr) * complement) / 100)
                     + lowr;
                r2 = (r > r1) ? r2 : (255 - r2);
                highg = (g > g1) ? g : g1;
                lowg = (g == highg) ? g1 : g;
                g2 = (((highg - lowg) * complement) / 100)
                     + lowg;
                g2 = (g > g1) ? g2 : (255 - g2);
                highb = (b > b1) ? b : b1;
                lowb = (b == highb) ? b1 : b;
                b2 = (((highb - lowb) * complement) / 100)
                     + lowb;
                b2 = (b > b1) ? b2 : (255 - b2);
                gl_setpixelrgb(x, (y + sy), r2, g2, b2);
            }
        }
    } else {
        int d = ax - (ay >> 1);
        while (y != y2)
        {
            if (d > 0 || (d == 0 && sy == 1))
            {
                x += sx;
                d -= ay;
            }
            y += sy;
            d += ax;
            percent = ((ABS(d) * 100) / ay);
            complement = 100 - percent;

            gl_getpixelrgb(x, y, &r1, &g1, &b1);
            highr = (r > r1) ? r : r1;
            lowr = (r == highr) ? r1 : r;
            r2 = (((highr - lowr) * percent) / 100)
                 + lowr;
            r2 = (r > r1) ? r2 : (255 - r2);
            highg = (g > g1) ? g : g1;
            lowg = (g == highg) ? g1 : g;
            g2 = (((highg - lowg) * percent) / 100)
                 + lowg;
            g2 = (g > g1) ? g2 : (255 - g2);
            highb = (b > b1) ? b : b1;
            lowb = (b == highb) ? b1 : b;
            b2 = (((highb - lowb) * percent) / 100)
                 + lowb;
            b2 = (b > b1) ? b2 : (255 - b2);
            gl_setpixelrgb(x, y, r2, g2, b2);

            if (ax2 > ay)
            {
                gl_getpixelrgb((x - sx), y, &r1, &g1, &b1);
                highr = (r > r1) ? r : r1;
                lowr = (r == highr) ? r1 : r;
                r2 = (((highr - lowr) * complement) / 100)
                     + lowr;
                r2 = (r > r1) ? r2 : (255 - r2);
                highg = (g > g1) ? g : g1;
                lowg = (g == highg) ? g1 : g;
                g2 = (((highg - lowg) * complement) / 100)
                     + lowg;
                g2 = (g > g1) ? g2 : (255 - g2);
                highb = (b > b1) ? b : b1;
                lowb = (b == highb) ? b1 : b;
                b2 = (((highb - lowb) * complement) / 100)
                     + lowb;
                b2 = (b > b1) ? b2 : (255 - b2);
                gl_setpixelrgb((x - sx), y, r2, g2, b2);
            }
            else {
                gl_getpixelrgb((x + sx), y, &r1, &g1, &b1);
                highr = (r > r1) ? r : r1;
                lowr = (r == highr) ? r1 : r;
                r2 = (((highr - lowr) * complement) / 100)
                     + lowr;
                r2 = (r > r1) ? r2 : (255 - r2);
                highg = (g > g1) ? g : g1;
                lowg = (g == highg) ? g1 : g;
                g2 = (((highg - lowg) * complement) / 100)
                     + lowg;
                g2 = (g > g1) ? g2 : (255 - g2);
                highb = (b > b1) ? b : b1;
                lowb = (b == highb) ? b1 : b;
                b2 = (((highb - lowb) * complement) / 100)
                     + lowb;
                b2 = (b > b1) ? b2 : (255 - b2);
                gl_setpixelrgb((x + sx), y, r2, g2, b2);
            }
        }
    }
}
```
