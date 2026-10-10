Note

*Remember that `WIDTH` and `HEIGHT` are defined internally by `vga.gl`, meaning that you should use other constants (e.g., `FONT_WIDTH`) to define fonts in your code.*

This little bit of code introduces three new vga.gl functions:

+   - `gl_expandfont(int fw, int fh, int c, void *sfp, void *dfp)`
+   - `gl_font8x8`
+   - `gl_setfont(int fw, int fh, void *fp)`

Starting from the inside, `gl_font8x8` is a packed-pixel bitmapped font that comes with vga.gl. It's the only font included in the SVGAlib package; you'll have to find others elsewhere or create your own. This font looks quite a bit like Courier, which you might be familiar with. The 8x8 refers to the fact that it's 8 pixels high by 8 pixels across. This is the standard size of SVGAlib fonts, and, because it's a bitmapped font, you can't change these dimensions. A little thought will reveal that a low-resolution screen mode (such as 320x200) will yield a large font, whereas a high-resolution mode will make bitmapped type appear much smaller. This is because the font is always 8 pixels by 8 pixels—such is life. You may be able to compensate for this by having textual screens (such as high score pages or instructions) display in low-res mode, while having the rest of the application in a higher resolution mode. To have a larger font while in screen mode 800x600, for example, you'll need to switch to something larger, such as 16x16. Don't worry; there'll be more on this later.

First, use `gl_expandfont()` to uncompress the font data. With it, you'll need to declare the dimensions of the font, the desired color, the location of the font file itself, and a pointer to a memory location to hold the resultant bitmaps. I've called the pointer `font`, but you can name it whatever you like.

With that done, you'll then need to call `gl_setfont()`, again stating the dimensions and the memory location (pointer). This lets SVGAlib know that you'll be using the font you just expanded, much in the same way you might set a color with `vga_setcolor()`. Now you're actually ready to render type on the screen. Listing 7.2 shows you how to do this.

**Listing 7.2** *Aren't you glad this doesn't say “Hello World”?*

```
```
char words[] = "SVGAlib is fun!";

gl_write(100, 100, words);
```
```

This plots your phrase/word/statement (or whatever) with point 100,100 as the upper left of the first character. The actual command is `gl_write(int x, int y, char *s)`. That's all you have to do. Figure 7.4 shows a close-up of how this might look.

Listing 7.3 has the entire code snippet. When you feel comfortable with that, you might experiment with `gl_written(int x, int y, int n, char *s)`, which only displays the first n characters of your string.