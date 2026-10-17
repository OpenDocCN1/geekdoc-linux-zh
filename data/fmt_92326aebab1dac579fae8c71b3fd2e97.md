
```c
void line(int x, int y, int color)
{
    int orx = x,
        ory = y;
    int i;

    vga_waitretrace();
    gl_putbox(x, y, 11, 19, box);
    mouse_line(x, y, orx, ory, color);
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

            mouse_line(x, y, orx, ory, color);
            gl_getbox(x, y, 11, 19, box);
            draw_cursor(x, y);
            ox = x;
            oy = y;
        }
    }
}
```

```c
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

```c
mouse_oldline[mouse_oldline_length][0] = x;

mouse_oldline[mouse_oldline_length][1] = y;

gl_getpixrgb(x, y,
    &mouse_oldline[mouse_oldline_length][2],
    &mouse_oldline[mouse_oldline_length][3],
    &mouse_oldline[mouse_oldline_length][4]);

mouse_oldline_length++;

gl_setpixel(x, y, c);

return 0;
```

```c
void rectangle(int x, int y, int color){    /* 留给你实现 */

return;}
```

```c
void circle(int x, int y, int color){

/* 留给你实现 */

return;}
```

```c
void flood_fill(int x, int y, int color){

/* 算法由 Paul Heckbert 编写 */

typedef struct
{
    short y,
    xl,
    xr,
    dy;

} Segment;

#define STACKMAX 10000

#define PUSH(Y, XL, XR, DY) \
if ((sp < (stack + STACKMAX)) && ((Y + DY) >= TOP) && \
    ((Y + DY) <= BOTTOM)) \
{ \
    sp->y = Y; \
    sp->xl = XL; \
    sp->xr = XR; \
    sp->dy = DY; \
    sp++; \
}

#define POP(Y, XL, XR, DY) \
{ \
    sp--; \
    Y = sp->y + (DY = sp->dy); \
```
