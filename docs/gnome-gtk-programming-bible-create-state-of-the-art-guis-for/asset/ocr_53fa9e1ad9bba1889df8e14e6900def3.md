*extend_selection"    void cb(GtkWidget *, gint, gfloat, gboolean, gpointer)
*scroll_horizontal"   void cb(GtkWidget *, gint, gfloat, gpointer)
*scroll_vertical"     void cb(GtkWidget *, gint, gfloat, gpointer)
*select_all"          void cb(GtkWidget *, gpointer)
*start_selection"     void cb(GtkWidget *, gpointer)
*toggle_add_mode"     void cb(GtkWidget *, gpointer)
*toggle_focus_row"    void cb(GtkWidget *, gpointer)
*undo_selection"      void cb(GtkWidget *, gpointer)
*unselect_all"        void cb(GtkWidget *, gpointer)

For an example, see the GtkList description earlier in this chapter.

# # GtkMenu

This is a container designed to operate as a pull-down menu.

# ## Inheritance

GtkMenu->GtkMenuShell->GtkContainer->GtkWidget->GtkObject

# ## Functions

```
void gtk_menu_append(GtkMenu *menu, GtkWidget *child)
void gtk_menu_attach_to_widget(GtkMenu *menu,
    GtkWidget *attach_widget, GtkMenuDetachFunc detacher)
void gtk_menu_detach(GtkMenu *menu)
GtkAccelGroup *gtk_menu_ensure_unique_accel_group(
    GtkMenu *menu)
GtkAccelGroup *gtk_menu_get_accel_group(GtkMenu *menu)
GtkWidget *gtk_menu_get_active(GtkMenu *menu)
GtkWidget *gtk_menu_get_attach_widget(GtkMenu *menu)
GtkType gtk_menu_get_type(void)
GtkAccelGroup *gtk_menu_get_unique_accel_group(GtkMenu *menu)
void gtk_menu_insert(GtkMenu *menu, GtkWidget *child,
    gint position)
GtkWidget *gtk_menu_new(void)
void gtk_menu_popup(GtkMenu *menu,
    GtkWidget *parent_menu_shell, GtkWidget *parent_menu_item,
    GtkMenuPositionFunc func, gpointer data, guint button,
    guint32 activate_time)
void gtk_menu_prepend(GtkMenu *menu, GtkWidget *child)
void gtk_menu_reorder_child(GtkMenu *menu, GtkWidget *child,
    gint position)
void gtk_menu_reposition(GtkMenu *menu)
void gtk_menu_set_accel_group(GtkMenu *menu, 
```