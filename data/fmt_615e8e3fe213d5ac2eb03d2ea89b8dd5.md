
```c
     GTK_SIGNAL_FUNC(eventDraw),NULL);

   gtk_signal_connect(GTK_OBJECT(area),"configure-event",

     GTK_SIGNAL_FUNC(eventConfigure),NULL);

   gtk_widget_show_all(app);

   gtk_main();

   exit(0);

}

gboolean eventDraw(GtkWidget *widget,

   GdkEvent *event,gpointer data) {

   gint xDelta = width / 5;

   gint yDelta = height / 5;

   gdk_draw_rectangle(widget->window,

     widget->style->white_gc,

     TRUE,

     0,0,

     width,height);

   gdk_draw_rectangle(widget->window,

     widget->style->black_gc,

     TRUE,

     xDelta,yDelta,

     width - (2 * xDelta),height - (2 * yDelta));

   xDelta *= 2;

   yDelta *= 2;

   gdk_draw_rectangle(widget->window,

     widget->style->white_gc,

     TRUE,

     xDelta,yDelta,

     width - (2 * xDelta),height - (2 * yDelta));

   return(TRUE);

}

gboolean eventConfigure(GtkWidget *widget,

   GdkEventConfigure *event,gpointer data) {

   width = event->width;

   height = event->height;

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

第 28 行至第 30 行创建了一个绘图区域并将其插入应用程序的主窗口中。每当主窗口大小调整时，绘图区域的大小也会随之调整。回调例程在第 32 行至第 35 行连接到绘图区域。`expose-event`在图形需要重绘时调用 `eventDraw()`。`configure-event`在绘图区域的高度或宽度发生变化时调用 `Configure()`。

矩形由第 41 行开始的回调函数 `eventDraw()` 绘制。用于确定矩形大小和位置的 `xDelta` 和 `yDelta` 值是根据高度和宽度的分数值计算得出的。第 46 行对 `gdk_draw_rectangle()` 的调用使用宽度和高度值将整个绘图区域清除为白色背景。使用分数值，第 52 行绘制一个黑色矩形，第 60 行在其内部绘制一个白色矩形。由于所有尺寸都是从窗口本身的大小计算得出的，图形将按比例绘制以适应窗口。图 10-10 展示了窗口在四种不同大小和形状下的外观。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_355_0.png)

**图 10-10：适应窗口重塑的矩形**

第 68 行的回调函数 `eventConfigure()` 在窗口配置发生变化时被调用。第 71 行和第 73 行获取新的高度和宽度值并存储它们，直到图形下一次被绘制。无需执行其他操作，因为`expose-event`总是跟随`configure-event`之后，并且会调用 `eventDraw()` 来渲染图形。

## 内存绘图和动画

有时，将图形写入内存中的某个位置而不是直接写入窗口会更方便。其中一个例子是在进行动画制作时，因为创建新帧的第一步是清除旧帧。如果直接在窗口上执行此操作，动画会在每一帧闪烁。幸运的是，可以绘制到位图中，然后使用该位图一次性更新整个窗口。

以下程序执行一个简单的动画：球从窗口顶部落下并在底部反弹。每个球会继续反弹，高度越来越低，直到最终从窗口的左侧或右侧消失。

```c
/** animation.c **/
#include <gnome.h>
#include <math.h>

static struct ballStruct {
	double x;
	double y;
	double xVelocity;
	double yVelocity;
} ball[5];

gint eventDelete(GtkWidget *widget,
	GdkEvent *event,gpointer data);
gint eventDestroy(GtkWidget *widget,
	GdkEvent *event,gpointer data);
gint nextFrame(gpointer data);
void newBall(struct ballStruct *b);
void nextBall(struct ballStruct *b);
gint nextFrame(gpointer data);

#define WIDTH 400
#define HEIGHT 300
#define GRAVITY 0.8
#define RADIUS 5
#define DIAMETER (RADIUS * 2)
#define INTERVAL 30

int main(int argc,char *argv[])
{
	int i;
	GtkWidget *app;
	GtkWidget *area;
	gnome_init("animation","1.0",argc,argv);
	app = gnome_app_new("animation",
		"Drawing Area Animation");
	gtk_container_set_border_width(GTK_CONTAINER(app),20);
```
