
既然我们已经详细讨论了 GtkList，是时候看看另一个类似的 Gtk+ 类——GtkTree 了。尽管它们很相似，但 GtkList 和 GtkTree 在 widget 层次结构中是互不关联的。正如你所看到的，GtkList 比 GtkTree 更具功能性。我的建议是对简单的单列列表使用 GtkList。如果你需要多列列表，或者需要 GtkList 提供的额外功能，请使用 GtkTree。

## GtkCList

### 类名

`GtkCList`

### 父类名

`GtkContainer`

## 宏

- Widget 类型宏：`GTK_TYPE_CLIST`
- 对象到 widget 转换宏：`GTK_CLIST(obj)`
- Widget 类型检查宏：`GTK_IS_CLIST(obj)`

### 表 6.4 信号

| 信号名称 | 触发信号的条件 |
|---|---|
| select_row | 列表中的某个项目状态变为已选中。 |
| unselect_row | 列表中的某个项目状态变为未选中。 |
| row_move | 列表中的某行被移动了。 |
| click | 列表中的某项被点击。 |
| resize | 列表调整了大小。 |
| focus | 焦点发生了切换。 |
| select_all | 执行了全选操作。 |
| unselect_all | 执行了取消全选操作。 |
| undo_selection | 状态被撤销。 |

*(注：由于原文文本后续部分出现了大量的格式重复和混乱，以下翻译已根据逻辑结构进行了清理和对齐)*

## 应用级 API 摘要（续）

设置 `clist` 的垂直调整：
``` 
void
gtk_clist_set_vadjust (GtkClist *clist, GtkAdjustment *adjustment);
```

获取 `clist` 的水平调整：
``` 
GtkAdjustment *
gtk_clist_get_hadjustment (GtkClist *clist);
```

获取 `clist` 的垂直调整：
``` 
GtkAdjustment *
gtk_clist_get_vadjustment (GtkClist *clist);
```

设置 `clist` 的边框样式：
``` 
void
gtk_clist_set_shadow_type (GtkClist *clist, GtkShadowType type);
```

设置 `clist` 的选择模式：
``` 
void
gtk_clist_set_selection_mode (GtkClist *clist, GtkSelectionMode mode);
```

启用或禁用 `clist` 对行进行重排序的能力：
``` 
gtk_clist_set_reorderable (GtkClist *clist, boolean reorderable);
```

启用或禁用拖拽图标的使用：
``` 
void
gtk_clist_set_use_drag_icons (GtkClist *clist, boolean use_icons);
```

设置 `clist` 按钮动作：
``` 
void
gtk_clist_set_button_actions (GtkClist *clist, guint guints8 button_actions);
```

冻结（禁用）`cl` 控件上的视觉更新：
``` 
void
gtk_clist_freeze (GtkClist *clist);
```

解冻（重新启用）`cl` 控件上的视觉更新：
``` 
void
gtk_clist_thaw (GtkClist *clist);
```

显示出现在 `clist` 列上方的标题按钮：
``` 
void
gtk_clist_column_titles_show (GtkClist *clist);
```

隐藏出现在 `clist` 列上方的标题按钮：
``` 
void
gtk_clist_column_titles_hide (GtkClist *clist *clist);
```

设置列标题为激活状态（响应按钮按下、预亮显示和键盘焦点）：
``` 
void
gtk_clist_column_title_active (GtkClist *clist, gint column);
```

设置列标题为非激活状态（不响应按钮按下、预亮显示和键盘焦点）：
``` 
void
gtk_clist_column_title_passive (GtkClist *clist, gint column);
```

设置所有列标题为激活状态（响应按钮按下、预亮显示和键盘焦点）：
``` 
gtk_clist_column_titles_active (GtkClist *clist);
```

设置所有列标题为非激活状态（不响应按钮按下、预亮显示和键盘焦点）：
``` 
void
gtk_clist_column_titles_passive (GtkClist *clist *clist);
```

将列标题按钮的文本设置为指定的字符串：
``` 
void
gtk_clist_set_column_title (GtkClist *clist, gint column, const gchar *title);
```

指定一个控件作为列标题的“标签”，而不是使用文本标签：
``` 
void
gtk_clist_set_column_widget (GtkClist *clist, gint column, GtkWidget *widget);
```

获取由列标题按钮拥有的控件：
``` 
GtkWidget *
gtk_clist_get_column_widget (GtkClist *clist, gint column);
```

指定 `clist` 中列的对齐设置：
``` 
void
gtk_clist_set_column_justification (GtkClist *clist, gint column, GtkJustification justification);
```

显示或隐藏 `clist` 中的某一列：
``` 
void
gtk_clist_set_column_visibility (GtkClist *clist, gint column, gboolean visible);
```

为特定列启用或禁用鼠标调整列大小的操作：
``` 
void
gtk_clist_set_column_resizable(GtkList *clist, gint column, gboolean sizeable);
```

指定列是否根据其内容自动调整大小到最佳宽度：
``` 
void
gtk_clist_set_column_auto_resize(GtkList *clist, gint column, gboolean auto_resize);
```

使列表中的所有列根据其内容自动调整大小到最佳尺寸：
``` 
gint
gtk_clist_columns_autosize(GtkList *clist);
```

获取显示指定列中所有内容所需的最小宽度（不裁剪）：
``` 
gint
gtk_clist_optimal_column_width(GtkList *clist, gint column);
```

显式设置某行的列宽：
``` 
void
gtk_clist_set_column_width(GtkList *clist, gint column, gint width);
```

设置列的最小宽度：
``` 
void
gtk_clist_set_column_min_width(GtkList *clist, gint column, gint min_width);
```

设置列的最大宽度：
``` 
void
gtk_clist_set_column_max_width(GtkList *clist, gint column, gint max_width);
```

设置某行的高度。0 表示高度与当前字体相同：
``` 
void
gtk_clist_set_row_height(GtkList *clist, guint height);
```

将列表的视图区域滚动到指定的列和行：
``` 
void
gtk_clist_moveto(GtkList *clist, gint row, gint column, gfloat row_align, gfloat col_align);
```

返回列表中指定行的可见性：
``` 
GtkVisibility
gtk_clist_row_is_visible(GtkList *clist, gint row);
```

获取列表指定指定单元格的单元格类型：
``` 
GtkCellType
gtk_clist_get_cell_type(GtkList *clist, gint row, gint column);
```

设置 `clist` 中指定行和列的单元格所显示的文本：evenvoid
``` 
gtk_clist_set_text(GtkClist *clist, gint row, gint column, const gchar *text);
```

获取 `clist` 指定行和列处显示的文本：
``` 
gint
gtk_clist_get_text(GtkClist *clist, gint row, gint column, gchar **text);
```

设置 `clist` 中指定位置单元格的位图（pixmap）：
``` 
void
gtk_clist_set_pixmap(GtkClist *clist, gint row, gint column, GdkPixmap *pixmap, GdkBitmap *mask);
```

获取 `clist` 指定位置单元格的位图：
``` 
gint
gtk_clist_get_pixmap(GtkClist *clist, gint row, gint column);
```

设置 `clist` 中指定位置单元格的位图，替换其当前内容：
``` 
void
gtk_clist_set_pixmap(GtkClist *clist, gint row, gint column, GdkPixmap *pixmap, GdkBitmap *mask);
```

设置 `clist` 中指定行和列的单元格的文本：
``` 
void
gtk_clist_set_text(GtkClist *clist, gint row, gint column, const gchar *text);
```

设置某行的前景颜色：
``` 
void
gtk_clist_set_foreground(GtkClist *clist, gint row, GdkColor *color);
```

获取 `clist` 中指定行单元格的前景颜色：
``` 
GdkColor
gtk_clist_get_foreground(GtkClist *clist, gint row);
```

设置某行的背景颜色：
``` 
void
gtk_clist_set_background(GtkClist *clist, gint row, GdkColor *color);
```

获取 `clist` 中指定行单元格的背景颜色：
``` 
GdkColor
gtk_clist_get_background(GtkClist *clist, gint row);
```

设置指定单元格的样式：
``` 
void
gtk_clist_set_style(GtkClist *clist, gint row);
```

获取指定行的样式：
``` 
GtkStyle
gtk_clist_get_style(GtkClist *clist, gint row);
```

设置某行的水平和垂直偏移：
``` 
void
gtk_clist_set_shift(GtkClist *clist, gint row, gint horizontal_shift, gint vertical_shift);
```

获取某行的水平和垂直偏移：
``` 
void
gtk_clist_get_shift(GtkClist *clist, gint row, gint *horizontal_shift, gint *vertical_shift);
```

设置某行的可选择属性：
``` 
void
gtk_clist_set_selectable(GtkClist *clist, gint row);
```

获取某行的可选择属性：
``` 
boolean
gtk_clist_get_selectable(GtkClist *clist, gint row);
```

将行插入到列表头部，返回其插入索引：
``` 
gint
gtk_clist_prepend(GtkClist *clist, gchar *text);
```

将行追加到列表末尾，返回其插入索引：
``` 
gint
gtk_clist_append(GtkClist *clist, gchar *text);
```

在指定索引插入行，根据排序属性可能不同，clist 插入：
``` 
gint
gtk_clist_insert(GtkClist *clist, gint index, gchar *text);
```

从列表中删除指定的行：
``` 
void
gtk_clist_remove(GtkClist *clist, gint row);
```

为某行关联任意数据：
``` 
void
gtk_clist_set_data(GtkClist *clist, gint row, gpointer data);
```

为某行关联任意数据，带有销毁回调：
``` 
void
gtk_clist_set_data_full(GtkClist *clist, gint row, gpointer data, GtkFree destroy);
```

获取某行关联的任意数据：
``` 
gpointer
gtk_clist_get_data(GtkClist *clist, gint row);
```

根据数据查找对应的行：
``` 
gint
gtk_clist_find_row_from_data(GtkClist *clist, gpointer data);
```

选择 `clist` 中指定的行和列：
``` 
void
gtk_clist_select_row(GtkClist *clist, gint row, gint column);
```

取消选择 `clist` 中指定的行和列：
``` 
void
gtk_clist_unselect_row(GtkClist *clist, gint row, gint column);
```

撤销上一次选择：
``` 
void
gtk_clist_undo_selection(GtkClist *clist);
```

移除 `clist` 中的所有项：
``` 
void
gtk_clist_clear(GtkClist *clist);
```

根据指定的 x 和 y 位置返回行：
``` 
gint
gtk_clist_get_selection_info(GtkClist *clist, gint x, gint y, gint *row, gint column);
```

选择所有行（仅支持多选和扩展）：
``` 
void
gtk_clist_select_all(GtkClist *clist);
```

取消所有行和列（浏览模式除外）：
``` 
void
gtk_clist_unselect_all(GtkClist *clist);
```

交换 `clist` 中两行的位置：
``` 
void
gtk_clist_swap_rows(GtkClist *clist, gint row1, gint row2);
```

将行移动到另一个位置：
``` 
void
gtk_clist_row_move(GtkClist *clist, gint source_row, gint dest_row);
```

设置排序函数，替换默认或最后设置的值：
``` 
void
gtk_clist_set_compare_func(GtkClist *clist, GtkClistCompareFunc cmp_func);
```

在排序操作之前指定用于排序的列：
``` 
void
gtk_clist_set_sort_column(GtkClist *clist, gint column);
```

## 应用级 API 摘要（续）

在进行排序操作之前指定排序类型：
``` 
void
gtk_clist_set_sort_type(GtkClist *clist, GtkSortType sort_type);
```

使用当前的排序函数和类型，在之前指定的列上对列表进行排序：
``` 
void
gtk_clist_sort(GtkClist *clist);
```

告诉 GtkClist 在项插入列表时自动排序：
``` 
void
gtk_clist_set_auto_sort(GtkClist *clist, gboolean auto_sort);
```
