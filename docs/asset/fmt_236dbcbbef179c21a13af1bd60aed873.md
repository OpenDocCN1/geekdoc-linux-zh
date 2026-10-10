
此程序显示如图 7-5 所示的窗口。该窗口显示光标的名称和光标本身。它有两个按钮，可用于在列表中前后移动，从而同时更改显示的名称和光标。显示的名称是调用 `gdk_cursor_new()` 创建光标时所使用的名称。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_214_0.png)

**图 7-5：** 内置光标之一的名称和外观

第 16 行至 97 行定义了一个结构体数组，用于存储光标的名称和数值。在该结构体中，字符串 `name` 用于显示在调用 `gdk_cursor_new()` 时使用的名称，而 `type` 则是用于向系统标识光标的枚举值。

第 117 行至 119 行创建要显示的窗口，将其添加到顶级窗口，然后调用 `setCursor()` 将光标设置为表中的当前光标。（默认索引为 0。）请记住，在调用 `gtk_widget_show()` 之前，无法修改窗口的光标。

从第 150 行开始的函数 `makeBox()` 使用盒子（box）来构建布局。使用水平盒子（horizontal box）来容纳两个按钮，使用垂直盒子（vertical box）来容纳标签和水平盒子。每个按钮都分配了一个回调函数——“Previous”按钮调用 `previous()`，“Next”按钮调用 `next()`。

从第 125 行开始的回调函数 `next()` 将光标索引值加 1——如果尚未到达数组末尾。数组成员数量的计数是通过将数组总大小除以单个成员大小计算得出的。回调函数 `previous()` 在索引大于零时将索引减 1。在这两个函数中，如果索引值发生变化，则会调用 `setCursor()` 来更改当前光标。

从第 140 行开始的 `setCursor()` 函数将当前光标更改为索引所指向的数组中的那个。如果已经创建了一个光标，则在创建新光标之前先销毁旧光标。如果程序使用了多个光标，可以一次创建它们并在需要时重复使用。通过调用 `gdk_cursor_new()` 创建 `GdkCursor` 对象。在使用此新光标的 `gtk_label_set_cursor()` 调用中，新光标将变为顶级窗口及其子元素所使用的光标。（按钮和标签的光标也会随之更改。）最后，通过调用 `gtk_label_set_text()` 更新标签的文本，以显示光标的名称。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_215_0.png)

> **注意**
> 内置光标均由文件 `gtk/gdk/gdkcursors.h` 中的命名值列表定义，该文件被 `gtk/gdk/gtkcursors.h` 包含，并用作枚举的主体。光标列表相当稳定——其中大多数已经存在多年。不过，可能会出现新的条目，如果有这种情况，你需要更新编译到此程序中的名称和值列表。

## 创建光标

创建自定义光标是一件简单的事情。位图实用程序（bitmap utility）可用于创建光标及其对应的掩码（mask）。然后，可以将这两个位图直接转换为当前光标。

光标通常是黑白的。它要么具有黑色主体和白色边框，要么具有白色主体和黑色边框。这样，光标可以放在任何颜色（包括黑色或白色）上方，仍然可见。此外，光标通常保持较小尺寸，以减少干扰性。然而，并没有限制光标只能使用黑白两色，你可以选择喜欢的任意两种颜色。以下示例创建了一个较大的、红色的 X 形光标，带有黑色边框。

在光标中，像素有三种渲染方式。它可以用两种颜色之一绘制，或者可以保持透明（不绘制像素可以让背景像素透过来）。这种透明选项是掩码位图存在的原因。

这两个位图大小相同。如果与像素相关的掩码位为 0，则该像素不会被绘制——它是透明的。如果掩码位为 1，则该像素会用两种颜色之一进行绘制（取决于另一个位图中对应位的值）。

前文所述的位图实用程序可用于创建光标。光标设计及其掩码都是位图。对于以下示例，光标设计如图 7-6 所示，其掩码如图 7-7 所示。该光标设计与默认根窗口光标非常相似，热区（hot spot）位于其中心。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_216_0.png)

**图 7-6：** 光标的黑白像素

![](img/8bcc1ba72831c7d67cfc8b395deab95f_216_1.png)

**图 7-7：** 定义光标轮廓的掩码

实用程序生成的两个位图如下所示：

```c
/* xbitmap.xbm */
#define xbitmap_width 24
#define xbitmap_height 24
#define xbitmap_x_hot 12
#define xbitmap_y_hot 11
static unsigned char xbitmap_bits[] = {
  0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x3c, 0x00,
  0x3c, 0x7c, 0x00, 0x3e, 0xfc, 0x00, 0x3f, 0xfc,
  0x81, 0x3f, 0xf8, 0xc3, 0x1f, 0xf0, 0xff, 0x0f,
  0xe0, 0xff, 0x07, 0xc0, 0xff, 0x03, 0x80, 0xff,
  0x01, 0x80, 0xff, 0x01, 0x80, 0xff, 0x01, 0x80,
  0xff, 0x01, 0xc0, 0xff, 0x03, 0xe0, 0xff, 0x07,
  0xf0, 0xff, 0x0f, 0xf8, 0xc3, 0x1f, 0xfc, 0x81,
  0x3f, 0xfc, 0x00, 0x3f, 0xc7, 0x3e, 0x3c,
  0x3f, 0x3c, 0x00, 0x00, 0x00, 0x00, 0x00};
```

```c
/* xmask.xbm */
#define xmask_width 24
#define xmask_height 24
static unsigned char xmask_bits[] = {
    0x00, 0x00, 0x00, 0x3c, 0x00, 0x7c, 0x7e, 0x00,
    0x7e, 0xfe, 0xc0, 0x07, 0xfe, 0x81, 0xff, 0xfe,
    0xc3, 0xff, 0xfc, 0xe7, 0x3f, 0xf8, 0xff, 0x1f,
    0xf0, 0xff, 0x0f, 0xe0, 0xff, 0x07, 0xc0, 0xff,
    0x03, 0x80, 0xff, 0x01, 0x80, 0xff, 0x01, 0xc0,
    0xff, 0x03, 0xe0, 0xff, 0x07, 0x0f, 0x0f,
    0xf8, 0xff, 0x1f, 0xfc, 0xe7, 0x3f, 0xfe, 0xc3,
    0x7f, 0xfe, 0x81, 0x7f, 0xfe, 0x00, 0x7f, 0x7e,
    0x00, 0x7e, 0x3e, 0x00, 0x7c, 0x00, 0x00, 0x00};
```

以下示例程序使用这些位图创建光标，并将其分配为当鼠标位于应用程序顶级窗口上方时出现的光标：

```c
1 /** xbmcursor.c **/
2 #include <gnome.h>
3
4 gint eventDelete(GtkWidget *widget,
5     GdkEvent *event, gpointer data);
6 gint eventDestroy(GtkWidget *widget,
7     GdkEvent *event, gpointer data);
8
9 #include "xbitmap.xbm"
10 #include "xmask.xbm"
11
12 static GdkColor oneColor = {0,0xFFFF,0x0000,0x0000};
13 static GdkColor zeroColor = {0,0x0000,0x0000,0x0000};
14
15 int main(int argc, char *argv[])
16 {
17     GtkWidget *topLevel;
18     GdkCursor *cursor;
19     GdkBitmap *bitmap;
20     GdkBitmap *mask;
21
22     gnome_init("lib/xbmcursor","1.0",argc,argv);
23     topLevel = gtk_window_new(GTK_WINDOW_TOPLEVEL);
24     gtk_window_set_default_size(GTK_WINDOW(topLevel),
25             150,150);
26
27     gtk_signal_connect(GTK_OBJECT(topLevel),"delete_event",
```
