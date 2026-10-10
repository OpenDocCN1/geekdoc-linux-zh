
![](img/8bcc1ba72831c7d67cfc8b395deab95f_128_1.png)

![](img/8bcc1ba72831c7d67cfc8b395deab95f_128_2.png)

最后两个参数用于控件周围的填充。通过修改第 10 行到第 12 行为以下内容，可以创建图 4-23 中的窗口：

```c
#define HOMOGENOUS FALSE
#define X_MARGIN 5
#define Y_MARGIN 10
```

每个控件的左右两侧各增加 5 个像素，上下两侧各增加 10 个像素。这意味着控件在垂直方向上彼此分隔 20 个像素（每个控件贡献 10 个像素），并与顶部或底部分隔 10 个像素。所得窗口如图 4-23 所示，扩展后如图 4-24 所示。通过扩展和收缩，控件始终保持其距离。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_129_0.png)

**图 4-23**：带有间距的非均匀窗口

![](img/8bcc1ba72831c7d67cfc8b395deab95f_129_1.png)

**图 4-24**：扩展后的带有间距的非均匀窗口

## 重叠的控件

如果一个控件位于另一个控件的相同位置，前面的控件会遮挡后面的控件。将控件添加到表格的顺序决定了哪个控件在顶层——第一个添加的控件保持在顶层。这一特性作为软件开发技术可能价值不大，但你应该意识到这一点，以便如果某个控件缺失，你可以找出它去了哪里。以下程序演示了重叠：

```c
1 /*** overlap.c **/
2 #include <gnome.h>
3
4 GtkWidget *makeTable();
5 gint eventDelete(GtkWidget *widget,
6                 GdkEvent *event, gpointer data);
7 gint eventDestroy(GtkWidget *widget,
8                  GdkEvent *event, gpointer data);
9
10 int main(int argc, char *argv[])
11 {
12     GtkWidget *window;
13     GtkWidget *table;
14
15     gnome_init("overlap", "1.0", argc, argv);
16     window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
17     gtk_signal_connect(GTK_OBJECT(window),
18                        "delete_event",
19                        GTK_SIGNAL_FUNC(eventDelete),
20                        NULL);
21     gtk_signal_connect(GTK_OBJECT(window),
22                        "destroy",
23                        GTK_SIGNAL_FUNC(eventDestroy),
24                        NULL);
25
26     table = makeTable();
27     gtk_container_add(GTK_CONTAINER(window), table);
28     gtk_widget_show(window);
29     gtk_main();
30     exit(0);
31 }
32
33 GtkWidget *makeTable() {
34     GtkWidget *table;
35     GtkWidget *button;
36
37     table = gtk_table_new(5, 4, TRUE);
38     gtk_widget_show(table);
39
40     button = gtk_button_new_with_label("1,2,1,2");
41     gtk_table_attach_defaults(GTK_TABLE(table), button,
42             1, 2, 1, 2);
43     gtk_widget_show(button);
44
45     button = gtk_button_new_with_label("0,2,0,2");
46     gtk_table_attach_defaults(GTK_TABLE(table), button,
47             0, 2, 0, 2);
48     gtk_widget_show(button);
49
50     button = gtk_button_new_with_label("1,5,3,4");
51     gtk_table_attach_defaults(GTK_TABLE(table), button,
52             1, 5, 3, 4);
53     gtk_widget_show(button);
54
55     button = gtk_button_new_with_label("3,4,0,5");
56     gtk_table_attach_defaults(GTK_TABLE(table), button,
57             3, 4, 0, 5);
58     gtk_widget_show(button);
59
60     return (table);
61 }
62
63 gint eventDelete(GtkWidget *widget,
64                 GdkEvent *event, gpointer data) {
65     return (FALSE);
66 }
67
68 gint eventDestroy(GtkWidget *widget,
69                  GdkEvent *event, gpointer data) {
70     gtk_main_quit();
71     return (0);
72 }
```

此程序创建了一个 5x4 的表格，并在其上放置了四个按钮，如图 4-25 所示。在左上角，一个较小的按钮位于一个较大的按钮之上。较小的按钮在顶层，因为它先被添加到表格中。如果它们按相反的顺序添加，较小的按钮将完全不可见。右下角的两个按钮相互交错，但宽按钮先被添加到表格中，因此它位于顶层。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_131_0.png)

**图 4-25**：遮挡其他按钮部分的按钮

## 组合盒体和表格

盒体（Box）、表格和其他控件可以自由组合。你可以将包含控件的盒体存储在表格中，而这些表格又可以存储在其他盒体和控件中。组合盒体和表格的好处是，生成的存储层可以拥有自己的定位和重新调整大小的规则，使你能够随心所欲地布局。

此程序展示了如何嵌套盒体和表格来创建一个包含多个控件的窗口：

```c
1 /** collection.c **/
2 #include <gnome.h>
3
4 GtkWidget *makeTable();
5 GtkWidget *makeCheckButtons();
6 GtkWidget *makeTextEntry();
7 GtkWidget *makeButtonBox();
8 gint eventDelete(GtkWidget *widget,
9                GdkEvent *event, gpointer data);
10 gint eventDestroy(GtkWidget *widget,
11                GdkEvent *event, gpointer data);
12
13 int main(int argc, char *argv[])
14 {
15     GtkWidget *window;
16     GtkWidget *table;
17
18     gnome_init("collection", "1.0", argc, argv);
19     window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
20     gtk_signal_connect(GTK_OBJECT(window),
21                    "delete_event",
22                    GTK_SIGNAL_FUNC(eventDelete),
23                    NULL);
```
