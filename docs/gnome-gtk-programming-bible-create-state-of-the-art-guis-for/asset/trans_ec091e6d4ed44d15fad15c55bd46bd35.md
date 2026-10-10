

![](img/8bcc1ba72831c7d67cfc8b395deab95f_108_0.png)

```c
4  GtkWidget *makeBoxes();
5  gint eventDelete(GtkWidget *widget,
    GdkEvent *event, gpointer data);
6  gint eventDestroy(GtkWidget *widget,
    GdkEvent *event, gpointer data);
7  void buttonFill(GtkWidget *box, gboolean expand,
    gboolean fill, guint spacing);

9  static gchar *buttonLabel[] = {
    "Purple",
    "Red",
    "Lavender\nBlue",
    "Yellow"
};

11 int main(int argc, char *argv[])
12 {
    GtkWidget *window;
    GtkWidget *box;

    gnome_init("vertboxes", "1.0", argc, argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_signal_connect(GTK_OBJECT(window),
        "delete_event",
        GTK_SIGNAL_FUNC(eventDelete),
        NULL);
    gtk_signal_connect(GTK_OBJECT(window),
        "destroy",
        GTK_SIGNAL_FUNC(eventDestroy),
        NULL);

    box = makeBoxes();
    gtk_container_set_border_width(
        GTK_CONTAINER(window), 25);
    gtk_container_add(GTK_CONTAINER(window), box);
    gtk_widget_show(box);
```

```c
92 }
93 GtkWidget *button;
94 gint i;

96 for(i=0; i<4; i++) {
    button = gtk_button_new_with_label(buttonLabel[i]);
    gtk_box_pack_start(GTK_BOX(box), button,
        expand, fill, spacing);
    gtk_widget_show(button);
    }
}
97 gint eventDelete(GtkWidget *widget,
    GdkEvent *event, gpointer data) {
    return(FALSE);
}
98 gint eventDestroy(GtkWidget *widget,
    GdkEvent *event, gpointer data) {
    gtk_main_quit();
    return(0);
}
```

第 15 行定义的颜色名称中包含一个换行符，这使得按钮显示两行文本而不是一行。不同行数的按钮在尺寸上会有所不同，这有助于展示定位机制的工作原理。

第 35 行对 `makeBoxes()` 的调用创建了一个包含在水平框中的垂直框集合，第 38 行将该水平框添加到主窗口。从第 61 行开始的三个嵌套循环通过切换值设置来创建所有八种可能的组合。第 73 至 76 行为每个垂直框创建一个标签。标签仅包含数字以确保显示正常，但此前图 4-8 中显示的数字与图 4-7 中显示的含义相同。

## 框内控件的间距

在框内控件之间插入空间有多种方式。你可以指定要在框内每个控件周围添加的像素数量，也可以逐个控件指定添加的空间量，或者同时执行这两种操作。这在水平和垂直框中的工作方式相同。本示例展示了垂直框中间距的工作方式。

```c
1 /* spacebox.c **/
2 #include <gnome.h>
3
4 GtkWidget *makeBox();
5 gint eventDelete(GtkWidget *widget,
    GdkEvent *event, gpointer data);
6 gint eventDestroy(GtkWidget *widget,
```

```c
8 GdkEvent *event, gpointer data);
9
10 #define ALL_SPACE 5
11 #define FIRST_SPACE 0
12 #define SECOND_SPACE 0
13 #define THIRD_SPACE 0
14 #define FOURTH_SPACE 0
15
16 int main(int argc, char *argv[]) {
17     GtkWidget *window;
18     GtkWidget *box;
19
20     gnome_init("spacebox", "1.0", argc, argv);
21     window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
22     gtk_signal_connect(GTK_OBJECT(window),
23         "delete_event",
24         GTK_SIGNAL_FUNC(eventDelete),
25         NULL);
26     gtk_signal_connect(GTK_OBJECT(window),
27         "destroy",
28         GTK_SIGNAL_FUNC(eventDestroy),
29         NULL);
30
31     box = makeBox();
32     gtk_container_add(GTK_CONTAINER(window), box);
33     gtk_widget_show(window);
34     gtk_main();
35     exit(0);
36 }
37
38 GtkWidget *makeBox() {
39     GtkWidget *box;
40     GtkWidget *btn;
41
42     box = gtk_vbox_new(FALSE, ALL_SPACE);
43     gtk_widget_show(box);
44
45     btn = gtk_button_new_with_label("The First Widget");
46     gtk_box_pack_start(GTK_BOX(box), btn,
47         FALSE, FALSE, FIRST_SPACE);
48     gtk_widget_show(btn);
49
50     btn = gtk_button_new_with_label("The Second Widget");
51     gtk_box_pack_start(GTK_BOX(box), btn,
52         FALSE, FALSE, SECOND_SPACE);
53     gtk_widget_show(btn);
54
55     btn = gtk_button_new_with_label("The Third Widget");
56     gtk_box_pack_start(GTK_BOX(box), btn,
57         FALSE, FALSE, THIRD_SPACE);
```

```c
59     gtk_widget_show(btn);
60     }
61     btn = gtk_button_new_with_label("The Fourth Widget");
62     gtk_box_pack_start(GTK_BOX(box), btn,
63         FALSE, FALSE, FOURTH_SPACE);
64     gtk_widget_show(btn);
65     }
66     return(box);
67 }
68 int eventDelete(GtkWidget *widget,
69     GdkEvent *event, gpointer data) {
70     return(FALSE);
71 }
72 int eventDestroy(GtkWidget *widget,
73     GdkEvent *event, gpointer data) {
74     gtk_main_quit();
75     return(0);
76 }
```

第 10 至 14 行定义的常数是用于定位垂直框内控件的间距值。值 `ALL_SPACE` 通过在第 44 行创建框时作为 `gtk_box_vbox_new()` 的参数而应用于框内的每个控件。其他四个值通过作为第 49、54、59 和 64 行各控件插入调用 `gtk_box_pack_start()` 的参数而应用于每个控件。

示例程序中的间距值——框的值为 5，每个具体控件的值为 0——导致了图 4-9 所示的窗口。当框执行间距时，它只在控件之间插入空间。顶部控件上方或底部控件下方没有插入空间，但在每对控件之间插入了 5 像素的空间。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_112_0.png)

# **图 4-9**：所有控件的垂直间距相同

可以为每个单独的控件指定间距。你可以通过修改第 10 至 14 行如下所示来创建图 4-10 中的显示效果：

```c
#define ALL_SPACE  0
#define FIRST_SPACE  5
#define SECOND_SPACE 10
#define THIRD_SPACE  20
#define FOURTH_SPACE 40
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_113_0.png)

由于控件本身请求边距，因此第一个控件上方插入了 5 像素的空间。当框布局控件时，它会询问每个控件需要多少空间。因为第一个控件的间距值设为 5，所以它实际上获得了 10 个额外的像素——即控件主体上方 5 像素，下方 5 像素。第二个控件随后请求 10 的间距，因此第一个和第二个控件之间实际总共插入了 15 像素。类似地，第二个和第三个控件之间插入了 30 像素（10 + 20），第三个和第四个控件之间插入了 60 像素（20 + 40）。第四个控件下方插入了 40 像素。

你可以同时为整个框和每个单独的控件指定间距。例如，你可以通过将第 10 至 14 行修改为以下内容来创建图 4-11 中的显示效果：

```c
#define ALL_SPACE 5
#define FIRST_SPACE 2
#define SECOND_SPACE 10
#define THIRD_SPACE 10
#define FOURTH_SPACE 2
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_113_1.png)

每种情况下应用的实际间距是所有通常适用间距的总和。第一个控件距离窗口顶部 2 像素，因为框只在控件之间插入 `ALL_SPACE` 值。第一个和第二个控件之间的间距总共是 17 像素——框指定了 5 像素，第一个控件增加了 2，第二个控件增加了 10。第二个和

第三个控件之间的空间是 25 像素，这是总间距 5 和两个单独控件各 10 的间距之和。第三个和第四个控件之间有 17 像素，第四个控件下方有 2 像素。

由于分配给控件的间距值会同时加在其上方和下方，因此使用此方法无法实现某些间距组合。没有直接方法可以将三个控件放置在一起并在其上下插入空间，而不插入另一个框来容纳它们（如下一节所示）。但是，通过在单个框内使用间距，可以定义许多特殊布局。例如，图 4-12 中的布局是通过将常量更改为以下内容来实现的：

```c
#define ALL_SPACE 0
#define FIRST_SPACE 0
#define SECOND_SPACE 30
#define THIRD_SPACE 0
#define FOURTH_SPACE 5
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_114_0.png)

这展示了控件之间的距离可以有很大差异。第一个控件没有定义间距，因此它紧贴其包含框的顶部放置。第二个控件在其上下方都插入了 30 像素。第四个控件在它和第三个控件之间，以及它和框底部之间都插入了 5 像素。

## 框中套框

通过将框放在其他框内部，你可以实现喜欢的任何间距和定位组合。框被设计用来容纳控件，而框本身*也是*控件，因此你可以随心所欲地在框内打包框。我在本章前面的一些示例中展示了这一点，但以下示例展示了如何使用框中套框来实现一些复杂的定位。假设你希望有一个窗口，顶部有一个按钮，中间聚集了三个按钮，底部并排有两个按钮，如图 4-13 所示。

