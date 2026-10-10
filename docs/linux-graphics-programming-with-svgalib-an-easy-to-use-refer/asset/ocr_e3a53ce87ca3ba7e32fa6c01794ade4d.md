![](bbox=[0.1, 0.08, 0.92, 0.46])

# Listing 7.3  The complete font code.

```
#define FONT_HEIGHT   8
#define FONT_WIDTH    8
#define COLOR         15

char words[] = "SVGAlb is fun!";
void *font = malloc(256 * FONT_WIDTH * FONT_HEIGHT * BYTESPERPIXEL);

gl_expandfont(FONT_WIDTH, FONT_HEIGHT, COLOR, gl_font8x8, font);
gl_setfont(FONT_WIDTH, FONT_HEIGHT, font);
gl_write(100, 100, words);
```

Some caution must be exercised with `gl_write()` and `gl_writen()`, however, as the following construction will not work:

```
gl_write(FONT_WIDTH, FONT_HEIGHT, "SVGAlb is fun!");
```

The reason is that the above string literal needs to end with `"\0"`, the standard "null character" (ASCII code 0) that tails all char arrays. Without it, you won't see anything on the screen. Let's try it again, this time with the proper string termination:

```
gl_write(FONT_WIDTH, FONT_HEIGHT, "SVGAlb is fun!\0");
```