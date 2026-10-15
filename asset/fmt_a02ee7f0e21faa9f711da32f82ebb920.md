
页面在笔记本内部以有序列表的形式保持，每个页面都有一个位置编号：第一个是 `0`，第二个是 `1`，以此类推。位置编号可用于在笔记本中已有的两个页面之间插入页面。例如，如果一个笔记本已经包含四个页面（编号为 `0`、`1`、`2` 和 `3`），可以使用此函数调用将新页面存储在列表的中心：

```c
gtk_notebook_insert_page(GTK_NOTEBOOK(notebook),
page,
label,
2);
```

调用此函数后，编号为 `3` 的页面现在变为编号 `4`，编号为 `2` 的页面移动到编号 `3`。新添加的页面编号为 `2`。您可以使用其位置编号来移除页面。例如，使用以下内容移除编号为 `2` 的页面：

```c
gtk_notebook_remove_page(GTK_NOTEBOOK(notebook),2);
```

如果您希望对显示有更多的控制——即想在程序内部选择选项卡——您可以调用 `gtk_notebook_set_page()` 选择任何活动页面作为当前活动页面。例如，以下代码使页面 `2` 成为活动页面：

```c
gtk_notebook_set_page(GTK_NOTEBOOK(notebook),2);
```

此函数调用可用于在之前的示例中确定当前活动的是哪个页面：

```c
gint loc;
loc = gtk_notebook_get_current_page(GTK_NOTEBOOK(notebook));
```

可以省略选项卡。这意味着用户将没有使用选项卡从一个页面切换到另一个页面的选项。然而，程序内部仍然具备切换的能力，因此在某些情况下这是有意义的。例如，如果您可以让程序运行在多种模式下，选项窗口可以维护为笔记本形式，并在每次模式改变时切换活动页面。默认情况下，选项卡是可见的。此函数调用省略选项卡：

```c
gtk_notebook_set_show_tabs(GTK_NOTEBOOK(notebook),FALSE);
```

通过指定 `TRUE` 代替 `FALSE`，可以使选项卡可见。

## 按钮盒

几乎每个窗口都至少有一个按钮，而大多数窗口都有多个。由于这种需求非常普遍，因此有一种特殊的容器控件专门设计用于对按钮进行分组。使用*按钮盒*的一个优势是可以全局设置间距和布局控制。换句话说，您可以通过单个设置来控制整个应用程序中所有按钮的布局。如果您希望拥有更多的控制，可以指定个别按钮盒的布局，并让其他按钮盒遵循您的默认设置。

本示例演示了使用按钮盒创建按钮组有多简单：

```c
1 /** hbuttonbox.c **/
2 #include <gnome.h>
3 GtkWidget *makeButtonBox();
4 gint eventDelete(GtkWidget *widget,
5 GdkEvent *event,gpointer data);
7 gint eventDestroy(GtkWidget *widget,
8 GdkEvent *event,gpointer data);
9
10 int main(int argc,char *argv[])
11 {
12 GtkWidget *window;
13 GtkWidget *buttonbox;
14
15 gnome_init("hbuttonbox","1.0",argc,argv);
16 window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
17 gtk_signal_connect(GTK_OBJECT(window),
18 "delete_event",
19 GTK_SIGNAL_FUNC(eventDelete),
20 NULL);
21 gtk_signal_connect(GTK_OBJECT(window),
22 "destroy",
23 GTK_SIGNAL_FUNC(eventDestroy),
24 NULL);
25
26 buttonbox = makeButtonBox();
27
28 gtk_container_add(GTK_CONTAINER(window),buttonbox);
29 gtk_widget_show_all(window);
30 gtk_main();
31 exit(0);
32 }
33 GtkWidget *makeButtonBox() {
34 GtkWidget *buttonbox;
35 GtkWidget *button;
36
37 buttonbox = gtk_hbutton_box_new();
38 gtk_container_set_border_width(
39 GTK_CONTAINER(buttonbox),10);
40
41 button = gtk_button_new_with_label("OK");
42 gtk_container_add(GTK_CONTAINER(buttonbox),button);
43
44 button = gtk_button_new_with_label("Refresh");
45 gtk_container_add(GTK_CONTAINER(buttonbox),button);
46
47 button = gtk_button_new_with_label("Clear");
48 gtk_container_add(GTK_CONTAINER(buttonbox),button);
49
50 button = gtk_button_new_with_label("Cancel");
51 gtk_container_add(GTK_CONTAINER(buttonbox),button);
52
53 return(buttonbox);
```

```c
54 }
55 gint eventDelete(GtkWidget *widget,
                    GdkEvent *event, gpointer data) {
56        return(FALSE);
57 }
58 }
59 gint eventDestroy(GtkWidget *widget,
                   GdkEvent *event, gpointer data) {
60        gtk_main_quit();
61        return(0);
62 }
63 }
```

从第 `33` 行开始的函数 `makeButtonBox()` 创建一个水平按钮盒，并在其中填充按钮。该按钮盒由第 `37` 行对 `gtk_hbutton_box_new()` 的调用创建，此函数不需要任何参数。每个按钮通过对第 `41` 行到第 `51` 行的 `gtk_container_add()` 调用被添加到按钮盒中。第 `38` 行对 `gtk_container_set_border_width()` 的调用在按钮组周围添加了一个 `10` 像素的边界——从而生成了图 `5-25` 中所示的窗口。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_169_0.png)

### 图 5-25：水平按钮盒

你只需改变一个字母即可创建一个垂直按钮盒。要创建图 `5-26` 中所示的显示效果，请将第 `37` 行修改为：

```c
buttonbox = gtk_vbutton_box_new();
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_169_1.png)

### 图 5-26：垂直按钮盒

按钮盒有四种不同的布局选项，可以通过使用以下五个值来设置：

- `GTK_BUTTONBOX_DEFAULT_STYLE`
- `GTK_BUTTONBOX_SPREAD`
- `GTK_BUTTONBOX_EDGE`
- `GTK_BUTTONBOX_START`
- `GTK_BUTTONBOX_END`

以下程序演示了为按钮盒设置每种选项的结果。该程序生成的四个按钮盒——每个设置了一种布局选项——如图 `5-27` 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_170_0.png)

所有布局选项都涉及当按钮盒大于最小尺寸时按钮的定位问题。`GTK_BUTTONBOX_SPREAD` 选项将按钮均匀分布在按钮盒中，并在按钮行的两端插入一些空间。`GTK_BUTTONBOX_EDGE` 选项也均匀分布按钮，但不增加开始或结束处的空间。`GTK_BUTTONBOX_START` 选项保持默认间距，并将所有按钮移至左侧。`GTK_BUTTONBOX_END` 选项也保持默认间距，但将按钮移至右侧。

`GTK_BUTTONBOX_DEFAULT_STYLE` 指定使用默认值配置按钮盒。除非你更改它，否则默认值是 `GTK_BUTTONBOX_EDGE`。
