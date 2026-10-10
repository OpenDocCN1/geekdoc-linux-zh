
### 表 F-1

| 信号名称 | 名称 | 回调原型 |
| :--- | :--- | :--- |
| "key_release_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "kill_char" | GtkEditable | void cb(GtkWidget *, gint, gpointer) |
| "kill_line" | GtkEditable | void cb(GtkWidget *, gint, gpointer) |
| "kill_word" | GtkEditable | void cb(GtkWidget *, gint, gpointer) |
| "layout_changed" | GnomeDock | void cb(GtkWidget *, gpointer) |
| "leave" | GtkButton | void cb(GtkWidget *, gpointer) |
| "leave_notify_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "map" | GtkWidget | void cb(GtkWidget *, gpointer) |
| "map_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "motion_notify_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "move_current" | GtkMenuShell | void cb(GtkWidget *, GtkMenuDirectionType, gpointer) |
| "move_cursor" | GtkEditable | void cb(GtkWidget *, gint, gint, gpointer) |
| "move_page" | GtkEditable | void cb(GtkWidget *, gint, gint, gpointer) |
| "move_to_column" | GtkEditable | void cb(GtkWidget *, gint, gint, gpointer) |
| "move_to_row" | GtkEditable | void cb(GtkWidget *, gint, gpointer) |
| "move_word" | GtkEditable | void cb(GtkWidget *, gint, gpointer) |
| "no_expose_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "orientation_changed" | GtkToolbar | void cb(GtkWidget *, gint, gpointer) |
| "output" | GtkSpinButton | gboolean cb(GtkWidget *, gpointer) |
| "parent_set" | GtkWidget | void cb(GtkWidget *, GtkObject *, gpointer) |
| "paste_clipboard" | GtkEditable | void cb(GtkWidget *, gpointer) |
| "pressed" | GtkButton | void cb(GtkWidget *, gpointer) |
| "property_notify_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "proximity_in_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "proximity_out_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "realize" | GtkWidget | void cb(GtkWidget *, gpointer) |
| "released" | GtkButton | void cb(GtkWidget *, gpointer) |
| "remove" | GtkContainer | void cb(GtkWidget *, GtkWidget *, gpointer) |
| "resize_column" | GtkCList | void cb(GtkWidget *, gint, gint, gpointer) |
| "row_move" | GtkCList | void cb(GtkWidget *, gint, gint, gpointer) |
| "scroll_horizontal" | GtkCList | void cb(GtkWidget *, GtkScrollType, gfloat, gpointer) |
| "scroll_horizontal" | GtkListItem | void cb(GtkWidget *, gint, gfloat, gpointer) |
| "scroll_vertical" | GtkCList | void cb(GtkWidget *, GtkScrollType, gfloat, gpointer) |
| "scroll_vertical" | GtkListItem | void cb(GtkWidget *, gint, gfloat, gpointer) |
| "select" | GtkItem | void cb(GtkWidget *, gpointer) |
| "select_all" | GtkCList | void cb(GtkWidget *, gpointer) |
| "select_all" | GtkListItem | void cb(GtkWidget *, gpointer) |
| "select_child" | GtkList | void cb(GtkWidget *, GtkWidget *, gpointer) |
| "select_child" | GtkTree | void cb(GtkWidget *, GtkWidget *, gpointer) |
| "select_icon" | GnomeIconList | void cb(GtkWidget *, guint, GdkEvent *, gpointer) |
| "select_row" | GtkCList | void cb(GtkWidget *, gint, GdkEvent *, gpointer) |
| "selection_changed" | GtkList | void cb(GtkWidget *, gpointer) |
| "selection_changed" | GtkTree | void cb(GtkWidget *, gpointer) |
| "selection_clear_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "selection_get" | GtkWidget | void cb(GtkWidget *, GtkSelectionData *, guint, guint, gpointer) |
| "selection_notify_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "selection_received" | GtkWidget | void cb(GtkWidget *, GtkSelectionData *, gpointer) |
| "selection_request_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "selection_started" | GnomeIconTextItem | void cb(GtkWidget *, gpointer) |
| "selection_stopped" | GnomeIconTextItem | void cb(GtkWidget *, gpointer) |
| "selection-done" | GtkMenuShell | void cb(GtkWidget *, gpointer) |
| "set_focus" | GtkWindow | void cb(GtkWidget *, gpointer) |
| "set_scroll_adjustments" | GtkCList | void cb(GtkWidget *, GtkAdjustment *, GtkAdjustment *, gpointer) |
| "set_scroll_adjustments" | GtkLayout | void cb(GtkWidget *, GtkAdjustment *, GtkAdjustment *, gpointer) |
| "set_scroll_adjustments" | GtkText | void cb(GtkWidget *, GtkAdjustment *, GtkAdjustment *, gpointer) |
| "set_scroll_adjustments" | GtkViewport | void cb(GtkWidget *, GtkAdjustment *, GtkAdjustment *, gpointer) |
| "set-editable" | GtkEditable | void cb(GtkWidget *, gboolean, gpointer) |
| "set-focus-child" | GtkContainer | void cb(GtkWidget *, GtkWidget *, gpointer) |
| "show" | GtkWidget | void cb(GtkWidget *, gpointer) |
| "size_allocate" | GtkWidget | void cb(GtkWidget *, gpointer, gpointer) |
| "size_request" | GtkWidget | void cb(GtkWidget *, gpointer, gpointer) |
| "start_query" | GtkTipsQuery | void cb(GtkWidget *, gpointer) |
| "start_selection" | GtkCList | void cb(GtkWidget *, gpointer) |
| "start_selection" | GtkListItem | void cb(GtkWidget *, gpointer) |
| "state_changed" | GtkWidget | void cb(GtkWidget *, GtkStateType, gpointer) |
| "stop_query" | GtkTipsQuery | void cb(GtkWidget *, gpointer) |
| "style_changed" | GtkToolbar | void cb(GtkWidget *, guint, gpointer) |
| "style_set" | GtkWidget | void cb(GtkWidget *, GtkStyle *, gpointer) |
| "switch_page" | GtkNotebook | void cb(GtkWidget *, guint, guint, gpointer) |
| "text_changed" | GnomeIconListItem | gboolean cb(GtkWidget *, gpointer) |
| "text_popped" | GtkStatusbar | void cb(GtkWidget *, guint, gchar *, gpointer) |
| "text_pushed" | GtkStatusbar | void cb(GtkWidget *, guint, gchar *, gpointer) |
| "toggle" | GtkItem | void cb(GtkWidget *, gpointer) |
| "toggle_add_mode" | GtkCList | void cb(GtkWidget *, gpointer) |
| "toggle_add_mode" | GtkListItem | void cb(GtkWidget *, gpointer) |
| "toggle_focus_row" | GtkCList | void cb(GtkWidget *, gpointer) |
| "toggle_focus_row" | GtkListItem | void cb(GtkWidget *, gpointer) |
| "toggled" | GtkCheckMenuItem | void cb(GtkWidget *, gpointer) |
| "toggled" | GtkToggleButton | void cb(GtkWidget *, gpointer) |
| "tree_collapse" | GtkCTree | void cb(GtkWidget *, GtkCTreeNode *, gpointer) |
| "tree_expand" | GtkCTree | void cb(GtkWidget *, GtkCTreeNode *, gpointer) |
| "tree_move" | GtkCTree | void cb(GtkWidget *, GtkCTreeNode *, GtkCTreeNode *, gpointer) |
| "tree_select_row" | GtkCTree | void cb(GtkWidget *, GtkCTreeNode *, gint, gpointer) |
| "tree_unselect_row" | GtkCTree | void cb(GtkWidget *, GtkCTreeNode *, gint, gpointer) |
| "undo_selection" | GtkCList | void cb(GtkWidget *, gpointer) |
| "undo_selection" | GtkCListItem | void cb(GtkWidget *, gpointer) |
| "unmap" | GtkWidget | void cb(GtkWidget *, gpointer) |
| "unmap_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "unrealize" | GtkWidget | void cb(GtkWidget *, gpointer) |
| "unselect_all" | GtkCList | void cb(GtkWidget *, gpointer) |
| "unselect_all" | GtkCListItem | void cb(GtkWidget *, gpointer) |
| "unselect_child" | GtkList | void cb(GtkWidget *, GtkWidget *, gpointer) |
| "unselect_child" | GtkTree | void cb(GtkWidget *, GtkWidget *, gpointer) |
| "unselect_icon" | GnomeIconList | void cb(GtkWidget *, gint, GdkEvent *, gpointer) |
| "unselect_row" | GtkCList | void cb(GtkWidget *, gint, gint, GdkEvent *, gpointer) |
| "value_changed" | GtkAdjustment | void cb(GtkWidget *, gpointer) |
| "visibility_notify_event" | GtkWidget | gboolean cb(GtkWidget *, GdkEvent *, gpointer) |
| "widget_entered" | GtkTipsQuery | void cb(GtkWidget *, GtkWidget *, gchar *, gchar *, gpointer) |
| "widget_selected" | GtkTipsQuery | gboolean cb(GtkWidget *, GtkWidget *, gchar *, gchar *, GdkEvent *, gpointer) |
| "width_changed" | GnomeIconTextItem | void cb(GtkWidget *, gpointer) |

♦ ♦ ♦
