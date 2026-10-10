```
    }
    gl_setpixel(x, y, color);
    
    return 0;
}
```

One pitfall that you might run into with this method is that the standard SVGAlib palette is rather dark (see Chapter 5 for a complete discussion). This, in turn, will make your buffer pixels not quite right, and your end result will appear to be nothing more than stupid-looking fat lines. To correct this, you may find it necessary to reset the palette to something brighter _before_ doing any drawing. Alternatively, if you want to leave the standard palette intact, you can simply use `gl_rgbcolor()` like I've done in Listing 6.7.

# **Listing 6.7 Adjusting colors with `gl_rgbcolor()`.**

```
    int c[256],
        i = 0,
        r,
        g,
        b;

    for (r = 0; r < 256; r += 51)
    {
        for (g = 0; g < 256; g += 51)
        {
            for (b = 0; b < 256; b += 51)
            {
                c[i] = gl_rgbcolor(r, g, b);
                i++;
            }
        }
    }
```

# # The Best Method

The next technique I'm about to show you was theorized and developed by Xiaolin Wu. It's interesting to note that Wu wasn't taken seriously at the time. His algorithm was seen as being too simple. Yet, today, it's taken for granted, thus becoming another irony in the world of computers. As for the professor who wouldn't listen to Wu, well, better luck next time.

You'll notice that this example also borrows heavily from `vga_drawline()`. The advantage here over the previous code is that the buffer pixels are shaded in a more intelligent manner. Rather than being all one color, their hues are based upon how far they lie from the “ideal” line. Have a look at Listing 6.8 to see what I mean.