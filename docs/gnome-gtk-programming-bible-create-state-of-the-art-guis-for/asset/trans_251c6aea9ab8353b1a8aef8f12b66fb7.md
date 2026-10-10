

## 附录 F

| **类型名称** | **值名称** |
| --- | --- |
| GtkSideType | `GTK_SIDE_TOP`, `GTK_SIDE_BOTTOM`, `GTK_SIDE_LEFT`, `GTK_SIDE_RIGHT` |
| GtkSignalRunType | `GTK_RUN_FIRST`, `GTK_RUN_LAST`, `GTK_RUN_BOTH`, `GTK_RUN_NO_RECURSE`, `GTK_RUN_ACTION`, `GTK_RUN_NO_HOOKS` |
| GtkSortType | `GTK_SORT_ASCENDING`, `GTK_SORT_DESCENDING` |
| GtkSpinButtonUpdatePolicy | `GTK_UPDATE_ALWAYS`, `GTK_UPDATE_IF_VALID` |
| GtkSpinType | `GTK_SPIN_STEP_FORWARD`, `GTK_SPIN_STEP_BACKWARD`, `GTK_SPIN_PAGE_FORWARD`, `GTK_SPIN_PAGE_BACKWARD`, `GTK_SPIN_HOME`, `GTK_SPIN_END`, `GTK_SPIN_USER_DEFINED` |
| GtkStateType | `GTK_STATE_NORMAL`, `GTK_STATE_ACTIVE`, `GTK_STATE_PRELIGHT`, `GTK_STATE_SELECTED`, `GTK_STATE_INSENSITIVE` |
| GtkSubmenuDirection | `GTK_DIRECTION_LEFT`, `GTK_DIRECTION_RIGHT` |
| GtkSubmenuPlacement | `GTK_TOP_BOTTOM`, `GTK_LEFT_RIGHT` |
| GtkTargetFlags | `GTK_TARGET_SAME_APP`, `GTK_TARGET_SAME_WIDGET` |
| GtkToolbarChildType | `GTK_TOOLBAR_CHILD_SPACE`, `GTK_TOOLBAR_CHILD_BUTTON`, `GTK_TOOLBAR_CHILD_TOGGLEBUTTON`, `GTK_TOOLBAR_CHILD_RADIOBUTTON`, `GTK_TOOLBAR_CHILD_WIDGET` |
| GtkToolbarSpaceStyle | `GTK_TOOLBAR_SPACE_EMPTY`, `GTK_TOOLBAR_SPACE_LINE` |
| GtkToolbarStyle | `GTK_TOOLBAR_ICONS`, `GTK_TOOLBAR_TEXT`, `GTK_TOOLBAR_BOTH` |
| GtkTreeViewMode | `GTK_TREE_VIEW_LINE`, `GTK_TREE_VIEW_ITEM` |
| GtkTroughType | `GTK_TROUGH_NONE`, `GTK_TROUGH_START`, `GTK_TROUGH_END`, `GTK_TROUGH_JUMP` |
| GtkUpdateType | `GTK_UPDATE_CONTINUOUS`, `GTK_UPDATE_DISCONTINUOUS`, `GTK_UPDATE_DELAYED` |
| GtkVisibility | `GTK_VISIBILITY_NONE`, `GTK_VISIBILITY_PARTIAL`, `GTK_VISIBILITY_FULL` |
| GtkWidgetFlags | `GTK_TOPLEVEL`, `GTK_NO_WINDOW`, `GTK_REALIZED`, `GTK_MAPPED`, `GTK_VISIBLE`, `GTK_SENSITIVE`, `GTK_PARENT_SENSITIVE`, `GTK_CAN_FOCUS`, `GTK_HAS_FOCUS`, `GTK_CAN_DEFAULT`, `GTK_HAS_DEFAULT`, `GTK_HAS_GRAB`, `GTK_RC_STYLE`, `GTK_COMPOSITE_CHILD`, `GTK_NO_REPARSE`, `GTK_APP_PAINTABLE`, `GTK_RECEIVES_DEFAULT` |
| GtkWindowPosition | `GTK_WIN_POS_NONE`, `GTK_WIN_POS_CENTER`, `GTK_WIN_POS_MOUSE` |
| GtkWindowType | `GTK_WINDOW_TOPLEVEL`, `GTK_WINDOW_DIALOG`, `GTK_WINDOW_POPUP` |

***

## 信号

由硬件设备接收的每个事件，作为用户某种操作的结果，能够通过调用回调函数向应用程序发出信号。表 F-1 列出了具有信号的类、信号的名称以及其对应回调函数的原型。

所有回调函数至少有两个参数，但可能有更多。第一个参数始终是指向发出信号的部件的指针。最后一个参数始终是应用程序传递给函数以注册回调到部件的指针。一些回调函数有其他参数；这些参数包含在部件指针和数据指针之间。

### 表 F-1

| **信号名称** | **类名称** | **回调原型** |
| --- | --- | --- |
| "abort_column_resize" | GtkCList | `void cb(GtkWidget *, gpointer)` |
| "activate" | GtkEditable | `void cb(GtkWidget *, gpointer)` |
| "activate" | GtkMenuItem | `void cb(GtkWidget *, gpointer)` |
| "activate_current" | GtkMenuShell | `void cb(GtkWidget *, gboolean, gpointer)` |
| "add" | GtkContainer | `void cb(GtkWidget *, GtkWidget *, gpointer)` |
| "button_press_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "button_release_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "cancel" | GtkMenuShell | `void cb(GtkWidget *, gpointer)` |
| "change_focus_row_expansion" | GtkCTree | `void cb(GtkWidget *, GtkCTreeExpansion, gpointer)` |
| "changed" | GtkAdjustment | `void cb(GtkWidget *, gpointer)` |
| "changed" | GtkEditable | `void cb(GtkWidget *, gpointer)` |
| "check_resize" | GtkContainer | `void cb(GtkWidget *, gpointer)` |
| "child_detached" | GtkHandleBox | `void cb(GtkWidget *, GtkWidget *, gpointer)` |
| "click_column" | GtkCList | `void cb(GtkWidget *, gint, gpointer)` |
| "clicked" | GtkButton | `void cb(GtkWidget *, gpointer)` |
| "client_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "collapse" | GtkTreeItem | `void cb(GtkWidget *, gpointer)` |
| "color_changed" | GtkColorSelection | `void cb(GtkWidget *, gpointer)` |
| "configure_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "copy_clipboard" | GtkEditable | `void cb(GtkWidget *, gpointer)` |
| "curve_type_changed" | GtkCurve | `void cb(GtkWidget *, gpointer)` |
| "cut_clipboard" | GtkEditable | `void cb(GtkWidget *, gpointer)` |
| "deactivate" | GtkMenuShell | `void cb(GtkWidget *, gpointer)` |
| "debug_msg" | GtkWidget | `void cb(GtkWidget *, gchar *, gpointer)` |
| "delete_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "delete_text" | GtkEditable | `void cb(GtkWidget *, gint, gint, gpointer)` |
| "deselect" | GtkItem | `void cb(GtkWidget *, gpointer)` |
| "destroy" | GtkObject | `void cb(GtkWidget *, gpointer)` |
| "destroy_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "disable_device" | GtkInputDialog | `void cb(GtkWidget *, gint, gpointer)` |
| "disconnect" | GtkData | `void cb(GtkWidget *, gpointer)` |
| "dock_detach" | GnomeDockItem | `void cb(GtkWidget *, gpointer)` |
| "dock_drag_begin" | GnomeDockItem | `void cb(GtkWidget *, gpointer)` |
| "dock_drag_end" | GnomeDockItem | `void cb(GtkWidget *, gpointer)` |
| "dock_drag_motion" | GnomeDockItem | `void cb(GtkWidget *, gint, gint, gpointer)` |
| "drag_begin" | GtkWidget | `void cb(GtkWidget *, GdkDragContext *, gpointer)` |
| "drag_data_delete" | GtkWidget | `void cb(GtkWidget *, GdkDragContext *, gpointer)` |
| "drag_data_get" | GtkWidget | `void cb(GtkWidget *, GdkDragContext *, GtkSelectionData *, guint, guint, gpointer)` |
| "drag_data_received" | GtkWidget | `void cb(GtkWidget *, GdkDragContext *, gint, gint, GtkSelectionData *, guint, guint, gpointer)` |
| "drag_drop" | GtkWidget | `gboolean cb(GtkWidget *, GdkDragContext *, gint, gint, guint, gpointer)` |
| "drag_end" | GtkWidget | `void cb(GtkWidget *, GdkDragContext *, gpointer)` |
| "drag_leave" | GtkWidget | `void cb(GtkWidget *, GdkDragContext *, gpointer)` |
| "drag_motion" | GtkWidget | `gboolean cb(GtkWidget *, GdkDragContext *, gint, gint, guint, gpointer)` |
| "draw" | GtkWidget | `void cb(GtkWidget *, gpointer, gpointer)` |
| "draw_default" | GtkWidget | `void cb(GtkWidget *, gpointer)` |
| "draw_focus" | GtkWidget | `void cb(GtkWidget *, gpointer)` |
| "editing_started" | GnomeIconTextItem | `void cb(GtkWidget *, gpointer)` |
| "editing_stopped" | GnomeIconTextItem | `void cb(GtkWidget *, gpointer)` |
| "enable_device" | GtkInputDialog | `void cb(GtkWidget *, gint, gpointer)` |
| "end_selection" | GtkCList | `void cb(GtkWidget *, gpointer)` |
| "end_selection" | GtkListItem | `void cb(GtkWidget *, gpointer)` |
| "enter" | GtkButton | `void cb(GtkWidget *, gpointer)` |
| "enter_notify_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "expand" | GtkTreeItem | `void cb(GtkWidget *, gpointer)` |
| "expose_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "extend_selection" | GtkCList | `void cb(GtkWidget *, GtkScrollType, gfloat, gboolean, gpointer)` |
| "extend_selection" | GtkListItem | `void cb(GtkWidget *, gint, gfloat, gboolean, gpointer)` |
| "focus" | GtkContainer | `gint cb(GtkWidget *, GtkDirectionType, GtkDirectionType, gpointer)` |
| "focus_in_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "focus_out_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |
| "grab_focus" | GtkWidget | `void cb(GtkWidget *, gpointer)` |
| "height_changed" | GnomeIconTextItem | `void cb(GtkWidget *, gpointer)` |
| "hide" | GtkWidget | `void cb(GtkWidget *, gpointer)` |
| "input" | GtkSpinButton | `void cb(GtkWidget *, gpointer, gpointer)` |
| "insert_text" | GtkEditable | `void cb(GtkEditable *, gchar *, gint, gpointer, gpointer)` |
| "key_press_event" | GtkWidget | `gboolean cb(GtkWidget *, GdkEvent *, gpointer)` |

