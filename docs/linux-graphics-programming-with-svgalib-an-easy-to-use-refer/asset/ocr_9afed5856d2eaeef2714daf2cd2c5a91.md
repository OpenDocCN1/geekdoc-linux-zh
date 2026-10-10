```
if (d > 0 || (d == 0 && sx == 1)) {
    y += sy;
    d -= ax;
}
x += sx;
d += ay;

} else {
    int d = ax - (ay >> 1);
    while (y != y2) {
#ifndef BACKGROUND
        vga_drawpixel(x, y);
#endif
#ifndef BACKGROUND
        _svgalib_fast_drawpixel(x, y);
#endif
        if (d > 0 || (d == 0 && sx == 1)) {
            x += sx;
            d -= ay;
        }
        y += sy;
        d += ax;
    }
}

#ifndef BACKGROUND
    vga_drawpixel(x, y);
#endif
#ifndef BACKGROUND
    _svgalib_fast_drawpixel(x, y);
    _svgalib_is_vt_switching_needed();
#endif

return 0;
```

(The actual source file, vgaline.c, is only 79 lines long, whereas vgapix.c is a whopping 492 lines long. Which would you rather work with? I thought so.) Now, let's use this code as a guide for creating your own functions.

First of all, you probably noticed the preponderance of statements using the BACK- GROUND variable—\#ifdef BACKGROUND and \#ifndef BACKGROUND, for example. This refers to a line in Makefile.cfg (remember that from Chapter 1?) in which you specified BACKGROUND = y (or else you left the line commented out with a hash mark) before compiling SVGAlib. More specifically, this variable serves to let SVGAlib know whether it can run in background mode. Of course, if you're using a kernel that's earlier than 2.0.36 or