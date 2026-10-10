```
    GTK_DIR_UP,
    GTK_DIR_DOWN,
    GTK_DIR_LEFT,
    GTK_DIR_RIGHT
  } GtkDirectionType;

typedef enum {
  GTK_RESIZE_PARENT,
  GTK_RESIZE_QUEUE,
  GTK_RESIZE_IMMEDIATE
  } GtkResizeMode;
```

# **Signals**

```
"add"            void cb(GtkWidget \*, GtkWidget \*, gpointer)
"check-resize"    void cb(GtkWidget \*, gpointer)
"focus"          gint cb(GtkWidget \*, GtkDirectionType,
                    GtkDirectionType, gpointer)
"remove"         void cb(GtkWidget \*, GtkWidget \*, gpointer)
"set-focus-child" void cb(GtkWidget \*, GtkWidget \*, gpointer)
```

# GtkCTree

This widget displays a hierachical tree (such as a directory tree) and enables the user to traverse the tree using the mouse.

# **Inheritance**

```
GtkCTree -> GtkClist -> GtkContainer -> GtkWidget -> GtkObject
```

# **Functions**

```
void gtk_ctree_collapse(GtkCTree \*ctree, GtkCTreeNode \*node)
void gtk_ctree_collapse_recursive(GtkCTree \*ctree,
              GtkCTreeNode \*node)
void gtk_ctree_collapse_to_depth(GtkCTree \*ctree,
              GtkCTreeNode \*node, gint depth)
void gtk_ctree_construct(GtkCTree \*ctree, gint columns,
              gint tree_column, gchar \*titles [] )
void gtk_ctree_expand(GtkCTree \*ctree, GtkCTreeNode \*node)
void gtk_ctree_expand_recursive(GtkCTree \*ctree,
              GtkCTreeNode \*node)
void gtk_ctree_expand_to_depth(GtkCTree \*ctree,
              GtkCTreeNode \*node, gint depth)
GNode \*gtk_ctree_export_to_gnode(GtkCTree \*ctree,
              GNode \*parent, GNode \*sibling, GtkCTreeNode \*node,
              GNode *defNodeFunc func, gpointer data)
gboolean gtk_ctree_find(GtkCTree \*ctree, GtkCTreeNode \*node,
              GtkCTreeNode \*child)
GList \*gtk_ctree_find_all_by_row_data(GtkCTree \*ctree,
              GtkCTreeNode \*node, gpointer data)
GList \*gtk_ctree_find_all_by_row_data_custom(GtkCTree \*ctree,
              GtkCTreeNode \*node, gpointer data, GCompareFunc func)
```