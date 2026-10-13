
| `user_data` | 在调用信号处理程序时传递的数据（在注册时指定） |

列表 7.2 显示了一个简单的 OK 回调示例。

### 列表 7.2 简单的 Ok 回调

```c
1: #include <gtk/gtk.h>
2: static char *filename;
3:
4: void simple_ok_callback(GtkWidget *was_clicked, GtkWidget *file_sel)
5: {
6:   gtk_widget_hide(file_sel);
7:   filename = gtk_file_selection_get_filename (GTK_FILE_SELECTION(file_sel));
8: }
```

![](img/7fa9959a9d28ad339fa75e44952feeb9_171_0.png)

第 2 行声明了一个私有全局变量，它仅在该文件中可见。因此，任何需要文件名的回调函数必须存在此文件中。这有助于防止全局变量名的潜在冲突，并保护 `filename` 不受其他回调函数的意外篡改。（这将位于与 `main()` 不同的源文件中，并且与任何可能冲突的回调函数分开。）

第 4–8 行显示了实际的 OK 回调，它只是隐藏了文件选择小部件并获取文件名，将其放在私有全局变量中。

为了将回调连接到确定和取消小部件，你需要查看 `GtkFileSelection`。以下是 `GtkFileSelection` 的定义：

# 需要考虑的额外小部件和问题

`typedef struct _GtkFileSelection GtkFileSelection;`

```c
struct _GtkFileSelection {
  GtkWindow window;
  GtkWidget *dir_list;
  GtkWidget *file_list;
  GtkWidget *selection_entry;
  GtkWidget *selection_text;
  GtkWidget *main_vbox;
  GtkWidget *ok_button;
  GtkWidget *cancel_button;
  GtkWidget *help_button;
  GtkWidget *history_pulldown;
  GtkWidget *history_menu;
  GList *history_list;
  GtkWidget *fileop_dialog;
  GtkWidget *fileop_entry;
  gchar *fileop_file, cmpl_state;
  GtkWidget *fileop_c_dir;
  GtkWidget *fileop_del_file;
  GtkWidget *fileop_ren_file;
};
```

如你所见，你可以访问构成文件选择小部件的所有小部件。`ok_button` 和 `cancel_button` 字段是常用的使用的。

列表 7.3 显示了在 `GtkLabel` 小部件中显示消息的代码。当用户从文件（File）菜单中选择“更改消息（Change Message）”项时，会显示文件选择小部件。初始路径（initial-path）显示了一个包含用户可能选择的不同消息的应用程序目录。`Gtklabel` 会根据文件选择的结果更新文本。（此处没有给出整个程序，仅提供了用于显示和更改消息的特定用户界面的代码。）

列表 7.3 中的代码生成图 7.4。

![](img/7fa9959a9d28ad339fa75e44952feeb9_172_0.png)

### 图 7.4

显示消息的程序。

### 列表 7.3 显示消息程序

```c
1: /* 创建 Label 项及其菜单 */
2: file_item = gtk_menu_item_new_with_label("File");
3: file_menu = gtk_menu_new();
4: change = gtk_menu_item_new_with_label("Change Message");
5: separator = gtk_menu_item_new(NULL);
6: exit_item = gtk_menu_item_new_with_label("Exit");
7:
8: /* 创建 Label 项 */
9: message = gtk_label_new("Your message is:\n There is a Software Design
10: "Meeting at 10:00 this morning.\n");
11:
12: /* 创建文件选择 */
13: message_fsb = gtk_file_selection_new("Select new message file");
14: gtk_file_selection_hide_fileop_buttons(GTK_FILE_SELECTION(message_fsb));
15: gtk_file_selection_set_filename(GTK_FILE_SELECTION(message_fsb),
16: "/home/messages/*");
17:
18: /* 2b. 设置属性 */
19: gtk_window_set_title(GTK_WINDOW(top_widget), "Message");
20: gtk_signal_connect(GTK_OBJECT(change), "activate",
21: GTK_SIGNAL_FUNC(gtk_widget_show), GTK_OBJECT(message_fsb));
22: gtk_signal_connect(GTK_OBJECT(message_fsb), "delete_event",
23: GTK_SIGNAL_FUNC(dialog_delete_handler), NULL);
24:
25: gtk_signal_connect(GTK_OBJECT(message_fsb),
26: GTK_FILE_SELECTION(message_fsb)->ok_button,
27: "clicked", ok_callback, message);
28: gtk_signal_connect(GTK_OBJECT(message_fsb),
29: GTK_FILE_SELECTION(message_fsb)->cancel_button,
30: "clicked",
31: GTK_SIGNAL_FUNC(gtk_widget_hide), GTK_OBJECT(label));
```

第 1-6 行显示了文件菜单及其成员的创建。`change` 和 `Exit` 项（带有一个分隔符）。第 9-10 行显示了用于显示的 label 创建。当用户选择“更改消息”项时，会显示文件选择小部件，以便用户可以选择新的消息文件。第 13-16 行显示了创建文件选择小部件 `message_fsb`，其标题为“选择消息文件（Select message file）”。不需要按钮，因此它们被隐藏了，并给了一个初始路径。

### 额外问题和小部件

第 1-6 行显示了文件菜单及其成员的创建。`change` 和 `Exit` 项（带有一个分隔符）。第 9-10 行显示了用于显示的 label 创建。当用户选择“更改消息”项时，会显示文件选择小部件，以便用户可以选择新的消息文件。第 13-16 行显示了创建文件选择小部件 `message_fsb`，其标题为“选择消息文件”。不需要按钮，因此它们被隐藏了，并给了一个初始路径。

### 额外问题和小部件

第 1-6 行显示了文件菜单及其成员的创建。`change` 和 `Exit` 项（带有一个分隔符）。第 9-10 行显示了用于显示的 label 创建。当用户选择“更改消息”项时，会显示文件选择小部件，以便用户可以选择新的消息文件。第 13-16 行显示了创建文件选择小部件 `message_fsb`，其标题为“选择消息文件”。不需要按钮，因此它们被隐藏了，并给了一个初始路径。

### 额外问题和小部件

第 1-6 行显示了文件菜单及其成员的创建。`change` 和 `Exit` 项（带有一个分隔符）。第 9-10 行显示了用于显示的 label 创建。当用户选择“更改消息”项时，会显示文件选择小部件，以便用户可以选择新的消息文件。第 13-16 行显示了创建文件选择小部件 `message_fsb`，其标题为“选择消息文件”。不需要按钮，因此它们被隐藏了，并给了一个初始路径。

### 额外问题和小部件

第 1-6 行显示了文件菜单及其成员的创建。`change` 和 `Exit` 项（带有一个分隔符）。第 9-10 行显示了用于显示的 label 创建。当用户选择“更改消息”项时，会显示文件选择小部件，以便用户可以选择新的消息文件。第 13-16 行显示了创建文件选择小部件 `message_fsb`，其标题为“选择消息文件”。不需要按钮，因此它们被隐藏了，并给了一个初始路径。

### 额外问题和小部件
