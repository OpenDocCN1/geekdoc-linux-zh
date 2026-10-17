
```c
// int bmXhot, bmYhot;   // Bitmap hotspot (ignored)
int result = XReadBitmapFileData(
"ts.xbm",
&bmWidth, &bmHeight,
&bitmap,
&bmXhot, &bmYhot );
if (result != BitmapSuccess) {
    cerr << "Failed to open ts.bmp file" << endl;
    exit(1);
}

// Fill global colors array using intBlackColor for the
// default color if any allocation fails.
//
GetColors(intBlackColor);

// Fill global points array with random coordinates
//
GetPoints(win, intWidth, intHeight); // Also sets polyColor

// The event loop.
//
bool done = false;
XEvent event;
while (!done) {
    XNextEvent(display, &event);
    switch (event.type) {
    case Expose:
        if (event.xexpose.count == 0) {
            XClearWindow(display, win);
            Paint(win, gc, intWidth, intHeight);
        }
        break;
    case ConfigureNotify:
        intWidth = event.xconfigure.width;
        intHeight = event.xconfigure.height;
        break;
    case ButtonPress:
        XFreePixmap(display, pixmap);
        GetPoints(win, intWidth, intHeight);
        XClearWindow(display, win);
        Paint(win, gc, intWidth, intHeight);
        break;
    case KeyPress:
        cout << "Keypress detected" << endl;
        done = true;  // Exit on any keypress
        break;
    }
}

// Free the pixmap and bitmap structures
//
XFreePixmap(display, pixmap);
XFree(bitmap);
```

```c
// Disconnect X server connection and exit.
// (Program may never get to here)
//
XCloseDisplay(display);
return 0;
}
```

```
...
```

```c
// Paint a colorful polygon
void Paint(Window win, GC gc, int winWidth, int winHeight)
{
    XSetTile(display, gc, pixmap);
    XSetFillRule(display, gc, EvenOddRule);
    XSetFillStyle(display, gc, FillTiled);
    XFillPolygon(display, win, gc, points, MAXPOINTS,
        Nonconvex, CoordModeOrigin);
}
```

为了保持程序简单，我将 `main()` 中的几个变量移出并设为全局变量。程序使用与 `xrainbow.cpp`（见本章清单 28.2）和 `xfill.cpp`（见清单 28.6）相同的颜色技术。要读取位图图像文件 `ts.xbm`，程序调用 `XReadBitmapFileData()`，其说明见 `xtile.cpp`（参考第 27 章清单 27.12）。书中未列出（但包含在 CD-ROM 上的文件中）的是本地函数 `GetPoints()` 中的额外步骤，该步骤填充全局 `points` 数组并为全局 `polyColor` 变量随机选择一种颜色。额外的编程将加载的位图图像转换为适合用于填充图形形状的 `pixmap`：

```c
int screenNum = DefaultScreen(display);
pixmap =
    XCreatePixmapFromBitmapData(
        display,
        win,
        (char *) bitmap,
        bmWidth, bmHeight,
        BlackPixel(display, screenNum),  // Foreground
        polyColor,                       // Background
        DefaultDepth(display, screenNum));
```

`pixmap` 变量是类型为 `Pixmap` 的全局对象。此步骤执行两项重要工作。它将单平面位图，也称为 `stipple`，转换为为客户端屏幕配置的结构。它还指定用于此图像的前景色和背景色。虽然前景色使用黑色，但这也可以是颜色像素值。与用纯色填充多边形（或其他形状）不同，`pixmap` 本身决定前景和背景像素值，而不是 `GC`。

该过程的最后一步是绘制多边形，由本地函数 `Paint()` 执行。此函数与 `xfill.cpp`（见清单 28.6）中的函数类似，但除了选择填充规则和样式外，还执行了为 `GC` 指定 `pixmap` 的额外步骤：

```c
XSetTile(display, gc, pixmap);
XSetFillStyle(display, gc, FillTiled);
```

这种情况下必须将样式设置为 `FillTiled` 才能使用 `pixmap` 作为多边形的背景。现在调用 `XFillPolygon()` 会根据当前生效的填充规则，用指定的颜色将 `pixmap` 平铺来绘制形状。

> Note
>
> 如果 `GC` 的样式设置为 `FillStippled` 或 `FillOpaqueStippled`，则会使用 `XSetStipple()` 设置的 `GC` 的位图。这与 `pixmap` 的使用方式类似，但由于 `stipple` 是一个单平面位图，因此 `GC` 的前景色和背景色会用于显示的像素值。

### SUMMARY

本章介绍了 X 编程的一些高级主题，例如调色板和填充多边形。调色板是一个查找表，用于将视频位平面值转换为 RGB 颜色或灰度强度级别。由于使用了调色板，X 客户端应用程序可以编写成在各种硬件上运行，从单位平面单色系统到 24 位真彩色显示器，后者正迅速成为标准，尤其是在 Linux 安装中。本章以选择线型和用纯色及 `pixmap` 图像填充多边形的细节结束。

有关本章介绍主题的更多信息，请参阅以下章节：

- Chapter 26, “Introducing X Programming”
- Chapter 27, “Controlling Xlib Input and Output”

## CHAPTER 29

## Introducing the V Class Library

### INSTALLATION

在从本书 CD-ROM 获取 V 的分发文件或从 Internet 下载后，按照以下步骤安装并编译库及其示例程序。在 CD-ROM 上，V 的分发文件存储在 `src/v` 目录的 `v-1_22_tar.gz` 文件中。这是一个“已打包并压缩”的文件，需要解包才能安装 V 的众多文件。将此文件复制到您的主目录或其他目录，然后输入以下命令将分发文件解包到自动创建的名为 `v` 的子目录中：

```
$ cp v-1_22_tar.gz /home/username
$ cd /home/username
$ gunzip v-1_22_tar.gz
$ tar -xvf v-1_22_tar
```

`gunzip` 实用程序会移除 `.gz` 文件名扩展名并扩展压缩文件。`tar` 实用程序会将单独归档的文件解包到各个子目录中。要在解包前检查这些文件名，请使用以下命令：

```
$ tar -tf v-1_22_tar
```

`tar` 完成后，您可以删除原始分发文件。接下来，您需要为在 Linux 下编译配置 V。为此，切换到 V 的新创建的主目录并查找名为 `Config.mk` 的文件。该文件包含 V 的 `Makefile` 编译库所需的目录和其他设置。您可能还想阅读 V 的 `Readme` 文件以获取额外的安装说明。
