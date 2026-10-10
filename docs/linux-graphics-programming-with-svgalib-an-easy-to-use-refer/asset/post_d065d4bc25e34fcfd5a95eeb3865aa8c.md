
## Chapter 9

### Keyboard Codes

Once you're in raw keyboard mode, your program looks for signals to indicate that a certain key has been pressed. This is accomplished with `keyboard_keypressed(int scancode)` and `keyboard_update(void)`. Basically, your program uses `keyboard_update()` to flush the buffer and `keyboard_keypressed()` to see whether any scan codes have been entered. Because `keyboard_update()` is nonblocking, it doesn't halt the execution of your program. Therefore, you should use it in your main loop, because the buffer must constantly be checked. Alternately, if you want your program to stop and wait for input, use the blocking `keyboard_waitforupdate(void)` instead.

For your convenience, Table 9.8 has the scan codes that `keyboard_keypressed()` recognizes, along with their associated numeric values. Although codes and values may be used interchangeably in programs, it's probably best to use the codes. Note that case makes no difference here; therefore, a capital A is identical to a lowercase a.

**Note**
Some code names may be unfamiliar to you, so I'll provide a few definitions. The `CURSORBLOCK` instances are the four arrow keys, meaning that `CURSORBLOCKUP` is the up arrow, and `CURSORBLOCKDOWN` is the down arrow, and so on. `GRAVE` is the "backtick" located on the same key as the tilde (~). Note that "Pause Break" returns `SCANCODE_BREAK` (101) on some keyboards and `SCANCODE_BREAK_ALTERNATIVE` (119) on others. Therefore, you should have your programs check for both if that key is important to you.

The scan code names are based on the U.S. keyboard layout. If you happen to have a non-American keyboard, the codes will pertain to the keys in the same physical location, although their inscriptions will be different.

After reviewing Table 9.8, it should be obvious that `SCANCODE_PRINTSCREEN` (99) is what you need for a screen grabber.

#### Table 9.8 Keyboard scancodes

| Scancode | Value |
| :--- | :--- |
| SCANCODE_ESCAPE | 1 |
| SCANCODE_1 | 2 |
| SCANCODE_2 | 3 |
| SCANCODE_3 | 4 |
| SCANCODE_4 | 5 |
| SCANCODE_5 | 6 |
| SCANCODE_6 | 7 |
| SCANCODE_7 | 8 |
| SCANCODE_8 | 9 |
| SCANCODE_9 | 10 |
| SCANCODE_0 | 11 |
| SCANCODE_MINUS | 12 |
| SCANCODE_EQUAL | 13 |
| SCANCODE_BACKSPACE | 14 |
| SCANCODE_TAB | 15 |
| SCANCODE_Q | 16 |
| SCANCODE_W | 17 |
| SCANCODE_E | 18 |
| SCANCODE_R | 19 |
| SCANCODE_T | 20 |
| SCANCODE_Y | 21 |
| SCANCODE_U | 22 |
| SCANCODE_I | 23 |
| SCANCODE_O | 24 |
| SCANCODE_P | 25 |
| SCANCODE_BRACKET_LEFT | 26 |
| SCANCODE_BRACKET_RIGHT | 27 |
| SCANCODE_ENTER | 28 |
| SCANCODE_LEFTCONTROL | 29 |
| SCANCODE_A | 30 |
| SCANCODE_S | 31 |
| SCANCODE_D | 32 |
| SCANCODE_F | 33 |
| SCANCODE_G | 34 |
| SCANCODE_H | 35 |
| SCANCODE_J | 36 |
| SCANCODE_K | 37 |
| SCANCODE_L | 38 |
| SCANCODE_SEMICOLON | 39 |
| SCANCODE_APOSTROPHE | 40 |
| SCANCODE_GRAVE | 41 |
| SCANCODE_LEFTSHIFT | 42 |
| SCANCODE_BACKSLASH | 43 |
| SCANCODE_Z | 44 |
| SCANCODE_X | 45 |
| SCANCODE_C | 46 |
| SCANCODE_V | 47 |
| SCANCODE_B | 48 |
| SCANCODE_N | 49 |
| SCANCODE_M | 50 |
| SCANCODE_COMMA | 51 |
| SCANCODE_PERIOD | 52 |
| SCANCODE_SLASH | 53 |
| SCANCODE_RIGHTSHIFT | 54 |
| SCANCODE_KEYPADMULTIPLY | 55 |
| SCANCODE_LEFTALT | 56 |
| SCANCODE_SPACE | 57 |
| SCANCODE_CAPSLOCK | 58 |
| SCANCODE_F1 | 59 |
| SCANCODE_F2 | 60 |
| SCANCODE_F3 | 61 |
| SCANCODE_F4 | 62 |
| SCANCODE_F5 | 63 |
| SCANCODE_F6 | 64 |
| SCANCODE_F7 | 65 |
| SCANCODE_F8 | 66 |
| SCANCODE_F9 | 67 |
| SCANCODE_F10 | 68 |
| SCANCODE_NUMLOCK | 69 |
| SCANCODE_SCROLLLOCK | 70 |
| SCANCODE_KEYPAD7 | 71 |
| SCANCODE_CURSORUPLEFT | 71 |
| SCANCODE_KEYPAD8 | 72 |
| SCANCODE_CURSORUP | 72 |
| SCANCODE_KEYPAD9 | 73 |
| SCANCODE_CURSORUPRIGHT | 73 |
| SCANCODE_KEYPADMINUS | 74 |
| SCANCODE_KEYPAD4 | 75 |
| SCANCODE_CURSORLEFT | 75 |
| SCANCODE_KEYPAD5 | 76 |
| SCANCODE_KEYPAD6 | 77 |
| SCANCODE_CURSORRIGHT | 77 |
| SCANCODE_KEYPADPLUS | 78 |
| SCANCODE_KEYPAD1 | 79 |
| SCANCODE_CURSORDOWNLEFT | 79 |
| SCANCODE_KEYPAD2 | 80 |
| SCANCODE_CURSORDOWN | 80 |
| SCANCODE_KEYPAD3 | 81 |
| SCANCODE_CURSORDOWNRIGHT | 81 |
| SCANCODE_KEYPAD0 | 82 |
| SCANCODE_KEYPADPERIOD | 83 |
| SCANCODE_LESS | 86 |
| SCANCODE_F11 | 87 |
| SCANCODE_F12 | 88 |
| SCANCODE_KEYPADENTER | 96 |
| SCANCODE_RIGHTCONTROL | 97 |
| SCANCODE_CONTROL | 97 |
| SCANCODE_KEYPADDIVIDE | 98 |
| SCANCODE_PRINTSCREEN | 99 |
| SCANCODE_RIGHTALT | 100 |
| SCANCODE_BREAK | 101 |
| SCANCODE_BREAK_ALTERNATIVE | 119 |
| SCANCODE_HOME | 102 |
| SCANCODE_CURSORBLOCKUP | 103 |
| SCANCODE_PAGEUP | 104 |
| SCANCODE_CURSORBLOCKLEFT | 105 |
| SCANCODE_CURSORBLOCKRIGHT | 106 |
| SCANCODE_END | 107 |
| SCANCODE_CURSORBLOCKDOWN | 108 |
| SCANCODE_PAGEDOWN | 109 |
| SCANCODE_INSERT | 110 |
| SCANCODE_REMOVE | 111 |
| SCANCODE_RIGHTWIN | 126 |
| SCANCODE_LEFTWIN | 125 |

### Writing The Application

It looks as though the gisave package were written for DOS, judging by the presence of the board.c file. Nevertheless, it can be easily adapted for Linux. Listing 9.4 shows how the main loop of a program using gisave might be written. I call this program ScreenShot.c.

**Listing 9.4** The main loop for ScreenShot.c.
```c
int main(void)
{
    vga_init();
    vga_setmode(G320x200x16);
    gl_setcontextvga(G320x200x16);

    if (keyboard_init())
    {
        vga_setmode(TEXT);
        printf("Could not initialize keyboard.\n");
        exit(1);
    }

    /* The actual drawing takes place here */
    /* Draw whatever you'd like */
    while (!keyboard_keypressed(SCANCODE_PRINTSCREEN))
    {
        keyboard_update();
    }

    DumpImage();

    keyboard_close();
    vga_setmode(TEXT);

    return 0;
}
```

As you can see, the program draws a picture (what exactly that picture is, I’ll leave to your imagination) and then it waits for the user to press the Print Screen button. After scan code 99 is received, the `DumpImage()` function is what actually writes the GIF file.

I’ve taken `DumpImage()` from the example.c program provided with gifsav. It works fairly well as is, but you will need to customize the `GetPixel()` function for SVGAlib. I did it as shown in Listing 9.5.

**Listing 9.5** Customized GetPixel().
```c
static int GetPixel(int x, int y)
{
    return(gl_getpixel(x, y));
}
```

I think you can handle that one. Next, you’ll need to create a few defines for your program. Specifically, you’ll need to define the GIF’s height, width, number of colors, and file name. Of course, this will need to match your screen mode. Listing 9.6 has the includes and defines for ScreenShot.c.

**Listing 9.6** Includes and defines for ScreenShot.c.
```c
#include <stdlib.h>
#include <vga.h>
#include <vgagl.h>
#include <vgakeyboard.h>
#include "gifsav.h"

#define GIFWIDTH    320
#define GIFHEIGHT   200
#define NUMCOLORS   16    /* DumpImage() must match */
#define COLORRES     4     /* number of bits per color */
#define FILENAME    "/tmp/book_example.gif"

static void DumpImage(void);
static int GetPixel(int x, int y);
```

Notice that I have the number of color bits set at 4, which is adequate for 16 colors. If I were going to have 256 colors, I'd need to increase the bits to 8.

Here, then, is the complete `DumpImage()` function, as shown in Listing 9.7. Note that I have the RGB values for 16 colors defined, matching what I have defined in Listing 9.6.

**Listing 9.7** `DumpImage()`.
```c
static void DumpImage(void)
{
    /* create and set up the GIF-file */
    GIF_Create(FILENAME, GIFWIDTH, GIFHEIGHT, NUMCOLORS, COLORRES);

    /* define a few colors matching the pixel values used */
    GIF_SetColor(0, 0, 0, 0);      /* black, the background */
    GIF_SetColor(1, 0, 0, 170);
    GIF_SetColor(2, 0, 170, 0);
    GIF_SetColor(3, 0, 170, 170);
    GIF_SetColor(4, 170, 0, 0);
    GIF_SetColor(5, 170, 0, 170);
    GIF_SetColor(6, 170, 85, 0);
    GIF_SetColor(7, 170, 170, 170);
    GIF_SetColor(8, 85, 85, 170);
    GIF_SetColor(9, 85, 85, 255);
    GIF_SetColor(10, 85, 255, 85);
    GIF_SetColor(11, 85, 255, 255);
    GIF_SetColor(12, 255, 85, 85);
    GIF_SetColor(13, 255, 85, 255);
    GIF_SetColor(14, 255, 255, 85);
    GIF_SetColor(15, 255, 255, 255);

    /* store the image, using the GetPixel function to extract pixel values */
    GIF_CompressImage(0, 0, -1, -1, GetPixel);

    /* finish it all and close the file */
    GIF_Close();
}
```

The `GIF_Create()`, `GIF_SetColor()`, `GIF_CompressImage`, and `GIF_Close()` functions are all contained in gifsave.c, so you'll need to include this file along with `ScreenShot.c` in your compilation command. Here's one way to compile:

```bash
gcc -O3 -Wall -o ScreenShot ScreenShot.c gifsave.c -lvglal -lvga
```
