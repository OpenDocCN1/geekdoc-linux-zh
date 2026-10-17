
# GNOME2 官方开发者指南

```c
    g_print("chooser chosen: R=%d, G=%d, B=%d, A=%d\n",

        red, green, blue, alpha);

}
```

此处理程序在用户点击 OK 按钮后显示来自文件浏览器的选择。其信号连接将在本节稍后讨论。

```c
/* file_browser 中选择的文件名 */

void print_filename(GtkButton *button, gpointer data)
{
    gchar *filename;
    g_object_get(file_browser, "filename", &filename, NULL);
    g_print("file chosen: %s\n", filename);
    g_free(filename);
}
```

创建文件浏览器对话框是一项相当的任务。你可以看到如何将前面的代码中的`print_filename`处理程序连接到浏览器的 OK 按钮，以及在用户点击 OK 或 Cancel 后如何移除窗口。

```c
/* 创建文件浏览器并附加信号 */

void make_file_dialog(GtkButton *button, gpointer data)
{
    file_browser = g_object_new(GTK_TYPE_FILE_SELECTION, NULL);
    gtk_window_set_title(GTK_WINDOW(file_browser), "Select a File");
    gtk_signal_connect(file_browser->ok_button,
        "clicked", G_CALLBACK(print_filename), NULL);
    gtk_signal_connect_swapped(file_browser->ok_button,
        "clicked", G_CALLBACK(gtk_widget_destroy),
        file_browser);
    gtk_signal_connect_swapped(file_browser->cancel_button,
        "clicked", G_CALLBACK(gtk_widget_destroy),
        file_browser);
    gtk_widget_show(GTK_WIDGET(file_browser));
}
```

主程序窗口使用简单的布局：所有控件将通过`VBox`放入一个单列中。

```c
int main(int argc, char **argv)
{
    GtkWindow *window;
    GtkColorSelection *color_chooser;
    GtkFontSelection *font_chooser;
    GtkButton *file_button;
    GtkBox *vbox;
    GtkLabel *color_label, *font_label, *file_label;

    /* 初始化 GTK+ */
    gtk_init(&argc, &argv);

    window = gtk_window_new(GTK_TYPE_TOP);
    gtk_window_set_title(GTK_WINDOW(window), "Chooser");
    g_signal_connect(window, "destroy", G_CALLBACK(end_program), NULL);

    vbox = gtk_box_new(GTK_ORIENTATION_VERTICAL, 0);
    gtk_container_add(GTK_CONTAINER(window), GTK_WIDGET(vbox));

    /* 颜色选择器 */
    color_chooser = g_object_new(GTK_TYPE_COLOR_SELECTION, NULL);
    color_label = gtk_label_new("Select Color:");
    gtk_box_pack_start(GTK_BOX(vbox), GTK_WIDGET(color_label), FALSE, FALSE, 0);
    gtk_box_pack_start(GTK_BOX(vbox), GTK_WIDGET(color_chooser), TRUE, TRUE, 0);

    /* 字体选择器 */
    font_chooser = g_object_new(GTK_TYPE_FONT_SELECTION, NULL);
    font_label = gtk_label_new("Select Font:");
    gtk_box_pack_start(GTK_BOX(vbox), GTK_WIDGET(font_label), FALSE, FALSE, 0);
    gtk_box_pack_start(GTK_BOX(vbox), GTK_WIDGET(font_chooser), TRUE, TRUE, 0);

    /* 文件选择 */
    file_button = gtk_button_new_with_label("Select File");
    file_label = gtk_label_new("No File Selected");
    gtk_box_pack_start(GTK_BOX(vbox), GTK_WIDGET(file_button), FALSE, FALSE, 0);
    gtk_box_pack_start(GTK_BOX(vbox), GTK_WIDGET(file_label), FALSE, FALSE, 0);

    g_signal_connect(color_chooser, "color-changed", G_CALLBACK(print_color), NULL);
    g_signal_connect(file_button, "clicked", G_CALLBACK(make_file_dialog), NULL);

    gtk_widget_show_all(GTK_WIDGET(window));
    gtk_main();
    return 0;
}
```

一个文件名属性是`show-files`（布尔型）。如果你将其设置为`TRUE`，文件浏览器框顶部将出现三个用于创建目录、删除文件和重命名文件的按钮。

如果你需要带有文件选择按钮的文件名，请考虑使用[第 4.3.5 节]中描述的`GnomeFileEntry`。

```c
/* 附加标准处理程序 */

g_signal_connect(window, "delete_event", G_CALLBACK(delete_event), NULL);
g_signal_connect(window, "destroy", G_CALLBACK(end_program), NULL);
```

为所有箭头创建小部件只是一个打字练习。注意箭头之间有垂直分隔符。

- 带有四个箭头（不同方向）的`HBOX`

```c
hbox[0] = g_object_new(GTK_HBOX, NULL);

arrow[0] = g_object_new(GTK_TYPE_ARROW, "arrow-type", GTK_ARROW_UP, NULL);

arrow[1] = g_object_new(GTK_TYPE_ARROW, "arrow-type", GTK_ARROW_DOWN, NULL);

arrow[2] = g_object_new(GTK_TYPE_ARROW, "arrow-type", GTK_ARROW_LEFT, NULL);

arrow[3] = g_object_new(GTK_TYPE_ARROW, "arrow-type", GTK_ARROW_RIGHT, NULL);
```

- 将箭头放入`hbox`，并放置分隔符

```c
for (i = 0; i < 4; i++)

  gtk_box_pack_defaults(GTK_HBOX(hbox[0]), GTK_WIDGET(arrow[i]));

  if (i < 3)

    v_sep[i] = g_object_new(GTK_TYPE_VSEPARATOR, NULL);

    gtk_box_pack_defaults(GTK_HBOX(hbox[0]), GTK_WIDGET(v_sep[i]));
```

现在是为每种样式添加框架了：

- 创建一个框架并将`hbox`放在上方
