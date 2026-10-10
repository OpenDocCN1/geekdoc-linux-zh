
在第 153 行，调用 `gtk_progress_bar_new()` 来创建进度条小部件。在第 155 行，我调用了 `gtk_progress_set_activity_mode()` 将进度小部件设置为活动模式。我这样做是因为进度条在某些情况下仅用于显示时间的流逝。我们无法使用从开始到结束的进度条，因为我们不知道连接需要多久。在第 170 行到 173 行，我创建了两个定时器。第二个定时器 `timer2` 将在 1 到 8 秒之间的随机时间触发。当 `timer2` 到期时调用的回调函数 `ActivityProgressDone()` 将启动下载。第一个定时器 `timer1` 每 10 秒触发一次。定时器函数 `ActivityProgress()` 每 10 秒触发一次。

```c
gboolean ActivityProgress(gpointer data)
{
    GtkProgressBar *progress = GTK_PROGRESS(data);
    double fraction;
    fraction = gtk_progress_bar_get_fraction(progress);
    fraction += 0.01;
    if (fraction > 1.0)
        fraction = 1.0;
    gtk_progress_bar_set_fraction(progress, fraction);
    return TRUE;
}
```

### 对话框创建

```c
if (new_val > adj->upper)
    new_val = adj->lower;
```

```c
gtk_progress_set_value (GTK_PROGRESS (data), new_val);
```

```c
return TRUE;
}
```

```c
static void
Connect(GtkWidget *widget, GtkEntry *entry)
{
    GtkWidget *dialog_window, *label, *progress, *button;
    char buf[] = {128 };
    int connecttime;

    char *server = gtk_entry_get_text ( entry );
    snprintf(buf, sizeof(buf) - 1, "Connecting to '%s...', server);

    dialog_window = gtk_dialog_new();
    gtk_window_set_modal(GTK_WINDOW(dialog_window),TRUE);

    gtk_window_position(GTK_WINDOW(dialog_window), GTK_WIN_POS_MOUSE);

    label = gtk_label_new ( buf );
    gtk_box_pack_start(GTK_BOX (GTK_DIALOG(dialog_window))->vbox,
    label, TRUE, 0);

    progress = gtk_progress_bar_new();
    gtk_progress_set_activity_mode(GTK_PROGRESS(progress), TRUE);

    gtk_progress_configure(GTK_PROGRESS(progress), 1.0, 1.0, 10.0);
    gtk_box_pack_start(GTK_BOX (GTK_DIALOG(dialog_window))->vbox,
    progress, TRUE, 0);

    button = gtk_button_new_with_label("Cancel");
    gtk_signal_connect(GTK_OBJECT (button), "clicked",
    GTK_SIGNAL_FUNC(CancelConnect), dialog_window);

    gtk_box_pack_start(GTK_BOX (GTK_DIALOG(dialog_window))->action_area,
    button, TRUE, 0);

    timer1 = gtk_timeout_add(100, ActivityProgressTimeout, progress);
    connecttime = RAND(0, 8000);
    ttimer2 = gtk_timeout_add(connecttime, ActivityProgressDone,
    (gpointer) dialog_window);

    gtk_widget_show_all (dialog_window);
}
```

```c
main(int argc, char *argv[])
{
    GtkWidget *dialog_window, hbox, button, *label, *entry;

    gtk_init(&argc, &argv);
    dialog_window = gtk_dialog_new();
    gtk_window_position(GTK_WINDOW(dialog_window), GTK_WIN_POS_MOUSE);
    hbox = gtk_hbox_new(FALSE, 5);
    gtk_box_pack_start(GTK_BOX(hbox), GTK_DIALOG(dialog_window) ->vbox,
    hbox, TRUE, TRUE, 0);

    label = gtk_label_new("Server:");
    entry = gtk_entry_new(entry, "ftp.gtk.org");
    gtk_entry_set_text(GTK_ENTRY (entry), "ftp.gtk.org");
    gtk_box_pack_start(GTK_BOX(hbox), label, TRUE, TRUE, 0);
    gtk_box_pack_start(GTK_BOX(hbox), entry, TRUE, TRUE, 0);

    button = gtk_button_new_with_label("Connect");
    gtk_signal_connect(GTK_OBJECT(button), "clicked",
    GTK_SIGNAL_FUNC(entry, entry);
    gtk_box_pack_start(GTK_BOX(GTK_DIALOG(dialog_window)) ->action_area,
    button, TRUE, TRUE, 0);

    gtk_widget_show_all (dialog_window);
    gtk_main();
}
```

![](img/1441ee0eb9a357efc9aff107f92bf0c0_791_0.png)

图 15.4 示例应用程序对话框

程序的结构如下。`main()` 函数创建一个对话框，如图 15.4 所示。当用户点击“连接”按钮时，会调用 `Connect()` 函数。`Connect()` 创建一个包含进度条和“取消”按钮的对话框。进度条的创建如下：
