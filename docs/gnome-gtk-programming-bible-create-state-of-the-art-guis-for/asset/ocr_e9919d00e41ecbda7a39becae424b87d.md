```
```
  gtk_menu_append(GTK_MENU(menu),item);
  group = gtk_radio_menu_item_group(
    GTK_RADIO_MENU_ITEM(item));
  item = gtk_radio_menu_item_new_with_label(group,
  "Third Radio");
  gtk_menu_append(GTK_MENU(menu),item);

  /* Add the label on top of the menu */
  item = gtk_menu_item_new_with_label("RadioMenu");
  gtk_menu_item_set_submenu(GTK_MENU_ITEM(item),
  menu);

  /* Append the menu to the menu bar */
  menubar = gtk_menu_bar_new();
  gtk_menu_bar_append(GTK_MENU_BAR(menubar),item);
  return(menubar);
}
```
```

![](bbox=[0.1, 0.44, 0.25, 0.53])

**Figure 21-40:** A set of three radio buttons on a menu

# # GtkRange

This is the base class for the group of widgets that involve graphic display and manipulation of a value bounded within a specific minimum and maximum value. These widgets are GtkHScale, GtkScrollbar, GtkVScale, and GtkVScrollbar.

**Inheritance**

GtkRange->GtkWidget->GtkObject

**Functions**

void gtk_range_clear_background(GtkRange *range)
void gtk_range_default_hmotion(GtkRange *range, gint xdelta, gint ydelta)
void gtk_range_default_hslider_update(GtkRange *range)
gint gtk_range_default_through_click(GtkRange *range, gint x, gint y, gfloat *jump_perc)
void gtk_range_default_vmotion(GtkRange *range, gint xdelta, gint ydelta)
void gtk_range_default_vslider_update(GtkRange *range)
gint gtk_range_default_vthrough_click(GtkRange *range, gint x, gint y, gfloat *jump_perc)