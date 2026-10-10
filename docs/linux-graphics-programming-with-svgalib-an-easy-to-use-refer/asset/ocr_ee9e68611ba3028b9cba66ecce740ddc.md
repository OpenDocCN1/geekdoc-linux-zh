# Listing 3.16 Neatly arranged boxes displaying the first 256 standard SVGA**colors**.

```
#include <stdlib.h>
#include <vga.h>
#include <vgagl.h>

int main(void)
{
    int x,
        y,
        c = 0;

    vga_init();
    vga_setmode(G320x200x256);
    gl_setcontextvga(G320x200x256);

    for (y = 2; y < 183; y += 12)
    {
        for (x = 2; x < 183; x += 12)
        {
            gl_fillbox(x, y, 10, 10, c++);
        }
    }

    vga_getch();
    vga_setmode(TEXT);
    return 0;
}

```

Figure 3.4 shows how this should turn out, minus the color.

Pretty cool, huh? If you only compile one program from this chapter, I’d suggest you do this one. Not only will you be able to impress your friends, you’ll have the option of using this as a programming reference for the future. Need a hue? Just fire up your 256-color table and choose one.

Notice that the second half of the colors is rather dark. Some people complain that the programs they’ve ported to SVGA**lib** are too dark; their colors aren’t exactly the same as

# Port

To alter software so that it can be run under a different operating system. If you’re rewriting the graphics in a Windows C program for SVGA**lib**, you’re porting the program to Linux. This is often easier said than done, regardless of the source or destination.