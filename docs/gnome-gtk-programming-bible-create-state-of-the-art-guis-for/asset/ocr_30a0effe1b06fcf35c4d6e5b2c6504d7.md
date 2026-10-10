# Functions

void gtk_tree_item_collapse(GtkTreeItem \*tree_item)
void gtk_tree_item_deselect(GtkTreeItem \*tree_item)
void gtk_tree_item_expand(GtkTreeItem \*tree_item)
GtkType gtk_tree_item_get_type(void)
GtkWidget \*gtk_tree_item_new(void)
GtkWidget \*gtk_tree_item_new_with_label(gchar \*label)
void gtk_tree_item_remove_subtree(GtkTreeItem \*item)
void gtk_tree_item_select(GtkTreeItem \*tree_item)
void gtk_tree_item_set_subtree(GtkTreeItem \*tree_item,
GtkWidget \*subtree)

# Signals

```
"collapse"        void cb(GtkWidget \*, gpointer)
"expand"          void cb(GtkWidget \*, gpointer)
```

For an example of GtkTreeItem, see the description of GtkTree.

# GtkVBox

GtkVBox is a container widget that organizes its contained widgets vertically (one on top of the other).

# Inheritance

GtkVBox->GtkBox->GtkContainer->GtkWidget->GObject

# Functions

GtkType gtk_vbox_get_type(void)
GtkWidget \*gtk_vbox_new(gboolean homogeneous, gint spacing)

Refer to Chapter 4 for a number of examples of GtkVBox.

# GtkVButtonBox

GtkVButtonBox is a container designed to display a collection of buttons vertically (one on top of the other).

# Inheritance

GtkVButtonBox->GtkButtonBox->GtkBox->GtkContainer->GtkWidget->
GObject