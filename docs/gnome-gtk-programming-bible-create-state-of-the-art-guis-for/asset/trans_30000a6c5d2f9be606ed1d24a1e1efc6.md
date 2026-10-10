

void gtk_notebook_set_show_tabs(GtkNotebook *notebook, gboolean show_tabs)
void gtk_notebook_set_tab_border(GtkNotebook *notebook, guint tab_border)
void gtk_notebook_set_tab_hborder(GtkNotebook *notebook, guint tab_hborder)
void gtk_notebook_set_tab_label(GtkNotebook *notebook, GtkWidget *child, GtkWidget *tab_label)
void gtk_notebook_set_tab_label_packing(GtkNotebook *notebook, GtkWidget *child, gboolean expand, gboolean fill, GtkPackType pack_type)
void gtk_notebook_set_tab_label_text(GtkNotebook *notebook, GtkWidget *child, const gchar *tab_text)
void gtk_notebook_set_tab_pos(GtkNotebook *notebook, GtkPositionType pos)
void gtk_notebook_set_tab_vborder(GtkNotebook *notebook, guint tab_vborder)

## 枚举

```c
typedef enum {
GTK_POS_LEFT,
GTK_POS_RIGHT,
GTK_POS_TOP,
GTK_POS_BOTTOM
} GtkPositionType;

typedef enum {
GTK_PACK_START,
GTK_PACK_END
} GtkPackType;
```

## 信号

```c
"switch_page"     void cb(GtkWidget *, gpointer, guint, gpointer)
```

有关 GtkNotebook 的示例，请参考第 5 章。

# GtkObject

这是 GTK+ 中所有对象的基类。

## 继承

GtkObject

## 函数

```c
gchar *Gtk_object_args_collect(GtkType object_type, GList **arg_list_p, GList **info_list_p, const gchar *first_arg_name, va_list var_args)
void gtk_object_add_arg_type(const char *arg_name,
    GTokenType arg_type, guint arg_flags, guint arg_id)
void gtk_object_arg_get(GtkObject *object, GtkArg *arg,
    GtkArgInfo *info)
gchar *gtk_object_arg_get_info(GtkType object_type,
    const gchar *arg_name, GtkArgInfo **info_p)
void gtk_object_arg_set(GtkObject *object, GtkArg *arg,
    GtkArgInfo *info)
void gtk_object_class_add_signals(GtkObjectClass *class,
    guint *signals, guint nsignals)
guint gtk_object_class_user_signal_new(GtkObjectClass *class,
    const gchar *name, GSignalFlags signal_flags,
    GSignalMarshal marshaller, GType return_val,
    guint params, ...)
guint gtk_object_class_user_signal_new2(GtkObjectClass *class,
    GSignalMarshal marshaller, GSignalFlags signal_flags,
    GType return_val, guint nparams)
void gtk_object_constructed(GtkObject *object)
void gtk_object_default_construct(GtkObject *object)
void gtk_object_destroy(GtkObject *object)
gpointer gtk_object_get_data(GtkObject *object,
    const gchar *key)
gpointer gtk_object_get_data_by_id(GtkObject *object,
    GQuark data_id)
GType gtk_object_get_data_type(GtkObject *object, const gchar *key)
gpointer gtk_object_get_user_data(GtkObject *object)
void gtk_object_getv(GtkObject *object, guint n_args,
    GtkArg *args)
void gtk_object_init(void)
GtkObject *gtk_object_new(GtkType object_type,
    const gchar *first_arg_name, ...)
GtkObject *gtk_object_new2(GtkType object_type, guint n_args,
    GtkArg *args)
void gtk_object_post_arg_parsing_init(void)
GtkArg *gtk_object_query_args(GtkType class_type,
    guint32 **arg_flags, guint *n_args)
void gtk_object_ref(GtkObject *object)
void gtk_object_remove_data(GtkObject *object,
    const gchar *key)
void gtk_object_remove_data_by_id(GtkObject *object,
    GQuark data_id)
void gtk_object_remove_no_notify(GtkObject *object,
    const gchar *key)
void gtk_object_remove_no_notify_by_id(GtkObject *object,
    GQuark key_id)
void gtk_object_set(GtkObject *object,
    const gchar *first_arg_name, ...)
void gtk_object_set_data(GtkObject *object, const gchar *key,
    gpointer data)
void gtk_object_set_data_by_id(GtkObject *object,
    GQuark data_id, gpointer data)
void gtk_object_set_data_by_id_full(GtkObject *object,
    GQuark data_id, gpointer data, GtkDestroyNotify destroy)
void gtk_object_set_data_full(GtkObject *object,
    const gchar *key, gpointer data, GtkDestroyNotify destroy)
void gtk_object_set_user_data(GtkObject *object, gpointer data)
void gtk_object_setv(GtkObject *object, guint n_args,
    GArgv *args)
void gtk_object_sink(GtkObject *object)
void gtk_object_unref(GtkObject *object)
void gtk_object_weakref(GtkObject *object,
    GtkDestroyNotify notify, gpointer data)
void gtk_object_weakunref(GtkObject *object,
    GtkDestroyNotify notify, gpointer data)
void gtk_trace_referencing(GtkObject *object,
    const gchar *func, guint dummy, guint line,
    gboolean do_ref)
```

## 枚举

```c
typedef enum {
  GTK_RUN_FIRST,
  GTK_RUN_LAST,
  GTK_RUN_BOTH,
  GTK_RUN_NO_RECURSE,
  GTK_RUN_ACTION,
  GTK_RUN_NO_HOOKS
} GtkSignalRunType;
```

## 信号

```c
"switch_page"    void cb(GtkWidget *, gpointer, guint,
       gpointer)
```

# GtkOptionMenu

该容器能够控制一级菜单，可用于多选选择。该小部件通常处于折叠状态，仅显示当前选择项。

## 继承

```
GtkOptionMenu->GtkButton->GtkBin->GtkContainer->GtkWidget->
GtkObject
```

## 函数

```c
GtkWidget *gtk_option_menu_get_menu(
      GtkOptionMenu *option_menu)
GtkType gtk_option_menu_get_type(void)
GtkWidget *gtk_option_menu_new(void)
void gtk_option_menu_remove_menu(GtkOptionMenu *option_menu)
void gtk_option_menu_set_history(GtkOptionMenu *option_menu,
guint index)
void gtk_option_menu_set_menu(GtkOptionMenu *option_menu,
GtkWidget *menu)
```

此示例创建一个包含三个按钮的菜单，并将其安装到 GtkOptionMenu 小部件中以便显示和控制。图 21-35 展示了该小部件在折叠和展开状态下的外观。

```c
static GtkWidget *makeWidget()
{
  GtkWidget *optionmenu;
  GtkWidget *menu;
  GtkWidget *item;

  menu = gtk_menu_new();
  item = gtk_menu_item_new_with_label("Open");
  gtk_menu_append(GTK_MENU(menu), item);
  item = gtk_menu_item_new_with_label("Close");
  gtk_menu_append(GTK_MENU(menu), item);
  item = gtk_menu_item_new_with_label("Save");
  gtk_menu_append(GTK_MENU(menu), item);

  optionmenu = gtk_option_menu_new();
  gtk_option_menu_set_menu(GTK_OPTION_MENU(optionmenu), menu);

  return(optionmenu);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_625_0.png)

**图 21-35：** GtkOptionMenu 小部件的两种状态

# GtkPacker

GtkPacker 是一个容器小部件，提供函数以允许程序对定位和间隔小部件的规则进行详细控制。间隔和大小组均为相对值，因此布局会自动调整以适应容器的高度和宽度。

**继承**

GtkPacker->GtkContainer->GtkWidget->GtkObject

## 函数

```c
void gtk_packer_add(GtkPacker *packer, GtkWidget *child,
                    GtkSideType side, GtkAnchorType anchor,
                    GtkPackerOptions options, guint border_width, guint pad_x,
                    guint pad_y, guint i_pad_x, guint i_pad_y)
void gtk_packer_add_defaults(GtkPacker *packer, GtkWidget *child, GtkSideType side, GtkAnchorType anchor,
                            GtkPackerOptions options)
GtkType gtk_packer_get_type(void)
GtkWidget *gtk_packer_new(void)
void gtk_packer_reorder_child(GtkPacker *packer, GtkWidget *child, gint position)
void gtk_packer_set_child_packing(GtkPacker *packer, GtkWidget *child, GtkSideType side, GtkAnchorType anchor,
                    GtkPackerOptions options, guint border_width, guint pad_x,
                    guint pad_y, guint i_pad_x, guint i_pad_y)
void gtk_packer_set_default_border_width(GtkPacker *packer, guint border)
void gtk_packer_set_default_ipad(GtkPacker *packer, guint i_pad_x, guint i_pad_y)
void gtk_packer_set_default_pad(GtkPacker *packer, guint pad_x, guint pad_y)
void gtk_packer_set_spacing(GtkPacker *packer, guint spacing)
```

## 枚举

```c
typedef enum {
    GTK_PACK_EXPAND,
    GTK_FILL_X,
    GTK_FILL_Y
} GtkPackerOptions;

typedef enum {
    GTK_SIDE_TOP,
    GTK_SIDE_BOTTOM,
    GTK_SIDE_LEFT,
    GTK_SIDE_RIGHT
} GtkSideType;

typedef enum {
    GTK_ANCHOR_CENTER,
    GTK_ANCHOR_NORTH,
    GTK_ANCHOR_NORTH_WEST,
    GTK_ANCHOR_NORTH_EAST,
    GTK_ANCHOR_SOUTH,
    GTK_ANCHOR_SOUTH_WEST,
    GTK_ANCHOR_SOUTH_EAST,
    GTK_ANCHOR_WEST,
    GTK_ANCHOR_EAST,
    GTK_ANCHOR_N,
    GTK_ANCHOR_NW,
```

