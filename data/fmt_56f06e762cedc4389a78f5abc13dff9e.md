
![](img/8bcc1ba72831c7d67cfc8b395deab95f_571_0.png)

## GtkCList

`GtkCList`小部件包含一个或多个文本列表，并允许用户选择一个或多个行。大量的控制函数使其成为一个非常灵活的小部件。

### 继承

`GtkCList` -> `GtkContainer` -> `GtkWidget` -> `GtkObject`

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
```
