
```c
#include <gtk/gtk.h>

/*
 * 简单的 MessageBox，不使用 GtkDialog
 */

void
MessageBox(char *message )
{
    GtkWidget *vbox1, *vbox2, *hbox, *separator, *label, *button,
        *dialog_window;

    dialog_window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_position(GTK_WINDOW (dialog_window), GTK_WIN_POS_MOUSE);

    gtk_signal_connect(GTK_OBJECT (dialog_window), "destroy",
        GTK_SIGNAL_FUNC(gtk_widget_destroyed), &dialog_window);

    gtk_window_set_title(GTK_WINDOW (dialog_window), "Message");
    gtk_container_border_width(GTK_CONTAINER (dialog_window), 0);

    /* 创建 hbox，用于包含控制区域 vbox、动作
       区域 hbox 以及它们之间的分隔符 */

    hbox = gtk_vbox_new(FALSE, 0);

    gtk_container_add(GTK_CONTAINER (dialog_window), hbox);

    /* 创建代表控制区域的 vbox。消息（作为

       GtkLabel 实例）将被添加到此 vbox 中。将控制

       区域 vbox 添加到外部 hbox */

    vbox1 = gtk_vbox_new(FALSE, 0);

    gtk_box_pack_start(GTK_BOX (hbox), vbox1, TRUE, 0);

    /* 创建分隔符，并将其添加到外部 hbox */

    separator = gtk_vseparator_new();

    gtk_box_pack_start(GTK_BOX (hbox), separator, TRUE, TRUE, 0);

    /* 创建代表动作区域的 vbox。OK 按钮将
       添加到此 vbox 中。将动作区域 vbox 添加到外部 hbox */

    vbox2 = gtk_vbox_new(FALSE, 5);

    gtk_container_border_width(GTK_CONTAINER (vbox2), 10);

    gtk_box_pack_start (GTK_BOX (hbox), vbox2, TRUE, TRUE, 0);

    /* 现在创建消息标签和 OK 按钮，并将它们
       分别添加到控制区域和动作区域 */

    button = gtk_button_new_with_label("OK");

    gtk_WIDGET_SET_FLAGS (button, GTK_CAN_DEFAULT);

    gtk_box_pack_start (GTK_BOX (vbox2), button, TRUE, TRUE, 0);

    gtk_signal_connect_object (GTK_OBJECT (button), "clicked",

        GTK_SIGNAL_FUNC (gtk_widget_destroy),

        GTK_OBJECT (dialog_window));

    label = gtk_label_new (message);

    gtk_misc_set_padding (GTK_MISC (label), 10, 10);

    gtk_box_pack_start (GTK_BOX (vbox1), label, TRUE, TRUE, 0);

    gtk_widget_grab_default (button);

    gtk_widget_show_all (dialog_window);

}
```

# GtkArrow

## 类名
`GtkArrow`

### 父类名
`GtkMisc`

## 宏
- 控件类型宏 `GTK_TYPE_ARROW`
- 对象到控件的转换宏：`GTK_ARROW(obj)`
- 控件类型检查宏：`GTK_IS_ARROW(obj)`

### 支持的参数
前缀：`GtkArrow::`

表 8.2 `GtkArrow`
| 名称 | 类型 | 权限 |
| --- | --- | --- |
| `arrow_type` | `GTK_TYPE_ARROW_TYPE` | 读写 |
| `shadow_type` | `GTK_TYPE_SHADOW_TYPE` | 读写 |

# 应用级概览
在运行时获取 `GTK_TYPE_ARROW` 常量：

```
GtkType

gtk_arrow_get_type(void);
```

创建一个新的 `GtkArrow` 实例：

```
GtkWidget *

gtk_arrow_new(GtkArrowType arrow_type, GtkShadowType shadow_type);
```

设置 `GtkArrow` 实例的箭头和阴影：

```
void

gtk_arrow_set(GtkArrow *arrow, GtkArrowType arrow_type, GtkShadowType shadow_type);
```

### 类描述
`GtkArrow` 是一个可以用于用户用户界面箭头装饰的控件。`GtkArrow` 类似于 `GtkLabel`，因为它不产生信号。如果需要产生信号，必须将箭头放在能够产生所需信号的容器中，例如 `GtkEvent` 或 `GtkButton` 实例。我将说明如何将 `GtkArrow` 实例整合到 `GtkButton` 实例中。

# 箭头和阴影类型
箭头可以是四种类型之一以及四种阴影类型之一。如图 8.4 所示，所选的阴影类型对箭头外观的影响很大。

![](img/b9af04aaed46302cb075052312fcd667_361_0.png)

图 8.4 箭头类型和阴影类型

# 第 8 章 分隔符、箭头、图像、位图和输入控件

从左到右，阴影类型为 `GTK_SHADOW_IN`、`GTK_SHADOW_OUT`、`GTK_SHADOW_ETCHED_IN` 和 `GTK_SHADOW_ETCHED_OUT`。箭头类型定义了箭头的方向，如表 8.3 所示。

表 8.3 箭头类型
| 类型 | 方向 |
| --- | --- |
| `GTK_ARROW_UP` | 箭头指向屏幕顶部。 |
| `GTK_ARROW_DOWN` | 箭头指向屏幕底部。 |
| `GTK_ARROW_LEFT` | 箭头指向屏幕左边缘。 |
| `GTK_ARROW_RIGHT` | 箭头指向屏幕右边缘。 |

图 8.4 展示了表 8.3 列出的箭头（从左到右：`GTK_ARROW_UP`、`GTK_ARROW_DOWN`、`GTK_ARROW_LEFT` 和 `GTK_ARROW_RIGHT`）。后面提供的 `GtkArrow` 函数都允许你在控件创建时或控件创建后的某个时候指定这些属性。

# 创建箭头控件
通过调用 `gtk_arrow_new()` 创建新的 `GtkArrow`：

```
GtkWidget *

gtk_arrow_new(GtkArrowType arrow_type, GtkShadowType shadow_type);
```

如上述图形和表格所示，`arrow_type` 是 `GTK_ARROW_UP`、`GTK_ARROW_DOWN`、`GTK_ARROW_LEFT` 或 `GTK_ARROW_RIGHT`，而 `shadow_type` 是 `GTK_SHADOW_IN`、`GTK_SHADOW_OUT`、`GTK_SHADOW_ETCHED_IN` 或 `GTK_SHADOW_ETCHED_OUT`。

# 设置箭头属性
一旦创建箭头，就可以通过 `gtk_arrow_set()` 更改箭头类型和阴影类型属性：

```
void

gtk_arrow_set(GtkArrow *arrow, GtkArrowType arrow_type, GtkShadowType shadow_type);
```

`arrow` 是 `GtkArrow` 实例。`arrow_type` 和 `shadow_type` 与传递给 `gtk_arrow_new()` 的同名参数相同。

并且在其右侧，是一个 `GtkArrow` 实例。下面的代码段说明了具有具有 `GTK_ARROW_UP` 和 `GTK_SHADOW_IN` 属性的按钮创建过程：

```
GtkWidget *button, *arrow, *hbox, *label;
```

```
// 创建一个按钮
```

```
button = gtk_button_new();
```

```
// 创建一个 GtkBox 实例来存放标签和箭头
// 组件，并将其添加到按钮中。如果按钮已经管理了
// 子组件，则 gtk_container_add() 将失败
```

```
hbox = gtk_hbox_new(FALSE, 0);
gtk_container_add(GTK_CONTAINER(button), hbox);
```

```
// 创建一个标签，并将其添加到 hbox 中，指定 5 像素的间隔
// 以使其与随后的箭头在视觉上保持区分
```

```
label = gtk_label_new("Click me!");
gtk_box_pack_start(GTK_BOX(hbox), label, TRUE, TRUE, 5);
```

```
// 创建一个箭头，并将其添加到 hbox 中
```

```
arrow = gtk_arrow_new(GTK_ARROW_UP, GTK_SHADOW_IN);
gtk_box_pack_start(GTK_BOX(hbox), arrow, TRUE, TRUE, 5);
```

## 图像与位图 (Images and Pixmaps)

`Gtk+` 1.2 实现了两个类：`GtkImage` 和 `GtkPixmap`，它们分别对 GDK 的图像和位图支持提供了封装。虽然 GDK 提供了支持创建和操作实际图像及位图所需的大代码，但 `GtkImage` 和 `GtkPixmap` 封装了这些功能，并允许图像和位图在需要 GWidget 的地方使用。例如，在第 6 节“列表”中，我们看到了如何将位图添加到 `GtkList` 实例中。在那个章节中，我说明了如何使用 GDK 程来创建实际的位图数据，然后使用 `GtkPixmap` 函数创建一个被添加到 `GtkList` 单元格的组件。

关于如何使用 GDK 创建位图数据，以及 `GtkPixmap` 如何使用这些数据的信息，可以在第 6 节关于 `GtkList` 的讨论中找到。在本节中，我将描述创建 `GtkImage` 实例之前的过程，包括如何使用 GDK 程来创建和修改图像数据。还将详细讨论 `GtkImage` 支持的 API。

## GtkPixmap

### 类名
`GtkPixmap`

### 父类名
`GtkWidget`

## 宏
- 组件类型宏：`GTK_TYPE_PIXMAP`
- 对象到组件的转换宏：`GTK_PIXMAP(obj)`
- 组件类型检查宏：`GTK_IS_PIXMAP(obj)`

### 应用层级 API 摘要
在运行时获取 `GTK_TYPE_PIXMAP` 常量：
```
GtkType

gtk_pixmap_get_type(void);
```

创建一个新的 `GtkPixmap` 实例，传递之前创建的 GDK 位图和掩码：
```
GtkWidget *

gtk_pixmap_new(GdkPixmap *pixmap, GdkBitmap *mask);
```

设置与 `GtkPixmap` 实例关联的掩码和 GDK 位图：
```
void

gtk_pixmap_set(GtkPixmap *pixmap, GdkBitmap *val, GdkBitmap *mask);
```

获取与 `GtkPixmap` 实例关联的掩码和 GDK 位图：
```
void

gtk_pixmap_get(GtkPixmap *pixmap, GdkBitmap **val, GdkBitmap **mask);
```

指定 `Gtk+` 是否应该保持与 `GtkPixmap` 实例对应的位图或位图的不敏感版本。如果 `GtkPixmap` 在此时是可见的，则队列重绘以反映变化：
```
void

gtk_pixmap_set_build_insensitive(GtkPixmap *pixmap, guint build);
```

### 类描述
在第 6 节中，我描述了如何使用 GDK 程根据 XPM 文件或嵌入在应用程序源码中的 XPM 数据创建位图数据。我还说明了如何从这些数据创建 `GtkPixmap` 实例，并使用它设置 `GtkListBox` 实例的位图数据。在本节中，我将记录 `GtkPixmap` 提供的函数。请参考第 6 节获取使用这些函数的示例。

## 创建位图组件
要创建 `GtkPixmap` 实例，你首先需要使用 GDK 提供的程创建一个 `GdkPixmap` 和掩码，并传递之前创建的 `GdkPixmap` 和掩码。诸如 `gdk_pixmap_colormap_create_from_xpm()` 等程可以在第 6 节中使用以创建必要的 GDK 数据。给定这些数据，你就可以调用 `gtk_pixmap_new()` 来创建 `GtkPixmap` 封装类，你可以将其用于影响 `GtkPixmap` 组件的 `Gtk+` 函数。`gtk_pixmap_new()` 的原型如下：
```
GtkWidget *

gtk_pixmap_new(GdkPixmap *pixmap, GdkBitmap *mask);
```
第一个参数是 `GdkPixmap`。该位图可以预先填充位图数据（例如，使用第 6 节中描述的函数之一）。

## 设置和获取位图数据
你可以通过调用 `gtk_pixmap_set()` 来更改与 `GtkPixmap` 实例关联的位图和掩码：
```
void

gtk_pixmap_set(GtkPixmap *pixmap, GdkBitmap *val, GdkBitmap *mask);
```
参数 `pixmap` 是 `GtkPixmap` 实例。参数 `val` 和 `mask` 分别是第 6 节中使用的 GDK 程获取的位图和掩码数据。同样，你可以通过 `gtk_pixmap_get()` 从 `GtkPixmap` 实例检索位图和掩码数据：
```
void

gtk_pixmap_get(GtkPixmap *pixmap, GdkBitmap **val, GdkBitmap **mask);
```
参数 `pixmap` 是 `GtkPixmap` 实例，返回时，`val` 指 `GdkBitmap`，`mask` 指 `GdkBitmap`。你的应用程序返回的是由 `GtkPixmap` 组件管理的 `GdkPixmap` 和 `GdkBitmap` 指针而不是拷贝。因此，确保释放这些指针引用的内存。前面的创建两个 `GtkButton` 实例显示的图像数据的函数。点击任何按钮都会导致图像交换。代码后面是详细说明。代码还使用了第 6 节描述的 GDK 位图程。

## Listing 8.4 GtkPixmap 应用程序
```c
#include <gtk/gtk.h>

GtkWidget *pixmap1, *pixmap2;

static void SwitchCallback(GtkWidget *widget, GtkWidget *dialog_window) {
    GtkPixmap *gdkPixmap1, *gdkPixmap2;
    GdkBitmap *gdkBitmap1, *gdkBitmap2;

    /* 获取当前值 */
    gtk_pixmap_get(GTK_PIXMAP(pixmap1), &gdkPixmap1, &gdkBitmap1);
    gtk_pixmap_get(GTK_PIXMAP(pixmap2), &gdkPixmap2, &gdkBitmap2);

    /* 交换它们 */
    gtk_pixmap_set(GTK_PIXMAP(pixmap1), gdkPixmap2, gdkBitmap2);
    gtk_pixmap_set(GTK_PIXMAP(pixmap2), gdkPixmap1, gdkBitmap1);
}

static GtkWidget *pixmap = NULL;

void * new_pixmap(char *file, GdkWindow *window, GdkColor *background) {
    GdkPixmap *pmap;
    GdkBitmap *mask;
    pmap = gdk_pixmap_create_from_xpm(window, &mask, background, file);
    return gtk_pixmap_new(pmap, mask);
}

int main(int argc, char *argv[]) {
    GtkWidget *button, *hbox, *dialog_window;
    gtk_init(&argc, argv);
    dialog_window = gtk_dialog_new();
    gtk_window_position(dialog_window, GTK_WINDOW, GTK_WIN_POS_MOUSE);
    gtk_widget_show(dialog_window);
    hbox = gtk_hbox_new(FALSE, 0);
```
