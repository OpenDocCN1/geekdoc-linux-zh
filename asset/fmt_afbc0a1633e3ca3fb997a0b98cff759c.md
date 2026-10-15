
### `configure_event`

* 创建合适大小的 `pixmap`
* 当然，每当窗口调整大小时都会调用此函数。
* 我们必须释放分配的内容。

```c
static gint configure_event(GtkWidget *widget, GdkEventConfigure *event)
{
  /* --- 如果创建了背景则释放 -- */
  if (pixmap) {
    gdk_pixmap_unref (pixmap);
  }
  /* --- 创建新大小的 pixmap -- */
  pixmap = gdk_pixmap_new (widget->window,
    widget->allocation.width,
    widget->allocation.height,
    -1);
  return TRUE;
}
```

### `expose_event`

* 当窗口暴露给视图或 `gdk_widget_draw` 例程被调用时，此例程被调用。
* 将背景 `pixmap` 拷贝到窗口。

```c
int expose_event (GtkWidget *widget, GdkEventExpose *event)
{
  /* --- 将 pixmap 拷贝到窗口 -- */
  gdk_draw_pixmap (widget->window,
    widget->style->fg_gc[GTK_WIDGET_STATE(widget)],
    pixmap,
    event->area.x, event->area.y,
    event->area.width, event->area.height);
  return FALSE;
}
```

### `quit`

* 退出应用程序

```c
void quit () {
  gtk_exit (0);
}
```

### `GetWidthHeight`

* 获取 `xpm` 数据的宽度高度

```c
void GetWidthHeight(gchar **xpm, int *width, int *height)
{
  sscanf(xpm [], "%d %d", width, height);
}
```

### `main`

* 程序从这里开始。

```c
int main(int argc, char *argv[])
{
  GtkWidget *window;
  GtkWidget *drawing_area;
  GtkWidget *vbox;
  /* -- 初始化 GTK+ -- */
  gtk_init(&argc, &argv);
  if (argc > 1) {
    bUseMask = FALSE;
  }
  /* 创建顶层窗口 -- */
  window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  hbox = gtk_hbox_new(FALSE, 0);
  gtk_container_add(GTK_CONTAINER(window), vbox);
  /* 创建绘制区域 -- */
  drawing_area = gtk_drawing_area_new();
  gtk_drawing_area_size(GTK_DRAWING_AREA(drawing_area), 200, 300);
  gtk_box_pack_start(GTK_BOX(vbox), drawing_area, TRUE, TRUE, 0);
}
```
