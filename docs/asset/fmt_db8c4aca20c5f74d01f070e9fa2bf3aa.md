
# 第 16 章

在创建包装框（packing box）时，你应该指定两个参数：对齐（homogeneous）和间距（spacing）：

```c
GtkWidget* hbox_new (gboolean homogeneous, gint spacing);

GtkWidget* vbox_new (gboolean homogeneous, gint spacing);
```

这些参数控制该特定包装框内所有控件的布局。`homogeneous` 是布尔值，当设置为 `TRUE` 时，将强制包含的控件占据相同的空间，无论其自身的大小如何。`spacing` 设置像素之间的间隙。

一旦创建了包装框，就可以使用 `gtk_box_pack_start` 和 `gtk_box_pack_end` 函数来添加控件。

```c
void gtk_box_pack_start (GtkBox *box, GtkWidget *child,
gboolean expand, gboolean fill,
int padding);

void gtk_box_pack_end (GtkBox *box, GtkWidget *child,
gboolean expand, gboolean fill,
int padding);
```

`gtk_box_pack_start` 将控件添加到 `GtkBox` 的左侧和 `GtkListBox` 的底部；相反，`gtk_box_pack_end` 从右侧和顶部添加。它们的参数控制包装框内每个控件的间距和格式。

| 参数 | 说明 |
|---|---|
| `GtkBox *box` | 要填充的包装框。 |
| `GtkWidget *child` | 要放置在包装框中的控件。 |
| `gboolean expand` | 如果为 `TRUE`，则填充与其他同样标记为 `TRUE` 的标志控件共享的所有可用空间。 |
| `gboolean fill` | 如果为 `TRUE`，此控件将填充分配给它的空间，而不是将其作为边缘周围的填充。仅在 `expand` 为 `TRUE` 时有效。 |
| `Guint padding` | 控件周围的填充大小（单位：像素）。 |

让我们来看看这些包装框控件，现在通过嵌套的框创建一个更复杂的用户界面。

## 试一试——容器布局

在这个示例中，我们将使用 `GtkBox` 和 `GtkListBox` 布局一些 `GtkLabel` 控件。`Label` 控件是简单的控件，用于显示短文本。我们将此程序命名为 `container`。

```c
#include <gtk/gtk.h>

void closeApp ( GtkWidget *window, gpointer data);

int main (int argc, char *argv[])
{
    GtkWidget *window;
    GtkWidget *label1, *label2, *label3;
    GtkWidget *hbox;
    GtkWidget *vbox;

    gtk_init(&argc, &argv);

    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);

    gtk_window_set_title(GTK_WINDOW(window), "窗口标题");

    gtk_window_set_position(GTK_WINDOW(window), GTK_WIN_POS_CENTER);

    gtk_window_set_default_size(GTK_WINDOW(window), 300, 200);

    gtk_signal_connect ( GTK_OBJECT (window), "destroy",
          GTK_SIGNAL_FUNC (closeApp), NULL);

    label1 = gtk_label_new("Label 1");

    label2 = gtk_label_new("Label 2");

    label3 = gtk_label_new("Label 3");

    hbox = gtk_hbox_new ( TRUE, 5 );

    vbox = gtk_vbox_new ( FALSE, 10);

    gtk_pack_start (GTK_BOX (vbox), label1, TRUE, FALSE, 5);

    gtk_pack_start (GTK_BOX (vbox), label2, TRUE, FALSE, 5);

    gtk_pack_start (GTK_BOX (hbox), vbox, FALSE, FALSE, 5);

    gtk_pack_start (GTK_BOX (hbox), label3, FALSE, FALSE, 5);

    gtk_container_add (GTK_CONTAINER (window), hbox);

    gtk_widget_show_all (window);

    gtk_main ();

    return 0;
}
```

当我们运行此程序时，我们在窗口中看到 `label` 控件的布局（参见图 16-6）。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_678_0.png)

## 工作原理

我们创建了两个包装框控件：`hbox` 和 `vbox`。使用 `gtk_box_start` 用 `label1` 和 `label2` 填充 `vbox`，因此 `label2` 出现在底部，因为它是在 `label1` 之后添加的。接下来，`vbox` 本身与 `label3` 一起被添加到 `hbox` 中。

`hbox` 最后被添加到窗口并使用 `gtk_widget_show_all` 显示在屏幕上。

包装框布局通过图表理解最好，如图 16-7 所示。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_679_0.png)

现在我们已经查看了控件、信号、回调和容器控件，涵盖了 `GTK+` 的基础知识。成为一个知识丰富的 `GTK+` 程序员需要理解如何最好使用可用控件。

## `GTK+` 控件

在本节中，我们将查看在应用程序中最常用的常用 `GTK+` 控件的 API。

### `GtkWindow`

`GtkWindow` 是所有 `GTK+` 的基础元素。到目前为止我们一直使用它来存放控件。

```
GtkWidget
  +-GtkContainer
    +-GtkBin
      +-GtkWindow
```

有几十个 `GtkWindow` API 调用，但这里列出值得关注的函数：

```
GtkWidget* gtk_window_new;
void gtk_window_set_title (GtkWindow *window, const gchar *title);
void gtk_window_set_position (GtkWindow *window, GtkWindowPosition position);
void gtk_window_set_default_size (GtkWindow *window, int width, int height);
void gtk_window_present (GtkWindow *window);
void gtk_window_hide (GtkWindow *window);
void gtk_window_destroy (GtkWindow *window);
```

`window_new (GtkWindowType type)` 创建了一个空窗口。窗口的标题是未定义的，正如我们所看到的。

### `GtkEntry`

...

## 试一试——用户名和密码输入

现在我们已经查看了 `GtkEntry` 的函数，让我们通过一个短程序来展示它们的实际用法。

1. 首先，我们定义了秘密密码，巧妙地选择为“secret”。

```c
const char * password = "secret";
```

2. 我们有两个回调函数，它们在窗口销毁和点击 `Ok` 按钮时被调用。

```c
void closeApp ( GtkWidget *window, gpointer data)
{
    gtk_main_quit();
}

void button_clicked (GtkWidget *button, gpointer data)
{
    const char *password_text = gtk_entry_get_text (GTK_ENTRY (GtkWidget *) data));

    if (strcmp(password_text, password) == 0)
        printf("Access granted!\n");
    else
}
```
