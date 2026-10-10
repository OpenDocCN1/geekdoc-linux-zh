

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

从第 33 行开始的函数 `makeButtonBox()` 创建一个水平按钮盒，并在其中填充按钮。该按钮盒由第 37 行对 `gtk_hbutton_box_new()` 的调用创建，此函数不需要任何参数。每个按钮通过对第 41 行到第 51 行的 `gtk_container_add()` 调用被添加到按钮盒中。第 38 行对 `gtk_container_set_border_width()` 的调用在按钮组周围添加了一个 10 像素的边界——从而生成了图 5-25 中所示的窗口。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_169_0.png)

### 图 5-25：水平按钮盒

你只需改变一个字母即可创建一个垂直按钮盒。要创建图 5-26 中所示的显示效果，请将第 37 行修改为：

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

以下程序演示了为按钮盒设置每种选项的结果。该程序生成的四个按钮盒——每个设置了一种布局选项——如图 5-27 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_170_0.png)

所有布局选项都涉及当按钮盒大于最小尺寸时按钮的定位问题。`GTK_BUTTONBOX_SPREAD` 选项将按钮均匀分布在按钮盒中，并在按钮行的两端插入一些空间。`GTK_BUTTONBOX_EDGE` 选项也均匀分布按钮，但不增加开始或结束处的空间。`GTK_BUTTONBOX_START` 选项保持默认间距，并将所有按钮移至左侧。`GTK_BUTTONBOX_END` 选项也保持默认间距，但将按钮移至右侧。

`GTK_BUTTONBOX_DEFAULT_STYLE` 指定使用默认值配置按钮盒。除非你更改它，否则默认值是 `GTK_BUTTONBOX_EDGE`。

```c
/* hbdemo.c */
#include <gnome.h>

typedef struct {
  gchar *name;
  GtkButtonBoxStyle value;
} layoutOption;

GtkWidget *makeButtonFrame(layoutOption *option);
GtkWidget *makeButtonBox(layoutOption *option);
void gtkMakeDisplay();
gint eventDelete(GtkWidget *widget,
                 GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
                  GdkEvent *event, gpointer data);

layoutOption option[] = {
  { "DEFAULT_STYLE", GTK_BUTTONBOX_DEFAULT_STYLE },
  { "SPREAD", GTK_BUTTONBOX_SPREAD },
  { "EDGE", GTK_BUTTONBOX_EDGE },
  { "START", GTK_BUTTONBOX_START },
  { "END", GTK_BUTTONBOX_END }
};

int main(int argc, char *argv[])
{
    GtkWidget *window;
    GtkWidget *demoDisplay;

    gnome_init("hbdemo", "1.0", argc, argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_signal_connect(GTK_OBJECT(window),
         "delete_event",
         GTK_SIGNAL_FUNC(eventDelete),
         NULL);
    gtk_signal_connect(GTK_OBJECT(window),
         "destroy",
         GTK_SIGNAL_FUNC(eventDestroy),
         NULL);

    demoDisplay = makeDisplay();

    gtk_container_add(GTK_CONTAINER(window), demoDisplay);
    gtk_widget_show_all(window);
    gtk_main();
    exit(0);
}

GtkWidget *makeDisplay()
{
    int i;
    GtkWidget *vbox;
    GtkWidget *frame;

    vbox = gtk_vbox_new(FALSE, 10);
    gtk_container_set_border_width(GTK_CONTAINER(vbox), 10);
    for(i=0; i<5; i++) {
        frame = makeButtonFrame(&option[i]);
        gtk_box_pack_start(GTK_BOX(vbox), frame,
                   FALSE, FALSE, 0);
    }
    return(vbox);
}

GtkWidget *makeButtonFrame(layoutOption *option)
{
    GtkWidget *frame;
    GtkWidget *buttonbox;

    frame = gtk_frame_new(option->name);
    buttonbox = makeButtonBox(option);
    gtk_container_add(GTK_CONTAINER(frame), buttonbox);
    return(frame);
}

GtkWidget *makeButtonBox(layoutOption *option)
{
    GtkWidget *buttonbox;
    GtkWidget *button;

    buttonbox = gtk_hbutton_box_new();
    gtk_button_box_set_layout(GTK_BUTTON_BOX(buttonbox),
                            option->value);
    gtk_container_set_border_width(
                    GTK_CONTAINER(buttonbox), 10);

    button = gtk_button_new_with_label("OK");
    gtk_container_add(GTK_CONTAINER(buttonbox), button);

    button = gtk_button_new_with_label("Refresh");
    gtk_container_add(GTK_CONTAINER(buttonbox), button);

    button = gtk_button_new_with_label("Clear");
    gtk_container_add(GTK_CONTAINER(buttonbox), button);

    button = gtk_button_new_with_label("Cancel");
    gtk_container_add(GTK_CONTAINER(buttonbox), button);

    return(buttonbox);
}

gint eventDelete(GtkWidget *widget,
                 GdkEvent *event, gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget,
                  GdkEvent *event, gpointer data) {
    gtk_main_quit();
    return(0);
}
```

从第 48 行开始的函数 `makeDisplay()` 创建了一个垂直盒，用于容纳所有可显示的窗口小部件。从第 56 行开始的循环通过使用在第 17 行定义的数组中存储的文本和值，创建了五个按钮框架——每个布局选项一个。对于每种布局，在第 57 行创建一个包含按钮盒的框架，并在第 58 行将其存储到垂直盒中。

从第 63 行开始的函数 `makeButtonFrame()` 创建一个框架，该框架使用布局选项的名称作为其标签。按钮盒在第 69 行通过对 `makeButtonBox()` 的调用创建，并在第 70 行插入到框架中。

从第 73 行开始的函数 `makeButtonBox()` 创建一个按钮盒，并往其中放入四个按钮。第 79 行对 `gtk_button_box_set_layout()` 的调用使用作为参数传入的布局值来设置布局选项。

相同的布局选项也适用于垂直按钮盒（如图 5-28 所示）。创建垂直按钮的程序与前面的示例几乎相同，只是将垂直替换为水平，反之亦然。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_173_0.png)

**图 5-28：** 具有不同布局的垂直按钮盒

如前所述，默认布局样式是 `GTK_BUTTONBOX_EDGE`。你可以更改默认值；新的默认值适用于所有未分配特定布局值的按钮。有两个函数可以做到这一点，每个方向各一个。例如，要将垂直按钮盒设置为 `START`，将水平按钮盒设置为 `SPREAD`：

```c
gtk_vbutton_box_set_layout_default(GTK_BUTTONBOX_START);
gtk_hbutton_box_set_layout_default(GTK_BUTTONBOX_SPREAD);
```

你可以按以下方式检索每种按钮盒方向当前的布局选项：

```c
gint vLayout;
gint hLayout;
...
vLayout = gtk_vbutton_box_get_layout_default();
hLayout = gtk_hbutton_box_get_layout_default();
```

在垂直和水平按钮盒中，按钮之间都有一个默认插入的空间。水平默认值为 30 像素，垂直默认值为 10 像素，但你可以更改这些默认设置。例如，要将垂直间距设置为 3 像素，水平间距设置为 15 像素：

```c
gtk_vbutton_box_set_spacing_default(3);
gtk_hbutton_box_set_spacing_default(15);
```

你可以按以下方式检索当前的默认间距值：

```c
gint vSpacing; 
gint hSpacing; 
...
 
vSpacing = gtk_vbutton_box_get_spacing_default(); 
hSpacing = gtk_hbutton_box_get_spacing_default();
```

## 总结

所有容器都旨在容纳**一个或多个窗口小部件**，而且所有容器*都是窗口小部件*。这意味着一个容器可以包含在另一个容器内部。例如，你可以将一些固定容器放置在表格内部，然后将表格插入到滚动窗口中，以便用户可以在表格中移动，最后将整体放入一个笔记本中，这样你就有一行标签可供使用多个其他窗口。本章探讨了容器的类型，以及以下事实：

- 窗口小部件可以几乎以任何配置进行定位和分组。这使得你能够创建清晰且易于理解的窗口成为可能。

- 定位窗口小部件的大部分工作都在容器内部自动完成，这使得将窗口小部件放置在你想要的位置变得非常容易。对于大多数容器来说，这仅仅是插入窗口小部件、检查结果并调整选项直到其外观符合你期望的过程。

- 用于在显示中放置窗口小部件的函数从一个容器到下一个容器是一致的，并且具有描述性强、易读的名称。

本章探讨的示例和解释——以及第 4 章中的示例和解释——为你提供了创建任何你能想到的窗口布局所需的所有工具的信息。第 6 章解释了如何通过从用户向应用程序发送消息使你的窗口小部件变得有用。

