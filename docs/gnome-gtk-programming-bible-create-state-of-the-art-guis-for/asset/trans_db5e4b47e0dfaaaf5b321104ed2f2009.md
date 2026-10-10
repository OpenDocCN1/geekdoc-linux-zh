

在第五章“布局容器”部分中，有一个使用一对 `GtkAdjustment` 对象来控制垂直和水平滚动条的示例。

## `GtkAlignment`

这是一个能够控制单个子组件大小的容器组件。`scale` 值从 0.0 到 1.0，表示子组件可以扩展以填充分配给 `GtkAlignment` 组件空间的最大比例。`align` 值决定了相对于 `GtkAlignment` 矩形左上角和右下角的 x 和 y 位置。`align` 值为 0.0 表示顶部或左侧，1.0 表示底部或右侧。

### 继承

`GtkAlignment` -> `GtkBin` -> `GtkContainer` -> `GtkWidget` -> `GtkObject`

### 函数

```c
GtkType gtk_alignment_get_type(void)
GtkWidget *gtk_alignment_new(gfloat xalign, gfloat yalign, gfloat xscale, gfloat yscale)
void gtk_alignment_set(GtkAlignment *alignment, gfloat xalign, gfloat yalign, gfloat xscale, gfloat yscale)
```

以下代码将一个 `GtkButton` 组件插入到 `GtkAlignment` 组件中。x 对齐值设置为 1.0，使按钮紧贴右边缘。y 对齐值为 0.5，使组件垂直居中。两个方向的 scale 值均设置为 0.15，限制按钮的扩展不超过可用面积的 15%。图 21-2 左侧显示了默认大小，此时 `GtkAlignment` 组件根据按钮请求的大小调整自身。右侧窗口显示了窗口扩大后的结果。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *alignment;
    GtkWidget *button;
    button = gtk_button_new_with_label("The Button Label");
    alignment = gtk_alignment_new(1.0, 0.5, 0.15, 0.15);
    gtk_container_add(GTK_CONTAINER(alignment), button);
    return (alignment);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_563_0.png)

## `GtkArrow`

这是一个简单的箭头组件，可以指向向上、向左、向下或向右。

### 继承

`GtkArrow` -> `GtkMisc` -> `GtkWidget` -> `GtkObject`

### 函数

```c
GtkType gtk_arrow_get_type(void)
GtkWidget *gtk_arrow_new(GtkArrowType arrow_type, GtkShadowType shadow_type)
void gtk_arrow_set(GtkArrow *arrow, GtkArrowType arrow_type, GtkShadowType shadow_type)
```

### 枚举

```c
typedef enum {
    GDK_ARROW_UP,
    GDK_ARROW_DOWN,
    GDK_ARROW_LEFT,
    GDK_ARROW_RIGHT
} GtkArrowType;

typedef enum {
    GTK_SHADOW_NONE,
    GTK_SHADOW_IN,
    GTK_SHADOW_OUT,
    GTK_SHADOW_ETCHED_IN,
    GTK_SHADOW_ETCHED_OUT
} GtkShadowType;
```

以下函数创建了图 21-3 中指向左侧的箭头，其绘制方式使得阴影效果使其看起来是凹陷的。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *arrow;
    arrow = gtk_arrow_new(GTK_ARROW_LEFT, GTK_SHADOW_IN);
    return (arrow);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_564_0.png)

## `GtkAspectFrame`

此容器组件将单个组件包裹在一个带标签的框架中，并对子组件施加纵横比约束。

### 继承

`GtkAspectFrame` -> `GtkFrame` -> `GtkBin` -> `GtkContainer` -> `GtkWidget` -> `GtkObject`

### 函数

```c
GtkType gtk_aspect_frame_get_type(void)
GtkWidget *gtk_aspect_frame_new(const gchar *label, gfloat xalign, gfloat yalign, gfloat ratio, gint obey_child)
void gtk_aspect_frame_set(GtkAspectFrame *aspect_frame, gfloat xalign, gfloat yalign, gfloat ratio, gint obey_child)
```

以下示例将一个 `GtkLabel` 封装在 `GtkAspectFrame` 内部。布尔值 **obey_child** 设置为 TRUE，因此 **ratio** 的值被忽略；取而代之的是，**ratio** 值是根据标签的首选大小推导出来的。**xalign** 和 **yalign** 的值将首选位置设置为距离顶部和左侧 60% 的距离。图 21-4 显示了该组件最初出现时的状态以及调整大小后的状态。窗口在水平方向上比垂直方向拉伸得更多。基本上，组件调整自身大小以使其尽可能大，同时保持相同的纵横比（左侧留出 60% 的空间，右侧留出 40%）。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *aspectframe;
    GtkWidget *label;

    label = gtk_label_new("The Label Text");
    aspectframe = gtk_aspect_frame_new("Table", 0.6, 0.6, 1.0, TRUE);
    gtk_container_add(GTK_CONTAINER(aspectframe), label);
    return (aspectframe);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_565_0.png)

**图 21-4：** 纵横比框架保持子组件的纵横比

## `GtkBin`

这是一个容器组件的基类，该容器仅包含一个子组件。此类包含所有仅包含单个子组件的组件共有的代码。

### 继承

`GtkBin` -> `GtkContainer` -> `GtkWidget` -> `GtkObject`

### 函数

```c
GtkType gtk_bin_get_type(void)
```

## `GtkBox`

这是 `GtkHBox` 和 `GtkVBox` 的 **基类**。它包含维护所包含组件列表所需的代码，但不负责定位它们。

### 继承

`GtkBox` -> `GtkContainer` -> `GtkWidget` -> `GtkObject`

### 函数

```c
GtkType gtk_box_get_type(void)
void gtk_box_pack_end(GtkBox *box, GtkWidget *child, gboolean expand, gboolean fill, guint padding)
void gtk_box_pack_end_defaults(GtkBox *box, GtkWidget *child)
void gtk_box_pack_start(GtkBox *box, GtkWidget *child, gboolean expand, gboolean fill, guint padding)
void gtk_box_pack_start_defaults(GtkBox *box, GtkWidget *child)
void gtk_box_query_child_packing(GtkBox *box, GtkWidget *child, gboolean *expand, gboolean *fill, guint *padding, GtkPackType *pack_type)
void gtk_box_reorder_child(GtkBox *box, GtkWidget *child, gint position)
void gtk_box_set_child_packing(GtkBox *box, GtkWidget *child, gboolean expand, gboolean fill, guint padding, GtkPackType pack_type)
void gtk_box_set_homogeneous(GtkBox *box, gboolean homogeneous)
void gtk_box_set_spacing(GtkBox *box, gint spacing)
```

### 枚举

```c
typedef enum {
    GTK_PACK_START,
    GTK_PACK_END
} GtkPackType;
```

## `GtkButton`

这是一个在框架内包含文本或位图标签的窗口。它可以响应鼠标操作。

### 继承

`GtkButton` -> `GtkBin` -> `GtkContainer` -> `GtkWidget` -> `GtkObject`

### 函数

```c
void gtk_button_clicked(GtkButton *button)
void gtk_button_enter(GtkButton *button)
GtkReliefStyle gtk_button_get_relief(GtkButton *button)
GtkType gtk_button_get_type(void)
void gtk_button_leave(GtkButton *button)
GtkWidget *gtk_button_new(void)
GtkWidget *gtk_button_new_with_label(const gchar *label)
void gtk_button_pressed(GtkButton *button)
void gtk_button_released(GtkButton *button)
void gtk_button_set_relief(GtkButton *button, GtkReliefStyle newrelief)
```

### 枚举

```c
typedef enum {
    GTK_RELIEF_NORMAL,
    GTK_RELIEF_HALF,
    GTK_RELIEF_NONE,
} GtkReliefStyle;
```

### 信号

```c
"clicked"     void cb(GtkWidget *, gpointer)
"enter"       void cb(GtkWidget *, gpointer)
"leave"       void cb(GtkWidget *, gpointer)
"pressed"     void cb(GtkWidget *, gpointer)
"released"    void cb(GtkWidget *, gpointer)
```

`GtkButton` 对象在全书中都有使用，因此几乎每一章都有相关示例。特别是，请参见第 3 章和第 4 章。

## `GtkButtonBox`

这是包含 `GtkHButtonBox` 和 `GtkVButtonBox` 公共函数的基类。这些是专门设计用于管理一组按钮的容器组件。`GtkButtonBox` 具有多种控制函数，可用于设置按钮的大小和位置。

### 继承

`GtkButtonBox` -> `GtkBox` -> `GtkContainer` -> `GtkWidget` -> `GtkObject`

### 函数

```c
void gtk_button_box_child_requisition(GtkWidget *widget, int *nvis_children, int *width, int *height)
void gtk_button_box_get_child_padding(GtkButtonBox *widget, gint *ipad_x, gint *ipad_y)
void gtk_button_box_get_child_padding_default(gint *ipad_x, gint *ipad_y)
void gtk_button_box_get_child_size(GtkButtonBox *widget, gint *width, gint *height)
void gtk_button_box_get_child_size_default(gint *width, gint *height)
GtkButtonBoxStyle gtk_button_box_get_layout(GtkButtonBox *widget)
gint gtk_button_box_get_spacing(GtkButtonBox *widget)
GtkType gtk_button_box_get_type(void)
void gtk_button_box_set_child_padding(GtkButtonBox *widget, gint ipad_x, gint ipad_y)
void gtk_button_box_set_child_padding_default(gint ipad_x, gint ipad_y)
void gtk_button_box_set_child_size(GtkButtonBox *widget, gint width, gint height)
void gtk_button_box_set_child_size_default(gint width, gint height)
void gtk_button_box_set_layout(GtkButtonBox *widget, GtkButtonBoxStyle layout_style)
void gtk_button_box_set_spacing(GtkButtonBox *widget, gint spacing)
```

### 枚举

```c
typedef enum {
    GTK_BUTTONBOX_DEFAULT_STYLE,
    GTK_BUTTONBOX_SPREAD,
    GTK_BUTTONBOX_EDGE,
    GTK_BUTTONBOX_START,
    GTK_BUTTONBOX_END
} GtkButtonBoxStyle;
```

## `GtkCalendar`

`GtkCalendar` 组件显示一个月。用户可以选择月份和年份，然后选择该月的具体日期。

### 继承

`GtkCalendar` -> `GtkWidget` -> `GtkObject`

### 函数

```c
void gtk_calendar_clear_marks(GtkCalendar *calendar)
void gtk_calendar_display_options(GtkCalendar *calendar, GtkCalendarDisplayOptions flags)
```

