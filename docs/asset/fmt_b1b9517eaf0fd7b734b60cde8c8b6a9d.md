
```c
/** hpaned.c **/
#include <gnome.h>

GtkWidget *makeHorizontalPane();
gint eventDelete(GtkWidget *widget,
                 GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
                 GdkEvent *event, gpointer data);

int main(int argc, char *argv[])
{
   GtkWidget *window;
   GtkWidget *pane;

   gnome_init("hpaned","1.0",argc,argv);
   window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
   gtk_window_set_default_size(GTK_WINDOW(window),
   200,200);

   gtk_signal_connect(GTK_OBJECT(window),
   "delete_event" ,
   GTK_SIGNAL_FUNC(eventDelete),
   NULL);

   gtk_signal_connect(GTK_OBJECT(window),
   "destroy" ,
   GTK_SIGNAL_FUNC(eventDestroy),
   NULL);

   pane = makeHorizontalPane();

   gtk_container_add(GTK_CONTAINER(window),pane);
   gtk_widget_show(window);
   gtk_main();
   exit(0);
}
GtkWidget *makeHorizontalPane() {
    int i;
    GtkWidget *leftText;
    GtkWidget *rightText;
    GtkWidget *paned;


    leftText = gtk_text_new(NULL,NULL);
    gtk_widget_show(leftText);
    rightText = gtk_text_new(NULL,NULL);
    gtk_widget_show(rightText);
    for(i=0; i<15; i++) {
      gtk_text_insert(GTK_TEXT(leftText),NULL,NULL,NULL,
"The quick brown fox jumped on the leftovers. \n",-1);

      gtk_text_insert(GTK_TEXT(rightText),NULL,NULL,NULL,
"The lazy gray dog slept by the leftovers. \n",-1);

    }


    paned = gtk_hpaned_new();
    gtk_widget_show(paned);
    gtk_paned_add1(GTK_PANED(paned),leftText);
    gtk_paned_add2(GTK_PANED(paned),rightText);

    return(paned);
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

```cpp
65    gint eventDestroy(GtkWidget *widget,
66                    GdkEvent *event, gpointer data) {
67       gtk_main_quit();
68       return(0);
69    }
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_153_0.png)

![](img/8bcc1ba72831c7d67cfc8b395deab95f_153_1.png)

从第 35 行开始的 `makeHorizontalPane()` 函数创建了一个分支容器，并将两个文本小部件插入其中。这些文本小部件在第 41 行至第 52 行之间创建并被填充了文本。

第 54 行对 `gtk_hpaned_new()` 的调用创建了一个水平分支小部件，其效果如图 5-13 和图 5-14 所示。

第 52 行对 `gtk_hpaned_new()` 函数的调用创建了一个新的水平分支小部件。在第 56 行和第 57 行，函数 `gtk_paned_add1()` 在左侧添加文本小部件，而 `gtk_paned_add2()` 在右侧添加文本小部件。

这就是全部内容。分支小部件及其包含的两个小部件会相互通信，以协调定位和大小调整。整个窗口可以调整大小，分隔条也可以左右移动，使所有小部件一起调整大小。小部件的最小尺寸不会限制分隔条的移动，可以将分隔条完全移到一侧，从而完全遮挡一个小部件，并将整个窗口分配给另一个小部件。

图 5-15 和图 5-16 展示了一个垂直分支容器。你可以通过更改示例代码中的一行来实现这种配置。第 54 行应变为：

```cpp
paned = gtk_vpaned_new();
```

其他内容可以保持不变。添加小部件到垂直 *分支* 容器时使用相同的函数。`gtk_paned_add1()` 函数在顶部添加一个小部件，而 `gtk_paned_add2()` 在底部添加一个小部件。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_154_0.png)

## **图 5-15：** 包含两个文本小部件的垂直分支

![](img/8bcc1ba72831c7d67cfc8b395deab95f_154_1.png)

## **图 5-16：** 包含两个文本小部件的垂直分支

可以调整分隔条的厚度和按钮的大小。例如，要生成如图 5-17 所示的配置，请在上述示例中的第 54 行后插入以下两个函数调用：

```cpp
gtk_paned_set_handle_size(GTK_PANED(paned), 30);
gtk_paned_set_gutter_size(GTK_PANED(paned), 20);
```

这使得手柄成为一个边长为 30 像素的正方形，并将分隔条宽度设置为 20 像素。然而，手柄的宽度受限于分隔条的宽度，因此最终手柄是一个 20x30 像素的矩形。默认手柄大小为 10，默认分隔条大小为 6。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_155_0.png)

## 布局容器

布局容器可以容纳任意数量的小部件。小部件通过 x 和 y 像素偏移量进行定位。该容器的大小没有限制，可以设置为你喜欢的高度和宽度。此外，还有一对特殊的调整对象，分别对应 x 轴和 y 轴，可用于指定容器的哪些部分可用。实际上，你就像通过一个舷窗查看容器窗口的某个部分一样；可以移动窗口，使其不同部分可见。

这个示例程序创建了一个布满按钮的布局容器，并使用一对滚动条的位置值来确定哪些按钮可见。

```cpp
 1 /** layout.c **/
 2 #include <gnome.h>
 3
 4 GtkWidget *makeLayout();
 5 void addButtons (GtkWidget *layout);
 6 gint eventDelete (GtkWidget *widget,
 7      GdkEvent *event, gpointer data);
 8 gint eventDestroy (GtkWidget *widget,
 9      GdkEvent *event, gpointer data);
10
11 int main (int argc, char *argv[])
12 {
13    GtkWidget *window;
14    GtkWidget *layout;
15
16    gnome_init ("layout", "1.0", argc, argv);
17    window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
```
