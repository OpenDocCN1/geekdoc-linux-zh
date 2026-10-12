
可以使用 `gnome_app_clear_stack` 快速简单地清空整个栈。虽然栈对于允许应用程序的不同部分同时使用状态栏而无干扰风险很有用，但你经常需要在借助栈的情况下显示临时信息。你可以使用 `gnome_appbar_set_status` 添加瞬态文本，它将保持可见，直到添加新的瞬态文本，或者栈被推入、弹出、清空或通过调用 `gnome_appbar_refresh` 刷新。

```c
void gnome_app_clear_stack(GnomeApp *appbar)
```

```c
void gnome_app_set_status(GnomeApp *appbar, const gchar *status)
```

```c
void gnome_app_refresh(GnomeApp *appbar);
```

当鼠标指针高亮菜单项时，GNOME 允许在状态栏上显示菜单提示，代价是调用一次：

```c
void gnome_app_install_menu_hints(GnomeApp *app, GnomeUIInfo *uiinfo);
```

`GnomeUIInfo` 结构体必须之前通过调用一个菜单创建函数来创建，以便其 `widget` 字段被填充。

# 第 8 章

## 进度条

进度条由一个 `GtkProgress` 组成，如果创建 `GnomeAppBar` 时带有可选的进度条，则可以返回指向 `GtkProgress` 的指针：

```c
GtkProgress *gnome_appbar_get_progress (GnomeApp *appbar)
```

最后，也是最重要的一点，你可以向 `GnomeApp` 添加内容：

```c
void gnome_app_set_contents (GnomeApp *app, GtkWidget *contents)
```

这等同于对传统的 `gtk_window` 使用 `gtk_container_add`。

## 对话框

对话框是任何 GUI 应用不可或缺的一部分，允许用户选择或输入数据，并向用户报告各种信息，如错误、通用消息和帮助文本。在典型的应用程序中，对话框的数量比中心窗口多得多，因此易于编程对话框是任何现代工具包的根本性需求。

对话框与普通窗口有某些不同之处：

- 它们有一个或多个按钮，用于信号应用程序调用或取消对话框的操作。
- 它们的窗口装饰框上没有最小化标签。
- 它们具有模态（modal）的选项，即在对话框关闭之前阻止使用应用程序的其他部分。

认识到这些区别，GNOME 通过扩展 `GtkWindow` 到对话框基类 `GtkDialog` 来实现对话框。这形成了一个包含各种函数的现构建对话框模板；因此，使用 GNOME 制作对话框是一件完全文明化的事情。

![](img/930f7611cac03a5cd5573f4bb94fd7b9_287_0.png)

然而，`GnomeDialog` 并不是故事的结束。还有三种特殊的对话框类型：

- `GnomeAbout`
- `GnomePropertyBox`
- `GnomeMessageBox`

这些使得更快速、更容易地为更特定的目的创建常用的对话框。此外，它们派自 `GnomeDialog`，共享其功能并帮助保持 GNOME 之间的一致性。让我们详细查看 `GnomeDialog`。

## 创建 GnomeDialog

要创建一个 `GnomeDialog` 控件，调用 `gnome_dialog_new` 并将窗口标题和以 NULL 终止的按钮列表（放置在对话框内）作为参数：

```c
GtkWidget *gnome_dialog_new(const gchar *title, ...)
```

按钮列表是用于按钮的字符串列表。与其传递简单的字符串，不如使用 GNOME 宏对于常用按钮这是一个更好的主意。就像菜单/工具栏宏一样，它提供了位图（pixmaps）来标准化界面。

宏列表持存在 `libgnome/gnome-stock.h` 中，包括：

- `GNOME_STOK_BUTTON_OK`
- `GNOME_STOK_BUTTON_CANCEL`
- `GNOME_STOK_BUTTON_YES`
- `GNOME_STOK_BUTTON_NO`
- `GNOME_STOK_BUTTON_CLOSE`
- `GNOME_STOK_BUTTON_APPLY`
- `GNOME_STOK_BUTTON_HELP`
- `GNOME_STOK_BUTTON_NEXT`
- `GNOME_STOK_BUTTON_PREV`
- `GNOME_STOK_BUTTON_UP`
- `GNOME_STOK_BUTTON_DOWN`
- `GNOME_STOK_BUTTON_FONT`

这些宏等同于简单的字符串，请注意如果你创建一个模态对话框，你可能会得到一段文本。

## 显示 GnomeDialog

创建一个简单的 OK/Cancel 对话框看起来如下：

```c
GtkWidget *dialog = gnome_dialog_new(
    "A Dialog with buttons",
    GNOME_STOK_BUTTON_OK,
    GNOME_STOK_BUTTON_CANCEL,
    NULL);
```

创建并填充对话框后，我们需要通过显示它来使其运行。显示对话框并等待用户响应的机制对于模态和非模态对话框来说非常不同。你应该在显示它之前通过调用 `gtk_window_set_modal` 设置其模态性。

```c
void gtk_window_set_modal(GtkWindow *window, gboolean modality);
```

## 非模态对话框

非模态对话框是不限制其他窗口使用的类型。这允许应用程序的其他部分正常操作，你必须连接 `GnomeDialog` 的回调函数，以便在按钮被点击或对话框关闭时通知你。一旦创建并填充了非模态 `GnomeDialog`，正常地使用 `gtk_widget_show` 使对话框可见。

```c
gtk_widget_show(dialog);
```

与其为单个按钮连接处理器，最好使用 `GnomeDialog` 自己的信号。它除了父类提供的信号外还发射两个：`clicked` 和 `close`；这些是为了提供对话框功能应该连接的信号。

> `clicked` 信号在对话框按钮被点击时发射。连接到 `clicked` 的回调函数提供三个参数：对话框指针、被点击按钮的编号和用户数据。

> `close` 信号在调用 `dialog_close` 时发射，有一个 GNOME 提供的默认处理器。该处理器默认通过调用 `gtk_widget_destroy` 销毁对话框，除非调用了 `gnome_dialog_close_hides` 并传递了 TRUE。

```c
void gnome_dialog_close_hides(GnomeDialog *dialog, gboolean setting);
```

在这种情况下，`close` 处理器将使用 `gtk_dialog_hide` 隐藏对话框。这意味着当你再次想要显示它时，不需要重新创建它。这对于复杂的对话框是理想的，即在对话框操作之间保留对话框中控件状态的情况。

你也可以为 `close` 连接你自己的处理器；它可以弹出一个“确定吗？”的消息，并返回一个返回值，告诉 GNOME 是否执行默认操作。

## 使用 GNOME/GTK+ 进行 GUI 编程

在点击按钮时发射 `close`（关闭）信号是有用的，因为这样就不需要手动销毁或隐藏对话框。要让 `GnomeDialog` 在点击按钮时同时发射 `close` 和 `clicked` 信号，请将 `gnome_dialog_set_close` 设置为 TRUE。

```c
void gnome_dialog_set_close(GnomeDialog dialog, gboolean setting);
```

## 模态对话框

模态对话框可以防止用户在处理对话框之前与其他窗口交互。使用模态对话框对于防止用户在对话框显示期间更改关键设置，或强制用户立即做出决策至关重要。由于在对话框显示期间应用程序的其他部分会被冻结，因此你的代码可以等待输入而不影响应用程序其他部分的功能。换句话说，我们不需要使用回调函数，因为只需显示对话框并等待事件发生即可。

这使得编写模态对话框比非模态等价物容易得多，这一事实使得它们在非模态对话框更合适的情况下深受程序员欢迎。要使用模态对话框，请像 usual一样创建并显示 `GnomeDialog`，然后调用 `gnome_dialog_run` 或 `gnome_dialog_run_and_close`（如果对话框被窗口管理器关闭，则返回 -1）。`run_and_close` 变会在对话框未通过正常手段销毁时销毁对话框并返回。

```c
int gnome_dialog_run(GnomeDialog *dialog)
```

```c
int gnome_dialog_run_and_close(GnomeDialog *dialog);
```
