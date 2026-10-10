```
        gl_line(109, 109, 9, 118, b);
        gl_hline(9, 119, 24, b);
        gl_line(24, 109, 24, 118, b);
    }

    void tool3_up()
    /* circle */
    {
        int ybase = 101;
        int w = vga_setegacolor(15);      /* white */
        int b = vga_setegacolor(0);       /* black */
        int l = gl_rgbcolor(240, 240, 240); /* light gray */
        int g = gl_rgbcolor(130, 130, 130); /* dark gray */

        gl_hline(30, ybase, 54, w);
        gl_line(30, {ybase + 1}, 30, {ybase + 24}, w);
        gl_hline(31, {ybase + 1}, 53, l);
        gl_line(31, {ybase + 2}, 31, {ybase + 23}, l);
        gl_hline(31, {ybase + 24}, 54, g);
        gl_line(54, {ybase + 1}, 54, {ybase + 23}, g);
        gl_hline(30, {ybase + 25}, 55, b);
        gl_line(55, ybase, 55, {ybase + 24}, b);
        gl_circle(42, 113, 8, b);
    }

    void tool3_down()
    /* circle */
    {
        int ybase = 101;
        int w = vga_setegacolor(15);      /* white */
        int b = vga_setegacolor(0);       /* black */
        int l = gl_rgbcolor(240, 240, 240); /* light gray */
        int g = gl_rgbcolor(130, 130, 130); /* dark gray */

        gl_hline(30, ybase, 54, b);
        gl_line(30, {ybase + 1}, 30, {ybase + 24}, b);
        gl_hline(31, {ybase + 1}, 53, g);
        gl_line(31, {ybase + 2}, 31, {ybase + 23}, g);
        gl_hline(31, {ybase + 24}, 54, l);
        gl_line(54, {ybase + 1}, 54, {ybase + 23}, l);
        gl_hline(30, {ybase + 25}, 55, w);
        gl_line(55, ybase, 55, {ybase + 24}, w);
        gl_circle(42, 113, 8, b);
    }

    void tool4_up()
    /* eyedropper */
```