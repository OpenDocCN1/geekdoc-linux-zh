

## 代码示例与分析

```c
97          y = new_y;
98      }
99      break;
100     case GDK_BUTTON_PRESS:
101         if (event->button.button == 1)
102             gnome_canvas_item_raise_to_top (item);
103         x = event->button.x;
104         y = event->button.y;
105         break;
106     default:
107         break;
108     }
109     return (0);
110 }
111 gint eventDelete(GtkWidget *widget,
112                 GdkEvent *event,gpointer data) {
113     return(FALSE);
114 }
115 gint eventDestroy(GtkWidget *widget,
116                  GdkEvent *event,gpointer data) {
117     gtk_main_quit();
118     return (0);
119 }
```

第 4 行和第 5 行包含了保存待显示的两个图像定义的文件的引用。如第 7 章所述，你可以将其他格式的图像转换为 XPM 格式，以便直接在程序内部进行编译。

第 37 行通过调用 `gdk_imlib_create_image_from_xpm()` 创建了一个 GdkImLibImage。该图像通过第 38 行对 `gnome_canvas_item_new()` 的调用被添加到画布中。GdkImLibImage 被作为“image”参数传递。x 和 y 的值指定了图像在画布窗口内的锚点，而 anchor 的值则确定了图像的哪一部分被放置在该点上。本示例使用 `GTK_ANCHOR_CENTER` 将图像的中心放置在锚点上。你可以通过使用表 9-1 中的值之一，将图像锚定在其某条边的中心或某个角落上。表中每个名称都有一个较长的形式——例如，名称 `GTK_ANCHOR_NORTH_EAST` 等同于 `GTK_ANCHOR_NE`。

尽管图像本身具有内置尺寸，但仍需同时提供高度和宽度值。图像会被缩放以适应你指定的尺寸，因此如果不希望图像自动缩放，你需要传入与原始图像定义相同的尺寸值。本示例中的三幅图像中有两幅按“实际”大小显示，但第 69 行和第 70 行设置了高度和宽度值的图像会自动重新缩放至更大尺寸，如图 9-5 所示。

### 表 9-1
**将图像连接到画布的锚点**

| 名称 | 通过...固定图像 |
| --- | --- |
| GTK_ANCHOR_CENTER | ...其中心 |
| GTK_ANCHOR_E | ...其右边缘的中点 |
| GTK_ANCHOR_N | ...其上边缘的中点 |
| GTK_ANCHOR_NE | ...其右上角 |
| GTK_ANCHOR_NW | ...其左上角 |
| GTK_ANCHOR_S | ...其下边缘的中点 |
| GTK_ANCHOR_SE | ...其右下角 |
| GTK_ANCHOR_SW | ...其左下角 |
| GTK_ANCHOR_W | ...其左边缘的中点 |

![](img/8bcc1ba72831c7d67cfc8b395deab95f_299_0.png)

一旦你的图像被添加到画布中，你可以选择将其删除，因为 GnomeCanvasItem 会创建自己的（可能经过缩放的）副本。第 37 行创建的图像在第 49 行被删除。另一幅图像，即第 51 行创建的那幅，直到它被用于创建两个 GnomeCanvasItem 时才被删除。它通过第 75 行对 `gdk_pixmap_destroy_image()` 的调用被删除。

回调函数 `dragEvent()` 基本上与前一个示例中的相同。在这个版本中，左键被选中用于将项目提升到显示堆栈的顶部（通过在第 101 行检查按钮编号实现）。左键也是用于在画布上移动项目的选定按键（通过在第 90 行检查状态位实现）。

## 画布文本

文本可以作为显示在画布上的项目使用。文本项具有与其他项目几乎相同的功能。以下示例创建三个文本项并将它们放置在画布上。

```c
/** canvastext.c **/
#include <gnome.h>

gint eventDelete(GtkWidget *widget,
              GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
              GdkEvent *event, gpointer data);
static gint dragEvent(GnomeCanvasItem *item,
                 GdkEvent *event, gpointer data);

#define WIDTH 600
#define HEIGHT 75

int main(int argc, char *argv[]) {
    GtkWidget *app;
    GtkWidget *canvas;
    GnomeCanvasGroup *rootGroup;
    GnomeCanvasItem *item;

    gnome_init("canvastext", "1.0", argc, argv);
    app = gnome_app_new("canvastext",
                        "Gnome Canvas Text");
    gtk_signal_connect(GTK_OBJECT(app), "delete_event",
                      GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(app), "destroy",
                      GTK_SIGNAL_FUNC(eventDestroy), NULL);

    canvas = gnome_canvas_new();
    gtk_widget_set_usize(canvas, WIDTH, HEIGHT);
    gnome_canvas_set_scroll_region(GNOME_CANVAS(canvas),
                         0.0, 0.0, WIDTH, HEIGHT);
    rootGroup = gnome_canvas_root(GNOME_CANVAS(canvas));
    gnome_app_set_contents(GNOME_APP(app), canvas);

    item = gnome_canvas_item_new(rootGroup,
                                 gnome_canvas_text_get_type(),
                                 "text", "This is on the left.",
                                 "x", (double)(WIDTH / 2),
                                 "y", (double)25,
                                 "anchor", GTK_ANCHOR_E,
                                 NULL);

    gtk_signal_connect(GTK_OBJECT(item), "event",
                       (GtkSignalFunc)dragEvent, NULL);

    item = gnome_canvas_item_new(rootGroup,
                                 gnome_canvas_text_get_type(),
                                 "text", "and this is on the right.",
                                 "x", (double)(WIDTH / 2),
                                 "y", (double)25,
                                 "anchor", GTK_ANCHOR_W,
                                 NULL);
    gtk_signal_connect(GTK_OBJECT(item), "event",
                       (GtkSignalFunc)dragEvent, NULL);

    item = gnome_canvas_item_new(rootGroup,
                                 gnome_canvas_text_get_type(),
                                 "text", "These larger red letters"
                                         " go all the way across.",
                                 "font", "12x24",
                                 "x", (double)(WIDTH / 2),
                                 "y", (double)50,
                                 "fill", "red",
                                 "anchor", GTK_ANCHOR_CENTER,
                                 NULL);
    gtk_signal_connect(GTK_OBJECT(item), "event",
                       (GtkSignalFunc)dragEvent, NULL);
    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}

static gint dragEvent(GnomeCanvasItem *item,
                      GdkEvent *event, gpointer data) {
    static gint x;
    static gint y;
    gint new_x;
    gint new_y;

    switch(event->type) {
    case GDK_MOTION_NOTIFY:
        if(event->button.state & 0x00000100) {
            new_x = event->button.x;
            new_y = event->button.y;
            gnome_canvas_item_move(item,
                                   (double)(new_x - x),
                                   (double)(new_y - y));
            x = new_x;
            y = new_y;
        }
        break;
    case GDK_BUTTON_PRESS:
        if(event->button.button_num == 1)
            gnome_canvas_item_raise_to_top(item);
        x = event->button.x;
        y = event->button.y;
        break;
    default:
        break;
    }
    return(0);
}

gint eventDelete(GtkWidget *widget,
    GdkEvent *event,gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget,
    GdkEvent *event,gpointer data) {
    gtk_main_quit();
    return(0);
}
```

三个文本项中的第一个通过第 36 行对 `gnome_canvas_item_new()` 的调用创建。文本本身被指定为一个字符串。你指定 x 和 y 坐标，并使用锚点来指定文本相对于用于定义文本项位置的点如何放置。可能的锚点位置列于表 9-1（在上一节中）。第一个文本项通过其右侧（即东端）连接到该点。

在第 46 行定义的第二个文本项使用与第一个相同的锚点，但它通过其左侧（即西端）连接到该点。因此，这两行文本连接在一起，看起来像是一行，如图 9-6 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_302_0.png)

**图 9-6：** 文本作为画布上的项目呈现

第三个文本项定义在第 56 行。该文本位于距离画布顶部 50 像素且在窗口水平中心的位置。使用锚点将文本通过其中心连接到该点，结果是居中的文本。指定了文本的颜色和字体名称。

