# Inheritance

```
GtkLayout->GtkContainer->GtkWidget->GtkObject
```

# Functions

```
void gtk_layout_freeze(GtkLayout *layout)
GtkAdjustment *gtk_layout_get_hadjustment(GtkLayout *layout)
GtkType gtk_layout_get_type(void)
GtkAdjustment *gtk_layout_get_vadjustment(GtkLayout *layout)
void gtk_layout_move(GtkLayout *layout,
                     GtkWidget *child_widget, gint x, gint y)
GtkWidget *gtk_layout_new(GtkAdjustment *hadjustment,
                          GtkAdjustment *vadjustment)
void gtk_layout_put(GtkLayout *layout, GtkWidget *child_widget,
                    gint x, gint y)
void gtk_layout_set_hadjustment(GtkLayout *layout,
                                GtkAdjustment *adjustment)
void gtk_layout_set_size(GtkLayout *layout, guint width,
                         guint height)
void gtk_layout_set_vadjustment(GtkLayout *layout,
                                GtkAdjustment *adjustment)
void gtk_layout_thaw(GtkLayout *layout)
```

# Signal

```
"set-scroll-adjustments"    void cb(GtkWidget *, GtkAdjustment
                                *, GtkAdjustment *, gpointer)
```

Chapter 5 provides an example of the GtkLayout container.

# GtkList

The GtkList container manages a list of text items and enables the selection of one or more items.

# Inheritance

```
GtkList->GtkContainer->GtkWidget->GtkObject
```

# Functions

```
void gtk_list_append_items(GtkList *list, GList *items)
gint gtk_list_child_position(GtkList *list, GtkWidget *child)
void gtk_list_clear_items(GtkList *list, gint start, gint end)
void gtk_list_end_drag_selection(GtkList *list)
void gtk_list_end_selection(GtkList *list)
void gtk_list_extend_selection(GtkList *list,
                               GkScrollType scroll_type, gfloat position,
                               gboolean auto_start_selection)
GtkType gtk_list_get_type(void)
void gtk_list_insert_items(GtkList *list, GList *items,
```