Tip
Certain pixmap dimensions might display faster on specific X servers. To find the ideal dimensions for your system, call XQueryBestTile().

The steps for creating a pixmap and using it to tile a window's background are complicated by the concept of depth in color displays. To be used for a window's background, a pixmap must have the same depth as the screen on which a window is displayed. There are some ways to subvert that rule by copying pixmaps to selected bit planes, but for most cases, the steps shown here are the ones to use for creating pixmaps that work on all types of X hardware.

Listing 27.12, xtile.cpp, shows the steps needed to read a bitmap file and convert it into a pixmap suitable for painting a window's background. Due to a possibly swelled ego coupled with a lack of artistic drawing skills, as Figure 27.6 shows, I demonstrate the basic steps for painting a window's background with a pixmap of my initials. (I always admire artists who can create credible-looking images in a 16-by-16 bitmap!) After the listing, I explain how to use the same technique with any pixmap image. Run the program and resize the window to see how it paints the entire background regardless of the window's size. Only a small 16-by-16 pixel bitmap is needed to produce this effect.

# Figure 27.6
Sample window tiled with a pixmap of the author's initials.

![](bbox=[0.32, 0.64, 0.62, 0.82])

# LISTING 27.12 XTILE.CPP (PARTIAL)

```
// Load bitmap from file for use as window background
//
unsigned int bmWidth, bmHeight;  // Bitmap width and height
int bmXhot, bmYhot;              // Bitmap hotspot (ignored)
unsigned char * p;               // Pointer to raw bitmap data
int result = XReadBitmapFileData(
    "ts.xbm",
    &bmWidth, &bmHeight,
    &p,
    &bmXhot, &bmYhot );
if (result != BitmapSuccess) {
    cerr << "Failed to open ts.bmp file" << endl;
    exit(1);
}

// Construct a pixmap using the raw bitmap data
//
Pixmap pixmap =
    XCreatePixmapFromBitmapData(
```