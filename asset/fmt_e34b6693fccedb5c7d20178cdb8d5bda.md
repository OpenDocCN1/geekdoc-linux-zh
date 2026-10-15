
本示例创建了一个 `GtkPreview` 对象，并设置了一个回调函数，在其窗口中绘制一个矩形，如所示图 21-37。由于实际窗口必须存在，因此必须在窗口显示后的回调函数中执行绘制操作。

```c
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

`GtkProgressBar` 组件显示一个移动指示器，用于表示某些任务的完成百分比。

### 继承

`GtkProgressBar` -> `GtkProgress` -> `GtkWidget` -> `GObject`

### 函数

```c
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

```c
typedef enum {
    GTK_PROGRESS_CONTINUOUS,
    GTK_PROGRESS_DISCRETE
} GtkProgressBarStyle;

typedef enum {
    GTK_PROGRESS_LEFT_TO_RIGHT,
    GTK_PROGRESS_RIGHT_TO_LEFT,
    GTK_PROGRESS_BOTTOM_TO_TOP,
    GTK_PROGRESS_TOP_TO_BOTTOM
} GtkProgressBarOrientation;
```

如图 21-38 所示，此示例创建了一个水平进度条，其从左侧的 0 移动到右侧的 100。`GtkAdjustment` 部件用于初始化限制值和当前进度设置。应用程序需要调用 `gtk_progress_bar_update()` 函数才能使进度条移动。

```c
static GtkWidget *makeWidget()
{
    GtkWidgeet *bar;
    GtkObject *adjustment;
    adjustment = gtk_adjustment_new(70.25, 0.0, 100.0,
                                    0.25, 0.0, 0.0);
    bar = gtk_progress_bar_new_with_adjustment(
           GTK_ADJUSTMENT(adjustment));
    gtk_progress_bar_set_bar_style(GTK_PROGRESS_BAR(bar),
                                   GTK_PROGRESS_CONTINUOUS);
    gtk_progress_bar_set_orientation(GTK_PROGRESS_BAR(bar),
                                     GTK_PROGRESS_LEFT_TO_RIGHT);
    return(bar);
}
```
