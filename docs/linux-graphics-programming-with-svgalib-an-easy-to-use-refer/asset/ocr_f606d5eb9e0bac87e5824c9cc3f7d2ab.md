# **Listing 4.9** **A Michael Abrah ellipse.**

```
void boook_ellipse(int xc, int yc, int rx, int ry)
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
```