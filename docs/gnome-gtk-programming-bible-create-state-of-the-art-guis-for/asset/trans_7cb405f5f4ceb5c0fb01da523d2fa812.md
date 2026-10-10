

- `*extend_selection"` 处理函数 cb(GtkWidget *, gint, gfloat, gboolean, gpointer)
- `*scroll_horizontal"` 处理函数 cb(GtkWidget *, gint, gfloat, gpointer)
- `*scroll_vertical"` 处理函数 cb(GtkWidget *, gint, gfloat, gpointer)
- `*select_all"` 处理函数 cb(GtkWidget *, gpointer)
- `*start_selection"` 处理函数 cb(GtkWidget *, gpointer)
- `*toggle_add_mode"` 处理函数 cb(GtkWidget *, gpointer)
- `*toggle_focus_row"` 处理函数 cb(GtkWidget *, gpointer)
- `*undo_selection"` 处理函数 cb(GtkWidget *, gpointer)
- `*unselect_all"` 处理函数 cb(GtkWidget *, gpointer)

例如，请参阅本章前面关于 GtkList 的说明。

## GtkMenu

这是一个被设计用作下拉菜单的容器。

### 继承

GtkMenu -> GtkMenuShell -> GtkContainer -> GtkWidget -> GtkObject

### 函数

```c
void gtk_menu_append(GtkMenu *menu, GtkWidget *child)
void gtk_menu_attach_to_widget(GtkMenu *menu,
    GtkWidget *attach_widget, GtkMenuDetachFunc detacher)
void gtk_menu_detach(GtkMenu *menu)
GtkAccelGroup *gtk_menu_ensure_unique_accel_group(
    GtkMenu *menu)
GtkAccelGroup *gtk_menu_get_accel_group(GtkMenu *menu)
GtkWidget *gtk_menu_get_active(GtkMenu *menu)
GtkWidget *gtk_menu_get_attach_widget(GtkMenu *menu)
GtkType gtk_menu_get_type(void)
GtkAccelGroup *gtk_menu_get_unique_accel_group(GtkMenu *menu)
void gtk_menu_insert(GtkMenu *menu, GtkWidget *child,
    gint position)
GtkWidget *gtk_menu_new(void)
void gtk_menu_popup(GtkMenu *menu,
    GtkWidget *parent_menu_shell, GtkWidget *parent_menu_item,
    GtkMenuPositionFunc func, gpointer data, guint button,
    guint32 activate_time)
void gtk_menu_prepend(GtkMenu *menu, GtkWidget *child)
void gtk_menu_reorder_child(GtkMenu *menu, GtkWidget *child,
    gint position)
void gtk_menu_reposition(GtkMenu *menu)
void gtk_menu_set_accel_group(GtkMenu *menu,
    GtkAccelGroup *accel_group)
void gtk_menu_set_active(GtkMenu *menu, guint index)
void gtk_menu_set_tearoff_state(GtkMenu *menu,
    gboolean torn_off)
void gtk_menu_set_title(GtkMenu *menu, const gchar *title)
```

以下示例创建了一个菜单栏，其中包含单个菜单，该菜单又包含一个子菜单（如图 21-34 所示）。创建菜单的过程就是创建各个独立部分并将它们连接在一起。

调用 `gtk_menu_new()` 会生成一个能够保存菜单项列表的 GtkMenu。要添加到菜单中的每个菜单项都是通过对 `gtk_menu_item_new_with_label()` 的调用来创建的。一旦创建了菜单，子菜单就会通过调用 `gtk_menu_append()` 附加到父菜单上。每个菜单都会通过调用 `gtk_menu_bar_append()` 附加到主菜单栏上。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *fileMenu;
    GtkWidget *fileNewMenu;
    GtkWidget *fileItem;
    GtkWidget *fileNewItem;
    GtkWidget *menuBar;

    /* Create the 'new' menu */
    fileNewMenu = gtk_menu_new();
    fileNewItem = gtk_menu_item_new_with_label("Template");
    gtk_menu_append(GTK_MENU(fileNewMenu), fileNewItem);
    fileNewItem = gtk_menu_item_new_with_label("Empty");
    gtk_menu_append(GTK_MENU(fileNewMenu), fileNewItem);

    /* Create the 'file' menu */
    fileMenu = gtk_menu_new();
    fileItem = gtk_menu_item_new_with_label("Open");
    gtk_menu_append(GTK_MENU(fileMenu), fileItem);
    fileItem = gtk_menu_item_new_with_label("Close");
    gtk_menu_append(GTK_MENU(fileMenu), fileItem);
    fileItem = gtk_menu_item_new_with_label("Save");
    gtk_menu_append(GTK_MENU(fileMenu), fileItem);

    /* Attach 'new' menu to 'file' menu */
    fileItem = gtk_menu_item_new_with_label("New");
    gtk_menu_append(GTK_MENU(fileMenu), fileItem);
    gtk_menu_item_set_submenu(GTK_MENU_ITEM(fileItem),
        fileNewMenu);

    /* Add the label on top of the 'file' menu */
    fileItem = gtk_menu_item_new_with_label("File");
    gtk_menu_item_set_submenu(GTK_MENU_ITEM(fileItem),
        fileMenu);

    /* Append the 'file' menu to the menu bar */
    menuBar = gtk_menu_bar_new();
    gtk_menu_bar_append(GTK_MENU_BAR(menuBar), fileItem);
    return (menuBar);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_618_0.png)

## GtkMenuBar

GtkMenuBar 是一个被设计用于管理一组下拉菜单的容器控件。它会显示其包含的每个菜单的标签。

### 继承

GtkMenuBar -> GtkMenuShell -> GtkContainer -> GtkWidget -> GtkObject

### 函数

```c
void gtk_menu_bar_append(GtkMenuBar *menu_bar,
    GtkWidget *child)
GType gtk_menu_bar_get_type(void)
void gtk_menu_bar_insert(GtkMenuBar *menu_bar,
    GtkWidget *child, gint position)
GtkWidget *gtk_menu_bar_new(void)
void gtk_menu_bar_prepend(GtkMenuBar *menu_bar,
    GtkWidget *child)
void gtk_menu_bar_set_shadow_type(GtkMenuBar *menu_bar,
    GtkShadowType type)
```

### 枚举

```c
typedef enum {
    GTK_SHADOW_NONE,
    GTK_SHADOW_IN,
    GTK_SHADOW_OUT,
    GTK_SHADOW_ETCHED_IN,
    GTK_SHADOW_ETCHED_OUT
} GtkShadowType;
```

请参阅 GtkMenu 的说明以获取 GtkMenuBar 的示例。

## GtkMenuItem

**GtkMenuItem** 是一个可以被插入菜单中的控件。它能够显示文本并充当子菜单的头部。

### 继承

`GtkMenuItem->GtkItem->GtkBin->GtkContainer->GtkWidget->GtkObject`

### 函数

- `void gtk_menu_item_activate(GtkMenuItem *menu_item)`
- `void gtk_menu_item_configure(GtkMenuItem *menu_item, gint show_toggle_indicator, gint show_submenu_indicator)`
- `void gtk_menu_item_deselect(GtkMenuItem *menu_item)`
- `GtkType gtk_menu_item_get_type(void)`
- `GtkWidget *gtk_menu_item_new(void)`
- `GtkWidget *gtk_menu_item_new_with_label(const gchar *label)`
- `void gtk_menu_item_remove_submenu(GtkMenuItem *menu_item)`
- `void gtk_menu_item_right_justify(GtkMenuItem *menu_item)`
- `void gtk_menu_item_select(GtkMenuItem *menu_item)`
- `void gtk_menu_item_set_placement(GtkMenuItem *menu_item, GtkSubmenuPlacement placement)`
- `void gtk_menu_item_set_submenu(GtkMenuItem *menu_item, GtkWidget *submenu)`

### 枚举

`typedef enum { GTK_DIRECTION_LEFT, GTK_DIRECTION_RIGHT } GtkSubmenuDirection;`

### 信号

- `"activate"` 处理函数 cb(GtkWidget *, gpointer)

**GtkMenuItem** 的示例，请参阅 **GtkMenu** 的说明。

## GtkMenuShell

这是 **GtkMenu** 和 **GtkMenuBar** 的基类。

### 继承

`GtkMenuShell->GtkContainer->GtkWidget->GtkObject`

### 函数

```c
void gtk_menu_shell_activate_item(GtkMenuShell *menu_shell, GtkWidget *menu_item, gboolean force_deactivate)
void gtk_menu_shell_append(GtkMenuShell *menu_shell,
    GtkWidget *child)
void gtk_menu_shell_deactivate(GtkMenuShell *menu_shell)
void gtk_menu_shell_deselect(GtkMenuShell *menu_shell)
GtkType gtk_menu_shell_get_type(void)
void gtk_menu_shell_insert(GtkMenuShell *menu_shell,
    GtkWidget *child, gint position)
void gtk_menu_shell_prepend(GtkMenuShell *menu_shell,
    GtkWidget *child)
void gtk_menu_shell_select_item(GtkMenuShell *menu_shell,
    GtkWidget *menu_item)
```

### 信号

- `"activate-current"` 处理函数 cb(GtkWidget *, gboolean, gpointer)
- `"cancel"` 处理函数 cb(GtkWidget *, gpointer)
- `"deactivate"` 处理函数 cb(GtkWidget *, gpointer)
- `"move-current"` 处理函数 cb(GtkWidget *, GtkMenuDirectionType, gpointer)
- `"selection-done"` 处理函数 cb(GtkWidget *, gpointer)

## GtkMisc

这是一个基类，为许多可显示的控件提供对齐方式和间距。

### 继承

```
GtkMisc->GtkWidget->GtkObject
```

### 函数

```c
GtkType gtk_misc_get_type(void)
void gtk_misc_set_alignment(GtkMisc *misc, gfloat xalign,
    gfloat yalign)
void gtk_misc_set_padding(GtkMisc *misc, gint xpad, gint ypad)
```

## GtkNotebook

GtkNotebook 对象是一种容器控件，它一次显示其包含的一个控件。显示区域顶部有一排选项卡，提供对每个独立控件的鼠标访问功能。

### 继承

```
GtkNotebook->GtkContainer->GtkWidget->GtkObject
```

### 函数

```c
void gtk_notebook_append_page(GtkNotebook *notebook, GtkWidget *child, GtkWidget *tab_label)
void gtk_notebook_append_page_menu(GtkNotebook *notebook, GtkWidget *child, GtkWidget *tab_label, GtkWidget *menu_label)
gint gtk_notebook_get_current_page(GtkNotebook *notebook)
GtkWidget *gtk_notebook_get_menu_label(GtkNotebook *notebook, GtkWidget *child)
GtkWidget *gtk_notebook_get_nth_page(GtkNotebook *notebook, gint page_num)
GtkWidget *gtk_notebook_get_tab_label(GtkNotebook *notebook, GtkWidget *child)
GtkType gtk_notebook_get_type(void)
void gtk_notebook_insert_page(GtkNotebook *notebook, GtkWidget *child, GtkWidget *tab_label, gint position)
void gtk_notebook_insert_page_menu(GtkNotebook *notebook, GtkWidget *child, GtkWidget *tab_label, GtkWidget *menu_label, gint position)
GtkWidget *gtk_notebook_new(void)
void gtk_notebook_next_page(GtkNotebook *notebook)
gint gtk_notebook_page_num(GtkNotebook *notebook, GtkWidget *child)
void gtk_notebook_popup_disable(GtkNotebook *notebook)
void gtk_notebook_popup_enable(GtkNotebook *notebook)
void gtk_notebook_prepend_page(GtkNotebook *notebook, GtkWidget *child, GtkWidget *tab_label)
void gtk_notebook_prepend_page_menu(GtkNotebook *notebook, GtkWidget *child, GtkWidget *tab_label, GtkWidget *menu_label)
void gtk_notebook_prev_page(GtkNotebook *notebook)
void gtk_notebook_query_tab_label_packing(GtkNotebook *notebook, GtkWidget *child, gboolean *expand, gboolean *fill, GtkPackType *pack_type)
void gtk_notebook_remove_page(GtkNotebook *notebook, gint page_num)
void gtk_notebook_reorder_child(GtkNotebook *notebook, GtkWidget *child, gint position)
void gtk_notebook_set_homogeneous_tabs(GtkNotebook *notebook, gboolean homogeneous)
void gtk_notebook_set_menu_label(GtkNotebook *notebook, GtkWidget *child, GtkWidget *menu_label)
void gtk_notebook_set_menu_label_text(GtkNotebook *notebook, GtkWidget *child, const gchar *menu_text)
void gtk_notebook_set_page(GtkNotebook *notebook, gint page_num)
void gtk_notebook_set_scrollable(GtkNotebook *notebook, gint scrollable)
void gtk_notebook_set_show_border(GtkNotebook *notebook, gint show_border)
```

