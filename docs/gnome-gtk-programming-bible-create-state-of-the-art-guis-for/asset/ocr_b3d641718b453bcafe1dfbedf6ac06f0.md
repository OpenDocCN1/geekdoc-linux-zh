```
GtkCellType

gtk_clist_get_cell_type(GtkCList *clist, gint row, gint column)

gtk_ctree_node_get_cell_type(GtkCTree *ctree,
	GtkCTreeNode *node, gint column)

```

```
GtkCTreeNode *

gtk_ctree_find_by_row_data(GtkCTree *ctree, GtkCTreeNode *node,
	gpointer data)

gtk_ctree_find_by_row_data_custom(GtkCTree *ctree,
	GtkCTreeNode *node, gpointer data, GCompareFunc func)

gtk_ctree_find_node_ptr(GtkCTree *ctree,
	GtkCTreeRow *ctree_row)

gtk_ctree_insert_gnode(GtkCTree *ctree, GtkCTreeNode *parent,
	GtkCTreeNode *sibling, GNode *gnode,
	GtkCTreeNodeFunc func, gpointer data)

gtk_ctree_insert_node(GtkCTree *ctree, GtkCTreeNode *parent,
	GtkCTreeNode *sibling, gchar *text[], guint8 spacing,
	GdkPixmap *pixmap_closed, GdkBitmap *mask_closed,
	GdkPixmap *pixmap_opened, GdkBitmap *mask_opened,
	gboolean is_leaf, gboolean expanded)

gtk_ctree_last(GtkCTree *ctree, GtkCTreeNode *node)

gtk_ctree_node_nth(GtkCTree *ctree, guint row)

```

```
GtkEnumValue *

gtk_type_enum_find_value(GtkType enum_type,
	const gchar *value_name)

gtk_type_enum_get_values(GtkType enum_type)

```