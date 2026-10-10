The tools appear above the palette menu and will be arranged in a manner similar to the color palette. However, they'll be a little larger for convenience, and they'll work in the same manner as radio buttons. Clicking on one will activate that tool and will deactivate the previous tool. Listing 18.5 demonstrates the two states of the freehand tool.

# Listing 18.5 The two states of the freehand button (up and down).

```
```c
void tool0_up()
/* freehand */
{
    int ybase = 75;
    int w = vga_setegacolor(15);       /* white */
    int b = vga_setegacolor(0);        /* black */
    int l = gl_rgbcolor(240, 240, 240); /* light gray */
    int g = gl_rgbcolor(130, 130, 130); /* dark gray */

    gl_hline(4, ybase, 28, w);
    gl_line(4, (ybase + 1), 4, (ybase + 24), w);
    gl_line(5, (ybase + 1), 27, l);
    gl_line(5, (ybase + 2), 5, (ybase + 23), l);
    gl_line(5, (ybase + 24), 28, g);
    gl_line(28, (ybase + 1), 28, (ybase + 23), g);
    gl_hline(4, (ybase + 25), 29, b);
    gl_line(29, ybase, 29, (ybase + 24), b);
    gl_fillbox(15, 86, 3, 3, b);
}

void tool0_down()
/* freehand */
{
    int ybase = 75;
    int w = vga_setegacolor(15);       /* white */
    int b = vga_setegacolor(0);        /* black */
    int l = gl_rgbcolor(240, 240, 240); /* light gray */
    int g = gl_rgbcolor(130, 130, 130); /* dark gray */

    gl_hline(4, ybase, 28, b);
    gl_line(4, (ybase + 1), 4, (ybase + 24), b);
    gl_line(5, (ybase + 1), 27, g);
    gl_line(5, (ybase + 2), 5, (ybase + 23), g);
    gl_line(5, (ybase + 24), 28, l);
    gl_line(28, (ybase + 1), 28, (ybase + 23), l);
    gl_line(4, (ybase + 25), 29, w);
    gl_line(29, ybase, 29, (ybase + 24), w);
    gl_fillbox(15, 86, 3, 3, b);
}
```
```