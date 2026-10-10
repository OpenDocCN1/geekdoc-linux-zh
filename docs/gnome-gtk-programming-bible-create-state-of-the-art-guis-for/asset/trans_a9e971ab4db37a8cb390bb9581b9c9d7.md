

## GtkPacker

```
typedef enum {
    GTK_ANCHOR_NW,
    GTK_ANCHOR_N,
    GTK_ANCHOR_NE,
    GTK_ANCHOR_S,
    GTK_ANCHOR_SW,
    GTK_ANCHOR_SE,
    GTK_ANCHOR_W,
    GTK_ANCHOR_E
} GtkAnchorType;
```

以下示例创建了图 21-36 中显示的窗口。向容器中添加了两个按钮，但每个按钮适用的规则不同。

```
static GtkWidget *makeWidget()
{
    GtkWidget *packer;
    GtkWidget *button;

    packer = gtk_packer_new();

    button = gtk_button_new_with_label("First Button");
    gtk_packer_add_defaults(GTK_PACKER(packer),button,
                        GTK_SIDE_LEFT,GTK_ANCHOR_SOUTH,GTK_FILL_Y);

    button = gtk_button_new_with_label("Second Button");
    gtk_packer_add_defaults(GTK_PACKER(packer),button,
                        GTK_SIDE_LEFT,GTK_ANCHOR_CENTER,GTK_PACK_EXPAND);

    gtk_widget_set_usize(GTK_WIDGET(packer),200,200);
    return(packer);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_627_0.png)

图 21-36：一个 `GtkPacker` 组件，包含使用不同规则的两个按钮

## GtkPaned

这是 `GtkHPaned` 和 `GtkVPaned` 的基类。

### 继承

GtkPaned --> GtkContainer --> GtkWidget --> GObject

### 函数

```
void gtk_paned_add1(GtkPaned *paned, GtkWidget *widget)
void gtk_paned_add2(GtkPaned *paned, GtkWidget *widget)
void gtk_paned_compute_position(GtkPaned *paned,
            gint allocation, gint child1_req, gint child2_req)
GtkType gtk_paned_get_type(void)
void gtk_paned_pack1(GtkPaned *paned, GtkWidget *widget,
            gboolean resize, gboolean shrink)
void gtk_paned_pack2(GtkPaned *paned, GtkWidget *widget,
            gboolean resize, gboolean shrink)
void gtk_paned_set_gutter_size(GtkPaned *paned, guint16 size)
void gtk_paned_set_handle_size(GtkPaned *paned, guint16 size)
void gtk_paned_set_position(GtkPaned *paned, gint position)
```

## GtkPixmap

`GtkPixmap` 组件包含一个基于内存（RAM）的窗口。您可以像操作普通窗口一样在其上渲染图形，但它本身不会显示任何内容。

### 继承

GtkPixmap --> GtkMisc --> GtkWidget --> GObject

### 函数

```
void gtk_pixmap_get(GtkPixmap *pixmap, GdkPixmap **val,
            GdkBitmap **mask)
GtkType gtk_pixmap_get_type(void)
GtkWidget *gtk_pixmap_new(GdkPixmap *val, GdkBitmap *mask)
void gtk_pixmap_set(GtkPixmap *pixmap, GdkPixmap *val,
            GdkBitmap *mask)
void gtk_pixmap_set_build_insensitive(GtkPixmap *pixmap,
            guint build)
```

`GtkPixmap` 的示例请参见第 7 章。

## GtkPixmapMenuItem

`GtkPixmapMenuItem` 组件用于调整菜单按钮的位置，以便在文本左侧为位图或切换按钮的出现腾出空间。在 GNOME 菜单中，系统会根据需要自动创建 `GtkPixmapMenuItem`。

### 继承

`GtkPixmapMenuItem` -> `GtkMenuItem` -> `GtkItem` -> `GtkBin` -> `GtkContainer` -> `GtkWidget` -> `GtkObject`

### 函数

```c
GtkType gtk_pixmap_menu_item_get_type(void)
GtkWidget *gtk_pixmap_menu_item_new(void)
void gtk_pixmap_menu_item_set_pixmap(
    GtkWidget *menu_item, GtkWidget *pixmap)
```

`GtkPixmapMenuItem` 由菜单生成软件内部使用，相关示例位于第 8 章。

## GtkPlug

`GtkPlug` 组件是一个顶层窗口，它可以被提供给创建它的进程之外的另一个进程使用。该独立进程使用 `GtkSocket` 访问该组件，就像访问本地组件一样。

### 继承

`GtkPlug` -> `GtkWindow` -> `GtkBin` -> `GtkContainer` -> `GtkWidget` -> `GtkObject`

### 函数

```c
void gtk_plug_construct(GtkPlug *plug, guint32 socket_id)
guint gtk_plug_get_type()
GtkWidget *gtk_plug_new(guint32 socket_id)
```

## GtkPreview

`GtkPreview` 组件提供一个图形窗口以及一些管理它的函数。应用程序用它来预览图形操作并显示可用颜色。

### 继承

`GtkPreview` -> `GtkWidget` -> `GtkObject`

### 函数

```
void gtk_preview_draw_row(GtkPreview *preview, gchar *data, gint x, gint y, gint w)
GdkColormap *gtk_preview_get_cmap(void)
GtkPreviewInfo *gtk_preview_get_info(void)
guint gtk_preview_get_type(void)
GdkVisual *gtk_preview_get_visual(void)
GtkWidget *gtk_preview_new(GtkPreviewType type)
void gtk_preview_put(GtkPreview *preview, GdkWindow *window, GdkGC *gc, gint srcx, gint srcy, gint destx, gint desty, gint width, gint height)
void gtk_preview_reset(void)
void gtk_preview_set_color_cube(guint nred_shades, guint ngreen_shades, guint nblue_shades, guint ngray_shades)
void gtk_preview_set_dither(GtkPreview *preview, GdkRgbdither dither)
void gtk_preview_set_expand(GtkPreview *preview, gint expand)
void gtk_preview_set_gamma(double _gamma)
void gtk_preview_set_install_cmap(gint _install_cmap)
void gtk_preview_set_reserved(gint reserved)
void gtk_preview_size(GtkPreview *preview, gint width, gint height)
void gtk_preview_uninit(void)
```

### 枚举

```
typedef enum {
    GTK_PREVIEW_COLOR,
    GTK_PREVIEW_GRAYSCALE
} GtkPreviewType;

typedef enum {
    GDK_RGB_DITHER_NONE,
    GDK_RGB_DITHER_NORMAL,
    GDK_RGB_DITHER_MAX
} GdkRgbdither;
```

本示例创建了一个 `GtkPreview` 对象，并设置了一个回调函数，在其窗口中绘制一个矩形，如所示图 21-37。由于实际窗口必须存在，因此必须在窗口显示后的回调函数中执行绘制操作。

```
static GtkWidget *makeWidget() 
{
    GtkWidget *preview;
    preview = gtk_preview_new(GTK_PREVIEW_COLOR);
    gtk_preview_size(GTK_PREVIEW(preview), 200, 100);
    gtk_signal_connect(GTK_OBJECT(preview), "event",
    GTK_SIGNAL_FUNC(eventDraw), NULL);
    return(preview);
}

static gboolean eventDraw(GtkWidget *widget,
    GdkEvent *event, gpointer data) {
    GdkGC *gc;
    GdkColor foreground;
    GdkColormap *colormap;

    colormap = gdk_colormap_get_system();
    gc = gdk_gc_new(widget->window);
    gdk_color_parse("blue", &foreground);
    gdk_color_alloc(colormap, &foreground);
    gdk_gc_set_foreground(gc, &foreground);

    gdk_draw_rectangle(widget->window, gc,
    TRUE, 20, 10, 160, 80);
    return(TRUE);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_631_0.png)

## GtkProgress

`GtkProgress` 组件是 `GtkProgressBar` 的基类。

### 继承

`GtkProgress` -> `GtkWidget` -> `GObject`

### 函数

```c
void gtk_progress_configure(GtkProgress *progress,
    gfloat value, gfloat min, gfloat max)
gfloat gtk_progress_get_current_percentage(
    GtkProgress *progress)
char *gtk_progress_get_current_text(GtkProgress *progress)
gfloat gtk_progress_get_percentage_from_value(
    GtkProgress *progress, gfloat value)
char *gtk_progress_get_text_from_value(
    GtkProgress *progress, gfloat value)
GtkType gtk_progress_get_type(void)
gfloat gtk_progress_get_value(GtkProgress *progress)
void gtk_progress_set_activity_mode(GtkProgress *progress,
    guint activity_mode)
void gtk_progress_set_adjustment(GtkProgress *progress,
    GtkAdjustment *adjustment)
void gtk_progress_set_format_string(GtkProgress *progress,
    gchar *format)
void gtk_progress_set_percentage(GtkProgress *progress,
    gfloat percentage)
void gtk_progress_set_show_text(GtkProgress *progress,
    gint show_text)
void gtk_progress_set_text_alignment(GtkProgress *progress,
    gfloat x_align, gfloat y_align)
void gtk_progress_set_value(GtkProgress *progress,
    gfloat value)
```

## GtkProgressBar

GtkProgressBar 组件显示一个移动指示器，用于表示某些任务的完成百分比。

### 继承

GtkProgressBar -> GtkProgress -> GtkWidget -> GObject

### 函数

```
GtkType gtk_progress_bar_get_type(void)
GtkWidget *gtk_progress_bar_new(void)
GtkWidget *gtk_progress_bar_new_with_adjustment(
    GtkAdjustment *adjustment)
void gtk_progress_bar_set_activity_blocks(
    GtkProgressBar *pbar, guint blocks)
void gtk_progress_bar_set_activity_step(GtkProgressBar *pbar,
    guint step)
void gtk_progress_bar_set_bar_style(GtkProgressBar *pbar,
    GtkProgressBarStyle bar_style)
void gtk_progress_bar_set_discrete_blocks(
    GtkProgressBar *pbar, guint blocks)
void gtk_progress_bar_set_orientation(GtkProgressBar *pbar,
    GtkProgressBarOrientation orientation)
void gtk_progress_bar_update(GtkProgressBar *pbar,
    gfloat percentage)
```

### 枚举

```
typedef enum {
    GTK_PROGRESS_CONTINUOUS,
    GTK_PROGRESS_DISCRETE
} GtkProgressBarStyle;

typedef enum {
```

