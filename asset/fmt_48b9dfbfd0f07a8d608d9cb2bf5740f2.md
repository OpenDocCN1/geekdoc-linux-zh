
```c
gint gtk_clist_get_selection_info(GtkClist *clist,
    int x,
    int y,
    int *row,
    int *column );
```

## 11. GtkList Widget

当我们检测到某些感兴趣的内容时，例如指针移动或点击列表中的某处，我们可以读取指针坐标并找出指针在列表中的位置。这很麻烦吗？幸运的是，有一种更简单的方法……

### 11.9 将其整合在一起的信号

与所有组件一样，有几个信号可以使用。`GtkCList`组件继承自`GtkContainer`组件，因此它拥有所有的信号，但也包含以下信号：

- `select_row` - 这将按顺序发送以下信息：`GtkCList *clist`, `gint row`, `gint column`, `KeyEventButton`

- `unselect_row` - 当用户取消选择某行时，会激活此信号。它发送与`select_row`相同的信息

- `click_column` - 发送`GtkCList *clist`, `gint`, `column`

所以，如果我们想为`select_row`连接一个回调函数，该回调函数的声明方式如下：

```c
void select_row_callback(GtkWidget *widget,
               int row,
               int column,
               KeyEvent *event,
               gpointer data);
```

回调函数按通常方式进行连接：

```c
gtk_signal_connect(GTK_OBJECT(clist),
"select_row",
GTK_SIGNAL_FUNC(select_row_callback),
NULL);
```

### 11.10 一个 GtkList 示例

```c
/* example-start clist list.c */

#include <gtk/gtk.h>

/* 用户点击了“添加列表”按钮。 */
void button_add_clicked(gpointer data )
{
    int index;

    /* 向列表中添加这些内容很蠢。4 行，每行 2 列 */
    gchar *drink[4][2] = { "Milk", "3 Oz" },
    { "Water", "6 1" },
    { "Carrots", "2" },
    { "Snakes", "55" };

    /* 这里我们执行实际的文本添加。对每一行执行一次 */
    * row.
    for (int index = 0; index < 4; index++)
        gtk_clist_append((GtkList *) data, drink[index]);

    return;
}
```

```c
/* 用户点击了“清除列表”按钮。 */
void button_clear_clicked(gpointer data)
{
    /* 使用 gtk_clist_clear 清除列表。这比
    * 为每一行调用一次 gtk_clist_remove 要快得多。
    */
    gtk_clist_clear((GtkList*) data);
    return;
}
```

```c
/* 用户点击了“隐藏/显示标题”按钮。 */
void button_hide_show_clicked(gpointer data)
{
    /* 仅记录状态的标记。0 = 当前可见 */
    static short int flag = 0;

    if (flag == 0)
    {
        /* 隐藏标题并将标记置为 1 */
        gtk_clist_column_titles_hide((GtkList*) data);
        flag++;
    }
    else
    {
        /* 显示标题并将标记重置为 0 */
        gtk_clist_column_titles_show((GtkList*) data);
        flag--;
    }
    return;
}
```

```c
/* 如果我们运行到这里，说明用户选择了列表中的某行。 */

void selection_made(GtkClist *clist,

                    int row,

                    int column,

                    GdkEvent *event,

                    gpointer data)

{

    gchar *text;

    /* 获取被选中行和列中的文本。我们将通过指针获取 */

    gtk_clist_get_text(GTK_CLIST(clist), row, column, &text);

    /* 输出关于选中行的信息 */

    g_print("你选择了第 %d 行，具体点击了第 %d 列，该单元格的文本为 %s\n",

           row, column, text);

}
```
