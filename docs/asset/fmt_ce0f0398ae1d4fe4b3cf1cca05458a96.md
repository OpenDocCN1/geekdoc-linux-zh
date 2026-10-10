
```
"XXXXX XXXXXX",

"XXXXX XXXXXX",

"XX  RBBB",

"XX  RBBB",

"XX  RBBB",

"XXXXX XXXXXX",

"XXXXX XXXXXX",

"    RBBB  XX",

"    RBBB  XX",

"    RBBB  XX",

"XXXXX XXXXXX",

"XXXXX XXXXXX",

"      RBBB   "

};
```

此 XPM 文件的语法定义为字符字符串数组。第一行上的注释必须存在，因为它被实用工具用于确定文件类型。

第 4 行包含四个数字，用于描述后续的数据。第一个数字指定像素图宽 12 像素，第二个数字指定高 14 像素。下一个数字指定绘制图形时使用四种颜色。最后一个数字指定每个颜色使用一个字母作为标签（稍后详细介绍）。

第 5 行至第 9 行是颜色定义。每个字符串以一个被分配颜色的字符开始。可以使用任何 ASCII 字符。第 5 行将空格字符定义为名为 `None` 的颜色。这指定不绘制像素并产生透明效果，因为背景未被覆盖。第 6 行将白色值分配给字母 `X`。十六进制值 `ffffff` 是白（白绿蓝，RGB）的值（在十进制中，值为 255 255 255）。第 8 行将十六进制值 `0000ff` 分配给字母 `G` 以赋予其绿色。第 7 行使用名称为字母 `R` 定义颜色——该名称必须被分配文件 `/usr/X11R6/lib/X11/rgb.txt` 中的某个 RGB 值。

图形本身从第 9 行开始，持续到第 22 行。每个字符串长 12 个字符，因为图形宽 12 像素，且仅使用一个字符表示一个像素。有 14 个这样的字符串，因为图形高 14 像素。每个像素通过包含前面定义的四种颜色字符之一而被赋予值。

XPM 文件可用于包含大型、高分辨率且具有大量颜色的图像。例如，在 Linux 发行版中，有一个名为 `logo.gif` 的文件，其中包含 Linux 企鹅。您可以使用以下命令将 GIF 文件转换为 XPM 文件：

```
convert logo.gif logo.xpm
```

其中包含超过 24 位色彩信息，且颜色数量超过了单个字符可以表示的范围。整个 XPM 文件长达 560 行。以下是一个摘录：

```c
/* XPM */
static char *magic[] = {
"257 303 251 2",
" " c Gray0",
"#" c #08080800404",
"X" c #08080808000",
"@" c Gray3",
"0" c #10104040404",
"+" c #1010100404",
...
"(" c #f0f0b8b80808",
")" c #f8f8b0b00808",
"]" c #f8f8b8b80808",
```

```
" X c #f0f0b0b01010",
```

```
"_X c #f0f0b8b81010",
```

```
"XX c #f8f8b8b81010",
```

```
"BX c #d8d8d8d8b8e8",
```

```
"VX c #e0e0e0d8d8b8",
```

```
"CX c #f0f0e8e8b8d8",
```

```
"ZX c Gray88",
```

```
"AX c Gray91",
```

```
"SX c #e8e8e8f0f0",
```

```
"DX c #f0f0f0e8e8e8",
```

```
"FX c #f0f0f0f0e8e8",
```

```
"GX c Gray94",
```

```
"HX c #f8f8f8f8fbf8",
```

```
"JX c None",
```

. . .

这个 XPM 图形宽 257 像素，高 303 像素。它总共包含 251 种颜色，并使用 2 个字符来表示每种颜色。前几个字符看起来似乎是由单个字符定义的，但实际上使用了两个字符，因为空格充当第二个字符。在文件稍后部分可以看到，使用了句点和 `X` 字符。由于需要 2 个字符来指定颜色，因此定义像素数字行的每个字符串长度必须为 514 个字符（257 的两倍）。

此外，请注意颜色的十六进制数有 12 位数字，而不是 6 位。这仍然是 RGB 格式，但每种颜色是 16 位（四个十六进制数字）。在 XPM 文件中，这两种长度都是有效的——读取文件的软件会通过计算数字位数来确定格式。文件 `/usr/X11R6/lib/X11/rgb.txt` 中的颜色以及在其他许多地方找到的颜色，都定义为三个 8 位值。这个简单的程序将三个 8 位值转换为 XPM 所需的长和短十六进制字符串：

```c
/* hexcolor */
#include <stdio.h>
#include <stdlib.h>
char *usage[] = {
    "Usage: hexcolor r g b",
    "Enter the three RGB color values in the",
    "range of 0 to 256. The output is both a",
    "24-bit and 48-bit hexadecimal number of the",
    "color that can be used in an XPM file."
};
int main(int argc, char *argv[])
{
    int i;
    int r, g, b;
    if (argc < 4) {
        for (i = 0; i < 5; i++)
            printf("%s\n", usage[i]);
        exit(1);
    }
    r = atoi(argv[1]);
    g = atoi(argv[2]);
    b = atoi(argv[3]);
    printf("#%02X%02X%02X\n", r, g, b);
    printf("#%02X00%02X00%02X00\n", r, g, b);
    exit(0);
}
```

## 从数据中显示 XPM

由于 `convert` 工具几乎可以将任何图形文件转换为 XPM 文件，而且 XPM 格式是 C 源代码，因此几乎任何图形都可以直接编译到你的程序中。这主要用于图标、按钮标签、列表项目符号以及其他装饰性元素。下面的程序是一个直接将 XPM 文件编译到代码中并显示它的示例：

```c
/** show_xpm_data.c **/
#include <gnome.h>
gint eventDelete(GtkWidget *widget,
                  GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
                  GdkEvent *event, gpointer data);
#include "essPixmap.xpm"
int main(int argc, char *argv[])
{
    GtkWidget *topLevel;
    GdkBitmap *mask;
    GdkPixmap *pixmap;
    GtkWidget *pixmapWidget;
    GtkStyle *style;
    gnome_init("show_xpm_data", "1.0", argc, argv);
    topLevel = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_set_default_size(GTK_WINDOW(topLevel),
                               200, 50);
    gtk_widget_show(topLevel);
    gtk_signal_connect(GTK_OBJECT(topLevel), "delete_event",
                       GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(topLevel), "destroy",
                       GTK_SIGNAL_FUNC(eventDestroy), NULL);
    style = gtk_widget_get_style(topLevel);
    pixmap = gdk_pixmap_create_from_xpm_d(topLevel->window,
                                           &mask, &style->bg[GTK_STATE_NORMAL],
```
