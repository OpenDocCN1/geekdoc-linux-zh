
KDE 程序的第 11 行创建了一个 `Q` 对象，它是应用程序的顶级窗口。Win32 程序的第 21 到 33 行定义了主窗口，第 35 行的 `RegisterClassEx()` 调用将其向操作系统注册。如你所看到的，创建一个 Win32 顶级窗口比创建一个 KDE 顶级窗口需要更多的设置。这是因为 Win32 必须指定所有的设置；而 KDE 对所有内容都使用一组标准的默认值，并提供了可用函数以便你的程序可以在窗口构建后更改内容。

## 响应事件

KDE 和 Win32 程序都是事件驱动的。换句话说，两个程序都经过初始化并显示它们的窗口。KDE 和 Win32 等待事件（鼠标、键盘或其他任何事件）的发生。当事件发生时，会调用一个函数将信息从系统传递给应用程序。两个程序都需要响应两个特定事件：窗口大小改变时，以及窗口的所有或部分被暴露并应该绘制时。

在第 21 行，KDE 程序重写了继承自 `QWidget` 的虚方法 `paintEvent()`，该方法在窗口需要重绘时就会被调用。

该函数使用从最近一次调用 `resizeEvent()` 获取的大小和位置值来绘制一组嵌套的框。Win32 程序通过第 64 行的 `case` 语句实现了相同的功能。

在第 44 行，KDE 程序重写了继承自 `QWidget` 的虚方法 `resizeEvent`，该方法在窗口出现且在大小改变之前都会被调用。Win32 程序通过第 62 行的 `case` 语句实现了相同的功能。在两种情况下，新信息都存储在局部变量 `xBox1`、`yBox1`、`xBox2` 和 `yBox2` 中。

> 这两种处理事件的方法相似性大于差异。KDE 应用为每个事件指定了不同的回调方法。在 Win32 程序中，单个回调函数可以作为分发器，包含针对每个事件的独立语句——从而为每个事件调用单独的函数。

## 主循环

KDE 程序在第 14 行调用了 `exec`。该函数在程序需要绘图之前不会返回。它的工作是等待事件并导致调用适当的方法（或多个方法）。Win32 程序的主循环在第 44 到 47 行。`GetMessage()` 函数等待直到接收到事件并返回。`TranslateMessage()` 将键盘代码转换为字符，而 `DispatchMessage()` 将事件转发给正确的窗口。

## 全局退出

在关闭 Win32 程序时，调用带有 `WM_DESTROY` 的回调函数。第 89 行调用 `PostQuitMessage` 将退出消息放入输入队列；当它被读取时，程序终止。这给了你在关机之前进行清理工作的机会。

KDE 应用在 `QApplication` 对象的初始化过程中关闭。关闭顶级窗口会关闭应用程序。窗口顶部的标题栏连接到退出过程，以便可以使用鼠标关闭它。

## 全局数据

由于 Win32 程序是用 C 语言编写的，它需要使用全局存储来保留回调函数调用之间的的值。当然，Win32 版本可以用 C++ 编写，并设计对象来封装全局数据，但这种方法并不是 API 的一部分。在示例中，全局数据存储在 7 到 10 行的变量 `xBox1`、`yBox1`、`xBox2` 和 `yBox2` 中。

## 参考与机制

KDE 使用 C++ 编写，能够在类内部存储数据。在示例中，最外层的矩形存储在头文件 12 到 15 行的 `xBox1`、`yBox1`、`xBox2` 和 `yBox2` 中。

## GNOME 程序

为了比较，下面的示例是一个 GNOME-GTK+ 程序，它也向窗口填充框。与之前的示例一样，如果窗口大小改变，框的大小也会改变。窗口看起来如图 20-3 所示。

```c
/** checkbox.c (Gnome) **/
#include <gnome.h>

2 int eventDelete(GtkWidget *widget,
3 GdkEvent *event,gpointer data);
4 int eventDestroy(GtkWidget *widget,
5 GdkEvent *event,gpointer data);
6 gboolean eventExpose(GtkWidget *widget,
7 GdkEvent *event,gpointer data);
8 int eventConfigure(GtkWidget *widget,
9 GdkEvent *event,gpointer data);
10
11 #define STEP 3
12
13 static char name[] = "Box";
14 static int xBox1;
15 static int yBox1;
16 static int xBox2;
17 static int yBox2;
18
19 int main(int argc,char *argv[])
20 {
21 GtkWidget *app;
22 GtkWidget *area;
23
24 gnome_init(gnome_app_new(name,"1.0",argc,argv));
25 app = gnome_app_new(name,"Boxes in Boxes");
26 gtk_signal_connect(GTK_OBJECT(app),"delete_event",
27 GTK_SIGNAL_FUNC(eventDelete),NULL);
28 gtk_signal_connect(GTK_OBJECT(app),"destroy",
29 GTK_SIGNAL_FUNC(eventDestroy),NULL);
30
31 area = gtk_drawing_area_new();
32 gnome_app_set_contents(GNOME_APP(app),area);
33
34 gtk_signal_connect(GTK_OBJECT(area),"expose_event",
35 GTK_SIGNAL_FUNC(eventExpose),NULL);
36 gtk_signal_connect(GTK_OBJECT(area),"configure_event",
37 GTK_SIGNAL_FUNC(eventConfigure),NULL);
38
39 gtk_widget_show_all(app);
40 gtk_main();
41 }
42 exit(0);
43 }
44 gboolean eventExpose(GtkWidget *widget,
45 GdkEvent *event,gpointer data) {
46 int x1;
47 int y1;
48 int x2;
49 int y2;
50
51 x1 = xBox1;
52 y1 = yBox1;
53 x2 = xBox2;
54 y2 = yBox2;
55 while((x1 < x2) && (y1 < y2)) {
56 gdk_draw_line(widget->window,
57 widget->style->black_gc,
58 x1,y1,x2,y1;
59 gdk_draw_line(widget->window,
60 widget->style->black_gc,
61 x2,y1,x2,y2;
62 gdk_draw_line(widget->window,
63 widget->style->black_gc,
64 x2,y2,x1,y2;
65 gdk_draw_line(widget->window,
66 widget->style->black_gc,
67 x1,y2,x1,y1;
68 x1 = STEP;
69 y1 = STEP;
70 x2 = STEP;
71 y2 = STEP;
72 }
73 return(TRUE);
74 }
75 int eventConfigure(GtkWidget *widget,
76 GdkEvent *event,gpointer data) {
77 xBox1 = 10;
78 yBox1 = 10;
79 xBox2 = event->width - 10;
80 yBox2 = event->height - 10;
81 return(TRUE);
82 }
83 int eventDelete(GtkWidget *widget,
84 GdkEvent *event,gpointer data) {
85 return(FALSE);
86 }
87 int eventDestroy(GtkWidget *widget,
88 GdkEvent *event,gpointer data) {
89 gtk_main_quit();
90 return(0);
91 }
```

![](img/c47d54674a4d92abc6eebed0dd05f5fb_607_0.png)

该程序包含一个 `main()` 函数，用于初始化 GNOME、创建要显示的窗口、指定回调函数并进入执行循环。还有四个函数，每个函数都会在特定事件到达时执行。
