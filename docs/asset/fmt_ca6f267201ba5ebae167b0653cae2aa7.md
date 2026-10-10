
# 第 8 章 开发一个简单的文字处理器

```c
gtk_toolbar_append_item (GTK_TOOLBAR (toolbar),
    "Cut", "Cut",
    CreateWidgetFromXpm (win_main, (gchar **) xpm_cut),
    (GtkSignalFunc) menu_Cut,
    NULL);
  /* ... 创建 复制按钮 ... */
  gtk_toolbar_append_item (GTK_TOOLBAR (toolbar),
    "Copy", "Copy",
    CreateWidgetFromXpm (win_main, (gchar **) xpm_copy),
    (GtkSignalFunc) menu_Copy,
    NULL);
}
```

```c
/*
 * 创建粘贴按钮
 * /
 */
gtk_toolbar_append_item (GTK_TOOLBAR toolbar,
    "Paste", "Paste",
    CreateWidgetFromXpm (win_main, gchar **) xpm_paste,
    (GtkSignalFunc) menu_paste,
    NULL);
```
}

## 杂项

此文件包含了从 `CreateMenu` 和 `CreateToolbar` 出的底层函数。该文件从之前关于菜单和工具栏的示例中提取，没有新元素。创建位图、菜单和子菜单的代码在这里很容易复用。

## showmessage.c

应用程序的几个区域需要向用户显示消息。为了防止代码重复，创建了一个名为 `showmessage` 的单函数来为用户显示对话框。此函数还调用了 `gtk_grab_add` 以确保弹出的对话框获得用户的注意力。

`gtk_grab_add` 函数使用户在关闭对话框之前无法执行其他功能。在按下 OK 按钮后，通过 `destroy` 回调函数中的 `gtk_grab_remove` 函数释放对话框。将代码放在 `destroy` 回调中，是因为对话框可能会在不按下 OK 或取消按钮的情况下被关闭。

`ShowMessage` 函数接收一个标题和一个消息，将标题放入对话框窗口，并将消息放入带有 OK 按钮的对话框中。

```c
/*
 * ShowMessage
 * 向用户显示弹出消息。
 * /
void ShowMessage(char *szTitle, char *szMessage)
{
    GtkWidget *label;
    GtkWidget *button;
    GtkWidget *dialog_window;
```

```c
/* --- 创建对话框窗口 --- */
dialog_window = gtk_dialog_new();
gtk_signal_connect(GTK_OBJECT (dialog_window), "destroy",
                   GTK_SIGNAL_FUNC (ClearShowMessage),
                   NULL);
/* 设置标题并添加边框 --- */
gtk_window_set_title(GTK_WINDOW (dialog_window), szTitle);
gtk_container_border_width(GTK_CONTAINER (dialog_window), 0);
/* --- 创建一个带有焦点的“OK”按钮 --- */
button = gtk_button_new_with_label('OK');
gtk_signal_connect(GTK_OBJECT (button), "clicked",
                   GTK_SIGNAL_FUNC (CloseShowMessage),
                   dialog_window);
/* --- 设置“OK”按钮为默认 --- */
GTK_WIDGET_SET_FLAGS(button, GTK_CAN_DEFAULT);
gtk_box_pack_start(GTK_BOX (GTK_DIALOG (dialog_window))
->action_area,
                   button, TRUE, TRUE, 0);
gtk_widget_grab_default(button);
gtk_widget_show(button);
/* --- 创建描述性标签 --- */
label = gtk_label_new(szMessage);
/* --- 在标签文字周围留空间 --- */
gtk_misc_set_padding(GTK_MISC (label), 10, 10);
/* --- 将标签添加到对话框的指定区域 --- */
gtk_box_pack_start(GTK_BOX (GTK_DIALOG (dialog_window))->hbox,
                   label, TRUE, TRUE, 0);
/* --- 显示标签 --- */
gtk_widget_show(label);
/* --- 显示对话框 --- */
gtk_widget_show(dialog_window);
/* --- 只有此窗口可以执行操作 --- */
gtk_grab_add(dialog_window);
}
```

为了让 `ShowMessage` 函数完美运行，需要通过事件处理两种情况。用户可能会点击 OK 按钮，可能会直接关闭对话框。这些操作会产生不同的事件。点击按钮产生一个 *clicked* 事件，但什么都不做。关闭窗口产生一个 `destroy` 事件，它并不会清理调用过 `gtk_grab_add` 函数的事实。为了在用户点击 OK 按钮时关闭窗口，在创建 *clicked* 事件时将其设置为调用 `CloseShowMessage` 函数。该函数需要调用 `gtk_grab_remove` 函数并销毁对话框窗口。注意，对话框是通过函数的数据参数传递的，因为在用 `gtk_signal_connect` 设置 *clicked* 事件时，对话框被配置为作为数据参数传递。

```c
/*
 -- CloseShowMessage
 * 关闭关于对话框窗口的例程。
 */
void CloseShowMessage(GtkWidget *widget, gpointer data) {
GtkWidget *dialog_widget = (GtkWidget *) data;
/* 关闭小部件 -- */
gtk_widget_destroy (dialog_widget);
}
```

如果用户在未点击 OK 的情况下关闭了窗口：

- `ClearShowMessage`
- 释放窗口 *grab*
- 清空全局 `dialog_window`，因为在对话框弹出时会检查该变量。

```c
void ClearShowMessage(GtkWidget *widget, gpointer data) {
gtk_grab_remove(widget);
}
```

## about.c

你可以使用 `ShowMessage` 代码在应用程序中创建简单的对话框。例如，显示应用程序信息的“关于...”菜单选项是在对话框中显示的。这些信息通常包括公司、作者和版本信息。整个“关于...”代码只是调用 `ShowMessage` 函数进行显示。

这种方法之所以可行，是因为在任何时候只有一个文件选择对话框打开——这是由 `gtk_grab_add` 函数保证的条件。你无法在关闭当前文件选择对话框的情况下创建另一个文件选择对话框。

```c
/*
* FileOk
*
* "OK" 按钮被点击。
* 调用函数 (func) 对文件进行* 需要的操作。
*/
void FileOk(GtkWidget *w, gpointer data)
{
    char *sTempFile;
    typeFileSelectionData *localdata;
    GtkWidget *filew;
    localdata = (typeFileSelectionData *) data;
    filew = localdata->filesel;
    /* ... 哪个文件？ ... */
    sTempFile = gtk_file_selection_get_filename (
        GTK_FILE_SELECTION (filew));
    /* ... 释放旧内存 ... */
```
