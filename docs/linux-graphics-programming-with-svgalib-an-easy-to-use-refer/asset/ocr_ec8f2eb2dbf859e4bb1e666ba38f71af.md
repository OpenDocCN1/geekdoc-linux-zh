```
```
)

mouse_oldline[mouse_oldline_length][0] = x;
mouse_oldline[mouse_oldline_length][1] = y;
gl_getpixrgb(x, y,
    &mouse_oldline[mouse_oldline_length][2],
    &mouse_oldline[mouse_oldline_length][3],
    &mouse_oldline[mouse_oldline_length][4]);
mouse_oldline_length++;
gl_setpixel(x, y, c);

return 0;
}

void rectangle(int x, int y, int color){    /* left for you */
return;}void circle(int x, int y, int color){
/* left for you */    return;} void flood_fill(int x, int y, int color){
/* Algorithm written by Paul Heckbert */

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
    XL = sp->xl; \
    XR = sp->xr; \
}
```
```