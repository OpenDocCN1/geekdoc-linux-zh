| Signal Name | Name | Callback Prototype |
| --- | --- | --- |
| "tree_expand" | GtkCTree | void cb(GtkWidget *,<br>GtkCTreeNode *,<br>gpointer) |
| "tree_move" | GtkCTree | void cb(GtkWidget *,<br>GtkCTreeNode *,<br>GtkCTreeNode *,<br>gpointer) |
| "tree_select_row" | GtkCTree | void cb(GtkWidget *,<br>GtkCTreeNode *,<br>gint, gpointer) |
| "tree_unselect_row" | GtkCTree | void cb(GtkWidget *,<br>GtkCTreeNode, gint,<br>gpointer) |
| "undo_selection" | GtkCList | void cb(GtkWidget *,<br>gpointer) |
| "undo_selection" | GtkCListItem | void cb(GtkWidget *,<br>gpointer) |
| "unmap" | GtkWidget | void cb(GtkWidget *,<br>gpointer) |
| "unmap_event" | GtkWidget | gbool<br>cb(GtkWidget *,<br>GdkEvent*, gpointer) |
| "unrealize" | GtkWidget | void cb(GtkWidget *,<br>gpointer) |
| "unselect_all" | GtkCList | void cb(GtkWidget *,<br>gpointer) |
| "unselect_all" | GtkCListItem | void cb(GtkWidget *,<br>gpointer) |
| "unselect_child" | GtkList | void cb(GtkWidget *,<br>GtkWidget *,<br>gpointer) |
| "unselect_child" | GtkTree | void cb(GtkWidget *,<br>GtkWidget *,<br>gpointer) |