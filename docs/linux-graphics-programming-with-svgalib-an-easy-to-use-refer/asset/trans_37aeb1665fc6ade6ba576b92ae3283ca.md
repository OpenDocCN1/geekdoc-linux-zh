

![](img/2e475714ef8969ed272622c46473d334_183_0.png)

**图 7.264**
FontBuilder 主菜单。

# **列表 7.6 FontBuilder.c。**

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <vg8.h>
#include <vgagl.h>

void init_chooser_font(int color);
void chooser_screen(void);
void draw_screen(int ascii);
void hollow_box(int x1, int y1, int x2, int y2);

int x,
     y,
     ascii,
     inkey,
     glyph[256][8];

FILE *ffile;

int main(int argc, char *argv[])
{
    /* This program needs a filename as an input argument */
    int a,
        b;

    char c[256];
    char *d = malloc(256);

    if (argc == 1)  /* Error if no file is specified. */
    {
        printf("Please specify an output file.\n");
        exit(1);
    }

    /* You might want to check if the specified file already
       exists, and return an error if it does. */

    FILE *file = fopen(argv[1], "w");
    if (file == NULL)
    {
        printf("Can't write to file.\n");
        exit(1);
    }

    /* Set all font strips to 0. */
    for (a = 0; a < 256; a++)
    {
        for (b = 0; b < 7; b++)
        {
            glyph[a][b] = 0;
        }
    }

    vga_init();
    vga_setmode(G320x200x256);
    g1_setcontextvga(G320x200x256);

    /* This is the main loop. The program alternates between
       the "chooser screen" (the main menu) and the drawing
       screen. Pressing "Q" while in the chooser screen quits
       and saves your font info to your selected filename.
       */

    do
    {
        ascii = 0;
        chooser_screen();

        /* Spacebar - ASCII code 32. */
        if (inkey == 32)
        {
            draw_screen(ascii);
        }

        /* "Esc" - ASCII code 27.
           "Q"   - ASCII code 81.
           "q"   - ASCII code 113. */
    } while ((inkey != 27) && (inkey != 81) && (inkey != 113));

    vga_setmode(TEXT);
    strcpy(c, "unsigned char font[2048] = {\n");
    fputs(c, file);
    for (a = 0; a < 256; a++)
    {
        strcpy(c, " ");
        for (b = 0; b < 8; b++)
        {
            /* This is essentially an "ftoa" function, since C
               mysteriously lacks one.
               */
            sprintf(d, "%d", glyph[a][b]);
            strcat(c, d);
            strcat(c, ", ");
        }
        strcat(c, "\n");
        fputs(c, file);
    }

    strcpy(c, "};\n");
    fputs(c, file);

    fclose(file);

    return 0;
    /* That's all, folks! */
}

void chooser_screen(void)
/* Main menu (see the screen shot). */
{
    int a = 0,
        x1 = 7,
        x2 = 18,
        y1 = 7,
        y2 = 18;

    vga_clear();
    init_chooser_font(3);
    gl_write(9, 155, "'a', 'd', 'w', 'x' to move. \0");
    gl_write(9, 165, "space to select. \0");
    gl_write(9, 175, "'q' to save and exit. \0");

    init_chooser_font(15);
    for (y = 9; y < 120; y += 12)
    {
        for (x = 9; x < 309; x += 12)
        {
            char c[] = {a, '\0'};
            gl_write(x, y, c);
            a++;
        }
    }
    y = 129;
    for (x = 9; x < 82; x += 12)
    {
        char c[] = {a, '\0'};
        gl_write(x, y, c);
        a++;
    }
    vga_setcolor(14);
    hollow_box(x1, y1, x2, y2);
    do
    {
        inkey = vga_getch();
        if (inkey == 100)  /* 'g' */
        {
            vga_setcolor(0);
            hollow_box(x1, y1, x2, y2);
            if (y1 < 116)
            {
                if (x1 != 295)
                {
                    x1 += 12;
                    x2 += 12;
                    ascii++;
                } else {
                    x1 = 7;
                    x2 = 18;
                    ascii -= 24;
                }
            } else {
                if (x1 != 67)
                {
                    x1 += 12;
                    x2 += 12;
                    ascii++;
                } else {
                    x1 = 7;
                    x2 = 18;
                    ascii = 250;
                }
            }

            vga_setcolor(14);
            hollow_box(x1, y1, x2, y2);
        }
        if (inkey == 97)
        /* "a" */
        {
            vga_setcolor(0);
            hollow_box(x1, y1, x2, y2);
            if (y1 < 116)
            {
                if (x1 != 7)
                {
                    x1 -= 12;
                    x2 -= 12;
                    ascii--;
                } else {
                    x1 = 295;
                    x2 = 306;
                    ascii += 24;
                }
            } else {
                if (x1 != 7)
                {
                    x1 -= 12;
                    x2 -= 12;
                    ascii--;
                } else {
                    x1 = 67;
                    x2 = 78;
                    ascii = 255;
                }
            }

            vga_setcolor(14);
            hollow_box(x1, y1, x2, y2);
        }
        if (inkey == 119)
        /* "w" */
        {
            vga_setcolor(0);
            hollow_box(x1, y1, x2, y2);
            if (y1 != 7)
            {
                y1 -= 12;
                y2 -= 12;
                ascii -= 25;
            } else {
                if (x1 < 68)
                {
                    y1 = 127;
                    y2 = 138;
                    ascii += 250;
                } else {
                    y1 = 115;
                    y2 = 126;
                    ascii += 225;
                }
            }
            vga_setcolor(14);
            hollow_box(x1, y1, x2, y2);
        }
        if (inkey == 120)
        /* "x" */
        {
            vga_setcolor(0);
            hollow_box(x1, y1, x2, y2);
            if (x1 < 68)
            {
                if (y1 != 127)
                {
                    y1 += 12;
                    y2 += 12;
                    ascii += 25;
                } else {
                    y1 = 7;
                    y2 = 18;
                    ascii -= 250;
                }
            } else {
                if (y1 != 115)
                {
                    y1 += 12;
                    y2 += 12;
                    ascii += 25;
                } else {
                    y1 = 7;
                    y2 = 18;
                    ascii -= 225;
                }
            }
            vga_setcolor(14);
            hollow_box(x1, y1, x2, y2);
        }
    } while ((!inkey || 32) && (!inkey || 113));
}

void draw_screen(int ascii)
{
    char c[] = {ascii, '\0'};
    int a,
        b,
        pos[64],
        p = 0,
        x1 = 59,
        x2 = 82,
        y1 = 5,
        y2 = 24;

    vga_clear();
    g1_fillbox(58, 4, 194, 162, 7);
    for (a = 0; a < 8; a++)
    {
        if (a == 0)
        {
            y = 6;
        }
        else
        {
            y += 20;
        }
        b = glyph[ascii][a];
        if (b > 127)
        {
            g1_fillbox(60, y, 22, 18, 3);
            b -= 128;
            pos[p] = 1;
        } else {
            g1_fillbox(60, y, 22, 18, 15);
            pos[p] = 0;
        }

        if (b > 63)
        {
            gl_fillbox(84, y, 22, 18, 3);
            b -= 64;
            pos[p + 1] = 1;
        } else {
            gl_fillbox(84, y, 22, 18, 15);
            pos[p + 1] = 0;
        }
        if (b > 31)
        {
            gl_fillbox(108, y, 22, 18, 3);
            b -= 32;
            pos[p + 2] = 1;
        } else {
            gl_fillbox(108, y, 22, 18, 15);
            pos[p + 2] = 0;
        }
        if (b > 15)
        {
            gl_fillbox(132, y, 22, 18, 3);
            b -= 16;
            pos[p + 3] = 1;
        } else {
            gl_fillbox(132, y, 22, 18, 15);
            pos[p + 3] = 0;
        }
        if (b > 7)
        {
            gl_fillbox(156, y, 22, 18, 3);
            b -= 8;
            pos[p + 4] = 1;
        } else {
            gl_fillbox(156, y, 22, 18, 15);
            pos[p + 4] = 0;
        }
        if (b > 3)
        {
            gl_fillbox(180, y, 22, 18, 3);
            b -= 4;
            pos[p + 5] = 1;
        } else {
            gl_fillbox(180, y, 22, 18, 15);
            pos[p + 5] = 0;
        }
        if (b > 1)
        {
            gl_fillbox(204, y, 22, 18, 3);
            b -= 2;
            pos[p + 6] = 1;
        } else {
            gl_fillbox(204, y, 22, 18, 15);
            pos[p + 6] = 0;
        }

        if (b > 0)
        {
            gl_fillbox(228, y, 22, 18, 3);
            pos[p + 7] = 1;
        } else {
            gl_fillbox(228, y, 22, 18, 15);
            pos[p + 7] = 0;
        }
        if (p != 55)
        {
            p += 8;
        }
    }

    vga_setcolor(14);
    hollow_box(x1, y1, x2, y2);
    gl_write(58, 175, "This character \0");
    gl_write(218, 175, c);
    init_chooser_font(3);
    gl_write(0, 185, "space to select, 'q' to return to menu \0");

    do
    {
        inkey = vga_getch();
        if (inkey == 97)
        /* "a" */
        {
            vga_setcolor(7);
            hollow_box(x1, y1, x2, y2);
            if (x1 != 59)
            {
                x1 -= 24;
                x2 -= 24;
            } else {
                x1 = 227;
                x2 = 250;
            }

            vga_setcolor(14);
            hollow_box(x1, y1, x2, y2);
        }
        if (inkey == 100)
        /* "d" */
        {
            vga_setcolor(7);
            hollow_box(x1, y1, x2, y2);
            if (x1 != 227)
            {
                x1 += 24;
                x2 += 24;
            } else {
                x1 = 59;
                x2 = 82;
            }
            vga_setcolor(14);
            hollow_box(x1, y1, x2, y2);
        }
        if (inkey == 119)
        /* "w" */
        {
            vga_setcolor(7);
            hollow_box(x1, y1, x2, y2);
            if (y1 != 5)
            {
                y1 -= 20;
                y2 -= 20;
            } else {
                y1 = 145;
                y2 = 164;
            }
            vga_setcolor(14);
            hollow_box(x1, y1, x2, y2);
        }
        if (inkey == 120)
        /* "x" */
        {
            vga_setcolor(7);
            hollow_box(x1, y1, x2, y2);
            if (y1 != 145)
            {
                y1 += 20;
                y2 += 20;
            } else {
                y1 = 5;
                y2 = 24;
            }
            vga_setcolor(14);
            hollow_box(x1, y1, x2, y2);
        }

        if (inkey == 32)
        /* spacebar */
        {
            p = 0;
            for (y = -5; y < 150; y += 20)
            {
                for (x = 59; x < 228; x += 24)
                {
                    if ((x == x1) && (y == y1))
                    {
                        if (pos[p] == 1)
                        {
                            gl_fillbox(x1 + 1, y1 + 1, 22, 18, 15);
                            pos[p] = 0;
                        }
                        else
                        {
                            gl_fillbox(x1 + 1, y1 + 1, 22, 18, 3);
                            pos[p] = 1;
                        }
                    }
                    p++;
                }
            }
        }
        /* "Esc" or "Q" or "q" */
    } while ((inkey != 27) && (inkey != 81) && (inkey != 113));

    /* Now, take all the data and turn it into font strips. */
    p = -1;
    for (y = 0; y < 8; y++)
    {
        glyph[ascii][y] = 0;
        for (x = 0; x < 8; x++)
        {
            p++;
            if ((x == 0) && (pos[p] == 1))
            {
                glyph[ascii][y] += 128;
            }
            if ((x == 1) && (pos[p] == 1))
            {
                glyph[ascii][y] += 64;
            }
            if ((x == 2) && (pos[p] == 1))
            {
                glyph[ascii][y] += 32;
            }
            if ((x == 3) && (pos[p] == 1))
            {
                glyph[ascii][y] += 16;
            }
            if ((x == 4) && (pos[p] == 1))
            {
                glyph[ascii][y] += 8;
            }
            if ((x == 5) && (pos[p] == 1))
            {
                glyph[ascii][y] += 4;
            }
            if ((x == 6) && (pos[p] == 1))
            {
                glyph[ascii][y] += 2;
            }
            if ((x == 7) && (pos[p] == 1))
            {
                glyph[ascii][y] += 1;
            }
        }
    }
}
```

