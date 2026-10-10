```
```text
)

ol dx = newx;

/* repeat for the other direction */
} else if (newx < oldx) {
    /* slide the existing background right by one pixel */
    vga_waitretrace();
    gl_copybox(0, 0, (WIDTH - 1), HEIGHT, 1, 0);

    gl_setcontext(virtualscreen);

    /* insert the new segment on the left */
    if (oldx > 960) {
        {
            x = 319 - (1280 - oldx);
            gl_putbox(0, 0, WIDTH, HEIGHT, &buffer4);
            gl_setcontext(physicalscreen);
            gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 0, 0);
        }
    } else if (oldx > 640) {
        x = 319 - (960 - oldx);
        gl_putbox(0, 0, WIDTH, HEIGHT, &buffer3);
        gl_setcontext(physicalscreen);
        gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 0, 0);
    } else if (oldx > 320) {
        x = 319 - (640 - oldx);
        gl_putbox(0, 0, WIDTH, HEIGHT, &buffer2);
        gl_setcontext(physicalscreen);
        gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 0, 0);
    } else {
        x = 319 - (320 - oldx);
        gl_putbox(0, 0, WIDTH, HEIGHT, &buffer1);
        gl_setcontext(physicalscreen);
        gl_copyboxfromcontext(virtualscreen, x, 0, 1, HEIGHT, 0, 0);
    }
}

gl_setcontext(physicalscreen);
oldx = newx;
)
```
```