
# Drawing Lines

Most of the tools should be pretty easy to implement. One of the harder ones, however, is the line tool. It may seem straightforward, but it's actually quite a challenge. Any good drawing program will let you click the mouse in one spot, thereby affixing one end of the line, and then allow you to drag the other end to where ever you need it to be. This technique allows the user much greater precision than the frehand "pencil." However, the problem is that you, the programmer, will be drawing several lines as the mouse moves about. You don't want them all simultaneously, of course—you only want one at a time. A mobile line allows the user to draw with confidence, but it's also a bit of a hassle. You need to be able to place and erase old versions of the line without disturbing what's underneath.

My solution to this problem is to store every pixel as the line is being drawn. When the mouse moves (assuming the left button is still pressed), the old line is erased (actually, it's painted over, using the array of values that were read when the line was first drawn) and then the new one is placed, with a new set of values saved. This process continues until the user releases the button.

I accept that my explanation may have made things even more confusing for you, so have a look at Listing 18.7 for the actual code.

### Listing 18.7 Mobile line.

```c
void line(int x, int y, int color)
{
    int origx = x,
         origy = y;
    int i;

    vga_waitretrace();
    gl_putbox(x, y, 11, 19, box);
    mouse_line(x, y, origx, origy, color);
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

            mouse_line(x, y, origx, origy, color);
            gl_getbox(x, y, 11, 19, box);
            draw_cursor(x, y);
            ox = x;
            oy = y;
        }
    }
}

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

# Quantization

The process of subdividing a large group into smaller sets. In computer graphics, this refers to a common method of color reduction, in which a few colors are mathematically chosen to represent a larger palette.

# Reading In Files

To allow the user to work with an existing image, I've added in some liblug reading and writing routines. For the time being, incoming graphic files must be specified on the command line. However, when the user interface is finished, they'll be accessible from a drop-down menu as well.

Unfortunately, this addition means that some programming contortions will be involved, due to the fact that image files can contain 16, 256, or an even greater number of colors. If the colors in the graphic file don't jive with the available colors in your chosen screen grade, then you're apt to see some corruption and distortion. Along these same lines, many graphic files contain their own palette, which will often clash with your screen's palette. To circumvent this scenario, I've taken the following precautions:

- 1. If the image has more than 256 colors, it will be quantized (reduced) to 256 colors.
- 2. The screen will then be set to a 256-color mode, and the palette will be set to match the incoming graphic's palette.
- 3. The image will be displayed, and its color information subsequently recorded into an array.
- 4. Finally, the screen will be reset to allow 32K colors, and the normal background and tool bars will be drawn. Then, the image will be recreated by reading the array created in Step 3.

In order to keep the image from momentarily flashing on the screen (while using 256 colors), I've employed two new functions: **vga_screenoff()** and **vga_screenon()**. These work exactly as they sound—the first turns the screen black, and the second restores it. No image data is lost. Since the screen starts out black, the user shouldn't even notice what's going on.

Finally, to help keep things organized, I've moved all of the screen preparation commands into their own function, **prep_screen()**. This will be where the menus are drawn, etc.

Listing 18.8 shows the basic liblug section. Remember that you'll need to change:

```c
int main(void)
```

into the more involved:

```c
int main(int argc, char *argv[])
```

to accept command-line variables.

### Listing 18.8 Reading in files.

```c
if (argc > 1)
{
    if ((a = read_lug_file(argv[1], &file)) == 0)
    {
        int c[file.xsize * file.ysize];
        int palr[256], palg[256], palb[256];
        byte *ptr;

        if (file.colors > 256)
        {
            quantize(&file, &quantfile, 256);
            copy_bitmap(&quantfile, &file);
            free_bitmap(&quantfile);
        }

        vga_setmode(G640x480x256);
        gl_setcontextvga(G640x480x256);
        vga_screenoff();

        a = 0;
        for (i = 0, ptr = file.cmap; i < file.colors; i++)
        {
            r = (double)*ptr++;
            palr[a] = r;
            g = (double)*ptr++;
            palg[a] = g;
            b = (double)*ptr++;
            palb[a] = b;
            gl_setpalettecolor(r, r>>2, g>>2, b>>2);
            a++;
        }

        gl_putbox(0, 0, file.xsize, file.ysize, file.r);

        a = 0;
        for (i = 0; i < file.ysize; i++)
        {
            for (j = 0; j < file.xsize; j++)
            {
                c[a] = vga_getpixel(j, i);
                a++;
            }
        }

        vga_setmouseesupport(1);
        vga_setmode(6640x480x32K);
        gl_setcontextvga(6640x480x32K);
        vga_screenon();

        prep_screen();

        a = 0;
        for (i = 0; i < file.ysize; i++)
        {
            for (j = 0; j < file.xsize; j++)
            {
                gl_setpixelrgb(LEFT + j, TOP + i, palr[c[a]],
                               palg[c[a]], palb[c[a]]);
                a++;
            }
        }
    } else {
        exit(1);
    }
} else {
    vga_setmouseesupport(1);
    vga_setmode(6640x480x32K);
    gl_setcontextvga(6640x480x32K);
    prep_screen();
}
```

# Complete Code

At this point, you have a working interface and some working tools. The next step will be to create the pull-down menus. Because menus are an integral element of any GUI, I've decided to give the subject complete coverage in Chapter 19.

The rectangle and circle routines can be copied more or less from the line functions. That leaves the flood fill, which I'll leave to you to figure out. You may find it easier to go with a different, yet similar, incarnation, in which every pixel of a certain color is changed, regardless of what it touches.

I'll leave you now with the complete code for this chapter. Listing 18.9 has everything I've discussed thus far, plus a little more. Again, the menus will be coded in the next chapter. In case you decide to create your own drawing tools, I've left you plenty of room.

### Listing 18.9 The (more or less) complete drawing program.

```c
#include <stdlib.h>
#include <math.h>
#include <unistd.h>
#include <lug.h>
#include <lugfnts.h>
#include <vga.h>
#include <vgagl.h>
#include <vgamouse.h>

/* parameters of drawing window */
#define LEFT      62
#define RIGHT     617
#define TOP        27
#define BOTTOM    457
#define BOX_WIDTH  555
#define BOX_HEIGHT 430

void move_cursor(int x, int y, int ox, int oy);
void draw_cursor(int x, int y);

void tool10_up();
void tool10_down();
void tool11_up();
void tool11_down();
void tool12_up();
void tool12_down();
void tool13_up();
void tool13_down();
void tool14_up();
void tool14_down();
void tool15_up();
```
