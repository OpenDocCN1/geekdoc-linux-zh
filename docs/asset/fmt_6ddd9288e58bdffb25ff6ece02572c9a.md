
# GtkCheckButton

```c
typedef struct _GtkCheckButton GtkCheckButton;

struct _GtkCheckButton {
  GtkToggleButton toggle_button;
};
```

# GtkMenuItem

```c
typedef struct _GtkMenuItem GtkMenuItem;

struct _GtkMenuItem {
  GtkMenuItem menu_item;
  guint active : 1;
  guint always_show_toggle : 1;
};
```

# GtkCLList

```c
typedef struct _GtkCLList GtkCLList;

struct _GtkCLList {
  GtkContainer container;
};
```

```c
guint16 flags;
/* mem chunks */
GMemChunk *row_mem_chunk;
GMemChunk *cell_mem_chunk;
```

![](img/7fa9959a9d28ad339fa75e44952feeb9_826_0.png)

```c
guint freeze_count;
/* allocation rectangle after the container_border_width
* and the width of the shadow border */
GdkRectangle internal_allocation;
/* rows */
gint rows;
gint row_center_offset;
gint row_height;
List *row_list;
GList *row_list_end;
/* columns */
gint columns;
GdkRectangle column_title_area;
GdkWindow *title_window;
/* dynamically allocated array of column structures */
GtkListColumn *column;
/* the scrolling window and its height and width to
* makes things a little speedier */
GdkWindow *clist_window;
gint clist_window_width;
gint clist_window_height;
/* offsets for scrolling */
gint hoffset;
gint voffset;
/* border style */
GtkShadowType shadow_type;
/* the list's selection mode (gtkenums.h) */
GtkSelectionMode selection_mode;
/* list of selected rows */
GList *selection;
GList *selection_end;
/* undo_selection */
GList *undo_selection;
gint undo_anchor;
/* mouse button actions */
guint8 button_actions[5];
```

* and */
`GtkCellListInfo` `click_cell`;
/* 滚动调整 */
`GtkAdjustment` *hadjustment;
`GtkAdjustment` *vadjustment;
/* 用于垂直拖动线的 xor GC */
`GdkGC` *xor_gc;
/* 用于绘制未选中单元格的 gc */
`GdkGC` *fg_gc;
`GdkGC` *bg_gc;
/* 用于指示拖拽的游标 */
`GtkCursor` *cursor_drag;
/* xor-拖动线的当前 x 像素位置 */
`gint` x_drag;
/* 焦点处理 */
`gint` focus_row;
/* 拖动选择项 */
`gint` anchor;
`GtkStateType` anchor_state;
`gint` drag_pos;
`gint` htimer;
`gint` vtimer;

`GtkSortType` sort_type;
`GtkListCompareFunc` compare;
`gint` sort_column;
};

# GtkColorSelection

```c
typedef struct _GtkColorSelection GtkColorSelection;

struct _GtkColorSelection {
  GtkVBox vbox;
  GtkWidget *wheel_area;
  GtkWidget *value_area;
  GtkWidget *sample_area;
  GtkWidget *sample_area_eb;
  GtkWidget *scales[8];
  GtkWidget *entries[8];
  GtkWidget *opacity_label;
```

# 录 E

```c
GdkGC *wheel_gc;
GdkGC *value_gc;
GdkGC *sample_gc;
GtkUpdateType policy;
int use_opacity;
int timer_active;
int timer_tag;
double values[8];
double old_values[8];
guchar *wheel_buf;
guchar *value_buf;
guchar *sample_buf;
};
```

# GtkColorSelectionDialog

```c
typedef struct _GtkColorSelectionDialog GtkColorSelectionDialog;

struct _GtkColorSelectionDialog {
  nGtkWindow window;
  GtkWidget *colorsel;
  GtkWidget *main_vbox;
  GtkWidget *ok_button;
  GtkWidget *reset_button;
  GtkWidget *cancel_button;
  GtkWidget *help_button;
};
```

# GtkCombo

```c
typedef struct _GtkCombo GtkCombo;
/* 你应该直接访问 entry 和 list 字段 */
struct _GtkCombo {
  nGtkBox hbox;
  GtkWidget *entry;
  GtkWidget *button;
  GtkWidget *popup;
  GtkWidget *popwin;
  GtkWidget *list;
};
```

`guint` entry_change_id;
`guint` list_change_id;
`guint` value_in_list:1;
`guint` ok_if_empty:1;
`guint` case_sensitive:1;
`guint` use_arrows:1;
`guint` use_arrows_always:1;

```c
guint16 current_button;
guint activate_id;
}
```

# GtkContainer

```c
typedef struct GtkContainer GtkContainer GtkContainer;
struct _GtkContainer
{
  GtkWidget widget;
  nGtkWidget *focus_child;
  guint border_width : 16;
  guint need_resize : 1;
  guint resize_mode : 2;
```

```c
/* 请求调整大小的子列表
*/
GSList *resize_widgets;
};
```

# GtkTree

```c
typedef struct GtkTree GtkTree
struct _GtkTree
{
  GtkList clist;
  nGdkGC *lines_indent;
  guint tree_indent;
  guint tree_spacing;
  guint tree_column;
  guint line_style : 2;
  guint expander_style : 2;
  guint show_stub : 1;
  GtkTreeCompareFunc drag_compare;
};
```

# GtkCurve

```c
typedef struct GtkCurve GtkCurve;
struct _GtkCurve
{
```
