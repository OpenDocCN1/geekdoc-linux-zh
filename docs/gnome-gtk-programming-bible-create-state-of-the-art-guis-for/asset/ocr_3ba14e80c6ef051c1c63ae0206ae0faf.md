```
GNOIME_DOCK_RIGHT,
GNOIME_DOCK_BOTTOM,
GNOIME_DOCK_LEFT,
GNOIME_DOCK_FLOATING
} GnomeDockPlacement;
```

For an example of docking, see the GnomeDock widget earlier in this chapter.

# # GnomeDockItem

The GnomeDockItem is a container with the ability of containing one widget. The GnomeDockItem is contained in a GnomeDockBand widget, which is contained in a GnomeDock widget.

# ### Inheritance

GnomeDockItem->GtkBin->GtkContainer->GtkWidget->GtkObject

# ### Functions

```
void gnome_dock_item_attach(GnomeDockItem *item, GtkWidget *parent, gint x, gint y)
gboolean gnome_dock_item_detach(GnomeDockItem *item, gint x, gint y)
void gnome_dock_item_drag_floating(GnomeDockItem *item, gint x, gint y)
GnomeDockItemBehavior gnome_dock_item_get_behavior(GnomeDockItem *dock_item)
GtkWidget *gnome_dock_item_get_child(GnomeDockItem *item)
void gnome_dock_item_get_floating_position(GnomeDockItem *item, gint *x, gint *y)
gchar *gnome_dock_item_get_name(GnomeDockItem *item)
GtkOrientation gnome_dock_item_get_orientation(GnomeDockItem *dock_item)
GtkShadowType gnome_dock_item_get_shadow_type(GnomeDockItem *dock_item)
guint gnome_dock_item_get_type(void)
void gnome_dock_item_grab_pointer(GnomeDockItem *item)
void gnome_dock_item_handle_size_request(GnomeDockItem *item, GtkRequisition *requisition)
GtkWidget *gnome_dock_item_new(const gchar *name, GnomeDockItemBehavior behavior)
gboolean gnome_dock_item_set_orientation(GnomeDockItem *dock_item, GtkOrientation orientation)
void gnome_dock_item_set_shadow_type(GnomeDockItem *dock_item, GtkShadowType type)
```

# ### Enum

```
typedef enum {
GNOIME_DOCK_ITEM_BEH_NORMAL,
GNOIME_DOCK_ITEM_BEH_EXCLUSIVE,
GNOIME_DOCK_ITEM_BEH_NEVER_FLOATING,
```