# ## GtkMenuItem

A **GtkMenuItem** is a widget that can be inserted into a menu. It is capable of displaying text and acting as the head of submenu.

### Inheritance

`GtkMenuItem->GtkItem->GtkBin->GtkContainer->GtkWidget->GtkObject`

### Functions

`void gtk_menu_item_activate(GtkMenuItem *menu_item)`

`void gtk_menu_item_configure(GtkMenuItem *menu_item, gint show_toggle_indicator, gint show_submenu_indicator)`

`void gtk_menu_item_deselect(GtkMenuItem *menu_item)`

`GtkType gtk_menu_item_get_type(void)`

`GtkWidget *gtk_menu_item_new(void)`

`GtkWidget *gtk_menu_item_new_with_label(const gchar *label)`

`void gtk_menu_item_remove_submenu(GtkMenuItem *menu_item)`

`void gtk_menu_item_right_justify(GtkMenuItem *menutitem)`

`void gtk_menu_item_select(GtkMenuItem *menu_item)`

`void gtk_menu_item_set_placement(GtkMenuItem *menu_item, GtkSubmenuPlacement placement)`

`void gtk_menu_item_set_submenu(GtkMenuItem *menu_item, GtkWidget *submenu)`

### Enums

`typedef enum { GTK_DIRECTION_LEFT, GTK_DIRECTION_RIGHT } GtkSubmenuDirection;`

### Signal

`"activate"    void cb(GtkWidget *, gpointer)`

For an example of **GtkMenuItem**, see the description of **GtkMenu**.

# ## GtkMenuShell

This is the base class for **GtkMenu** and **GtkMenuBar**.

### Inheritance

`GtkMenuShell->GtkContainer->GtkWidget->GtkObject`

### Functions

`void gtk_menu_shell_activate_item(GtkMenuShell *menu_shell, GtkWidget *menu_item, gboolean force_deactivate)`