
| `target` | 与你想要移除的目标名称对应的原子值。 |

# `gtk_target_list_unref()`

```
void gtk_target_list_unref( GtkTargetList *list )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 指向 `GtkTargetList` 的指针，应减少其引用计数。 |

# `gtk_tearoff_menu_item_new()`

```
GtkWidget gtk_tearoff_menu_item_new( void )
```

返回新的可拆卸菜单项。

# `gtk_text_freeze()`

```
void gtk_text_freeze( GtkText *text )
```

| 参数 | 描述 |
| --- | --- |
| `text` | 你正在冻结的 `GtkText`。 |

# `gtk_text_thaw()`

```
void gtk_text_thaw( GtkText *text )
```

| 参数 | 描述 |
| --- | --- |
| `text` | 你正在解冻的 `GtkText`。 |

# `gtk_text_insert()`

```
void gtk_text_insert( GtkText *text, GdkFont *font, GdkColor *fore, GdkColor *back, const char *chars, gint length )
```

| 参数 | 描述 |
| --- | --- |
| `text` | 你正在插入文本的 `GtkText` 小部件。 |
| `font` | 用于文本的字体。`Gtktext` 小部件支持多种字体。 |
| `fore`, `back` | 文本的前景颜色和背景颜色。 |
| `chars` | 要插入的字符。 |
| `length` | 你插入的字符数量。`-1` 表示插入所有字符。 |

# 函数原型

## `gtk_text_new()`

```
GtkWidget * gtk_text_new( GtkAdjustment *hadj, GtkAdjustment *vadj)
```

返回新的文本小部件。

| 参数 | 描述 |
| --- | --- |
| `hadj` | 水平调整对象，控制水平方向的范围。如果为 `NULL`，则文本小部件将创建自己的。 |
| `vadj` | 垂直调整对象，控制垂直方向的范围。如果为 `NULL`，则文本小部件将创建自己的。 |

## `gtk_text_set_editable()`

```
void gtk_text_set_editable( GtkText *text, gboolean editable )
```

| 参数 | 描述 |
| --- | --- |
| `text` | 你正在设置其编辑性的 `GtkText`。 |
| `is_editable` | 如果文本可以编辑则为 `TRUE`（默认值）；否则为 `FALSE`。 |

## `gtk_text_set_line_wrap()`

```
void gtk_text_set_line_wrap( GtkText *text, gint line_wrap )
```

| 参数 | 描述 |
| --- | --- |
| `text` | 你正在设置其换行的 `GtkText`。 |
| `line_wrap` | `TRUE` 导致在遇到可见区域结束时换行；`FALSE` 导致行继续延伸（因此部分内容不可见）。 |

## `gtk_text_set_word_wrap()`

```
void gtk_text_set_word_wrap( GtkText *text, gint word_wrap )
```

## `gtk_timeout_add()`

```
guint gtk_timeout_add( guint interval, GtkCallback function, gpointer data )
```

返回一个 ID。

| 参数 | 描述 |
| --- | --- |
| `interval` | 间隔（毫秒）。 |
| `function` | 回调函数。 |
| `data` | 传递的数据。 |

# 附录

```
void gtk_timeout_remove(int timeout_id )
```

| 参数 | 描述 |
| --- | --- |
| `timeout_id` | 要移除的 ID。 |

# `gtk_text_new`

```
GtkWidget * gtk_text_new(void )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 指向 `GtkTargetList` 的指针，在该列表中查找目标。 |
| `list` | 指向 `GtkTargetList` 的指针，新目标必须存储其中。 |
| `list` | 指向 `GtkTargetList` 的指针，应增加其引用计数。 |
| `list` | 指向 `GtkTargetList` 的指针，应减少其引用计数。 |

# `_list_unref`

```
void gtk_text_freeze( G(Text *text )
```

| 参数 | 描述 |
| --- | --- |
| `text` | 你正在冻结的 `GtkText`。 |

# `_text________text_`

| 参数 | 描述 |
| --- | --- |
| `text` | 你正在解冻的 `GtkText`。 |

```
void gtk_text_set_editable()
```

```text
void gtk_text_set_editable( G_Text *text, gbooleaneditable )
```

| 参数 | 描述 |
| --- | --- |
| `text` | 你正在设置其可编辑性的 `GtkText`。 |

```
void gtk_text_set_editable( GtkText *text, gboolean editable )
```

# 函数原型

## `gtk_target_list_find()`

```
boolean gtk_target_list_find(GtkTargetList *list, GdkAtom target, guint *info )
```

如果找到目标则返回 `TRUE`，否则返回 `FALSE`。

| 参数 | 描述 |
| --- | --- |
| `list` | 指向 `GtkTargetList` 的指针，在该列表中查找目标。 |
| `target` | 与目标名称对应的原子值，你想要获取该名称的 `info` 字段。 |
| `info` | 指向 `geist` 变量的指针，如果可以检索到，将用它存储 `info` 值。 |

## `gtk_target_list_new()`

```
GtkTargetList* gtk_target_list_new(const GtkTargetEntry *targets, guint ntargets )
```

返回新创建的 `GtkTargetList` 指针。

| 参数 | 描述 |
| --- | --- |
| `targets` | 指向填充 `GtkTargetEntry` 结构体数组的指针。 |
| `ntargets` | `targets` 中的项数。如果将 `targets` 设置为 `NULL` 且 `ntargets` 设置为 `0`，则将创建一个空的 `GtkTargetList`。 |

## `gtk_target_list_ref()`

```
void gtk_target_list_ref( GtkTargetList *list )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 指向 `GtkTargetList` 的指针，应增加其引用计数。 |

## `gtk_target_list_remove()`

```
void gtk_target_list_remove( GtkTargetList *list, GdkAtom target )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 指向 `GtkTargetList` 的指针，新目标必须存储其中。 |
| `target` | 与你想要移除的目标名称对应的原子值。 |

# `gtk_target_list_unref()`

```
void gtk_target_list_unref( GtkTargetList *list )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 指向 `GtkTargetList` 的指针，应减少其引用计数。 |
