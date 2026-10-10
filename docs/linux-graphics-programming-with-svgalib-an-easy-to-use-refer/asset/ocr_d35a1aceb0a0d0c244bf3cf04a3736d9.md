You might be wondering how I knew what the RGB values were for the 16 primary VGA colors. What I did was somewhat primitive, but effective. First, I drew 16 colors with `vga_drawpixel()`. Next, I set the RGB palette with `gl_setrgbpalette()` and then I read the color values of the 16 pixels I had drawn with `gl_getpixlergb()`. Hey, it works. You can use this same procedure to deduce the RGB values for 256-color GIFs as well.

With that, `ScreenShot.c` is wrapped up. I’ve had some difficulties using it with highly-colored images, but this might be resolvable by using `gl_rgbcolor()` to define all your screen colors to match your `GIF_setcolor()` colors.

Of course, you might choose not to bother with gifsave at all. I included gifsave for versatility, but some of you might have deduced that you can replace all of it with two commands: vga1’s `gl_getbox()` and liblug’s `write_gif_file()`.

# Conclusion

Graphic files can save you a lot of time. This applies both to programming *and* to program execution (if you use a complicated image). They allow you to share your work with others, who might be on a different operating system. This will be especially relevant when you get to the chapter on creating a paint program.

Although SVGAlib has no provision for reading and writing from graphic files, knowing the specifications of the BMP file and having libraries such as liblug can make the task much easier. Don’t you agree?

# Summary Of Functions Introduced In This Chapter

Here is a summary of the functions covered in this chapter:

+   - void gl_putbox(int x, int y, int w, int h, void *dp)
+   - void gl_getbox(int x, int y, int w, int h, void *dp)
+   - int keyboard_init(void)
+   - void keyboard_close(void)
+   - int keyboard_keypressed(int scanode)
+   - int keyboard_update(void)
+   - void keyboard_waitforupdate(void)