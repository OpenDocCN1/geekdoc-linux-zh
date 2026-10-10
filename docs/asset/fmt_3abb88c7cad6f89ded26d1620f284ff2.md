
如前所述，你的应用程序可以指定比较函数在计算行相等时使用的排序列。默认列是第 0 列。然而，你可以通过调用 `gtk_clist_set_sort_column();` 设置你想要的任何列。

```c
void
gtk_clist_set_sort_column(GtkList *clist, gint column);
```

参数 `column` 的范围是 `[0, n - 1]`，其中 `n` 是每行的列数。用户代理提供了一个应用程序更改默认排序列的常见示例。`clist` 可用于显示文件夹的内容，其中列表中的每行都是一个消息、发送者、日期、主题以及正在显示的消息中的信息，这些都作为行中的列。邮件用户通常希望按日期或发送者对电子邮件进行排序，可能较少地按在文件夹列表中显示为列的消息字段进行排序。为了实现这一点，邮件程序会在用作列标题的按钮上注册回调函数。在回调函数中，`clist` 对应的列将作为列表的排序列，并通过调用 `gtk_clist_sort()` 对列表排序。

```c
void
gtk_clist_sort(GtkList *clist);
```

`gtk_clist_sort()` 函数接收一个 `GtkClist` 实例参数。调用此函数将根据客户端指定的排序列和比较函数对列表进行排序，如果客户端未指定，则使用默认值。信号函数的实现可能如下：

```c
void
gclist_click_column(GtkList *clist, int column, gpointer data)
{
    gtk_clist_set_sort_column(clist, column);
    gtk_clist_sort(clist);
}
```

# 256 第 6 章 • 列表

```c
028 main(int argc, char *argv[])
029 {
030 GtkWidget *button, hbox, *dialog_window;
031     char *texts[5];
032 
033     static char *titles[] = 
034     {
035         "部件 #", "描述", "单价", "数量", "总量"
036     };
037 }
038 
039     gtk_init(&argc, &argv);
040 
041     dialog_window = gtk_dialog_new();
042     gtk_window_position(GTK_WINDOW (dialog_window), GTK_WIN_POS_MOUSE);
043 
044     hbox = gtk_box_new(FALSE, 0);
045     gtk_container_add(GTK_CONTAINER (GTK_DIALOG (dialog_window)), hbox);
046 
047 
048     list = gtk_list_new_with_titles(5, titles);
049 
050     texts[0] = "36123-A", texts[1] = "木凿子";
051     texts[2] = "9.99", texts[3] = "1", texts[4] = "9.99";
052     gtk_list_append(GTK_LIST (list), texts);
053 
054     texts[0] = "45661-A", texts[1] = "工作手套";
055     texts[2] = "5.99", texts[3] = "1", texts[4] = "5.99";
056     gtk_list_append(GTK_LIST (list), texts);
057 
058     texts[0] = "34991-Q", texts[1] = "羊锤";
059     texts[2] = "7.99", texts[3] = "1", texts[4] = "7.99";
060     gtk_list_append(GTK_LIST (list), texts);
061 
062     texts[0] = "30125-S", texts[1] = "豪华割草机";
063     texts[2] = "12.99", texts[3] = "1", texts[4] = "12.99";
064     gtk_list_append(GTK_LIST (list), texts);
065 
066     gtk_box_pack_start(GTK_BOX (hbox), list, FALSE, FALSE, 0);
067 
068     button = gtk_button_new_with_label("退出");
069     gtk_box_pack_start(GTK_BOX (GTK_DIALOG (dialog_window)->action_area), 
070     button, TRUE, TRUE, 0);
071     gtk_signal_connect(GTK_OBJECT(button), "clicked",
072     GTK_SIGNAL (QuitCallback), dialog_window);
073     button = gtk_button_new_with_label("添加");
074     gtk_box_pack_start(GTK_BOX (GTK_DIALOG (dialog_window)->action_area), 
075     button, TRUE, TRUE, 0);
076     gtk_signal_connect(GTK_OBJECT(button), "clicked",
077     GTK_SIGNAL (AddCallback), dialog_window);
078     gtk_widget_show_all(dialog_window);
079 } 
gtk_main();
```

## GtkList

主例程创建了一个对话框，其中包含一个放置在 `GtkBox` 中的列表，列表下方添加了两个按钮：一个标记为“退出”，另一个标记为“添加”。列表在第 049 行到 063 行之间初始化了四行数据。执行时，会显示一个顶层对话框，其大小会根据列表进行调整，并包含下方的“退出”和“添加”按钮。问题出现在点击“添加”按钮时，它调用了回调例程。在这个回调中，列表被添加了 100 行。结果是灾难性的：列表会自动调整大小以适应新内容，这反过来导致容器及其父级对话框也随之调整。在运行 Enlightenment 窗口管理器的 Linux 系统上，对话框调整大小，导致对话框的底部以及“添加”和“退出”按钮位于屏幕下方。如果尺寸调整无法让窗口的所有部分在屏幕上可见，更好的做法是为列表添加滚动条，让它们根据需要出现，从而随着列表内容的增长和减少来改变对话框的几何形状。考虑到这一点，处理此类情况的方法是将列表或其容器调整到足够的大小，以容纳新项目的添加而不会引起重新调整，或者为列表添加垂直滚动条。

在列表上获取滚动条最直接的方法是将列表放置在滚动窗口 `GtkScrolledWindow` 容器中。我将在第 11 章“更多容器类”中讨论这个小部件。以下代码说明了为了在列表上获取滚动条所需要的列表类型。差异出现在 `main()` 函数的前几行：
