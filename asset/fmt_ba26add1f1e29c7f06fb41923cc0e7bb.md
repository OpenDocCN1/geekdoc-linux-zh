
```
node1_1 = makeNode(widget,NULL,NULL,1,1);

makeNode(widget,NULL,node1_1,1,2);

node1_3 = makeNode(widget,NULL,node1_1,1,3);

makeNode(widget,NULL,node1_1,1,4);

makeNode(widget,node1_1,NULL,2,2);

makeNode(widget,node1_1,NULL,2,2);

makeNode(widget,node1_3,NULL,2,1);

makeNode(widget,node1_3,NULL,2,2);

return(widget);

}

static GtkCTreeNode *makeNode(GtkWidget *widget,

GtkCTreeNode *parent,GtkCTreeNode *sibling,

gint level,gint count)

{

GtkCTreeNode *node;

gchar *txt[2];

gchar line1[20];

gchar line2[20];

txt[0] = line1;

txt[1] = line2;

sprintf(line1,"Level %d",level);

sprintf(line2,"Number %d",count);

node = gtk_ctree_insert_node(GTK_CTREE(widget),

parent,

sibling,

text,

0,

NULL,NULL,NULL,NULL,

FALSE,TRUE);

return(node);

}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_586_0.png)

图 21-12: 一个显示选择和展开的两层 GtkCTree

## GtkCurve

该控件显示一个网格，并沿着一系列点在其上绘制图形。有三种类型的轨迹可用。你可以使用鼠标交互地添加新点并移动现有的点。

### 继承

`GtkCurve`->`GtkDrawingArea`->`GtkWidget`->`GtkObject`

### 函数

`GtkType gtk_curve_get_type(void)`
`void gtk_curve_get_vector(GtkCurve *c, int vecilen, gfloat vector [ ])`
`GtkWidget *gtk_curve_new(void)`
`void gtk_curve_reset(GtkCurve *c)`
`void gtk_curve_set_curve_type(GtkCurve *c, GtkCurveType new_type)`
`void gtk_curve_set_gamma(GtkCurve *c, gfloat gamma)`
`void gtk_curve_set_range(GtkCurve *curve, gfloat min_x, gfloat max_x, gfloat min_y, gfloat max_y)`
`void gtk_curve_set_vector(GtkCurve *c, int vecilen, gfloat vector [ ])`

### 枚举

```c
typedef enum {
GTK_CURVE_TYPE_LINEAR,
GTK_CURVE_TYPE_SPLINE,
GTK_CURVE_TYPE_FREE
} GtkCurveType;
```

### 信号

`"curve_type_changed"`    `void cb(GtkWidget *, gpointer)`

以下示例创建了一个 100x100 的显示区域。使用鼠标来添加和定位图 21-13 中显示的点。曲线是样条曲线，因此它通过每个点生成平滑的弯曲线条。

```c
static GtkWidget *makeWidget()
{
GtkWidget *widget;
widget = gtk_curve_new();
gtk_curve_set_range(GTK_CURVE(widget),
0.0, 100.0, 0.0, 100.0);
gtk_curve_set_curve_type(GTK_CURVE(widget),
GTK_CURVE_TYPE_SPLINE);
return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_587_0.png)

图 21-13: 一个显示样条曲线的 GtkCurve 控件

## GtkData

继承自基类 `GtkData` 的控件具有包含在两个或多个控件之间共享的数据的能力。示例包括 `GtkAdjustment`、`GtkTooltips` 和 `GtkAdjustment`。

### 继承

`GtkData`->`GtkObject`

### 函数

`GtkType gtk_data_get_type(void)`

### 信号

`"disconnect"`        `void cb(GtkWidget *, gpointer)`

## GtkDial

`GtkDial` 控件显示一个表示从 0 百分到 100 百分的值指针盘。如果不在仅查看模式下，你可以使用鼠标调整指针盘。

### 继承

`GtkDial`->`GtkWidget`->`GObject`

### 函数

`GtkAdjustment *gtk_dial_get_adjustment(GtkDial *dial)`
`gfloat gtk_dial_get_percentage(GtkDial *dial)`
`guint gtk_dial_get_type()`
`gfloat gtk_dial_get_value(GtkDial *dial)`
`GtkWidget *gtk_dial_new(GtkAdjustment *adjustment)`
`void gtk_dial_set_adjustment(GtkDial *dial, GtkAdjustment *adjustment)`
`gfloat gtk_dial_set_value(GtkDial *dial, gfloat percent)`
`void gtk_dial_set_update_policy(GtkDial *dial, GtkUpdateType policy)`
`gfloat gtk_dial_set_value(GtkDial *dial, gfloat value)`
`void gtk_dial_set_view_only(GtkDial *dial, gboolean view_only)`

### 枚举

```c
typedef enum {
  GTK_UPDATE_CONTINUOUS,
  GTK_UPDATE_DISCONTINUOUS,
  GTK_UPDATE_DELAYED
} GtkUpdateType;
```

以下示例构建了图 21-14 中所示的 GtkDial 控件。当前设置值 44 是从最小值 0 到最大值 200 距离的 22 百分。

```c
static GtkWidget *makeWidget()
{
  GtkWidget *widget;
  GObject *adjustment;
  adjustment = gtk_adjustment_new(44.0,
    0.0, 200.0, 1.0, 0.0, 0.0);
  widget = gtk_dial_new(GTK_ADJUSTMENT(adjustment));
  return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_588_0.png)

图 21-14: 一个处于 22 百分的 GtkDial 控件

## GtkDialog

`GtkDialog` 控件是一个带有预装和配置好的容器的窗口，你可以使用这些容器创建自己的弹出对话框。

### 继承

`GtkDialog`->`GtkWindow`->`GtkBin`->`GtkContainer`->`GtkWidget`->`GtkObject`

### 函数

`GtkType gtk_dialog_get_type(void)`
`GtkWidget *gtk_dialog_new(void)`

以下示例（见图 21-15）在两个可用的容器中各放置了三个按钮。名为 `vbox` 的垂直框被配置在顶部，设计用于工具栏和菜单。此外，你还可以将垂直框用作位图窗口和文本标签的容器。名为 `action_area` 的水平框将控件居中排列，设计用于响应按钮。

```c
static void makeWidget()
{
  GtkWidget *dialog;
  GtkWidget *button;
  GtkWidget *vbox;
  GtkWidget *hbox;
  dialog = gtk_dialog_new();
```
