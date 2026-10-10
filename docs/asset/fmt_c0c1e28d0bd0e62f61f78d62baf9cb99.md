
`selection`（选择）和 `target`（目标）是你在调用 `gtk_selection_convert()` 时提供的值。`type` 是一个原子（atom），用于识别由选择顺序返回的数据类型。某些值为 `"STRING"`（一组 latin-1 字符的字符串）、`"ATOM"`（一组原子的字符串）、`"INTEGER"`（一个整数）等。大多数目标只能返回一种类型。`format` 给出了单位（例如字符）以字节为单位的长度。通常你不需要关心接收数据时的这个值。`data` 是指向返回数据的指针，`length` 是返回数据的长度（以字节计）。如果 `length` 为负数，则发生了错误且无法获取选择。这可能发生在没有应用程序请求该选择，或者你请求了应用程序不支持的目标。缓冲区实际上保证比 `length` 长一个字节；额外的字节将为零，因此没有必要为了终止字符串而对其进行复制。

在下面的示例中，我们获取了特殊的 `"TARGETS"`，它是一个选择可以转换的所有目标的列表。

```c
/* example-selection getargets.c */

#include <gtk/gtk.h>

void selection_received(GtkWidget *widget, GtkSelectionData *selection_data, gpointer data);

/* 用户点击 "Get Targets" 按钮时调用的信号处理函数 */

void get_targets(GtkWidget *widget, gpointer data)
{
    static GdkAtom targets_atom = GDK_NONE;
    /* 获取对应字符串 "TARGETS" 的原子 */
    if (targets_atom == GDK_NONE)
        targets_atom = gdk_atom_intern("TARGETS", FALSE);
    /* 为主选择请求 "TARGETS" 目标 */
    gtk_selection_convert(widget, GDK_SELECTION_PRIMARY, targets_atom, GDK_CURRENT_TIME);
}

/* 当选择所有返回数据时调用的信号处理函数 */
void selection_received(GtkWidget *widget, GtkSelectionData *selection_data, gpointer data)
{
    GdkAtom *atoms;
    GList *item_list;
    int i;
    /* **** 重要 **** 检查获取是否成功 */
    if (selection_data->length < 0)
    {
        g_print("Selection retrieval failed\n");
        return;
    }
    /* 打印我们收到的原子 */
    atoms = (GtkAtom *)selection_data->data;
    item_list = NULL;
    for (i=0;i<selection_data->length/sizeof(GtkAtom); i++)
    {
        char *name;
        name = gdk_atom_name (atoms[i]);
        if (name != NULL)
            g_print("%s\n",name);
        else
            g_print("bad atom\n");
    }
    return;
}

int main (int argc, char *argv[])
{
    GtkWidget *window;
    GtkWidget *button;
    gtk_init(&argc, &argv);
    /* 创建顶层窗口 */
    window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
    gtk_window_set_title (GTK_WINDOW (window), "Event Box");
    gtk_container_set_border_width (GTK_CONTAINER (window), 10);
    gtk_signal_connect (GTK_OBJECT (window), "destroy", GTK_SIGNAL_FUNC (gtk_exit), NULL);
    /* 创建用户可以点击以获取目标的按钮 */
    button = gtk_button_new_label ("Get Targets");
    gtk_container_add (GTK_CONTAINER (window), button);
    gtk_signal_connect (GTK_OBJECT (button), "clicked", GTK_SIGNAL_FUNC (get_targets), NULL);
    gtk_signal_connect (GTK_OBJECT (button), "selection-received", GTK_SIGNAL_FUNC (selection_received), NULL);
    gtk_widget_show (button);
    gtk_widget_show (window);
    gtk_main();
    return 0;
}
/* example-end */
```

### 19.3 提供选择

提供选择要复杂一些。你必须注册在当你的选择被请求时调用的处理函数。对于你将处理的每个选择/目标对，你需要调用：

```c
void gtk_selection_add_handler( GtkWidget *widget, GdkAtom selection, GdkAtom target, GtkSelectionFunction function, GtkSelectionRemoveFunction remove_func, gpointer data );
```

`widget`、`selection` 和 `target` 标识了该处理程序将管理的请求。`remove_func` 如果为 `NULL`，则在信号处理程序被移除时被调用。这非常有用，例如对于需要跟踪数据引用计数的解释型语言来说。

回调函数的签名如下：

```c
typedef void (*GtkSelectionFunction)( GtkWidget *widget, GtkSelectionData *selection_data, gpointer data );
```

`GtkSelectionData` 与上述相同，但这次我们负责填充 `type`、`format`、`data` 和 `length` 字段。`format` 实际上非常重要，因为 X 服务器使用它来判断数据是否需要进行字节交换。通常情况下，你不需要关心接收数据时的这个值。`data` 是指向返回数据的指针，`length` 是返回数据的长度（以字节计）。如果 `length` 为负数，则发生了错误且无法获取选择。这可能发生在没有应用程序请求该选择，或者你请求了应用程序不支持的目标。缓冲区实际上保证比 `length` 长一个字节；额外的字节将为零，因此没有必要为了终止字符串而对其进行复制。

# 20. glib

（字符串与唯一整数标识符的双向关联）、键值数据列表（可以通过字符串或整数 ID 访问的数据元素列表）、关系和元组（可以在任意数量字段上索引的数据表）以及缓存。

以下是 glib 功能的概述；此处未涵盖具体的函数、数据结构或操作。有关 glib 例行过程的更完整信息，请参阅 glib 文档。glib 文档的一个来源是 `http://www.gtk.org/`；`http://www.gtk.org/`。

如果您使用的是 C 以外的语言，则应该咨询您对应语言的绑定文档。在某些情况下，您的语言可能内置了等效的功能，而在另一些情况下可能没有。

## 20.1 定义

许多标准类型的极值定义如下：

```
G_MINFLOAT
G_MAXFLOAT
G_MINDOUBLE
G_MAXDOUBLE
G_MINSHORT
G_MAXSHORT
G_MININT
G_MAXINT
G_MINLONG
G_MAXLONG
```

此外，还有以下类型定义。未指定的项根据架构动态设置。记住，如果您希望代码具有可移植性，请不要依赖指针的大小！例如，Alpha 上的指针是 8 字节，但在 Intel 80x86 系列的 CPU 上是 4 字节。

```
char gchar;
short gahort;
long glong;
int gint;
char gouble;
```

```
unsigned char guchar;
```
