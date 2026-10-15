
```c
static GtkWidget *makeWidget()
{
    GtkWidget *widget;
    GtkObject *adjustment;
    adjustment = gtk_adjustment_new(45.0, 0.0, 100.0,
        1.0, 0.0, 0.0);
    widget = gtk_vscale_new(GTK_ADJUSTMENT(adjustment));
    return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_656_0.png)

## GtkVScrollbar

`GtkVScrollbar` 显示一个带有滑块和一对箭头按钮的垂直滚动条。要创建滚动条，必须指定起始值和结束值、滑块的大小、初始滑块位置以及鼠标点击槽时滑块应移动的距离。

### 继承

`GtkScrollbar -> GtkScrollbar -> GtkRange -> GtkWidget -> GObject`

### 函数

```c
GtkType gtk_vscrollbar_get_type(void)
GtkWidget *gtk_vscrollbar_new(GtkAdjustment *adjustment)
```

以下示例创建一个范围从 0 到 100 的垂直滚动条，如图 21-47 所示。范围的设置指定从一端到另一端有 100 个单位（起始值和结束值之间的差值）。点击某一端的箭头会使滑块移动一个单位。点击槽会使滑块移动 5 个单位。滑块被设置为 20 个单位的宽度。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *widget;
    GtkObject *adjustment;
    adjustment = gtk_adjustment_new(45.0, 0.0, 100.0,
        1.0, 5.0, 20.0);
    widget = gtk_vscrollbar_new(GTK_ADJUSTMENT(adjustment));
    return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_657_0.png)

**图 21-47：** 滑块大小为 20% 的垂直滚动条

## GtkVSeparator

`GtkVSeparator` 小部件绘制一条垂直线，您可以将其用作水平组织的一组小部件之间的分隔符。

### 继承

`GtkVSeparator -> GtkSeparator -> GtkWidget -> GObject`

### 函数

```c
GtkType gtk_vseparator_get_type(void)
GtkWidget *gtk_vseparator_new(void)
```

以下示例将一个垂直分隔线打包到两个按钮之间的一个框中，如图 21-48 所示。如果容器不会调整分隔线的大小，您必须设置其宽度，因为它默认为零且不可见。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *box;
    GtkWidget *button;
    GtkWidget *separator;
    box = gtk_hbox_new(FALSE, 0);
    button = gtk_button_new_with_label("Button One");
    gtk_box_pack_start(GTK_BOX(box), button, FALSE, FALSE, 0);
    separator = gtk_vseparator_new();
    gtk_box_pack_start(GTK_BOX(box), separator, FALSE, FALSE, 0);
    gtk_widget_set_usize(separator, 20, 0);
    button = gtk_button_new_with_label("Button Two");
    gtk_box_pack_start(GTK_BOX(box), button, FALSE, FALSE, 0);
    return(box);
}
```
