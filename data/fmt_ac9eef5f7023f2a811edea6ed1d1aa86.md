
## 支持的参数

前缀：`GtkNotebook::`

表 10.9 `GtkNotebook` 参数

| 名称 | 类型 | 权限 |
|---|---|---|
| `page` | `GTK_TYPE_INT` | `GTK_ARG_READWRITE` |

## 表 10.9 GtkNotebook 参数（续）

| 名称 | 类型 | 权限 |
| --- | --- | --- |
| `tab_pos` | `GTK_TYPE_POSITION_TYPE` | `GTK_ARG_READWRITE` |
| `tab_border` | `GTK_TYPE_UINT` | `GTK_ARG_WRITABLE` |
| `tab_h` | `GTK_TYPE_UINT` | `GTK_ARG_READWRITE` |
| `tab_vborder` | `GTK_TYPE_UINT` | `GTK_ARG_READWRITE` |
| `show_tabs` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |
| `show_border` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |
| `scrollable` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |
| `enable_popup` | `GTK_TYPE_STRING` | `GTK_ARG_READWRITE` |
| `tab_label` | `GTK_TYPE_STRING` | `GTK_ARG_READWRITE` |
| `menu_label` | `GTK_TYPE_STRING` | `GTK_ARG_READWRITE` |
| `position` | `GTK_TYPE_INT` | `GTK_ARG_READWRITE` |
| `tab_fill` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |
| `tab_pack` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |

## 应用级 API 摘要

在运行时获取常量 `GTK_TYPE_NOTEBOOK`：

```
GtkType

gtk_notebook_get_type(void);
```

创建 `GtkNotebook` 实例：

```
GtkWidget *

gtk_notebook_new(void);
```

使用指定的标签将控件添加到笔记本中：

```
void

gtk_notebook_append_page(GtkNotebook *notebook, GtkWidget *child,

GtkWidget *tab_label);
```

使用指定的标签将控件添加到菜单，并在笔记本的弹出菜单中添加菜单项：

```
void

gtk_notebook_append_page_menu(GtkNotebook *notebook,

GtkWidget *child, GtkWidget *tab_label, GtkWidget *menu_label);
```

## 应用级 API 摘要（续）

使用指定的标签将控件插入到笔记本开头：
```
void

gtk_notebook_prepend_page(GtkNotebook *notebook, GtkWidget *child,

GtkWidget *tab_label);
```

使用指定的标签将控件插入到笔记本开头，并在笔记本的弹出菜单中添加菜单项：

```
void

gtk_notebook_prepend_page_menu(GtkNotebook *notebook,

GtkWidget *child, GtkWidget *tab_label, GtkWidget *menu_label);
```

使用指定的标签将控件插入笔记本中：

```
void

gtk_notebook_insert_page(GtkNotebook *notebook, GtkWidget *child,

GtkWidget *tab_label, gint position);
```

使用指定的标签将控件插入笔记本中，并在笔记本的弹出菜单中添加菜单项：

```
void

gtk_notebook_insert_page_menu(GtkNotebook *notebook,

GtkWidget *child, GtkWidget *tab_label, GtkWidget *menu_label,

gint position);
```

从笔记本中移除一个页：

```
void

gtk_notebook_remove_page(GtkNotebook *notebook, gint page_num);
```

获取当前显示页的索引：

```
gint

gtk_notebook_current_page(GtkNotebook *notebook);
```

获取笔记本中第 n 页对应的控件：

```
GtkWidget *

gtk_notebook_get_nth_page(GtkNotebook *notebook, gint page_num);
```

根据控件确定其在笔记本中的页：

```
gint

gtk_notebook_get_page(GtkNotebook *notebook, GtkWidget *child);
```

显示指定的页：

```
void

gtk_notebook_set_page(GtkNotebook *notebook, gint page_num);
```

切换到笔记本中的下一页：

```
void

gtk_notebook_next_page(GtkNotebook *notebook);
```

切换到笔记本中的上一页：

```
void

gtk_notebook_prev_page(GtkNotebook *notebook);
```

## 应用级 API 摘要（续）

切换边框的显示：

```
void

gtk_notebook_set_show_border(GtkNotebook *notebook, boolean show_border);
```

切换标签的显示：

```
void

gtk_notebook_set_show_tabs(GtkNotebook *notebook, boolean show_tabs);
```

更改笔记本中标签的位置：

```
void

gtk_notebook_set_tab_pos(GtkNotebook *notebook, GtkPositionType pos);
```

启用（禁用）等宽大小的笔记本标签：

```
void

gtk_notebook_set_homogeneous_tabs(GtkNotebook *notebook, boolean homogeneous);
```

设置标签的边框宽度：

```
void

gtk_notebook_set_tab_border(GtkNotebook *notebook, gint border_width);
```

设置标签的水平边框宽度：

```
void

gtk_notebook_set_tab_hborder(GtkNotebook *notebook, gint tab_h);
```

设置标签的垂直边框宽度：

```
void

gtk_notebook_set_tab_vborder(GtkNotebook *notebook, gint tab_vborder);
```

启用（禁用）笔记本的滚动功能：

```
void

gtk_notebook_set_scrollable(GtkNotebook *notebook, boolean scrollable);
```

启用笔记本弹出菜单的显示：

```
void

gtk_notebook_popup_enable(GtkNotebook *notebook);
```

禁用笔记本弹出菜单的显示：

```
void

gtk_notebook_popup_disable(GtkNotebook *notebook);
```

获取与控件关联的标签：

```
GtkWidget *

gtk_notebook_get_tab_label(GtkNotebook *notebook, GtkWidget *child);
```

## 应用级 API 摘要（续）

设置与控件关联的标签：

```
void

gtk_notebook_set_tab_label(GtkNotebook *notebook, GtkWidget *child, GtkWidget *tab_label);
```

设置与控件关联的标签文本：

```
void

gtk_notebook_set_tab_label_text(GtkNotebook *notebook, GtkWidget *child, const gchar *tab_text);
```

获取与控件关联的菜单标签：

```
GtkWidget *
```
