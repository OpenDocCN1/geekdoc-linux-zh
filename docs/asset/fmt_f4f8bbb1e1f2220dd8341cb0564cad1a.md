
```c
19: gtk_init(&argc, argv);

20:

21: /* 2a. Create widgets */

22: top_widget = gtk_window_new( GTK_WINDOW_TOPLEVEL );

23: vbox = gtk_vbox_new( FALSE, NO_SPACING );

24: menu_bar = gtk_menu_bar_new( );

25:

/* Create the File item and its menu */

file_item = gtk_menu_item_new_with_label("File");

file_menu = gtk_menu_new();

exit_item = gtk_menu_item_new_with_label("Exit");

/* Create the Plot item */

plot_item = gtk_menu_item_new_with_label("Plot");

/* Create the Help item */

help_item = gtk_menu_item_new_with_label("Help");

/* Create the Work Area */

plot_area = gtk_drawing_area_new();

/* 2. Set Attributes */

gtk_window_set_title(GTK_WINDOW(top_widget), "Plotter");

gtk_drawing_area_size(GTK_DRAWING_AREA(plot_area), 300, 200);

/* 3. Registering callbacks */

gtk_signal_connect(GTK_OBJECT(top_widget), "delete_event", GTK_SIGNAL_FUNC(delete_event_handler), NULL);

gtk_signal_connect(GTK_OBJECT(top_widget), "destroy", GTK_SIGNAL_FUNC(print_and_quit), NULL);

gtk_signal_connect(GTK_OBJECT(exit_item), "activate", print_and_quit, NULL);

gtk_signal_connect(GTK_OBJECT(plot_item), "activate", plot_line, plot_area);

/* 4. Defining the Hierarchy */

gtk_container_add(GTK_CONTAINER(top_widget), vbox);

gtk_box_pack_start(GTK_BOX(vbox), menu_bar, FALSE, FALSE, NO_PADDING);

gtk_box_pack_start(GTK_BOX(vbox), plot_area, FALSE, FALSE, NO_PADDING);

/* 5. Pack the Menu Bar and move It Far Right */

gtk_menu_bar_append(GTK_MENU_BAR(menu_bar), file_item);

gtk_menu_bar_append(GTK_MENU_BAR(menu_bar), plot_item);

gtk_menu_bar_append(GTK_MENU_BAR(menu_bar), help_item);

gtk_menu_item_right_justify(GTK_MENU_ITEM(help_item));

/* Attach and pack the menus */

gtk_menu_item_set_submenu(GTK_MENU_ITEM(file_item), file_menu);

gtk_menu_bar_append(GTK_MENU_BAR(menu_bar), exit_item);

/* 5. Showing the Widgets */

gtk_widget_show_all(top_widget);

/* 6. Main Loop */

gtk_main();

g_print("Bye!\n");
```

第 17 行指示了创建此代码段中的菜单和项所需的额外组件变量。第 3 行创建了一个菜单以附加到列表 5.1 中的帮助项。第 4 行将空菜单附加到帮助项。Windows 用户习惯帮助右对齐（见图 5.2）。

要在菜单栏上实现右对齐的帮助，只需在创建帮助项后调用 `gtk_menu_item_right_justify()`。这是该函数的原型：
`void gtk_menu_item_right_justify( GtkMenuItem *menu_item )`

`gtk_menu_item_right_justify()` 的参数如下：

| 参数 | 说明 |
|---|---|
| `menu_item` | 你想要右对齐的 `GtkMenuItem` |

列表 5.1 显示了带有右对齐帮助项的绘图仪。

## 列表 5.1 带有右对齐帮助项的绘图仪

```c
1: #include <gtk/gtk.h>

2: #define NO_PADDING 0

3: #define NO_SPACING 0

4: 

5: /* Callbacks /

6: void line_plot( GtkMenuItem *was_clicked, GtkWidget *where_to_draw );

7: void print_and_quit( GtkButton *was_clicked, GtkWidget *gpointer user_data );

8: boolean delete_handler( GtkWidget *widget, GdkEvent *event, g gpointer user_data );

9:

10: int main(int argc, char *argv[])

11: {

12: GtkWidget *top_widget;

13: GtkWidget *vbox, *menu_bar, *file_item, *file_menu, *exit_item;

14: GtkWidget *plot_area;

15: GtkWidget *plot_item;

16: GtkWidget *help_item;

17:

18: /* 1. Initialize the environment */

19: gtk_init(&argc, argv);

20:

21: /* 2a. Create widgets */

22: top_widget = gtk_window_new( GTK_WINDOW_TOPLEVEL );

23: vbox = gtk_vbox_new( FALSE, NO_SPACING );

24: menu_bar = gtk_menu_bar_new( );

25:

/* Create the File item and its menu */

file_item = gtk_menu_item_new_with_label("File");

file_menu = gtk_menu_new();

exit_item = gtk_menu_item_new_with_label("Exit");

/* Create the Plot item */

plot_item = gtk_menu_item_new_with_label("Plot");

/* Create the Help item */

help_item = gtk_menu_item_new_with_label("Help");

/* Create the Work Area */

plot_area = gtk_drawing_area_new();

/* 2. Set Attributes */

gtk_window_set_title(GTK_WINDOW(top_widget), "Plotter");

gtk_drawing_area_size(GTK_DRAWING_AREA(plot_area), 300, 200);

/* 3. Registering callbacks */

gtk_signal_connect(GTK_OBJECT(top_widget), "delete_event", GTK_SIGNAL_FUNC(delete_event_handler), NULL);

gtk_signal_connect(GTK_OBJECT(top_widget), "destroy", GTK_SIGNAL_FUNC(print_and_quit), NULL);

gtk_signal_connect(GTK_OBJECT(exit_item), "activate", print_and_quit, NULL);
```
