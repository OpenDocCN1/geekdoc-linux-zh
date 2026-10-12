
这些调用会自动使对话框变为模态——我们不需要事先使用 `gtk_window_set_modal`。记住按钮从 0 开始编号，按照它们传递给 `gnome_dialog_new` 的顺序：

```c
GtkWidget *dialog;

int result;

dialog = gnome_dialog_new ("Do you really want to quit?",
	GNOME_STOCK_BUTTON_YES,
	GNOME_STOCK_BUTTON_NO,
	NULL);

tk_widget_show(dialog);

result = gnome_dialog_run_and_close ( GNOME_DIALOG (dialog) );

witch (result) {
	case 0: g_print("You clicked Yes\n");
		break;
	case 1: g_print("You clicked No\n");
		break;
	deault: g_print("You closed the dialog\n");
	}
```

# 第 8 章

## GnomeAbout

我们在讨论 `GnomeDialog` 时提到它有三个子类，提供了进一步的专门化。`GnomeAbout` 是其中第一个，它是无处不在的“关于”对话框的模板，提供有关应用程序版本、作者、版权和其他注释的信息。为了更加专业，我们甚至可以添加一个 logo！

```c
GtkWidget gnome_about_new(const gchar *title,
const gchar *version,
const gchar *copyright,
const gchar **authors,
const gchar *comments,
const gchar *logo);
```

唯一的强制性字段是字符串数组。`GnomeAbout` 包含一个 OK 按钮，点击时会销毁对话框：

![](img/930f7611cac03a5cd5573f4bb94fd7b9_291_0.png)

`GnomeAbout` 对话框应该设置为在点击帮助菜单中的“关于”项时显示。

## GnomePropertyBox

`GnomePropertyBox` 是 `GnomeDialog` 的一个大得扩展。正如名称所示，这是一个属性或偏好对话框的模板。它包含一个 `GtkNotebook` 控件，允许将偏好分到多个页面，以及四个按钮：OK、Apply、Cancel 和 Help。

![](img/930f7611cac03a5cd5573f4bb94fd7b9_291_1.png)

`GnomePropertyBox` 允许通过发射“apply”和“help”信号来辅助编码对话框。如果点击了 OK 或 Cancel 按钮，它会自动关闭对话框。创建 `GnomePropertyBox` 涉及调用 `gnome_property_box_new`，它不接受参数。与 `GnomeAbout` 一样，对话框标题默认设置为应用程序名称。

```c
GtkWidget * gnome_property_box_new();
```

Apply 按钮最初是不可用的——也就是说，它是灰色的，表示偏好设置中没有待处理的更改。如果任何页面上的任何控件被修改，那么就由程序员负责使 Apply 按钮变为可用。为了做到这一点，我们对 `GnomePropertyBox` 中控件的“changed”信号响应并调用 `gnome_property_box_changed`。

```c
void gnome_property_box_changed(GnomePropertyBox *box);
```

当然，我们首先使用 `gnome_property_box_append_page` 向对话框添加页面，它返回刚添加的页面的编号：

```c
gint gnome_property_box_append_page(GnomePropertyBox *box,
GtkWidget *page, GtkWidget *tab);
```

`page` 是要添加到新页面的控件，如果它只包含一个控件，它可能是一个 `GtkFrame` 或容器控件，以便页面看起来体。`tab` 是放置在 notebook 中的控件，它允许使用位图和文本来识别每个页面。

当点击 Apply 或 OK 按钮时，`GnomePropertyBox` 会发射“apply”信号；作为响应，我们的代码应该处理页面的状态。在需要手动设置状态的极少数情况下，可以使用 `gnome_properties_set_state`：

```c
void gnome_properties_set_state(GnomePropertyBox *box, gboolean setting);
```

当点击 Apply 或 OK 按钮时，`GnomePropertyBox` 会发射“apply”信号；作为响应，我们的代码应该处理页面的状态。在需要手动设置状态的极少数情况下，可以使用 `gnome_properties_set_state`：

```c
void gnome_properties_set_state(GnomePropertyBox *box, gboolean setting);
```

当点击 Apply 或 OK 按钮时，`GnomePropertyBox` 会发射“apply”信号；作为响应，我们的代码应该处理页面的状态。在需要手动设置状态的极少数情况下，可以使用 `gnome_properties_set_state`：

```c
void gnome_properties_set_state(GnomePropertyBox *box, gboolean setting);
```

当点击 Apply 或 OK 按钮时，`GnomePropertyBox` 会发射“apply”信号；作为响应，我们的代码应该处理页面的状态。在需要手动设置状态的极少数情况下，可以使用 `gnome_properties_set_state`：

```c
void gnome_properties_set_state(GGPropertyBox *box,, setting);
```

当点击 Apply 或 OK 按钮时，`GnomePropertyBox` 的 "apply" 信号；；作为响应，我们的代码应该处理页面的状态。在需要手动设置状态的极少数情况下，可以使用 `gnome_properties_set_state`：

```c
void gnome_properties_set_state(GnomePropertyBox *box, the setting);
```

当点击 Apply 或 OK 按钮时，`GnomePropertyBox` 发射 "apply" 信号；作为响应，我们的代码应该处理页面的状态。在需要手动设置状态的极少数情况下，可以使用 `gnome_properties_set_state`：

```c
void gnome_properties_set_state(GnomePropertyBox *box,, setting);
```

## GnomeMessageBox

`Gtk` 的子类是 `GnomeMessageBox`，一个显示消息的简单对话框。它处理页面的状态。在需要手动设置状态的极少数情况下，可以使用 `gnome_properties_set_state`：

- `GNOME_MESSAGE_INFO`
- `GNOME_MESSAGE_ERROR`
- `GNOME_MESSAGE_QUESTION`
- `GNOME_MESSAGE_GENERIC`

这是一个用法示例：

```c
GtkWidget gnome_message_new(GnomeMessageType type, Gchar *title, Gchar *text, ...);
```

创建一个___(__,,,,,);:

```c
GtkWidget *message;
message = gnome_message_new(GNOME_MESSAGE_ERROR, "Error", "An error occurred", NULL);
gtk____(();
______
gtk_widget_show(message);
```

要关闭消息，可以使用：

```c
int gnome_message_run(GnomeMessageBox *message);
int gnome_message_run_and_close(GnomeMessageBox *message);
```
