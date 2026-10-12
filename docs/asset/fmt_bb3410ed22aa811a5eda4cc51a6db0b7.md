
`void`

`panel_clean_applet(AppletInfo *info)` {

    `g_return_if_fail(info != NULL)`;

    `if(info->widget)` {

        `if(info->type == APPLET_STATUS)` {

            `status_applet_put_offscreen(info->data)`;

            `gtk_widget_destroy(info->widget)`;

        }

    }

}

如果没有 `g_assert_fail`，如果传递的 `info` 为 `NULL`，`panel_clean_applet` 将遇到问题。有了断言宏后，`g_return_if_fail` 会返回错误：

> CRITICAL **: file panel.c: line 227 (`panel_clean_applet`):
assertion '`info != NULL`' failed.

这会直接指向问题所在。函数内部的一致性检查通常使用断言宏完成：

```c
g_assert(condition)
```

如果条件失败，将调用 `abort` 并生成核心转储（core dump）：

```
file test.c: line 9 (assert_test):
assertion failed: (pointer != NULL)
aborting...
Aborted (core dumped)
```

## 使用 GNOME-GTK+ 进行 GUI 编程

由于 `g_assert` 会结束程序的执行，因此在失败并非致命的情况下，在函数内部最好使用 `g_return_if_fail`。

为了表示永远不应该执行的代码区域，glib 提供了：

```c
g_assert_not_reached()
```

如果被执行，它将带错误信息并中止：

```
** ERROR**: file search_window.c: line 733 (update_search_clist):
should not be reached
naborting...
Aborted (core dumped)
$ 
```

这在一个或多个条件永远不应该满足的条件语句中非常有用。例如，在代码片段中：

```c
current_page = gtk_notebook_get_current_page (GTK_NOTEBOOK (search_notebook));
switch (current_page)
  case TITLE_PAGE:
    clist = lookup_widget (GTK_WIDGET button), "title_search_clist";
    break;
  case MEMBER_PAGE:
    clist = lookup_widget (GTK_WIDGET button), "member_search_clist";
    break;
  case DISK_PAGE:
    clist = lookup_widget (GTK_WIDGET button), "disk_search_clist";
    break;
  default:
    g_assert_not_reached();
}
```

我们确保在 `switch` 语句中 `current_page` 等于 `TITLE_PAGE`、`MEMBER_PAGE` 或 `DISK_PAGE`。

GNOME 和 GTK+ 经常使用这些宏；这也是为什么它们容易编写，以及发现错误非常直观的原因。我们通过示例学习——使用宏将减少你一半搜索 `NULL` 指针和其他烦人错误的时间。

## 字符串函数

C 语言中的字符串处理是一项笨拙的任务，每个程序员都深知。处理字符数组、字符指针、指针数组的指针等，需要一致且无瑕的编程。

越界内存边界和指针的不当使用构成了运行时错误的主体，而 `string.h` 中的标准字符串函数也毫不留错，相比之下，glib 提供了更清晰、安全、可移植的替代方案，并在进行切割、更改和通用字符串操作时包含了许多实用的额外函数。

glib 健壮字符串库的一个良好例子是 `g_snprintf`。该函数等同于 `sprintf`，但它只会将格式字符串的前 `n` 个字符复制到 `buf`，并保证字符串以 `NULL` 终止。注意 `n` 个字符包含了 `NULL` 终止符。

```c
int g_snprintf(gchar *buf, g_int n, const gchar *format, ...);
```

但在使用 `g_snprintf` 之前，你必须为格式化字符串分配足够的空间：

```c
gchar *msg = g_mallococ(50);
g_snprintf(msg, 50, "Error occurred. %s", err, action);
```

在这种情况下，更方便的方法是使用 `g_strdupprintf`：

```c
gchar *g_strdupprintf(const gchar *format, ...);
```

`g_strdupprintf` 分配存储格式化字符串所需的正确空间，不再需要猜测并计算所需的长度：

```c
gchar *msg = g_strdupprintf("Error occurred. %s", err, action);
```

在这两种情况下，分配的缓冲区仍然必须使用 `g_free` 释放。我们稍后会查看更多 glib 的内存管理。为了将字符串复制到新分配的字符串中，我们有 `g_strdup`、`g_strncpy`，如所述，`g_strdup` 复制完整字符串，`g_strncpy` 只复制前 `n` 个字符：

```c
g_free(msg);
```

## 内存分配

glib 通过其等效函数 `g_malloc` 和 `g_free` 封装了 C `malloc` 和 `free` 函数的潜在问题。在使用 `--enable-mem-profile` 编译选项时，glib 配对提供了实用的内存分析。`mem_profile` 将程序的内存使用信息输出到控制台。具体来说，`mem_profile` 会输出不同大小的分配频率、总分配字节数、总释放数以及这些值之间的差；即仍在使用的字节数。内存泄漏变得容易发现。

与 `malloc` 不同，`g_malloc` 会处理大小为 0 的分配请求并返回 `NULL` 指针。`g_malloc` 在分配失败时会立即中止程序，从而避免了检查 `NULL` 指针的需求。这可以被视为一个缺点，因为没有失败时的回退机制。与 `free` 不同，`g_free` 会忽略它的 `NULL` 指针。

由于两个分配器 `malloc` 和 `g_malloc` 可能使用独立的内存池，因此将 `g_free` 与 `g_malloc` 配对至关重要，同样 `free` 和 `malloc` 也必须成对使用。

```c
gpointer g_malloc(gulong size)
void g_free(gpointer mem)
```

`g_realloc` 是熟悉的 `realloc` 的 glibget，用于重新分配缓冲区的大小。与 `g_malloc` 一致，`g_realloc` 在传入零长度缓冲区时返回 `NULL`。`g_memdup` 将内存块复制到新分配的缓冲区。

```c
gpointer g_realloc(gpointer mem, gulong size)
gpointer g_memdup(gconstpointer mem, gulong bytesize)
```

## 列表

在单链表或双向链表中存储数据是一个非常常见的编程需求，glib 提供了优秀的资源来以简洁且高效的方式实现两者。

双向链表 `GList` 包含指向前一个元素和下一个元素的指针：

```c
- 双向链表
struct GList {
  gpointer data;
  GList *next;
  GList *prev;
}
```

与单链表 `GSList` 不同，`GList` 允许正向和反向遍历列表：

```c
- 单链表
struct GSList {
  gpointer data;
  GSList *next;
};
```

请注意，两个列表中的数据都存储为 `gpointers`，但你可以通过使用宏 `GLINT_TO_POINTER`、`GPOINTER_TO_INT`、`GUINT_TO_POINTER` 和 `GPOINTER_TO_UINT` 轻松地存储整数。

要创建一个空单链表，只需初始化一个 NULL 指针：

```
GSList *single_list = NULL;
```

同样地，通过以下方式创建双向链表：

```c
GList *double_list = NULL;
```
