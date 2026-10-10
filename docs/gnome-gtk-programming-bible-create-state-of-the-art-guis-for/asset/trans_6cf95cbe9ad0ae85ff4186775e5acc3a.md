
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

```cpp
18  gtk_window_set_default_size(GTK_WINDOW(window),
                  200,200);
19
20  gtk_signal_connect(GTK_OBJECT(window),
                 "delete_event",
                 GTK_SIGNAL_FUNC(eventDelete),
                 NULL);
21
22  gtk_signal_connect(GTK_OBJECT(window),
                 "destroy",
                 GTK_SIGNAL_FUNC(eventDestroy),
                 NULL);
23
24
25  layout = makeLayout();
26
27  gtk_container_add(GTK_CONTAINER(window),layout);
28
29  gtk_widget_show_all(window);
30
31  gtk_main();
32
33  exit(0);
34}
35
36 GtkWidget *makeLayout()
37{
38   GtkWidget *layout;
39   GtkWidget *vscroll;
40   GtkWidget *hscroll;
41   GtkWidget *table;
42   GtkAdjustment *horizAdj;
43   GtkAdjustment *vertAdj;
44
45   vertAdj = (GtkAdjustment *)gtk_adjustment_new(
                      0.0,
                      0.0,
                      1000.0,
                      1.0,
                      10.0,
                      20.0);
46
47   horizAdj = (GtkAdjustment *)gtk_adjustment_new(
                      0.0,
                      0.0,
                      1000.0,
                      1.0,
                      10.0,
                      20.0);
48
49   layout = gtk_layout_new(horizAdj,vertAdj);
50   gtk_layout_set_size(GTK_LAYOUT(layout),1000,1000);
51   addButtons(layout);
52
53   vscroll = gtk_vscrollbar_new(vertAdj);
54   hscroll = gtk_hscrollbar_new(horizAdj);
55
56   table = gtk_table_new(2,2,FALSE);
57}
```

```cpp
69 gtk_table_attach_defaults(GTK_TABLE(table),layout,
70 0,1,0,1);
71 gtk_table_attach(GTK_TABLE(table),vscroll,
72 1,2,0,1,
73 GTK_FILL,GTK_FILL,0,0);
74 gtk_table_attach(GTK_TABLE(table),hscroll,
75 0,1,1,2,
76 GTK_FILL,GTK_FILL,0,0);
77
78 return(table);
79 }
80 void addButtons(GtkWidget *layout)
81 {
82 gint i;
83 gint j;
84 GtkWidget *button;
85 gchar label[20];
86
87 for(i=100; i<1000; i += 100) {
88 for(j=100; j<1000; j+= 50) {
89 sprintf(label,"(%d,%d)",i,j);
90 button = gtk_button_new_with_label(label);
91 gtk_layout_put(GTK_LAYOUT(layout),button,i,j);
92 }
93 }
94 }
95 gint eventDelete(GtkWidget *widget,
96 GdkEvent *event,gpointer data) {
97 return(FALSE);
98 }
99 gint eventDestroy(GtkWidget *widget,
100 GdkEvent *event,gpointer data) {
101 gtk_main_quit();
102 return(0);
103 }
```

此示例创建了一个 2x2 的表格，该表格在左上角容纳一个布局小部件，在右侧和底部容纳滚动条——如图 5-18 所示。布局上在规则的间隔处放置了按钮。每个按钮的标签都是其在布局容器内的 x 和 y 坐标值。因此，你可以移动布局并查看所有按钮，布局使用的 `GtkAdjustment` 对象与滚动条使用的是相同的对象。

从第 36 行开始的 `makeLayout()` 函数创建了一个表格，并将各种小部件插入其中。该表格是一个 2x2 网格，左上角是布局，右上角是垂直滚动条，左下角是水平滚动条。右下角的单元格中没有任何内容。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_158_0.png)

### 图 5-18：布局容器使其窗口的部分区域可见

第 45 行至第 58 行创建了一对 `GtkAdjustment` 对象，用于控制布局容器的位置。其中一个调整对象用于水平定位，另一个用于垂直定位。`gtk_adjustment_new()` 函数需要六个浮点数值。第一个参数是初始值，它必须是介于第二和第三个参数值之间的某个值。第二个和第三个参数分别是布局容器位置的起始值和结束值。在这个示例中，垂直和水平大小均被设置，使得取值范围为 0 到 1000。

`gtk_adjustment_new()` 的最后三个参数是向任何软件元素（如滚动条）发出的指令，用于更新当前的 `GtkAdjustment` 值。参数 1.0 是步长增量。它是窗口可以移动的最小幅度。（在此示例中，值 1.0 恰好对应 1 像素。）参数 10.0 是布局跳转时要移动的单位数（即，当你用鼠标选择滚动条的槽位时）。最后一个值是一页的大小，如果你希望软件能够按整页上下移动，则可使用此值。

布局容器在第 60 行创建。它接收两个调整对象作为参数。要更改布局容器在可显示舷窗中的位置，只需调整调整对象的当前值即可。第 62 行设置布局对象的大小，第 62 行调用 `add_button()` 来用按钮填充它。从第 80 行开始的 `add_buttons()` 函数是一个简单的循环，它创建按钮并将它们以一个大矩形的形式放置在布局容器上。按钮通过第 91 行的 `gtk_layout_put()` 挂接在布局的表面上。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_158_1.png)

注意第 32 行对 `gtk_widget_show_all()` 的调用。这会导致指定小部件（在本例中为主窗口）及其所有子小部件被显示。其效果与对每个单独小部件调用 `gtk_widget_show()` 相同。
