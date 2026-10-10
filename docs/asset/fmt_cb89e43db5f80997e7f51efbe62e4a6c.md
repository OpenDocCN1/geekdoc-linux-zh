
| `gtk_box_pack(box, button,` | | `TRUE, FALSE,` | `0);` |

| `gtk_box_pack(box, button,` | | `TRUE, TRUE,` | `0);` |

| `gtk_hbox_new(TRUE, 0);` | | `button,` | `TRUE, FALSE,` | `0);` |

| `gtk_box_pack(box, button,` | | `TRUE, TRUE,` | `0);` |

每一行包含一个带有多个按钮的水平框 (`hbox`)。对每个按钮进行 `pack` 调用是将其每个按钮封装到 `hbox` 中的调用简写。每个按钮都以相同的方式进行封装（即使用与 `gtk_box_pack_start()` 函数相同的相同的参数）。

这是 `gtk_box_pack_start` 函数的示例。

```c
void gtk_box_pack_start(GtkBox *box,
                             GtkWidget *child,
                             gint expand,
                             gint fill,
                             gint padding, gpointer data);
```

第一个参数是你是否正在封装该对象，第二个参数是对象。目前这些对象将都是按钮，所以我们将框封装到框中。

`gtk_box_pack_start()` 和 `gtk_box_pack_end()` 的 `expand` 参数控制小部件在框中的布局，以填充扩展到填充分配区域的额外空间 (`TRUE`)。或者缩小框以适应部件 (`FALSE`)。将 `expand` 设置为 `FALSE` 允许你对部件进行右对齐或左对齐。否则，它们将扩展以适应框，这种效果仅使用 `gtk_box_pack_start` 或 `gtk_box_pack_end` 中的任何一个即可实现。

`gtk_box_pack` 的 `fill` 参数控制额外的空间是分配给对象本身 (`TRUE`)，还是作为这些对象周围框的额外内边 (`FALSE`)。它只有在 `expand` 参数也为 `TRUE` 时才起作用。

创建框时，函数形式如下：

```c
GtkWidget *gtk_hbox_new(gint homogeneous,
                                     gint spacing);
```

`gtk_hbox_new` 的 `homogeneous` 参数（`gtk_box_new` 相同）控制框是否具有相同的大小（即 `hbox` 中的宽度，或 `vbox` 中的高度）。如果设置了该参数，`gtk_box_pack` 句例的 `expand` 参数将始终开启。

`spacing`（创建框时）和 `padding`（封装元素时）之间的区别是什么？`spacing` 添加在对象之间，而 `padding` 添加在每个对象的两侧。下面的图应该会让它更清晰：

![](img/82031bb12124328f3aeb452ec445b3ae_22_0.png)

这里使用的代码用于创建这些图像。我注释得相当详尽，希望你遵循时不会遇到任何问题。你自己编译并玩玩看吧。

### 4.3 封装演示程序

```c
/* example-start pack packbox.c */

#include <stdio.h>
#include <gtk/gtk.h>

void delete_event(GtkWidget *widget,
                   GdkEvent *event,
                   gpointer data )
{
    gtk_main_quit();
}

/* 创建一个填充有按钮标签的新框。我们感兴趣的
 * 变量的参数传递给此函数。
 * 我们不显示框，但会显示内部的所有内容。 */
GtkWidget *make_box(int homogeneous,
                    gint spacing,
                    gint expand,
                    gint padding)
{
    GtkWidget *box;
    GtkWidget *button;
    char padstr[80];

    /* 创建一个具有适当均匀性
     * 间距设置的新框 */
    box = gtk_box_new(homogeneous, spacing);

    /* 创建系列具有适当设置的按钮 */
    button = gtk_button_new_with_label("gtk_box_pack");
    gtk_box_pack_start(GTK_BOX(box), button, expand, fill, padding);
    gtk_widget_show(button);

    button = gtk_button_new_with_label("box");
    gtk_box_pack_start(GTK_BOX(box), button, expand, fill, padding);
    gtk_widget_show(button);

    button = gtk_button_new_with_label("button");
    gtk_box_pack_start(GTK_BOX(box), button, expand, fill, padding);
    gtk_widget_show(button);
```

```c
/* 根据 expand 的值创建一个带有标签
 * 的按钮。 */
if (expand == TRUE)
    button = gtk_button_new_with_label("TRUE,");
else
    button = gtk_button_new_with_label("FALSE");
```

```c
gtk_box_pack_start (GTK_BOX (box), button, expand, fill, padding);
gtk_widget_show (button);
```

```c
/* 这与上面 "expand" 的按钮创建
* 相同，但使用了简写形式。 */
button = gtk_button_new_with_label (fill ? "TRUE," : "FALSE");
gtk_box_pack_start (GTK_BOX (box), button, expand, fill, padding);
gtk_widget_show (button);
```

```c
printf("%d:", padstr);

button = gtk_button_new_with_label (padstr);
gtk_box_pack_start (GTK_BOX (box), button, expand, fill, padding);
gtk_widget_show (button);
```

```c
}
```

```c
int main ( int argc,
    char *argv[])
{
    GtkWidget *window;
    GtkWidget *button;
    GtkWidget *box1;
    GtkWidget *box2;
    GtkWidget *separator;
    GtkWidget *label;
    GtkWidget *quitbox;
    int width;
```

```c
/* 我们的，不要忘记这个 :) */
gtk_init (&argc, &argv);
```

```c
if (argc != 2) {
    fprintf(stderr, "usage: pack num is 1, 2, or 3.\n/* 这清理 GTK 并以状态 1 退出。 */");
    gtk_exit (1);
}
```

```c
int num = atoi (argv[1]);
```

```c
/* 创建我们的窗口 */
window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
```

```c
/* 你应该将 destroy 信号连接到
* 主窗口。这对于正确的行为非常重要 */
gtk_signal_connect (GTK_OBJECT (window), "delete_event",
    GTK_SIGNAL_FUNC (delete_event), NULL);
```

```c
gtk_container_set_border_width (GTK_CONTAINER (window), 10);
```
