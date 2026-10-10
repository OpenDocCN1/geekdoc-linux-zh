
```c
    gtk_signal_connect(GTK_OBJECT(app),"destroy",
                        GTK_SIGNAL_FUNC(eventDestroy),NULL);

    area = gtk_drawing_area_new();
    gtk_widget_set_usize(area,WIDTH,HEIGHT);
    gnome_app_set_contents(GNOME_APP(app),area);

    gtk_signal_connect(GTK_OBJECT(area),"event",
                        GTK_SIGNAL_FUNC(eventDraw),NULL);

    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}
gboolean eventDraw(GtkWidget *widget,
                   GdkEvent *event,gpointer data) {
    gint i;
    GdkPoint *p = malloc(sizeof(points));
    gint pointCount = sizeof(points)/sizeof(GdkPoint);

    for(i=0; i<pointCount; i++) {
        p[i].x = points[i].x;
        p[i].y = points[i].y;
    }
    gdk_draw_polygon(widget->window,
                     widget->style->black_gc,
                     FALSE,
                     p,
                     pointCount);

    for(i=0; i<pointCount; i++)
        p[i].x += 140;
    gdk_draw_polygon(widget->window,
                     widget->style->white_gc,
                     TRUE,
                     p,
                     pointCount);

    for(i=0; i<pointCount; i++)
        p[i].x += 140;
    gdk_draw_polygon(widget->window,
                     widget->style->black_gc,
                     FALSE,
                     p,
                     pointCount);
    gdk_draw_polygon(widget->window,
                     widget->style->white_gc,
                     TRUE,
                     p,
                     pointCount);

    for(i=0; i<pointCount; i++)
        p[i].x += 140;
    gdk_draw_polygon(widget->window,
                     widget->style->white_gc,
                     TRUE,
                     p,
                     pointCount);
    gdk_draw_polygon(widget->window,
                     widget->style->black_gc,
                     FALSE,
                     p,
                     pointCount);

    free(p);
    return(TRUE);
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

多边形本身定义在第 16 行的 `points` 数组中。由于使用相同的形状来绘制所有多边形，因此执行实际绘制的例程——即第 52 行名为 `eventDraw()` 的函数——需要创建该数组的副本并调整坐标，以便将多边形从一个位置移动到另一个位置。数组的工作副本在第 55 行构建，数组中点的总数在第 56 行计算。原始数组在第 58 行开始的循环中被复制。由于 `eventDraw()` 函数可以被调用任意次数，因此将分配的内存归还给系统至关重要——第 102 行通过调用 `free()` 实现了这一点。

图 10-5 中左侧的多边形由第 62 行对 `gdk_draw_polygon()` 的调用绘制。使用了内置的黑色 `GdkGC`。填充参数设置为 `FALSE`，这导致仅绘制轮廓。

第 68 行的循环通过将数组中所有 `x` 值增加 140，将工作多边形向右移动 140 个像素。第 70 行对 `gdk_draw_polygon()` 的调用使用内置的白色 `GdkGC` 绘制了一个填充的多边形。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_342_0.png)

**图 10-5：** 正在填充并绘制轮廓的多边形

第 76 行至第 87 行将数组坐标向右移动，并绘制两个多边形。第一个绘制的是黑色轮廓，第二个是白色填充的形状。适用于矩形的情况同样适用于多边形——轮廓比填充形式稍大。与矩形一样，垂直的右边比填充区域向右多一个像素，水平的底边比填充区域向下多一个像素。从图中第三个多边形边缘的图案可以看出，填充的多边形覆盖了部分像素，而留出了其他部分。

右侧的多边形由第 89 行至第 100 行绘制，先绘制填充区域，然后在上面绘制轮廓。这样，多边形周围的轮廓就是完整的。

## 绘制圆形、椭圆形和弧线

以下程序演示了曲线形状的绘制和填充。圆和椭圆使用同一个函数进行绘制（圆仅仅是高度和宽度相同的椭圆）。此函数还能够将绘制限制在圆形或椭圆的一部分。此外，还可以选择将图形绘制为轮廓，或填充由该形状创建的区域。

```c
/** arcs.c **/
#include <gnome.h>

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);
gboolean eventDraw(GtkWidget *widget, GdkEvent *event, gpointer data);

static void drawArcs(GtkWidget *widget, gint y, gint fill);
#define WIDTH 455
#define HEIGHT 140

int main(int argc, char *argv[])
{
    GtkWidget *app;
    GtkWidget *area;
    gnome_init("arcs", "1.0", argc, argv);
    app = gnome_app_new("arcs", "Drawing Circles and Ellipses");
    gtk_container_set_border_width(GTK_CONTAINER(app), 20);
    gtk_signal_connect(GTK_OBJECT(app), "delete_event",
```
