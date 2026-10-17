
```c
/* 允许文本组件被编辑 */
gtk_text_set_editable (GTK_TEXT (text), TRUE);

/* 将组件设置为“只读”模式 */
gtk_text_set_editable (GTK_TEXT (text), FALSE);
```

光标位置可以使用 `gtk_text_set_point` 函数设置。`gtk_text_set_point` 函数期望一个确定光标位置的索引。该索引是基于字符的。例如：

```c
/* 将光标设置为第十个字符之后 */
gtk_text_set_point (GTK_TEXT (text), 10);
```

可以使用 `gtk_text_get_point` 函数查询光标位置。它将返回一个表示光标所在文本偏移量的索引。

```c
/* 查找光标位置 */
nPos = gtk_text_get_point (GTK_TEXT (text));
```

可以使用 `gtk_text_get_length` 函数查询文本组件以找到组件中有多少个字符。你可以使用 `gtk_editable_get_chars` 函数获取文本组件中的文本。例如，要获取文本组件中的所有字符，以下代码就足够：

```c
/* --- 获取组件中的字符数量 ... */
nLength = gtk_text_get_length (GTK_TEXT (text));

/* --- 获取组件中的文本 ... */
buffer = gtk_editable_get_chars (GTK_EDITABLE (text),
(int) 0,
(int) nLength);
```

与其计算组件内文本的长度，不如使用值 -1 来表示最后一个字符。

```c
/* --- 获取组件中的文本 ... */
buffer = gtk_editable_get_chars (GTK_EDITABLE (text),
(int) 0,
(int) -1);
```

`gtk_editable_get_chars` 函数返回的缓冲区是专门为返回值分配的一块新内存。将内存一直悬空直到应用程序退出是一种糟糕的编程习惯。当不再需要该内存时，应该使用 `g_free` 函数来释放内存。

```c
/* 内存处理完毕，释放它 ... */
g_free(buffer);
```

# 108 第 6 章 更多小部件：框架、文本、对话框、文件选择对话框、进度条

```c
/* 创建部件 ... */
text = gtk_text_new(NULL, NULL);
/* 将部件添加到布局格表中 ... */
gtk_table_attach(GTK_TABLE, text, 0, 1, 0, 1,
GTK_EXPAND | GTK_SHRINK | GTK_FILL,
GTK_EXPAND | GTK_SHRINK | GTK_FILL, 0, 0, 0);
```

```c
/* 使其可见 ... */
gtk_widget_show(text);
```

当文本位于布局表中时，可以为该部件添加滚动条。滚动条结构包含 `hadj` 字段和 `vadj` 字段，它们是 `GtkAdjustment` 指针。要创建一个滚动条并将字段的 `GtkAdjustment` 与滚动条关联，只需在创建滚动条时传入该 `GtkAdjustment` 即可。

```c
/* 创建一个水平滚动条 ... */
/* ... */
hscroll = gtk_hscroll_new(GTK_TEXT(text)->hadj);
```

```c
/* 将水平滚动条放在文本部件下方 ... */
gtk_table_attach(GTK_TABLE, hscroll, 0, 1, 1, 2,
GTK_EXPAND | GTK_SHRINK | GTK_FILL, 0, 0, 0);
```

```c
/* 显示部件 ... */ */
gtk_widget_show(hscroll);
```

```c
/* 创建一个垂直滚动条 ... */
/* ... */
vscroll = gtk_vscroll_new(GTK_TEXT(text)->vadj);
```

```c
/* 将垂直滚动条放在文本的右侧 ... * */
gtk_table_attach(GTK_TABLE, vscroll, 1, 2, 0, 1,
GTK_EXPAND | GTK_SHRINK | GTK_FILL, 0, 0, 0);
```

```c
/* 使其可见 ... */
gtk_widget_show(vscroll);
```

如果不需要水平滚动条，你可以简单地创建一个布局盒，并将垂直滚动条放在文本部件旁边。以下代码显示了一个示例：

```c
/* 创建部件 ... */
text = gtk_text_new(NULL, NULL);
```

```c
/* 将文本部件添加到布局盒 ... */
gtk_box_pack_start(GTK_BOX(hbox), text, FALSE, FALSE, 0);
```

```c
/* --- 创建一个垂直滚动条 --- */
vscroll = gtk_vscrollbar_new(GTK_TEXT(text)->vadj);
```

```c
/* --- 添加滚动条。应该在文本部件的右侧 --- */
gtk_box_pack_start(GTK_BOX(hbox), FALSE, FALSE, 0);
```

```c
/* --- 使对话框可见 --- */
gtk_widget_show(vscroll);
```

## 对话框

对话框是通过 `gtk_dialog_new` 函数创建的，该函数会创建一个没有按钮或文本的基础对话框。创建的对话框有两个布局盒（`hbox`、`action_area`），可以在其中添加其他部件。`hbox` 用于用于放置标签或其他信息，而按钮则放置在 `action_area` 中。在添加文本部件或按钮之前，普通的对话框是没用的；除非它向用户传递信息，否则它是没有意义的。让对话框变得实用的最简单方法是显示带有“确定”按钮的文本。我们可以使用以下代码创建标签并将其添加到对话框的 `vbox` 布局中：

```c
/* --- 创建标签 --- */
label = gtk_label_new(szMessage);
```

```c
/* --- 给它留出一点呼吸空间 --- */
gtk_misc_set_padding(GTK_MISC(label), 10, 10);
```

```c
/* --- 将其添加到对话框的 vbox 区域 --- */
gtk_box_pack_start(GTK_BOX(GTK_DIALOG(dialog_window))->vbox,
FALSE, TRUE, 0);
```

```c
/* --- 始终让它可见 --- */
gtk_widget_show(label);
```

很好，但它仍然没有提供任何用户交互。要实现这一点，你应该向 `action_area` 添加一个按钮。当你向对话框添加一个按钮时，通常给该按钮设置 `GTK_CAN_DEFAULT` 标志是好的。`GTK_CAN_DEFAULT` 标志指定了作为对话框默认操作的部件，并允许用户按 Enter 键而不是点击按钮。`gtk_widget_grab_default` 函数将默认按钮设置为该部件。这个简单的示例中只有一个按钮；因此，我们可以将其设为对话框的默认按钮，这样用户在对话框弹出时只需按 Enter 键即可。默认按钮周围有一个宽边框，用以指示它是默认的。为用户添加一个可以点击的“确定”按钮非常简单：

```c
/* --- 创建按钮 --- */
button = gtk_button_new_with_label("Ok");
```

```c
/* --- 允许按钮设置为默认值 */
GTK_WIDGET_SET_FLAGS(button, GTK_CAN_DEFAULT);
```

```c
/* --- 将部件添加到操作区域 --- */
gtk_box_pack_start(GTK_BOX(GTK_DIALOG(dialog_window))->action_area, button, TRUE, 0);
```

```c
/* --- 获取焦点 --- */
gtk_widget_grab_default(button);
```

```c
/* --- 使其可见 --- */
gtk_widget_show(button);
```

```c
/* --- 等待按钮被点击 --- */
gtk_signal_connect(GTK_OBJECT(button), "clicked", GTK_SIGNAL_FUNC(OkClicked), &return_value);
```
