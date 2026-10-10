```
int main(void)
{
    byte        *ptr;
    
    bitmap_hdr in;
    
    vga_init();
    vga_setmode(GI1024x768x256);
    gl_setcontextvga(GI1024x768x256);
    gl_setrgbpallete();
    
    read_gif_file("sample.gif", &in);
    gl_putbox(0, 0, in.xsize, in.ysize, in.r);
    
    vga_getch();
    vga_setmode(TEXT);
    
    return 0;
}
```

Now, I suppose some explanations are in order. First, note that I've included `<lbug.h>` and `<lugfonts.h>`. (I went ahead and copied all the liblbug header files to /usr/include). I've also declared in to be a bitmap_hdr structure, which is defined in liblbug.h. This is a nice structure, as it not only includes the image itself, but it also includes the dimensions. GIF images can only hold 256 colors, so I chose a 256-color mode. Finally, note that I've set gl_setrgbpallete().

Even with gl_setrgbpallete(), however, the colors still don't look right. Don't fret; liblbug provides an example of how to correct this, as seen below in Listing 9.2.

# Listing 9.2 Color corrections for liblbug.

```
for (i = 0, ptr = in.cmap; i < in.colors; i++)
{
    r = (double)*ptr++;
    g = (double)*ptr++;
    b = (double)*ptr++;
    gl_setpalettecolor(i, r>>2, g>>2, b>>2);
}
```

Therefore, the entire code would be like I've shown in Listing 9.3. You can get fancy and set the screen mode based upon the dimensions given by in.xsize and in.ysize, but I'll let you figure that one out on your own.

# Listing 9.3 Complete program using liblbug.

```
#include <stdio.h>
#include <vga.h>
```