
参数 `homogeneous` 和 `spacing` 在之前的 `GtkBox` 节中已描述过。将 `homogeneous` 设置为 `TRUE` 会告诉容器在每个封装的组件之间平分垂直维度。例如，如果三个组件封装到容器中，每个组件将占据可用区域的三之一。如果 `homogeneous` 为 `FALSE`，则容器内的垂直空间将被分配。

参数 `spacing` 定义了容器内组件之间放置像素数，同样在水平维度上。

`GtkBox` 提供的所有函数适用于 `GtkVBox` 实例。当为其中一个 `GtkBox` 函数调用 `GtkBox` 参数时，使用 `Gtk_BOX()` 宏将其转换为 `GtkBox *`。

# GtkHBox

## 类名

`GtkBox`

## 父类名

`GtkBox`

## 宏

组件类型宏：`GTK_TYPE_HBOX`  
对象到组件转换宏：`GTK_HBOX(obj)`  
组件类型检查宏：`GTK_IS_HBOX(obj)`

## 应用级 API 摘要

在运行时获取常量 `GTK_TYPE_HBOX`：

```c
GtkType
gtk_hbox_get_type(void);
```

创建 `GtkHBox` 的新实例：

```c
GtkWidget *
gtk_hbox_new(gboolean homogeneous, gint spacing);
```

# GtkHBox 描述

与 `GtkVBox` 类似，`GtkHBox` 是 `GtkBox` 的子类。`GtkBox` 的实例在使用函数 `gtk_box_pack_start()` 添加到容器时会从左到右封装组件，当使用 `gtk_box_pack_end()` 将组件添加到容器时则从右到左封装。要创建 `GtkHBox` 的实例，只需调用 `gtk_hbox_new()`：

```c
GtkWidget *
gtk_hbox_new(gboolean homogeneous, gint spacing);
```

参数 `homogeneous` 和 `spacing` 在之前的 `GtkBox` 节中已描述过。将 `homogeneous` 设置为 `TRUE` 会告诉容器在每个封装的组件之间平分水平维度。例如，如果三个组件封装到容器中，每个组件将占据可用区域的三之一。如果 `homogeneous` 为 `FALSE`，则容器内的水平空间将被分配。

参数 `spacing` 定义了容器内组件之间放置像素数，同样在垂直维度上。

## 父类名称

`GtkBox`

## 宏

控件类型宏：`GTK_TYPE_BUTTON_BOX`  
对象到组件的转换宏：`GTK_BUTTON_BOX(obj)`  
组件类型检查宏：`GTK_IS_BUTTON_BOX(obj)`

## 应用级 API 摘要

在运行时获取常量 `GTK_TYPE_BUTTON_BOX`

```c
GtkType
gtk_button_box_get_child_type(void);
```

获取子组件的默认最小宽度和最小高度值：

```c
void
gtk_button_box_get_child_size_default(gint *min_width, gint *min_height);
```

获取默认的按钮内边距：

```c
void
gtk_button_box_get_child_padding_default(gint *ipad_x, gint *ipad_y);
```

设置子组件的默认最小宽度和最小高度值：

```c
void
gtk_button_box_set_child_size_default(gint *min_width, gint *min_height);
```

设置默认的按钮内边距：

```c
void
gtk_button_box_set_child_padding_default(gint ipad_x, gint ipad_y);
```

获取子组件间距：

```c
gint
gtk_button_box_get_spacing(GtkButton *widget);
```

获取按钮框样式（参见正文）：

```c
GtkBoxStyle
gtk_button_box_get_layout(GtkButton *widget);
```

获取子尺寸：

```c
void
gtk_button_box_get_child_size(GtkButton *widget, gint *min_width, gint *min_height);
```

## 应用级 API 摘要（续）

获取子内边距：

```c
void
gtk_button_box_get_child_padding(GtkButtonBox *widget, gint ipad_x, gint *ipad_y);
```

设置子组件间距：

```c
void
gtk_button_box_set_spacing(GtkButtonBox *widget, gint spacing);
```

设置按钮框样式（设置正文）：

```c
void
gtk_button_box_set_layout(GtkButtonBox *widget, GtkButtonStyle layout_style);
```

设置子尺寸：

```c
void
gtk_button_box_set_child_size(GtkButtonBox *widget, gint min_width, gint min_height);
```

设置子内边距：

```c
void
gtk_button_box_set_child_padding(GtkButtonBox *widget, gint ipad_x, gint ipad_y);
```
