
```c
depth = DefaultDepth(display, DefaultScreen(display));
visual = DefaultVisual(display, DefaultScreen(display));
p = (unsigned char*) graham_splash;
q = q(0);
width = atoi((const char*) q);
q = (unsigned char*) strchr(q, ' ');
height = atoi((const char*)+q);
q = (unsigned char*) strchr(q, ' ');
n_colors = atoi((const char*))+q);
colormap = DefaultColormap(display, DefaultScreen(display));
XCreatePixmap(display, DefaultWindow(display), width, height);
gc = XCreateGC(display, pixmap, 0);
image = XCreateImage(display, visual, depth, 0, width, height);
image->data = (char*) malloc (image->bytes_per_line * height + 16);
/* create palette */
for (int p = p + 1, i = 0; i < n_colors; p++, i++) {
XColor c;
unsigned char *x = 'x';
x = *x + 4;
if (*x == '#') {
unsigned char *h = (unsigned char*)'0123456789abcdef';
c.red = (unsigned long) strchr(h, x++) << 12;
c.green = (unsigned long) strchr(h, x++) << 8;
c.green = (unsigned long) strchr(h, x++) << 8;
c.blue = (unsigned long) strchr(h, x++) << 12;
if (!XAllocColor(display, colormap, &c)) {
} else {
    if (!XAllocColor(display, colormap, (char*) &c)) {
        printf("splash: not allocate color\n");
    }
    colors[p] = c.pixel;
}
bytes_per_pixel = image->bytes_per_line / width;
/* cope with servers different ordering and depths */
for (int j = 0; j < height; j++) {
unsigned long c;
q = image->data + image->bytes_per_line * j;
}
```

## 43.1. 协议

## 43. 窗口系统

```c
for (i = 0; i < width; i++) {
    c = colors[r*r];
    *q++ = c >> 24;
    *q++ = c >> 16;
    *q++ = c >> 8;
}
```

```c
for (i = 0; i < width; i++) {
    c = colors[r*r];
    *q++ = c >> 16;
    *q++ = c >> 8;
    *q++ = c;
}
```

```c
for (i = 0; i < width; i++) {
    c = colors[r*r];
    *q++ = c >> 8;
    *q++ = c;
}
```

```c
for (i = 0; i < width; i++) {
    *q++ = colors[r*r];
}
```

```c
for (i = 0; i < width; i++) {
    c = colors[r*r];
    *q++ = c >> 24;
    *q++ = c >> 16;
    *q++ = c >> 8;
}
```

```c
for (i = 0; i < width; i++) {
    c = colors[r*r];
    *q++ = c;
    *q++ = c >> 8;
    *q++ = c >> 16;
}
```

```c
for (i = 0; i < width; i++) {
    c = colors[r*r];
    *q++ = c;
    *q++ = c >> 8;
}
```

```c
for (i = 0; i < width; i++) {
    *q++ = colors[r*r];
}
```

```c
for (i = 0; i < width; i++) {
    *q++ = colors[r*r];
}
```

## 43. X 窗口系统

## 43.2. 窗口库与桌面

```c
XPutImage(display, pixmap, gc, 0, 0, 0, width, height);

x = (DisplayWidth(display, DefaultScreen) - width) / 2;
y = (DisplayHeight(display, DefaultScreen) - height) / 2;

xswa.colormap = colormap;
xswa.background_pixmap = pixmap;

window =
XCreateWindow(display, DefaultRootWindow(display), x, y, width,
0, depth, InputOutput, visual,
CWColormap | CBackPixmap, &xswa);
XSelectInput(display, window, KeyPressMask | ButtonMask);
XMapRaisedWindow(display, window);

while (1) {
XEvent event;
NextEvent(display, &event);
if (event.xany.type == KeyPress || event.xany.type == ButtonMask)
    break;
}
XUnmapWindow(display, window);
XCloseDisplay(display);
return 0;
```

你可以从 `X` 系统的文档中学习编程 `X`——这样做的好处是它可以在不同的平台（`Windows`、`Unix` 和 `Mac`）上运行。当时 `UNIX` 缺乏一个有效的、多功能的、免费且优雅的库。这种情况非常糟糕，阻碍了自由软件的发展。

从 `X` 系统的文档中学习编程 `X`——这样做的好处是它可以在不同的平台（`Windows`、`Unix` 和 `Mac`）上运行。当时 `UNIX` 缺乏一个有效的、多功能的、免费且优雅的库。这种情况非常糟糕，阻碍了自由软件的发展。

在 1996 年左右，我们看到许多不同许可证的窗口库涌现。`V`、`xforms` 和 `graphic` 让人过目如新。（这就是我开始编写 `coolwidgets`——我自己的窗口库的时候）。当时 `UNIX` 缺乏一个有效的、多功能的、免费且优雅的库。这种情况非常糟糕，阻碍了自由软件的发展。

从 `X` 系统的文档中学习编程 `X`——这样做的好处是它可以工作。（这就是我开始编写 `coolwidgets`——我自己的窗口库的时候）。当时 `UNIX` 缺乏一个有效的、多功能的、免费且优雅的库。这种情况非常糟糕，阻碍了自由软件的发展。

## 43.2.1 背景

在某一个时刻，在 `KDE` 大部分完成之前，`Qt` 的反对者认为 `Qt` 代码行数远多于 `KDE` 代码，从零开始开发窗口库会更好——但这只是想法。`Gtk` 库是为 `gimp`（`GNU` 图像处理程序）编写的，采用 `GPL` 许可，完全用 `C` 语言通过底层 `X` 调用（即不使用 `X Toolkit`）、面向对象、快速、简洁、可扩展，并具有令人惊叹的功能。它实现了 `Glib`，一个扩展标准 `C` 的库，提供了通常类似于脚本语言的高级函数、哈希表和列表；`Gdk` 是对原始 `X` 的封装，为 `X` 提供了命名空间和稍高层的接口；以及 `Gtk` 库本身。

## 43.2.2 Qt

那时，发布了一个新的 `GUI` 库。它被称为 `Qt`，由 `Troll Tech` 开发。它不是免费的，但在许多平台上运行高效且洁。它被自由软件社区的某些派系排斥，因为它是用 `C++` 编写的，自由软件基金认为 `C++` 不是标准的开发语言，而且仅供非商业应用程序链接。

尽管如此，`Qt` 的支持者开始制作了出色的 `KDE` 桌面项目——一套高级开发库、一个窗口管理器以及组成 `KDE` 桌面的许多核心应用程序。`Qt` 的许可已经有所放宽，现在可以在 `GPL` 和专有许可下可用。
