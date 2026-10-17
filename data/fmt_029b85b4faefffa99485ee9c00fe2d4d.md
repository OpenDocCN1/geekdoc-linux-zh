
```c
void
efficient_append(GList** list, GList** list_end, gpointer data)
{
    g_return_if_fail(list != NULL);
    g_return_if_fail(list_end != NULL);

    if (*list != NULL) {
        assert(*list_end == NULL);
        *list = g_list_append(*list, data);
        *list_end = *list;
    } else {
        *list_end = g_list_append(*list_end, data)->next;
    }
}
```

要使用此函数，你需要将列表及其末尾存储在处，并将它们的地址传递给 `efficient_append()`：

```c
GList* list = NULL;
GList* list_end = NULL;

efficient_append(&list, &list_end, gstrdup("Foo"));
efficient_append(&list, &list_end, gstrdup("Bar"));
efficient_append(&list, &list_end, gstrdup("Baz"));
```

当然，注意不要使用任何可能改变列表而未更新 `list_end` 的列表函数。

```c
#include <glib.h>
GList* g_list_append(GList* list, gpointer data);
g_list_prepend(GList* list, gpointer data);
g_list_insert(GList* list, gpointer data, gint position);
g_list_remove(GList* list, gpointer data);
```

图 2-13. 修改链表内容

为了访问列表元素，提供了图 2-14 中的函数。这些函数中没有一个会改变列表的结构。`g_list_foreach()` 对列表的每个元素应用 `GFunk`。`GFunk` 的定义如下：

```c
typedef void (*GFunc)(gpointer data, gpointer user_data);
```

在 `g_list_foreach()` 中使用的 `GFunk` 会在列表的每个 `list->data` 上被调用，并将你传递给 `g_list_foreach()` 的 `user_data`。`g_list_foreach()` 类似于 Scheme 中的 'map' 函数。

例如，你可能有一个字符串列表，并且可能想要创建一个对字符串应用某些转换的并行列表。这里是一些代码，使用了之前示例中的 `efficient_append()` 函数：

```c
typedef struct _AppContext AppendContext;
struct _AppContext {
  GList* list;
  GList* list_end;
  const gchar* append;
};

static void
  append_foreach(gpointer data, gpointer user_data)
{
  AppContext* ac = (AppContext*) user_data;
  gchar* oldest = (gchar*)data;

  efficient_append(&ac->list, ac->list_end,
                   g_strcat(oldest, ac->append, NULL));
}
```

```c
GList*
copy_with_append(GList* list_of_strings, const gchar* append) {
AppContext* ac;

ac->list = NULL;
ac->list_end = NULL;
ac->append = append;

g_list_foreach(list_of_strings, append_foreach, &ac);

return ac->list;
}
```

`glib` 和 `GTK+` 使用“函数和用户数据”的用法。如果你有函数式编程经验，这就像使用 lambda 表达式来创建闭包。（闭包将函数与环境——一组名称绑定——结合在一起。在这种情况下，“环境”就是你传递给 `append_foreach()` 的用户数据，而“闭包”就是函数与用户数据的组合。）

```c
#include <glib.h>

GList* g_list_find(GList* list, gpointer data);
GList* g_list_nth(GList* list, int n);
gpointer g_list_nth_data(GList* list, int n);
GList* g_list_last(GList* list);
gint g_list_index(GList* list, gpointer data);
void g_list_foreach(GList* list, GFunc func, gpointer user_data);
```

### 图 2-14. 访问链表数据

有一些方便的列表操作例程，列在图 2-15 中。除了 `g_slist_copy()` 之外，所有这些列表都是原地操作的。这意味着你必须赋值返回值并忘记传递的指针，就像你在添加或删除列表元素时一样；`g_slist_copy()` 返回一个新分配的列表，因此你可以继续使用两个列表并最终释放这两个列表。

```c
#include <glib.h>

guint g_slist_length(GList* list);
GList* g_slist_concat(GList* list1, GList* list2);
GList* g_slist_reverse(GList* list);
GList* g_slist_copy(GList* list);
```

图 2-15. 链表的多次追加

最后，还有一些针对排序列表的规定，如图 2-16 所示。要使用这些规定，你必须编写一个 `GCompareFunc`，它就像标准 C `qsort()` 中的比较函数一样。使用 glib 类型，这变为：

```c
typedef int (*GCompareFunc) (gpointer a, gpointer b);
```

如果 `a < b`，函数应该返回一个负值；如果 `a > b`，返回一个正值；如果 `a == b`，返回 0。一旦你有了比较函数，就可以将元素插入到已排序的列表中，或者按升序排序整个列表。你甚至可以利用 `GCompareFunc` 来查找元素，使用 `g_slist_find()`。（注意：`GCompareFunc` 在 `glib` 中的用法不一致；它有时期望一个谓词而不是 qsort 风格的函数。然而，在列表 API 中的用法是一致的。）注意排序列表：使用它们可能会变得低效。例如，`g_slist_insert_sorted` 是 O(n) 操作，但如果你在循环中使用它插入多个元素，循环将呈指数级运行。更好的做法是简单地追加所有元素，然后调用 `g_slist_sort()`。）

仅用于创建根节点；提供了方便宏，可以根据需要自动创建节点。

```
#include <glib.h>

GNode* g_node_new(gpointer data);
```

### 图 2-22. 创建 GNode

要构建树，需要使用图 2-23 所示的基础操作。每个操作都会返回新添加的节点，以便在编写循环或递归遍历树时方便。与 `GList` 不同，忽略返回值是安全的。

```c
#include <glib.h>
GNode* g_node_insert(GNode* parent, gint position, GNode* node);
GNode* g_node_insert_before(GNode* parent, GNode* sibling, GNode* node);
GNode* g_node_prepend(GNode* parent, GNode* node);
```

### 图 2-23. 构建 GNode

图 2-24 所示的方便宏是基于功能性操作实现的。`g_node_append()` 类似于 `g_node_prepend()`；其余操作接受一个数据参数，自动为其分配节点，并调用相应的基础操作。

```c
#include <glib.h>
g_node_append(parent, node);
g_node_insert_data(parent, position, data);
g_node_insert_data_before(parent, sibling, data);
g_node_prepend_data(parent, data);
g_node_append_data(parent, data);
```

### 图 2-24. 构建 GNode
