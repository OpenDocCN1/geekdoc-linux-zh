
```c
gint eventDelete(GtkWidget *widget,
        GdkEvent *event,gpointer data);
gint eventDestroy(GtkWidget *widget,
        GdkEvent *event,gpointer data);
gboolean eventDraw(GtkWidget *widget,
        GdkEvent *event,gpointer data);

#define WIDTH 400
#define HEIGHT 200

int main(int argc,char *argv[])
{
    GtkWidget *app;
    GtkWidget *area;

    gnome_init("pixels","1.0",argc,argv);
    app = gnome_app_new("pixels","Drawing Pixels");
    gtk_signal_connect(GTK_OBJECT(app),"delete_event",
               GTK_SIGNAL_FUNC(eventDelete),NULL);
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
    static GdkPoint points[] = {
        { 50,100 }, { 51,100 }, { 50,101 }, { 51,101 },
        { 60,100 }, { 61,100 }, { 60,101 }, { 61,101 },
        { 55,105 }, { 56,105 }, { 55,106 }, { 56,106 },
        { 50,110 }, { 51,111 }, { 52,112 }, { 53,112 },
        { 54,113 }, { 55,113 }, { 56,113 }, { 57,113 },
        { 58,112 }, { 59,112 }, { 60,111 }, { 61,110 },
    };
    gint x = WIDTH/4;
    gint i = 0;

    gint i;

    while(y < HEIGHT) {
        for(i=0; i<10; i++) {
            gdk_draw_point(widget->window,
                widget->style->black_gc,
                x++,
                y);
        }
        for(i=0; i<10; i++) {
            gdk_draw_point(widget->window,
                widget->style->white_gc,
                x,
                y++);
        }
    }

    srand(1);
    for(i=0; i<2000; i++) {
        x = (int)((double)rand()*WIDTH)/RAND_MAX);
        y = (int)((double)rand(*HEIGHT)/RAND_MAX);
        gdk_draw_point(widget->window,
            widget->style->white_gc,
            x,
            y);
    }

    gdk_draw_points(widget->window,
        widget->style->black_gc,
        points,
        sizeof(points)/sizeof(GdkPoint));

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

第 26 行至第 31 行创建绘图区域，将其附加到应用程序窗口，并为其分配回调函数 `eventDraw()`。像素是在回调函数中绘制到窗口上的。

从第 51 行开始的循环像图 10-2 中所示那样在窗口上画出一条对角线锯齿线。第 53 行对 `gdk_draw_point()` 的调用绘制一个黑色像素。因为它位于一个循环中（从第 52 行开始），且每次绘制像素时 `x` 坐标都会递增，所以结果就是锯齿线的水平部分。第二个循环从第 58 行开始，调用 `gdk_draw_point()` 在递增 `y` 坐标的同时绘制白色像素——这就是锯齿线的垂直部分。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_335_0.png)

**图 10-2:** 绘制到窗口上的单个像素

第 66 行至第 73 行在窗口周围随机散布白色像素。使用常量值为随机数生成器播种（如第 66 行对 `srand()` 的调用），会生成相同的伪随机数序列。在这种情况下，能够重放相同序列是一种优势，因为窗口每次暴露时都能以完全相同的方式绘制自身。第 68 行和第 69 行调用 `rand()` 为 `x` 和 `y` 生成新值。函数 `rand()` 返回 0 到 `RAND_MAX` 之间的数字，因此需要将数字缩放到可能的像素位置范围。对 `gdk_draw_point()` 的调用使用白色 `GdkGC` 绘制像素。你可以在图 10-2 中看到散布在窗口周围的白色斑点。

第 76 行至第 79 行使用另一种方法绘制像素。不是计算每个像素的位置并逐个绘制，而是将像素位置存储在第 39 行定义的 `GdkPoint` 结构体数组中。当作为黑色像素绘制时，它表现为图 10-2 左侧的笑脸。`GdkPoint` 结构体仅包含一个 `x` 值和一个 `y` 值：

```c
struct _GdkPoint {
  gint16 x;
  gint16 y;
};
```

第 76 行对 `gdk_draw_points()` 的调用需要点数组的地址和数组成员的数量。第 79 行通过数组大小除以单个成员的大小来确定数组成员的数量。

有一个标准的 X 实用工具可以帮助你更轻松地检查像素。运行它时，从命令行输入 `xmag`，然后选择显示区域某部分的左上角——它不限于单个窗口。图 10-3 显示了本示例写入的像素详情。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_336_0.png)

**图 10-3:** 示例写入的像素详情

## 绘制和填充矩形

矩形可以绘制为色块或轮廓。通过结合两者，你可以拥有一个带轮廓的矩形。

```c
/** rectangles.c **/
#include <gnome.h>
```
