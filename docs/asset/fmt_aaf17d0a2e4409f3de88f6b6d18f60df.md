
```c
001 #include <gtk/gtk.h>
002 #include <stdlib.h>
003
004 static GtkPixmap *pmap;
005 static GtkGC *gc;
006 GtkObject *adj1, *adj2;
007
008 void
009 Adjustments(GtkObject *adj1, GtkObject *adj2, int width, int height)
010 GTK_ADJUSTMENT(adj1)->lower = 0.0;
011 GTK_ADJUSTMENT(adj2)->upper = (float) height - 1.0;
012 GTK_ADJUSTMENT(adj1)->step_increment = 1.0;
013 GTK_ADJUSTMENT(adj2)->page_increment = 25.0;
014 GTK_ADJUSTMENT(adj1)->page_size = 1.0;
015 GTK_ADJUSTMENT(adj2)->value = 0.0;
016
017 GTK_ADJUSTMENT(adj2)->lower = 0.0;
018 GTK_ADJUSTMENT(adj1)->upper = (float) width - 1.0;
019 GTK_ADJUSTMENT(adj2)->step_increment = 1.0;
020 GTK_ADJUSTMENT(adj1)->page_increment = 25.0;
021 GTK_ADJUSTMENT(adj2)->page_size = 1.0;
022 GTK_ADJUSTMENT(adj1)->value = 0.0;
023 }
024
025 static void
026 AdjustmentChanged(GtkAdjustment *w, gpointer data)
027 GtkWidget *drawing = (GtkWidget *)data;
028 int x = GTK_ADJUSTMENT(adj2)->value;
029 int y = GTK_ADJUSTMENT(adj1)->value;
030
031 gdk_draw_pixmap(drawing->window, gc, pmap, x, y, 0, 0, 100, 75);
032 }
033 main(int argc, char *argv)
034 int *argc;
035 char **argv[] =;
036 {
037 Gtkwidget *window, *hsb, *vsb, *vbox, *hbox, *drawing;
038 int width, height, x, y, depth;
040 int hsbwidth, hheight, vsbwidth, vsheight;
041 GtkBitmap *mask;
042
043 gtk_init(&argc, &argv);
044 window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
045 gtk_window_position(GTK_WINDOW(window), GTK_WIN_POS_MOUSE);
046 gtk_widget_set_size(window, 100, 75);
047 gtk_window_policy(GTK_WINDOW( window ), FALSE, FALSE, TRUE);
048 gtk_widget_show(window)
049 gtk_window_set_title(GTK_WINDOW(window), "GtkAdjustment Demo");
050 vbox = gtk_vbox_new(FALSE, 0);
051 gtk_container_add(GTK_CONTAINER( window ), vbox);
052 hbox = gtk_hbox_new(FALSE, 0);
053 gtk_box_pack_start(GTK_BOX( hbox ), FALSE, TRUE, 0);
054 drawing = gtk_drawing_area_new(0.0, 0.0, 1.0, 5.0, 0.0);
055 adj1 = gtk_adjustment_new(0.0, 0.0, 1.0, 5.0, 0.0);
056 gtk_signal_connect(GTK_OBJECT(adj1), "value_changed", GTK_SIGNAL_FUNC(AdjustmentChanged), drawing);
057 vsb = gtk_scrollbar_new(GTK_ADJUSTMENT(adj1));
058 gtk_box_pack_end(GTK_BOX( hbox ), vbox, FALSE, TRUE, 0);
059 adj2 = gtk_adjustment_new(0.0, 0.0, 1.0, 5.0, 0.0);
060 gtk_signal_connect(GTK_OBJECT(adj2), "value_changed", GTK_SIGNAL_FUNC(AdjustmentChanged), drawing);
061 hsb = gtk_hscrollbar_new(GTK_ADJUSTMENT(adj2));
062 gtk_box_pack_start(GTK_BOX( hbox ), drawing, FALSE, TRUE, 0);
063 gtk_widget_show_all(GTK_WIDGET( window ));
064 pmap = gdk_pixmap_create_from_window(drawing->window, &mask, (GtkColor*) NULL, "adjustment.xpm");
065 gc = gtk_gc_new(drawing->window);
066 gdk_window_get_geometry((GdkWindow*)hsb->window, &x, &y, &width, &height, &depth);
067 gdk_window_get_geometry((GdkWindow*)vbox->window, &x, &y, &width, &height, &depth);
068 gdk_window_get_geometry((GdkWindow*)pmap, &x, &y, &width, &height, &depth);
```

# GtkAdjustment 689

```
SetAdjustments(adj1, adj2, (width - 100) + vssbwidth,
      (height - 75) + hsbwidth);
gtk_main();
```

## 下一个示例

下一个示例与之前的非常相似。第二个示例程序没有加载图像，而是创建一个大小为 `512×512` 像素的离屏位图（`pixmap`）。该程序用 32 行 16×16 的矩形平铺了该位图（每行共绘制 32 个矩形）。每个矩形的颜色在绘制时是随机计算的。`page_size` 属性设置为 `16`，`lower` 设置为 `0`（如前文所示），`upper` 设置为窗口页面的 `page_size` 宽度，`step_increment` 值为 `16` 像素，而 `page_increment` 设置为 `32`。用户将看到每次点击滚动条时都会移动一行或一列（取决于点击了哪一个滚动条），而点击则会使显示移动两行或两列。我们设置了顺序，以便用户在滚动其他类型的数据（如电子表格中的单元格，或其他）时，滚动距离不小于显示的数据的大小。如果您正在管理一个包含特定高度单元格的表格，则滚动单位应基于单元格的高度（水平滚动条则基于宽度）。如果您正在显示某种类型的文本，垂直滚动条应该朝向显示文本的字体中字符的平均高度（以像素为单位，或者也许是该字体中最高字符的高度）。同样，在这种情况下，您将初始化一个水平滚动条调整对象，其滚动单位基于显示文本的字体中字符的平均宽度。

这里我仅展示创建位图的函数（供对细节感兴趣的读者）以及对 `SetAdjustments()` 函数所做的更改：

### 13.3 GtkAdjustment Example 2
