```
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

```