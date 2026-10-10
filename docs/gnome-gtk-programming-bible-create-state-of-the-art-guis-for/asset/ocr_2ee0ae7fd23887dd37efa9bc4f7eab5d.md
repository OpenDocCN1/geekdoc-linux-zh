# Functions

```
gint gnome_mdi_add_child(GnomeMDI *mdi, GnomeMDIChild *child)
gint gnome_mdi_add_toplevel_view(GnomeMDI *mdi, GnomeMDIChild *child)
gint gnome_mdi_add_view(GnomeMDI *mdi, GnomeMDIChild *child)
GnomeMDIChild *gnome_mdi_find_child(GnomeMDI *mdi, gchar *name)
GnomeMDIChild *gnome_mdi_get_active_child(GnomeMDI *mdi)
GtkWidget *gnome_mdi_get_active_view(GnomeMDI *mdi)
GnomeApp *gnome_mdi_get_app_from_view(GtkWidget *view)
GnomeApp *gnome_mdi_get_toplevel(GnomeMDI *mdi)
GnomeUIInfo *gnome_mdi_get_child_menu_info(GnomeApp *app)
GnomeUIInfo *gnome_mdi_get_menubar_info(GnomeApp *app)
GnomeUIInfo *gnome_mdi_get_view_from_window(GnomeMDI *mdi, GnomeApp *app)
guint gnome_mdi_get_type()
GtkWidget *gnome_mdi_get_view_from_window(GnomeMDI *mdi, GnomeApp *app)
GtkObject *gnome_mdi_new(gchar *appname, gchar *title)
void gnome_mdi_open_toplevel(GnomeMDI *mdi)
void gnome_mdi_register(GnomeMDI *mdi, GtkObject *object)
gint gnome_mdi_remove_all(GnomeMDI *mdi, gint force)
gint gnome_mdi_remove_child(GnomeMDI *mdi, GnomeMDIChild *child, gint force)
gint gnome_mdi_remove_view(GnomeMDI *mdi, GtkWidget *view, gint force)
void gnome_mdi_set_active_view(GnomeMDI *mdi, GtkWidget *view)
void gnome_mdi_set_child_list_path(GnomeMDI *mdi, const gchar *path)
void gnome_mdi_set_child_menu_path(GnomeMDI *mdi, const gchar *path)
void gnome_mdi_set_menubar_template(GnomeMDI *mdi, GnomeUIInfo *menu_tmpl)
void gnome_mdi_set_mode(GnomeMDI *mdi, GnomeMDIMode mode)
void gnome_mdi_set_toolbar_template(GnomeMDI *mdi, GnomeUIInfo *tbar_tmpl)
void gnome_mdi_unregister(GnomeMDI *mdi, GtkObject *object)
void gnome_mdi_update_child(GnomeMDI *mdi, GnomeMDIChild *child)
```

Chapter 17 provides examples of GnomeMDI.

# GnomeMDIChild

The GnomeMDIChild object is a base class used to create widgets that GnomeMDI can manage as MDI windows. Unless you have some special need, you can use a GnomeMDIGenericChild, which is based on GnomeMDIChild.

# Inheritance

GnomeMDIChild->GtkObject