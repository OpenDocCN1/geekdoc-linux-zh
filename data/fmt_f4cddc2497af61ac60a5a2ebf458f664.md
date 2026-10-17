
# 附录 C

## `GNOME_APP_MENUBAR_NAME`

```c
#define GNOME_APP_MENUBAR_NAME "MenuBar";
```

将菜单栏上的标题更改为 `"MenuBar"`。

## `GNOME_APP_TOOLBAR_NAME`

```c
#define GNOME_APP_TOOLBAR_NAME "ToolBar";
```

将工具栏的名称更改为 `"Toolbar"`。

## `gnome_app_set_menus`

```c
void gnome_app_set_menus ( GnomeApp * app, GtkMenuBar * menubar );
```

设置应用窗口的菜单栏。

## `gnome_app_set_toolbar`

```c
void gnome_app_set_toolbar ( GnomeApp * app, GtkToolbar * toolbar );
```

设置应用窗口的主工具栏。

## `gnome_app_set_statusbar`

```c
void gnome_app_set_statusbar ( GnomeApp * app, GtkWidget * statusbar );
```

设置应用窗口的状态栏。

## `gnome_app_set_contents`

```c
void gnome_app_set_contents ( GnomeApp * app, GtkWidget * contents );
```

设置 GNOME 应用程序主窗口的内容区域。

## `gnome_app_add_toolbar`

```c
void gnome_app_add_toolbar ( GnomeApp * app, GtkToolbar * toolbar, const gchar * name, GnomeDockItemBehavior behavior, GnomeDockPlacement placement, gint bind_num, gint bind_position, gint offset );
```

创建一个包含工具栏的新 `GnomeDockItem` 小部件，并根据指定的布局信息将其添加到应用的 dock 容器（这是一个灵活的小部件容器）中。注意，如果启用了自动布局，布局将被保存的配置覆盖。

## `gnome_app_add_docked`

```c
void gnome_app_add_docked ( GnomeApp * app, GtkWidget * widget, const gchar * name, GnomeDockItemBehavior behavior, GnomeDockPlacement placement, gint band_num, gint band_position, gint offset );
```

根据指定的布局信息将小部件作为 dock 项添加。注意，如果启用了自动布局配置，布局将被保存的配置覆盖。

## `gnome_app_add_dock_item`

```c
void gnome_app_add_dock_item ( GnomeApp * app, GnomeDockItem * item, GnomeDockPlacement placement, gint band_num, gint band_position, gint offset );
```

根据指定的布局信息添加项。注意，如果启用了自动布局配置，布局将被保存的配置覆盖。

## `gnome_app_enable_layout_config`

```c
void gnome_app_enable_layout_config ( GnomeApp * app, gboolean enable );
```

指定应用每当 dock 布局配置更改时，是否通过 `gnome-config` 自动保存。

## `gnome_app_get_dock`

```c
GnomeDock * gnome_app_get_dock ( GnomeApp * app );
```

检索 `GnomeApp` 中包含的 `GnomeDock` 小部件。

## `gnome_app_get_dock_item_by_name`

```c
GnomeDockItem * gnome_app_get_dock_item_by_name ( GnomeApp * app, const gchar * name );
```

检索匹配名称的 dock 项。

## `GnomeAppBar`

一个 GNOME 应用程序放在窗口底部的栏，用于显示状态、进度、菜单项提示或用于某种响应的最小缓冲区。这在第 11 章中首次描述。

## `gnome_app_appbar_new`

```c
GtkWidget * gnome_appbar_new ( gboolean has_progress, gboolean has_status, GnomePreferencesType interactivity );
```

创建一个新的 GNOME 应用程序状态栏。

```c
void gnome_appbar_set_default ( GnomeAppBar * appbar, const gchar * default_status );
```

这设置了没有其他内容时显示的内容。默认为空。换句话说，这规定了当没有向小部件传递应该显示什么的信息时，`AppBar` 上显示的是什么。

## `gnome_appbar_push`

```c
void gnome_appbar_push ( GnomeAppBar * appbar, const gchar * status );
```

将一个新的状态消息推入状态栏栈中并显示它。

## `gnome_appbar_pop`

```c
void gnome_appbar_pop ( GnomeAppBar * appbar );
```

移除当前的状态消息，并显示之前的状态消息（如果有）。在空栈上调用此函数是安全的。

## `gnome_appbar_clear_stack`

```c
void gnome_appbar_clear_stack ( GnomeAppBar * appbar );
```

从 `appbar` 中移除所有状态消息并显示默认状态消息（如果有）。

## `gnome_appbar_get_progress`

```c
GtkProgress gnome_appbar_get_progress ( GnomeAppBar * appbar );
```

返回一个 `GtkProgress` 小部件指针，以便对进度条进行进一步操作。

## `gnome_appbar_refresh`

```c
void gnome_appbar_refresh ( GnomeAppBar * appbar );
```

将栈当前的状态刷新为默认值。如果你需要强制让 `set_status` 消失，这很有用。

## `gnome_appbar_set_prompt`

```c
void gnome_appbar_set_prompt ( GnomeAppBar * appbar, const gchar * prompt, gboolean modal );
```

在 `appbar` 中放入一个提示并等待响应。当用户响应时。

## `gnome_appbar_clear_prompt`

```c
void gnome_appbar_clear_prompt ( GnomeAppBar * appbar );
```

从 `appbar` 中移除提示。

## `gnome_appbar_get_status`

```c
gchar * gnome_appbar_get_status ( GnomeAppBar * appbar );
```

获取当前的状态消息。

## `gnome_appbar_set_status`

设置当前的状态消息。
