```
```
x = 0;
c = white;
book_example(x, y, c);
vga_getch();

vga_setmode(TEXT);

return 0;
}
```
```

Now that's entertainment! (Well, maybe if you're intoxicated.) Nevertheless, it does work as planned. To speed things up, you could decrement x by more than one pixel per cycle. For example, try this:

```
```
for (x = 300; x > 0; x -= 5)
```
```

By experimenting with different values, you can find the speed that's right for your application.

A word of caution, though—the simplicity of this method is offset by the fact that it produces programs that only look goon on your computer, or others with the same processor and clock speed.

# ## Animation With Vgagl

As always, *vgagl* can do it better, faster, and with less typing on your part. Recall **gl_getbox()** and **gl_putbox()** from the last chapter; they'll make things a lot easier for you. Here's how you might animate using vgagl:

+   1. Take a “snapshot” of the background with **gl_getbox()**. That space is now saved in memory and is pointed to by *\*dp*. Remember? It's **gl_getbox(int x, int y, int w, int h, void \*dp)**.
+   2. Draw your image in the same location.
+   3. Now take a snapshot of the image you just drew, using a different pointer.
+   4. Finally, use **gl_putbox()** to alternate placing the two images on the screen. Erase with the first image (the blank background), move your point of reference, and then redraw with the second image.

I don't know about you, but I find that square in Listing 10.3 a little boring. Let's read in an image from a GIF file and play with that, shall we? That will necessitate using good ol' ltbgu from Chapter 9—no problem there.

For this next example, let's assume that the GIF has 256 colors and is sized 10 pixels wide by 10 pixels high. Remember to use the **-Jlug** command line flag when compiling (see Chapter 9 for more details). You'll find the code for this example in Listing 10.4.