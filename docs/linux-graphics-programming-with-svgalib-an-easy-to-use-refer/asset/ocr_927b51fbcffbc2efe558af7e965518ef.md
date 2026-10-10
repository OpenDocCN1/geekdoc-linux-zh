```
small bitmaps can reside in one image and be used for different surfaces.

\*/

\#define TD\_MULCONSTANT 4096

\#include \#<config.h>
\#include \#<math.h>
\#include \#<stdlib.h>
\#include \#<stdio.h>

\#ifndef DO\_NOT\_USE\_VGALIB
\#include \#<vga.h>
\#endif

\#include \#<vgagl.h>
\#include \"3dkit.h\"

\/*global for holding a surface temporarily:\*/
extern TD\_Short\_Point \*temp;

static void xchg (int \*a, int \*b)
\{
int t = \*a;
\*a = \*b;
\*b = t;
\}

void TD\_drawwrapsurface (TD\_Solid \* s, int which)
\{

TD\_Surface \*surf = &s->surf\[which\];
int w = surf->\~w;
int l = surf->\~l;
int bitmapwidth = surf->bitmapwidth;
int bitmaplength = surf->bitmaplength;
int i = 0, j = 0, k = 0, c = surf->mesh\_color;
void (\*dl) (int, int, int, int, int) = s->draw\_line;

void (\*dsw) (int, int, int, int,
```