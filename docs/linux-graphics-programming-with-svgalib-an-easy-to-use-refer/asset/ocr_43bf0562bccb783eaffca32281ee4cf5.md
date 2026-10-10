```
```
)

int l = 0, x1, x2, dy, old;
Segment stack[STACKMAX], *sp = stack;

gl_putbox(x, y, 11, 19, box);

if ((old = gl_getpixel(x, y)) == color)
{
    draw_cursor(x, y);
    return;
}

PUSH(y, x, x, 1);
PUSH(y + 1, x, x, -1);

while (sp > stack)
{
    POP(y, x1, x2, dy);
    for (x = x1; x <= RIGHT && gl_getpixel(x, y) == old; x--)
    {
        gl_setpixel(x, y, color);
    }
    if (x > x1)
    {
        goto skip;
    }
    l = x + 1;
    if (l < x1)
    {
        PUSH(y, l, x1 - 1, -dy);
    }
    x = x1 + 1;
do
{
    for (; x < RIGHT && gl_getpixel(x, y) == old; x++)
    {
        gl_setpixel(x, y, color);
    }
    PUSH(y, l, x - 1, dy);
    if (x > (x2 + 1))
    {
        PUSH(y, x2 + 1, x - 1, -dy);
    }
}
```
```