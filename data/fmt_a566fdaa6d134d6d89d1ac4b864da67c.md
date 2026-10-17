
```
38:   gtk_file_selection_set_filename(GTK_FILE_SELECTION(message_fsb),
39:                               "/home/messages/*");
40:
41:   /* 2b. 设置属性 */
42:   gtk_window_set_title(GTK_WINDOW(top_widget), "Message");
43:
44:   /* 3. 注册回调例程 */
45:   gtk_signal_connect(GTK_OBJECT(top_widget), "delete_event",
46:                             GTK_SIGNAL_FUNC(delete_event_handler), NULL);
47:   gtk_signal_connect(GTK_OBJECT(top_widget), "print_and_quit",
48:                              "destroy", NULL);
49:   gtk_signal_connect_object(GTK_OBJECT(object), "change", "activate",
50:                             GTK_SIGNAL_FUNC(gtk_widget_show), GTK_OBJECT(message_fsb));
51:   gtk_signal_connect(GTK_OBJECT(message_fsb), "delete_event",
52:                             GTK_SIGNAL_FUNC(dialog_handler), NULL);
53:   gtk_signal_connect_object(GTK_OBJECT(top_widget),
54:                             GTK_FILE_SELECTION(message_fsb)->ok_button,
55:                             "clicked", ok_callback, message);
56:   gtk_signal_connect_object(GTK_OBJECT(top_widget),
57:                             GTK_FILE_SELECTION(message_fsb)->cancel_button,
58:                             "clicked", GTK_SIGNAL_FUNC(gtk_widget_hide));
59:   return 0;
60: }
```

第 20-23 行显示了 Change 和 Exit 菜单项。Change widget 的 ID 被存储，以便在第 49-50 行执行 `gtk_signal_connect_object()`。分隔符和 Exit 菜单项的 widget ID 在主程序的其余部分不需要；`display_message` 函数比主函数短，并且通过 `append_menu_item()` 来构建了 GUI。

## 数据共享

使用全局变量通常不是数据共享的推荐方案，因为应用程序并不简单。在编写程序时如果遇到全局变量的需求，这在该范围内并不是简单的解决方案。幸运的是，在编写 GTK+ 时遇到的一个常见问题是回调函数需要某些信息；简单的解决方案是通过 `user_data` 参数传递结构体的地址。结构体的定义必须是全局的，以便主函数和回调都能访问它的字段。然而，在 `display_message` 程序中，`GtkLabel` 是 OK 按钮的祖先，可以通过 `gtk_widget_ancestor()` 获取必要的 widget ID。另一种可能性是将数据附加到小部件本身。GTK+ 类树中的每个对象都可以通过 `gtk_object_set_data()` 调用存储数据。获取回调必须在设置期间将 ID 分配数据，然后通过 `gtk_object_get_data()` 获取数据。

以下是 `gtk_object_set_data()` 的函数原型：

```
void gtk_object_set_data(GtkObject *object, const gchar *key, gpointer data)
```

`gtk_object_set_data()` 的参数如下：

| 参数 | 说明 |
| :--- | :--- |
| `object` | 要附加的对象 |
| `key` | 标识数据的字符串 |
| `data` | 要附加的数据 |

以下是 `gtk_object_get_data()` 的函数原型：

```
gpointer gtk_object_get_data(GtkObject *object, const gchar *key)
```

返回上一个 `gtk_object_set_data()` 的数据。`gtk_object_get_data()` 的参数如下：

| 参数 | 说明 |
| :--- | :--- |
| `object` | 从中获取数据的对象 |
| `key` | 标识提取数据的字符串 |

在列表 7.2 的简单 OK 回调中，文件名可以附加到对象而不是存储在全局变量中。在 `display_message` 中，你可以将 message widget 的对象数据设置为 `message_fsb` widget ID，因为 `message` 被传递给了 `ok_callback`，如下：

```
gtk_object_set_user_data( GTK_OBJECT( message ), "message_fsb", message_fsb );
gtk_signal_connect( GTK_OBJECT(GTK_FILE_SELECTION(message_fsb))->ok_button,
    "clicked", ok_callback, message );
```

使用的 key 与存储 widget ID 的变量相同。key 不需要变量名的字符串版本，但通常是这样编程的。新的 `ok_callback` 将改变它检索文件选择 widget ID 的方式，如列表 7.8 所示。

## 列表 7.8 带有数据的 ok_callback

```
1: void ok_callback( GtkWidget *was_clicked, GtkWidget * label )
2: {
3:     FILE *msg_fd;                   /* 文件描述符 */
4:     gchar msg_file;                 /* 文件名 */
5:     gchar c;                        /* 从文件中检索的字符 */
6:     GString text;                   /* 消息文本 */
7:     GtkWidget *file_sel;           /* 父文件选择小部件 */
8:
9:
10:    file_sel = GTK_WIDGET(gtk_object_get_data(GTK_OBJECT(label),
11:                             "message_fsb"));
12:    gtk_widget_hide(file_sel);
13:    /* 打开文件 *//
14:    msg_file=gtk_file_selection_get_filename(GTK_FILE_SELECTION(file_sel));
15:    msg_fd = fopen(msg_file, "r");
16:
17:    /* 为消息文本创建一个空的 GString *//
18:    text = g_string_new("");
19:
20:    /* 获取消息 *//
21:    while ((c = fgetc(msg_fd)) != EOF)
22:        g_string_append(text, c);
23:
24:    /* 更新标签的文本 *//
25:    gtk_label_set_text(GTK_LABEL(label), text->str);
26: }
```

166

第 7 天

你可以通过 `gtk_object_set_data()` 为数据分配唯一名称，从而将多个单元的数据存储在对象中。检索程序 `gtk_object_get_data()` 只需要知道数据的名称以及对象 ID 即可。

在向回调函数发送数据时，以及在回调函数中创建信息但其生命周期超过回调函数时（例如，在回调函数中创建并在回调退出后仍然存在的小部件），就会发生数据共享问题。新小部件的 ID 可以存储在私有全局变量中（这种情况下所有相关函数都将保留在该源文件中），也可以使用数据处理例程将新小部件的 ID 放置到对象上。
