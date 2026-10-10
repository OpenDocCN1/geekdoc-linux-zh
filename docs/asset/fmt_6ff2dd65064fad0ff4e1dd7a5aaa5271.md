
```
032   gtk_timeout_add(1000, TimeoutFunc, (gpointer) packer );
033   gtk_packer_set_default_pad( GTK_PACKER ( packer ), 20, 0 );
034   options = GTK_FILL_X | GTK_EXPAND;
035
036   one = gtk_label_new("one");
037   gtk_packer_add_defaults( GTK_PACKER ( packer ), one,
038   GTK_SIDE_LEFT, GTK_ANCHOR_CENTER, options );
039   gtk_widget_show( one );
040
041   two = gtk_label_new("two");
042   gtk_packer_add_defaults( GTK_PACKER ( packer ), two,
043   GTK_SIDE_LEFT, GTK_ANCHOR_CENTER, options );
044   gtk_widget_show( two );
045
046   three = gtk_label_new("three");
047   gtk_packer_add_defaults( GTK_PACKER ( packer ), three,
048   GTK_SIDE_LEFT, GTK_ANCHOR_CENTER, options );
049   gtk_widget_show( three );
050
051   four = gtk_label_new("four");
052   gtk_packer_add_defaults( GTK_PACKER ( packer ), four,
053   GTK_SIDE_LEFT, GTK_ANCHOR_CENTER, options );
054   gtk_widget_show( four );
055
056   five = gtk_label_new("five");
057   gtk_packer_add_defaults( GTK_PACKER ( packer ), five,
058   GTK_SIDE_LEFT, GTK_ANCHOR_CENTER, options );
059   gtk_widget_show( five );
060
061   gtk_widget_show( packer );
062   gtk_container_add( GTK_CONTAINER ( window ), packer );
```

## 宏

部件类型宏：`GTK_TYPE_FRAME`

对象到部件转换宏：`GTK_FRAME(obj)`

部件类型检查宏：`GTK_IS_FRAME(obj)`

## 支持的参数

前缀：`GtkFrame` ::

表 11.6 GtkFrame 参数
| 名称 | 类型 | 权限 |
| --- | --- | --- |
| label | `GTK_TYPE_STRING` | `GTK_ARG_READWRITE` |
| label_align | `GTK_TYPE_FLOAT` | `GTK_ARG_READWRITE` |
| label_valign | `GTK_TYPE_FLOAT` | `GTK_ARG_READWRITE` |
| shadow | `GTK_TYPE_SHADOW_TYPE` | `GTK_ARG_READWRITE` |

## 应用级 API 摘要

在运行时获取常量 `GTK_TYPE_FRAME`：
```
GtkType
gtk_frame_get_type(void);
```

创建一个带有可选标签的 `GtkFrame` 实例（如果不需要标签则传递 `NULL`）：
```
GtkWidget *
gtk_frame_new(const gchar *label);
```

将 `GtkFrame` 实例的标签设置为特定值（如果不需要标签则传递 `NULL`）：
```
void
gtk_frame_set_label(GtkFrame *frame, const gchar *label);
```

设置 `GtkFrame` 实例的标签对齐方式：
```
void
gtk_frame_set_label_align(GtkFrame *frame, gfloat xalign, gfloat yalign);
```

设置 `GtkFrame` 实例的阴影类型：
```
void
gtk_frame_set_shadow_type(GtkFrame *frame, GtkShadowType type);
```

# ClassFrame 说明

`GtkFrame` 是容器类，与本章描述的其他类一样，用于管理其他部件类的实例。`GtkFrame` 的父类是 `GtkBin`，而 `GtkBin` 又是 `GtkContainer` 的子类。`GtkFrame` 与 `GtkBin` 的区别在于它的子组件周围绘制边界（或框架）以标识区域。框架可以包含一个标签，帮助用户更容易地识别框架中控件或其他项目所属的逻辑分组。像任何容器一样，`GtkFrame` 的实例可以管理其他容器，包括 `GtkFrame` 实例、`GtkBox` 等。

# 创建框架部件

通过调用 `gtk_frame_new()` 创建框架：
```
GtkWidget *
gtk_frame_new(const gchar *label);
```

参数 `label` 如果不为 `NULL`，则指向一个 `NULL` 终止的 C 字符串，该字符串将用于 `GtkFrame` 标记框架标签。如果你的应用程序不需要使用框架，只需传递 `(gchar *) NULL`。

## 示例

在以下代码中，我创建了一个包含三个 `GtkList` 实例的对话框，每个列表包含相同数量的项目。这些列表在对话框的控制区域从左到右打包。定义宏 `#define USE_FRAMES` 将导致每个列表都被一个 `GtkFrame` 实例包裹。如图 11.17 和 11.18 所示，框架不仅为三个列表提供了更好的视觉隔离，框架标签还帮助识别每个列表的内容。

![](img/1441ee0eb9a357efc9aff107f92bf0c0_549_0.png)

图 11.17 不带框架的三个列表

![](img/1441ee0eb9a357efc9aff107f92bf0c0_550_0.png)

图 11.18 带框架的三个列表

代码列表 11.4 图 11.17 和 11.18 的部分源码
```
#include <gtk.h>

void
GtkFrameDialog() {
    GtkWidget *frame, *dialog_window, *hbox1, *outerbox,
    *list, *list_item;
    GList *list_item;
    dialog_window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_position(GTK_WINDOW (dialog_window), GTK_WINDOW_POS_MOUSE);
    gtk_signal_connect(GTK_OBJECT (dialog_window), "destroy",
        GTK_SIGNAL_FUNC(gtk_widget_destroyed), &dialog_window);
    gtk_window_set_title(GTK_WINDOW (dialog_window), "GtkFrame Demo");
    gtk_container_border_width(GTK_CONTAINER (dialog_window), 0);
    outbox = gtk_box_new(FALSE, 0);
    gtk_container_add (GTK_CONTAINER (dialog_window), outbox);
    #if defined(USE_FRAMES) 
    frame = gtk_frame_new("Shirt");
    gtk_box_pack_start (GTK_BOX (hbox1), frame, FRAME, TRUE, 0);
    #endif
    list = gtk_list_new();
    list_item = NULL;
    list_item = gtk_list_item_new_with_label("Dress, short sleeve");
    list_item = g_list_append(list, list_item);
    list_item = gtk_list_item_new_with_label("Dress, long sleeve");
    list_item = g_list_append(list, list_item);
```
