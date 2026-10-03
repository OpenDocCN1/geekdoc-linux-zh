
# 附录 C

## gnome_appbar_set_status

```c
void gnome_appbar_set_status ( GnomeAppBar * appbar, const gchar * status );
```

设置当前的状态消息。

## gnome_canvas_set_pixels_per_unit

```c
void gnome_canvas_set_pixels_per_unit ( GnomeCanvas * canvas, double n );
```

通过指定一个画布单位对应的像素数来设置画布的缩放因子。

## gnome_canvas_scroll_to

```c
void gnome_canvas_scroll_to ( GnomeCanvas * canvas, gint cx, gint cy );
```

使画布滚动到指定的偏移量，偏移量以画布像素单位给出。画布将调整视图，使其不超出滚动区域。此函数通常不使用，因为使用滚动条来调整画布布局的滚动效果更好。

## gnome_canvas_get_scroll_offsets

```c
void gnome_canvas_get_scroll_offsets ( GnomeCanvas * canvas, gint * cx, gint * cy );
```

查询画布的滚动偏移量。值以画布像素单位返回。

## gnome_canvas_update_now

```c
void gnome_canvas_update_now ( GnomeCanvas * canvas );
```

强制画布进行立即更新和重绘。如果画布没有待处理的重绘请求，则不采取任何操作。这通常仅用于需要显式控制显示更新时间的应用程序（例如游戏）。普通应用程序不需要它。

## gnome_canvas_get_item_at

```c
GnomeCanvasItem * gnome_canvas_get_item_at ( GnomeCanvas * canvas, double x, double y );
```

查找指定位置下的项，该位置必须以世界坐标指定。

## gnome_canvas_request_redraw_uta

```c
void gnome_canvas_request_redraw_uta ( GnomeCanvas * canvas, ArtUta * uta );
```

通知画布指定的区域（以微单元 microtile 给出）需要重绘。这仅供项的实现类使用。

## gnome_canvas_request_redraw

```c
void gnome_canvas_request_redraw ( GnomeCanvas * canvas, gint x1, gint y1, gint x2, gint y2 );
```

这是一个便利函数，通知画布指定的矩形需要重绘。该函数将矩形转换为微单元并将其传递给`gnome_canvas_request_redraw_uta`。矩形包含`x1`和`y1`，但不包含`x2`和`y2`。仅供项的实现类使用。

## gnome_canvas_w2c_affine

```c
void gnome_canvas_w2c_affine ( GnomeCanvas *canvas, double affine[6] );
```

获取从世界坐标到画布像素坐标的仿变换。

## gnome_canvas_w2c

```c
void gnome_canvas_w2c ( GnomeCanvas * canvas, double wx, double wy, gint * cx, gint * cy );
```

将世界坐标转换为画布像素坐标。

## gnome_canvas_w2c_d

```c
void gnome_canvas_w2c_d ( GnomeCanvas * canvas, double wx, double wy, double * cx, double * cy );
```

将世界坐标转换为画布像素坐标，使用双精度浮点数代替整数。

## gnome_canvas_c2w

```c
void gnome_canvas_c2w ( GnomeCanvas * canvas, gint cx, gint cy, double * wx, double * wy );
```

将画布像素坐标转换为世界坐标。

## gnome_canvas_window_to_world

```c
void gnome_canvas_window_to_world ( GnomeCanvas * canvas, double winx, double winy, double * worldx, double * worldy );
```

将窗口相对坐标转换为世界坐标。例如，当你需要将鼠标坐标转换为世界坐标时可以使用它。

## gnome_canvas_world_to_window

```c
void gnome_canvas_world_to_window ( GnomeCanvas * canvas, double worldx, double worldy, double * winx, double * winy );
```

将世界坐标转换为窗口相对坐标。

# 附录 C

## gnome_canvas_get_color

```c
gint gnome_canvas_get_color ( GnomeCanvas * canvas, const gchar * spec, GdkColor * color );
```

根据指定的 X 颜色规范分配颜色。为了方便项的实现类，如果分配了颜色则返回 TRUE，如果规范为 NULL 则返回 FALSE。画布认为颜色规范是透明的。

## gnome_canvas_set_stipple_origin

```c
void gnome_canvas_set_stipple_origin ( GnomeCanvas * canvas, GdkGC * gc );
```

根据画布设置指定`gc`的点彩起点（stipple origin），使其与画布项使用的其他点彩图案对齐。这通常仅项项的实现类。

## GnomeCanvasItem

自定义画布项允许你扩展画布；如果内置项（或放置在`GnomeCanvasGroup`中的某些组合）不能满足你的需求，请考虑编写画布项。你可以在第 13 章中阅读相关内容。

## gnome_canvas_item_affine_absolute

```c
void gnome_canvas_item_affine_absolute ( GnomeCanvasItem * item, const double affine[6] );
```

将项的仿变换矩阵设置为指定的矩阵。

## gnome_canvas_item_affine_relative

```c
void gnome_canvas_item_affine_move ( GnomeCanvasItem * item, double dx, double dy );
```

通过创建仿变换移动画布项。

## gnome_canvas_item_affine_move

```c
void gnome_canvas_item_affine_move ( GnomeCanvasItem * item, double dx, double dy );
```

通过创建仿变换移动画布项。

## gnome_canvas_item_construct

```c
void gnome_canvas_item_construct ( GnomeCanvasItem * item, GnomeCanvas * parent );
```

使用父画布构造项。

## gnome_canvas_item_constructv

```c
void gnome_canvas_item_constructv ( GnomeCanvasItem * item, GnomeCanvas * parent, guint nargs, GtkArg * args );
```

使用父画布和参数构造项。

## gnome_canvas_item_affine_absolute

```c
void gnome_canvas_item_affine_absolute ( GnomeCanvasItem * item, const double affine[6] );
```

将项的仿变换矩阵设置为指定的矩阵。

## gnome_canvas_item_get_bounds

```c
void gnome_canvas_item_get_bounds ( GnomeCanvasItem * item, double * x1, double * y1, double * x2, double * y2 );
```

查询项的边界框。

## gnome_canvas_item_request_focus

```c
void gnome_canvas_item_request_focus ( GnomeCanvasItem * item );
```

使该项获取键盘焦点。

## gnome_canvas_item_hide

```c
void gnome_canvas_item_hide ( GnomeCanvasItem * item );
```

隐藏画布项。

## gnome_canvas_item_i2w

```c
void gnome_canvas_item_i2w ( GnomeCanvasItem * item, double * wx, double * wy );
```

将项相对坐标转换为世界坐标。

## gnome_canvas_item_i2c_affine

```c
void gnome_canvas_item_i2c_affine ( GnomeCanvasItem * item, double affine[6] );
```

获取从项相对坐标到画布像素坐标的仿变换。

## gnome_canvas_item_i2c

```c
void gnome_canvas_item_i2c ( GnomeCanvasItem * item, double wx, double wy, gint * cx, gint * cy );
```

将项相对坐标转换为画布像素坐标。

## gnome_canvas_item_i2w_d

```c
void gnome_canvas_item_i2w_d ( GnomeCanvasItem * item, double wx, double wy, double * cx, double * cy );
```

将项相对坐标转换为画布像素坐标，使用双精度浮点数代替整数。

# gnome_canvas_item_raise_to_top

```c
void gnome_canvas_item_raise_to_top ( GnomeCanvasItem * item );
```

将项置于其父级堆栈的顶端。

# gnome_canvas_item_repaint

```c
void gnome_canvas_item_repaint ( GnomeCanvasItem * item, GnomeGroup * new_group );
```

将指定项的父级更改为新组。项保留其相对于旧父级的组内坐标；但该项在画布内的绝对位置可能会发生变化。

# gnome_canvas_item_request_update

```c
void gnome_canvas_item_request_update ( GnomeCanvasItem * item );
```

仅供项的实现使用。请求画布对指定的项进行更新队列。

# gnome_canvas_item_set

```c
void gnome_canvas_item_set ( GnomeCanvasItem * item, const gchar * first_arg_name, ..., NULL );
```

配置画布项。项中的参数将被设置为指定的值，并根据需要重绘该项。

# gnome_canvas_item_set_v

```c
void gnome_canvas_item_set_v ( GnomeCanvasItem * item, guint nargs, GtkArg * args );
```

配置画布项。项中的参数将被设置为指定的值，并根据需要重绘该项。

# gnome_canvas_item_set_valist

```c
void gnome_canvas_item_set_valist ( GnomeCanvasItem * item, const gchar * first_arg_name, va_list args );
```

配置画布项。项中的参数将被设置为指定的值，并根据需要重绘该项。

# gnome_canvas_item_show

```c
void gnome_canvas_item_show ( GnomeCanvasItem * item );
```

显示画布项。如果项已经显示，则不采取任何操作。

# 附录 C

```c
void gnome_canvas_item_ungrab ( GnomeCanvasItem * item, guint32_etime );
```

取消项的捕取（该项必须在画布中已被捕取），并释放鼠标捕取。

# gnome_canvas_item_w2i

```c
void gnome_canvas_item_w2i ( GnomeCanvasItem * item, double * x, double * y );
```

将坐标对从世界坐标转换为项的相对坐标。

# GnomeClient

`GnomeClient`对象实现了会话管理。

# GNOME_CLIENT_CONNECTED

```c
#define GNOME_CLIENT_CONNECTED ( obj );
```

如果客户端 (`obj`) 已连接到会话管理器，则返回 TRUE。

# GnomeInteractFunction

```c
void GnomeInteractFunction ( GnomeClient * client, GnomeDialogType dialog_type, gpointer data );
```

用于执行用户交互的回调函数。

# gnome_client_disable_master_connection

```c
void gnome_client_disable_master_connection ( void );
```

不要让主客户端连接到会话管理器。

# gnome_master_client

```cpp
GnomeClient * gnome_master_client ( void );
```

获取主会话管理客户端。该主客户端将获得一个客户端 ID。主客户端将由`gnome-init`生成。如果可能，主客户端将在命令行解析完成后联系会话管理器。主客户端还会在您的应用程序的客户端窗口上设置`SM_CLIENT_ID`属性。它返回一个指向主客户端的指针。

# gnome_client_disconnect

```c
void gnome_master_client ( GnomeClient * client );
```

将客户端从会话管理器断开。

# GNOME API 参考

# gnome_client_get_config_prefix

```c
gchar * gnome_client_get_config_prefix ( GnomeClient * client );
```

获取客户端的配置前缀。该配置前缀提供了一个合适的地方用于存储客户端状态的任何细节，这些细节无法通过其应用程序命令行参数（如重启命令）来描述。您可以使用`gnome_config_push_prefix`推送返回的值并写入您所需的任何值。

# gnome_client_set_restart_style

```c
void gnome_client_set_restart_style ( GnomeClient * client, GnomeRestartStyle style );
```

`GNOME_RESTART_IF_RUNNING`会导致客户端如果上一个会话退出时正在运行，则在下次会话中重启。重启通过您设置的重启命令完成。`GNOME_RESTART_ANYWAY`意味着用户在注销之前退出客户端时，客户端将重启。`GNOME_RESTART_IMMEDIATELY`则会在客户端崩溃或退出时立即重启客户端。

```c
void gnome_client_set_restart_command ( GnomeClient * client, gint argc, gchar * argv[] );
```

当客户端崩溃或用户注销并重新登录时，它们会被重启。在本地主机上执行重启命令应该尽可能地再现会话发生时该客户端的状态。

# gnome_client_add_static_arg

```c
void gnome_client_add_static_arg ( GnomeClient * client, ..., NULL );
```

您可以使用此函数向重启命令的`argv`中添加参数。此函数提供了一种向重启命令添加新参数的替代方法。

# gnome_client_set_discard_command

```c
void gnome_client_add_static_arg ( GnomeClient * client, gint argc, gchar * argv[] );
```
