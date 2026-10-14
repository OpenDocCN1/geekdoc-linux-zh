
活动模式用于无法确定当前任务需要多长时间的情况。例如，在遍历目录树时，没有好的办法可以告诉操作将花费多久。因此，你可以每当程序运行 100 个文件时推进一次指示器。设置 `fraction` 以退出活动模式。

示例还显示，你可以顺利地在普通模式和活动模式之间切换——这种行为你可能在某些浏览器中遇到过。（当然，许多人认为这种行为非常烦人。）

## 3.4 容器与布局控件

在没有容器控件的情况下，组织控件在实践上是不可能的。每个容器都根据参数和打包顺序以特定方式排列其控件。

容器的主要类型如下：

- **水平和垂直框。** 这些是最重要且最基础的容器。当你需要在一行或一列排列多个控件时，应该使用框。这里的两个类分别是用于水平行的 `GtkBox` 和用于列的 `GtkVBox`，它们都派生自 `GtkBox`。还有特殊的子类 `GtkButtonBox` 和 `GtkBox` 用于按钮组。它们的工作方式与其他框类似，只是打包到这些框中的控件具有一致的外观和布局。Button boxes 适用于按钮，但对其他任何东西都不好。
- **水平和垂直面板。** 面板由两个相邻的容器组成。一个水平面板 (`GtkHPane`) 的典型用法是带有主面板和另一侧列表的窗口。客户端可以使用垂直容器 (`GtkVPane`) 来分离消息和显示。抽象的 `GtkPane` 是这两个容器的类。
- **Notebook。** 这些控件 (`GtkNotebook`) 在边缘持有多个页面供用户选择和查看。程序经常使用 notebooks 进行属性设置。
- **Tables。** 如果需要在网格中排列控件，`GtkTable` 可能是最佳选择。表格的常见用途包括矩阵，例如井棋游戏；当你添加或删除控件时，单元格坐标会变化；如果你在做这类事情，可能需要 Glade 的帮助（见第 5 章）。
- **Alignment。** 这些简单的容器 (`GtkAlignment`) 指定单个控件的大小和对齐。为了控制这些，我们已经看到了 HBoxes 和 VBoxes 的示例。下面的程序演示了框、面板和表格。注意主程序中的控件是通过容器分组的。

```c
/* container.c */

#include <gtk/gtk.h>

/* standard handlers */

gint delete_event(GtkWidget *widget, GdkEvent, gpointer data) {

    return FALSE;

}

void end_program(GtkWidget *widget, gpointer data) {

    gtk_main();

}

int main(int argc, char **argv) {

    GtkWindow *window;

    GtkHPane *h_pane;

    GtkVPane *v_pane;

    GtkButton *button_column; /* button elements */

    GtkButton *button[3]; /* button elements */

    GtkTable *table; /* table elements */

    int i, j;

    GtkNotebook *notebook; /* notebook elements */

    GtkLabel *page_1_content;

    GtkImage *page_2_apple;

    GtkButton *page_3_button;

    GtkLabel *page_1_title, *page_2_title, *page_3_title;

    /* initialize GTK+, create a window, attach handlers */

    gtk_init(&argc, &argv);

    window = g_object_new(GTK_TYPE_WINDOW,

      "title", "Container Madness",

      "default_height", 200,

      "default_width", 300,

      "border-width", 12,

      NULL);

    /* attach standard event handlers */

    g_signal_connect(window, "delete_event", G_CALLBACK(delete_event), NULL);

    g_signal_connect(window, "destroy", G_CALLBACK(end_program), NULL);

    // 程序将主窗口分为两个面板，用户可以左右滑动水平面板。

    /* Divide window horizontally with a pane */

    h_pane = g_object_new(GTK_TYPE_HPANE, NULL);

    gtk_container_add(GTK_CONTAINER(window), GTK_WIDGET(h_pane));

    // 到此为止这个应用程序还没有新东西。现在让我们通过前面的代码在左面板放置另一个控件（具体来说是一个垂直面板）：
```

```c
/* create a vertical container and put it
in the left side of the horizontal pane above */
v_pane = g_object_new(GTK_TYPE_VPANE, NULL);
gtk_pane_add(GTK_PANED(h_pane), GTK_WIDGET(v_pane));
```

注意包含容器的打包在这里是 `gtk_pane_add(1)`，将控件放入左面板。如果这是一个垂直容器，它会将控件放入顶面板。关于面板容器的更多信息请参考节 3.4.3。

接下来的三个语句创建了按钮；它们没什么异常。

```c
/* create three buttons */
button[0] = g_object_new(GTK_TYPE_BUTTON, "label", "Foo", NULL);
button[1] = g_object_new(GTK_TYPE_BUTTON, "label", "Bar", NULL);
button[2] = g_object_new(GTK_TYPE_BUTTON, "label", "Zaz", NULL);
```

垂直框持有按钮。因为框是 `GtkBox` 的形式，打包函数与普通框相同（见节 3.4.1）。

```c
/* put the buttons in a vertical box */
button_column = g_object_new(GTK_TYPE_V_BOX, NULL);
for (i=0; i<3; i++) {
  gtk_box_pack_start(GTK_BOX(button_column), GTK_WIDGET(button[i]));
}
```

// 如后续代码所示，此框将进入垂直包含面板的顶面板（回想容器在窗口的左侧）。

```c
/* put the vertical box into the top pane of v_pane, from earlier */
gtk_pane_add(GTK_PANED(v_pane), GTK_WIDGET(button_column));
```

// 后面的代码展示了如何创建一个表格。因为创建所有控件的工作

# GNOME 开发者官方指南

表格可能是枯燥的，通过一个短循环可以为表格中的每个单元格创建一个按钮。请参见第 3.4.2 节表格容器的属性和方法。
