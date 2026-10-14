however, you might want to inspect the function result more closely. This result can equal BitmapOpenFailed if the file cannot be opened, BitmapFileInvalid if the file contains unrecognized data, or BitmapNoMemory if enough memory is not available for allocating space to hold the image data.

After successfully loading a bitmap image, the next step converts it into a pixmap in a form that the X server can use to paint the window's background. To do this, call XCreatePixmapFromBitmapData() as shown here:

```
Pixmap pixmap =
    XCreatePixmapFromBitmapData(
        display,
        win,
        (char *) p,
        bmWidth, bmHeight,
        intBlackColor, intWhiteColor,
        DefaultDepth(display, intScreenNum));
```

The function result is a value of type Pixmap, which is merely an integer ID that identifies the converted image held in the X server. Pass the initialized server display pointer and window ID to this function. The third argument is a char pointer to the raw bitmap image data loaded by XReadBitmapFileData(). It could also be a pointer to image data created by other means—for example, a static array of byte values.

# Note

> The type cast expression (char *) in the preceding statement avoids a compiler warning. Apparently, XReadBitmapFileData() is designed to use an unsigned char* while XCreatePixmapFromBitmapData() uses a char* declaration for its bitmap pointer parameter. Because the char type is signed by default in ANSI C++, this results in a type-mismatch warning. This is a small discrepancy of no consequence, although both functions probably should declare their parameters simply as type char*.

The final arguments passed to XCreatePixmapFromBitmapData() are the width and height of the raw bitmap image, the background and foreground colors to use, and the depth of the screen obtained here by calling the DefaultDepth() macro for the X server display pointer and default screen number. The resulting pixmap is now ready for use in tiling the window's background. Call the following function to tell the server to use the image this way:
XSetWindowBackgroundPixmap(display, win, pixmap);

You can perform the preceding steps after creating and mapping the window before it first appears, or at anytime later. However, after the client has received at least one Expose event for the window, to make a change to the background visible, follow the preceding statement with calls to XClearWindow() and XFlush(). This forces the X server to repaint the window's background immediately and also results in a new Expose event sent to the client for the window. At that time, the client can repaint any graphics over the new tiled background.