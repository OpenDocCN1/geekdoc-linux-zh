# Antialiasing

Computers are well known for their "choppy," or jagged, diagonal lines. This is one drawback of the bitmap-style screen matrix; vertical and horizontal lines run evenly along the grid, but diagonal lines must be comprised of several disjointed pixels, especially in low-resolution modes. Antialiasing is the process of smoothing these lines, and it works by shading the outside edges of a line with gray or colored pixels. This shading works to blend the line with the background color, and reduces the "jaggies," or undesirably sharp edges are known.

![](bbox=[0.06, 0.27, 0.65, 0.33])

**Figure 7.2**  
Bitmapmed fonts are choppy.

![](bbox=[0.06, 0.4, 0.4, 0.53])

**Figure 7.3**  
A bitmapped font and a scalable font.

edges. Certainly, scalable fonts are preferable. Compare the two fonts in Figure 7.3. Which do you favor?

TrueType fonts such as Arial and Helvetica (commonly found on other operating systems and denoted by the .TTF extension) are scalable. Now, unfortunately, I’ve got some bad news: SVGAlib’s internal font-rendering functions are only capable of handling bitmapped fonts. However, you can get around this by using yet another library, as you’ll see later in this chapter.

# Coding Fonts

To use SVGAlib fonts, we must return to our old friend vga1. The process is really quite simple. First you prepare the font by loading it into memory, and then you render it on the screen, much like you would with a standard shape function. Listing 7.1 will get you started.

+   Listing 7.1 Preparing a font for use.

```
```c
#define FONT_HEIGHT 8
#define FONT_WIDTH 8
#define COLOR 15

void *font = malloc(256 * FONT_WIDTH * FONT_HEIGHT * BYTESPERPIXEL);

gl_expandfont(FONT_WIDTH, FONT_HEIGHT, COLOR, gl_font8x8, font);
gl_setfont(FONT_WIDTH, FONT_HEIGHT, font);
```
```