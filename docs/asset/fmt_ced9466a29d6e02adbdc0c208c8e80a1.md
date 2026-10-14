
`model`和`path`参数帮助你检索模型数据；如果`path_currently_selected`是当前选择的一部分，则为`TRUE`。

你的应用程序可以使用`GtkTreeSelectionFunc`来判断是否可以选择行，你也可以用它根据搜索路径来选择行。

> 注意：选择函数非常强大，但你应该在使用它们的地方保持小心。用户在面对列表或树时，通常期望他们可以选中视图中的任何内容。如果你的应用程序使用`GtkTreeSelectionFunc`导致无法选择某些行，那么理由应该是显而易见的。例如，如果你使用了带有子标题的视图，用户应该理解为什么不能点击这些子标题之一。

为了理解潜在的困惑，考虑一个拥有大量受访者列表的调查应用程序。如果某项特定调查是针对选民的，那么从受访者列表中排除 18 岁以下的人是逻辑。然而，如果 18 岁以下的人出现在列表中，用户在点击鼠标后没有任何反应将会感到困惑。最好是排除这些条目。

## 3.11 选择行

### 3.11.4 扩展示例

到此时，你已经有了关于树和模型的很多细节，但还没有实际代码。本节包含一个较大的示例程序，显示了 Rxico, Inc.（1951年以来家庭和工业用翻器与垃圾）的人员组织。

程序的第一部分为员工数据定义了一个小型数据集。该结构包含一个符合 GTK+ 字符串路径规范的路径组件。在现实的数据集中，情况可能并非如此，因此你必须以其他方式定义路径。

```c
/* -coding: utf-8; */

/* tree.c -- Rxico Inc. 人员 */

#include <gtk/gtk.h>

/* 员工结构体 */
typedef struct _employee {

    gchar *path;
    gchar *last_name;
    gchar *first_name;
    boolean on_site;
    gchar *job_title;
    int gmin_node; /* 如果员工不在岗，则为 -1 */

} employee;

/* 员工数据 */
employee staff[] = {
  {"0:0","Rischaw","George",FALSE,"Majority Shareholder", -1 },
  {"1:0","Kolakowski","Edna",FALSE,"Shareholder", -1 },
  {"2:0","Zimmerman","Walter",TRUE,"Merith",TRUE,"General Manager", 100 },
  {"2:1","Zimmerman","Walter",TRUE,"General Manager", 100 }, 
};
```

# GNOME 开发者官方指南

```c
GtkCellRenderer room_no_renderer, *text_renderer,
*bold_renderer, *check_renderer;
GtkTreeViewColumn room_no_col, *title_col, *last_name_col,
*first_name_col, *on_site_col);
```

```c
/* 初始化 GTK */
gtk_init(&argc, &argv);
window = g_object_new(GTK_TYPE_WINDOW,
    "title", "Rixico Inc.",
    "default-width", 600,
    "default-height", 400,
    NULL);
```

<< 为主窗口附加标准处理程序 >>
创建和更新树模型的过程与 3.11 节中之前的示例非常相似，由于它具有树形结构。`node_insert()` 函数也可以展示如何使用 3.11.1 节中的函数将字符串路径转换为迭代器（iterator）。

```c
/* 创建树模型 */
company = gtk_tree_store_new(NUM_COLS,
    G_TYPE_STRING,
    G_TYPE_STRING,
    G_TYPE_BOOLEAN,
    G_TYPE_STRING,
    G_TYPE_INT);
```

```c
/* 指向人员数据的起始 */
person = staff;

/* 用人员数据填充模型 */
while (person->path != NULL) {
    GtkTreeIter iter;
    path = gtk_tree_path_new_from_string(person->path);
    node_insert(company, path);
    gtk_tree_model_get_iter(GTK_TREE_MODEL(company), &iter, path);
    gtk_tree_path_free(path);
    gtk_tree_store_set(company, iter,
        LASTNAME_COL, person->last_name,
        FIRSTNAME_COL, person->first_name,
        ONSITE_COL, person->on_site,
        TITLE_COL, person->job_title,
        ROOMNO_COL, person->room_no,
        -1);
    person++;
}
```

这里有几种变体。

```c
/* 为房间号创建一个右对齐的渲染器 */
room_no_renderer = gtk_cell_renderer_text_new();
g_object_set(room_no_renderer, "xalign", 1.0, NULL);
```

```c
/* 一个普通的文本渲染器 */
text_renderer = gtk_cell_renderer_text_new();
```

```c
/* 一个加粗文本的渲染器（用于最后一列） */
```

### 3.11.4 扩展示例

```c
bold_renderer = gtk_cell_renderer_text_new();
g_object_set(bold_renderer, "weight", 500, NULL);

/* 一个复选框渲染器 */
check_renderer = gtk_cell_renderer_toggle_new();
```

现在是时候查看列并将渲染器放入列中了。房间号渲染器从此处获取了一个特殊的 `room_convert()` 数据函数：

```c
/* 创建列 */
room_no_col = gtk_tree_view_column_new_with_attributes(
  "Room", room_no_renderer,
  NULL);
gtk_tree_view_column_set_cell_data_func(room_no_col, room_no_renderer,
  room_convert,
  NULL, NULL);
```

标题是你可以移动的唯一列。其他列是相对固定的：

```c
title_col = gtk_tree_view_column_new_with_attributes(
  "Title", text_renderer,
  "text", TITLE_COL,
  NULL);
```

```c
/* 允许用户移动列 */
g_object_set(title_col, "reorderable", TRUE, NULL);
```

```c
last_name_col = gtk_tree_view_column_new_with_attributes(
  "Last name", bold_renderer,
  "text", LASTNAME_COL,
  NULL);
```

```c
first_name_col = gtk_tree_view_column_new_with_attributes(
  "First name", text_renderer,
  "text", FIRSTNAME_COL,
  NULL);
```

```c
on_site_col = gtk_tree_view_column_new_with_attributes(
  "On site?", check_renderer,
  "active", ONSITE_COL,
  NULL);
```

创建顶层视图几乎与创建列表完全相同，因为我们将列封装到视图中。

```c
/* 创建整体视图 */
view = g_object_new(GTK_TYPE_TREE_VIEW,
  "model", company,
  "rules-hint", TRUE,
```
