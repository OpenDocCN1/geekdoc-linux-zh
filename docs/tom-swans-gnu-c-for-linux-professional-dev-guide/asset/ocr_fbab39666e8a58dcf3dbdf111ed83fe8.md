The next step, shown in the sample listing in local function ShowFontName(), is to determine where in the window you want text to appear. For displaying lines of text, this means determining the relative y coordinate value for the text's height in pixels. Two values—ascent and descent—combined equal the maximum height of any character in the font. Adding a little to this value separates multiple lines. There are many other schemes for calculating text coordinate values relative to the window, but this formula works well enough in many cases:

```
y += font->ascent + font->descent + 10;
```

The next step sets the font into the GC obtained earlier. You don't have to do this every time before displaying a string—once set, the font remains in the GC until changed. Call XSetFont() to select a font loaded by XLoadQueryFont():

```
XSetFont(display, gc, font->fid);
```

Pass three arguments to the function: the X server display pointer, the gc variable obtained earlier for the window, and the fid (font ID) field for the loaded font. Finally, you are ready to display text in the selected font. Calling XDrawString() is the simplest method. It takes several arguments as shown here:

```
XDrawString(display, win, gc, 10, y, fontName, strlen(fontName));
```

Pass the display pointer, window ID, and graphics context variables as the first three arguments. The next two arguments are the x and y coordinate values of the pixel in the window where you want the string to appear. This pixel is typically located at the font's origin, a point just to the left of a character's base line. The ascent value mentioned earlier counts the pixels above this line; the descent counts those below. As a general rule, however, unless you really want to be fancy in positioning text, you can consider the coordinate values passed to XDrawString() to be about in the middle of lowercase letters with tails and smack on the bottom line of capitals. The last two arguments passed to XDrawString() are the string and its length in characters. You always must specify the length even when displaying an entire string.

> Note
> Don't assume that a graphics context refers to a default font in the X server. This might be true of some servers, but for best results, you should always load a font as explained in this section before displaying text by calling XDrawString() and other Xlib text-output functions.

# GRAPHICS OUTPUT FUNCTIONS

Xlib provides a number of functions, called graphics primitives, for drawing lines and shapes in windows. In general, to draw graphics, a client application performs three essential steps:

+   - It initializes a graphics context (GC) for the display and window.
+   - It calls Xlib graphics primitive functions such as XDrawLine().
+   - It stores information needed to redraw the window's contents—for example, when it is uncovered by another window.