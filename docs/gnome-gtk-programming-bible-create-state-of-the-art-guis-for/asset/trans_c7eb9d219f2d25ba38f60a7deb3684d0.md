
## GtkCalendar

```c
void gtk_calendar_freeze(GtkCalendar *calendar)
void gtk_calendar_get_date(GtkCalendar *calendar, guint *year,
guint *month, guint *day)
GtkType gtk_calendar_get_type(void)
gint gtk_calendar_mark_day(GtkCalendar *calendar, guint day)
GtkWidget *gtk_calendar_new(void)
void gtk_calendar_select_day(GtkCalendar *calendar, guint day)
gint gtk_calendar_select_month(GtkCalendar *calendar,
guint month, guint year)
void gtk_calendar_thaw(GtkCalendar *calendar)
gint gtk_calendar_unmark_day(GtkCalendar *calendar, guint day)
```

### 枚举

```c
typedef enum {
GTK_CALENDAR_SHOW_HEADING,
GTK_CALENDAR_SHOW_DAY_NAMES,
GTK_CALENDAR_NO_MONTH_CHANGE,
GTK_CALENDAR_SHOW_WEEK_NUMBERS,
GTK_CALENDAR_WEEK_START_MONDAY
} GtkCalendarDisplayOptions;
```

每当创建一个新的日历小部件时，它默认显示当前的日期和时间，其显示效果如图 21-5 所示。

```c
static GtkWidget *makeWidget()
{
GtkWidget *widget;
widget = gtk_calendar_new();
return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_569_0.png)

图 21-5: 显示的 GtkCalendar 小部件

## GtkCheckButton

GtkCheckButton 小部件显示一个带有标签的小按钮。可以通过鼠标切换该按钮的开/关状态，并且它会保持该状态，直到再次被切换。

### 继承

GtkCheckButton -> GtkToggleButton -> GtkButton -> GtkBin -> GtkContainer -> GtkWidget -> GtkObject

### 函数

```c
GtkType gtk_check_button_get_type(void)
GtkWidget *gtk_check_button_new(void)
GtkWidget *gtk_check_button_new_with_label(
const gchar *label)
```

以下示例显示了图 21-6 中展示的窗口。

```c
static GtkWidget *makeWidget()
{
GtkWidget *widget;
widget = gtk_check_button_new_with_label(
"Check Button Label");
return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_570_0.png)

## GtkCheckMenuItem

此小部件显示一个切换按钮和一个标签。由于它继承自 GtkMenuItem，因此旨在用作菜单中的切换按钮。

### 继承

GtkCheckMenuItem -> GtkMenuItem -> GtkItem -> GtkBin -> GtkContainer -> GtkWidget -> GtkObject

### 函数

```c
GtkType gtk_check_menu_item_get_type(void)
GtkWidget *gtk_check_menu_item_new(void)
GtkWidget *gtk_check_menu_item_new_with_label(
const gchar *label)
void gtk_check_menu_item_set_active(
GtkCheckMenuItem *check_menu_item, Gboolean is_active)
void gtk_check_menu_item_set_show_toggle(
GtkCheckMenuItem *menu_item, Gboolean always)
void gtk_check_menu_item_toggled(
GtkCheckMenuItem *check_menu_item)
```

### 信号

- "toggled" void cb(GtkWidget *, gpointer)

以下示例显示了图 21-7 中展示的窗口。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *widget;
    
    widget = gtk_check_menu_item_new_with_label(
             " Check Label");
    gtk_check_menu_item_set_show_toggle(
             GTK_CHECK_MENU_ITEM(widget), TRUE);
    return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_571_0.png)

## GtkCList

GtkCList 小部件包含一个或多个文本列表，并允许用户选择一个或多个行。大量的控制函数使其成为一个非常灵活的小部件。

### 继承

GtkCList -> GtkContainer -> GtkWidget -> GtkObject

### 函数

```c
gint gtk_clist_append(GtkCList *clist, gchar *text [ ])
void gtk_clist_clear(GtkCList *clist)
void gtk_clist_column_titles_active(GtkCList *clist, 
             gint column)
void gtk_clist_column_titles_passive(GtkCList *clist, 
             gint column)
void gtk_clist_column_titles_active(GtkCList *clist)
void gtk_clist_column_titles_passive(GtkCList *clist)
void gtk_clist_column_titles_show(GtkCList *clist)
gint gtk_clist_columns_autosize(GtkCList *clist)
void gtk_clist_construct(GtkCList *clist, gint columns, 
             gchar *titles [ ])
gint gtk_clist_find_row_from_data(GtkCList *clist, 
             gpointer data)
void gtk_clist_freeze(GtkCList *clist)
GtkStyle *gtk_clist_get_cell_style(GtkCList *clist, gint row, 
             gint column)
GtkCellType gtk_clist_get_cell_type(GtkCList *clist, gint row,
gint column)
gchar *gtk_clist_get_column_title(GtkCList *clist, gint column)
GtkWidget *gtk_clist_get_column_widget(GtkCList *clist,
gint column)
GtkAdjustment *gtk_clist_get_hadjustment(GtkCList *clist)
gint gtk_clist_get_pixmap(GtkCList *clist, gint row,
gint column, GdkPixmap *pixmap, GdkBitmap *mask)
gint gtk_clist_get_pixtext(GtkCList *clist, gint row,
gint column, gchar *text, guint8 *spacing,
GdkPixmap *pixmap, GdkBitmap *mask)
gpointer gtk_clist_get_row_data(GtkCList *clist, gint row)
GtkStyle *gtk_clist_get_row_style(GtkCList *clist, gint row)
gboolean gtk_clist_get_selectable(GtkCList *clist, gint row)
gint gtk_clist_get_selection_info(GtkCList *clist, gint x,
gint y, gint *row, gint *column)
gint gtk_clist_get_text(GtkCList *clist, gint row, gint column,
gchar *text)
gchar gtk_clist_get_type(void)
GtkAdjustment *gtk_clist_get_vadjustment(GtkCList *clist)
gint gtk_clist_insert(GtkCList *clist, gint row,
gchar *text [])
void gtk_clist_moveto(GtkCList *clist, gint row, gint column,
gfloat row_align, gfloat col_align)
GtkWidget *gtk_clist_new(gint columns)
GtkWidget *gtk_clist_new_with_data(gint columns,
gchar *titles [])
gint gtk_clist_optimal_column_width(GtkCList *clist,
gint column)
gint gtk_clist_prepend(GtkCList *clist, gchar *text [])
void gtk_clist_remove(GtkCList *clist, gint row)
GtkVisibility gtk_clist_row_is_visible(GtkCList *clist,
gint row)
void gtk_clist_row_move(GtkCList *clist, gint source_row,
gint dest_row)
void gtk_clist_select_all(GtkCList *clist)
void gtk_clist_select_row(GtkCList *clist, gint row,
gint column)
void gtk_clist_set_auto_sort(GtkCList *clist,
gboolean auto_sort)
void gtk_clist_set_background(GtkCList *clist, gint row,
GdkColor *color)
void gtk_clist_set_button_actions(GtkCList *clist,
guint button, guint8 button_actions)
void gtk_clist_set_cell_style(GtkCList *clist, gint row,
gint column, GtkStyle *style)
void gtk_clist_set_column_auto_resize(GtkCList *clist,
gint column, gboolean auto_resize)
void gtk_clist_set_column_justification(GtkCList *clist,
gint column, GtkJustification justification)
void gtk_clist_set_column_max_width(GtkCList *clist,
gint column, gint max_width)
void gtk_clist_set_column_min_width(GtkCList *clist,
 gint column, gint min_width)
void gtk_clist_set_column_resizable(GtkCList *clist,
 gint column, gint resizable)
void gtk_clist_set_column_title(GtkCList *clist, gint column,
 const gchar *title)
void gtk_clist_set_column_visibility(GtkCList *clist,
 gint column, gboolean visible)
void gtk_clist_set_column_widget(GtkCList *clist, gint column,
 GtkWidget *widget)
void gtk_clist_set_column_width(GtkCList *clist, gint column,
 gint width)
void gtk_clist_set_compare_func(GtkCList *clist,
 GtkCListCompareFunc cmp_func)
void gtk_clist_set_foreground(GtkCList *clist, gint row,
 GdkColor *color)
void gtk_clist_set_hadjustment(GtkCList *clist,
 GtkAdjustment *adjustment)
void gtk_clist_set_pixmap(GtkCList *clist, gint row,
 gint column, GdkPixmap *pixmap, GdkBitmap *mask)
void gtk_clist_set_pixtext(GtkCList *clist, gint row,
 gint column, const gchar *text, guint8 spacing,
 GdkPixmap *pixmap, GdkBitmap *mask)
void gtk_clist_set_reorderable(GtkCList *clist,
 gboolean reorderable)
void gtk_clist_set_row_data(GtkCList *clist, gint row,
 gpointer data)
void gtk_clist_set_row_data_full(GtkCList *clist, gint row,
 gpointer data, GtkDestroyNotify destroy)
void gtk_clist_set_row_height(GtkCList *clist, guint height)
void gtk_clist_set_row_style(GtkCList *clist, gint row,
 GtkStyle *style)
void gtk_clist_set_selectable(GtkCList *clist, gint row,
 gboolean selectable)
void gtk_clist_set_selection_mode(GtkCList *clist,
 GtkSelectionMode mode)
void gtk_clist_set_shadow_type(GtkCList *clist,
 GtkShadowType type)
void gtk_clist_set_shift(GtkCList *clist, gint row,
 gint column, gint vertical, gint horizontal)
void gtk_clist_set_sort_column(GtkCList *clist, gint column)
void gtk_clist_set_sort_type(GtkCList *clist,
 GtkSortType sort_type)
void gtk_clist_set_text(GtkCList *clist, gint row, gint column,
 const gchar *text)
void gtk_clist_set_use_drag_icons(GtkCList *clist,
 gboolean use_icons)
void gtk_clist_set_vadjustment(GtkCList *clist,
 GtkAdjustment *adjustment)
void gtk_clist_sort(GtkCList *clist)
void gtk_clist_swap_rows(GtkCList *clist, gint row1, gint row2)
```

