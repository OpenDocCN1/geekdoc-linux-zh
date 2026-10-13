
# 函数原型

```c
void gtk_menu_append( GtkMenu *menu, GtkWidget *child )
```

```c
void gtk_menu_prepend( GtkMenu *menu, GtkWidget *child )
```

```c
void gtk_menu_insert( GtkMenu *menu, GtkWidget *child, gint position )
```

| 参数 | 描述 |
| --- | --- |
| `menu` | 你正在添加的菜单 |
| `child` | 你正在添加的控件 |
| `position` | 添加子的位置（位置数字）（仅用于 `gtk_menu_insert()`） |

```c
void gtk_menu_bar_append( GtkMenuBar *menu_bar, GtkWidget *child )
```

```c
void gtk_menu_bar_prepend( GtkMenuBar *menu_bar, GtkWidget *child )
```

| 参数 | 描述 |
| --- | --- |
| `menu_bar` | 你正在添加或置前的菜单栏 |
| `child` | 你正在添加的控件 |

```c
GtkWidget* gtk_menu_new( void )
```

```c
GtkWidget* gtk_menu_new_with_label( const gchar *label )
```

| 参数 | 描述 |
| --- | --- |
| `label` | 指向预定义字符串的指针，该字符串将显示在标签中 |

# 函数原型

`gtk_list_clear_items()`

```c
void gtk_list_clear_items(GtkList *list, gint start, gint end)
```

| 参数 | 描述 |
|---|---|
| `list` | 函数将作用的 `GtkList` 指针 |
| `start` | 将移除的控件范围的数值起始位置 |
| `end` | 将移除的控件范围的数值结束位置 |

`gtk_list_insert_items()`

```c
void gtk_list_insert_items(GtkList *list, GList *items, gint position)
```

| 参数 | 描述 |
|---|---|
| `list` | 函数将作用的 `GtkList` 指针。 |
| `items` | 指向 `GtkListItem` 结构 `GList` 指针，这些结构体将被插入到 `GtkList` 中。 |
| `position` | 插入项的 `GtkListItem` 之前的数值位置。使用 `-1` 将列表项插入到 `GtkList` 的末尾；这与使用 `gtk_list_append_items()` 函数的效果相同。 |

`gtk_list_item_new()`

```c
GtkWidget* gtk_list_item_new(void)
```

返回指向新创建的 `GtkListItem` 指针。

`gtk_list_item_new_with_label()`

```c
GtkWidget* gtk_list_item_new_with_label(const gchar *label)
```

| 参数 | 描述 |
|---|---|
| `label` | 指向预定义字符串的指针，该字符串将显示在标签中 |

该函数返回指向新创建的 `GtkListItem` 指针。

`gtk_list_prepend_items()`

```c
void gtk_list_prepend_items(GtkList *list, GList *items)
```

# 附录 D

| 参数 | 描述 |
| --- | --- |
| `list` | 函数将作用的 `GtkList` 指针 |
| `items` | 指向 `GtkListItem` 结构 `GList` 指针，这些结构将被置于 `GtkList` 内容的前面 |

`gtk_list_remove_items()`

```c
void gtk_list_remove_items(GtkList *list, GList *items )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 函数将作用的 `GtkList` 指针 |
| `items` | 指向 `GtkListItem` 结构 `GList` 指针，这些结构体将被销毁并从 `GtkList` 中移除 |

`gtk_list_remove_items_no_unref()`

```c
void gtk_list_remove_items_no_unref( GtkList *list, GList *items )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 函数将作用的 `GtkList` 指针 |
| `items` | 指向 `GtkListItem` 结构 `GList` 指针，这些结构体将被从 `GtkList` 中移除 |

`gtk_list_select_all()`

```c
void gtk_list_select_all( GtkList *list )
```

```c
void gtk_list_unselect_all( GtkList *list )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 所有项将被全部选中或取消选择的 `GtkList` 指针 |

`gtk_list_select_item()`

```c
void gtk_list_select_item( GtkList *list, gint item )
```

```c
void gtk_list_unselect_item( GtkList *list, gint item )
```

`gtk_list_select_child()`

```c
void gtk_list_select_child( GtkList *list, GtkWidget *child )
```

```c
void gtk_list_unselect_child( GtkList *list, GtkWidget *child )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 函数将作用的 `GtkList` 指针 |
| `item` | 将选中或取消选择的 `GtkListItem` 的数值位置 |
| `child` | 将选中或取消选择的 `GtkListItem` 指针 |

```c
void gtk_list_set_selection_mode( GtkList *list, guint mode )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 函数将作用的 `GtkList` 指针 |
| `mode` | 对应新选择模式的值（参见表 1.2） |

```c
void gtk_main( void )
```

```c
void gtk_main_quit( void )
```
