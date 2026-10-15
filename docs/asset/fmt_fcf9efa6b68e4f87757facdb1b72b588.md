
```c
5: line_pts = (XPoint *)XtMalloc(sizeof(XPoint) * 5);
6: line_num_pts = 5;
```

然后它将矩形的每个角赋予第 8-18 行中 `pts` 数组对应的元素：

```c
20: line_pts[4].x = box->x;
21: line_pts[4].y = box->y;
```

如果没有最后一步，生成的线将向左开口的 U 形。

对于用户创建的 `GXLine`，调用 `create_line` 函数，并对该对象进行类似于 `Line` 和 `Pencil` 对象的管理。

考虑下一节引入的类似于 `Box` 对象的 `Arrow` 对象

## Arrow 对象

通过从图形面板选择图 22.2 所示的箭头图标，用户可以开始 `Arrow` 对象的创建。

![](img/786ba9bd5cd671beb490264fd2e6aae1_437_0.png)

### 图 22.2 创建创建图标。

`Arrow` 对象像 `Box` 对象一样被视为模板对象，因为箭头形状是由创建过程强制的。与 `Box` 对象相似的是，`Button` 事件开始创建过程，`ButtonRelease` 事件结束。

与 `ButtonPress` 关联的事件点确定正在创建对象的左上角，`ButtonRelease` 事件标记对象的右下角。

列表 22.4 引入了在第 3 章 `gxDraw` 数组中赋值的 `gx_arrow` 函数。

### 列表 22.4 gx_arrow 函数

```c
1: void gx_arrow( XEvent *event )
2: {
3:     static XRectangle *rubber_box = NULL;
4:     GXLinePtr arrow;
5: 
6:     if (event == NULL) {
7:         rubber_box = NULL;
8:     } else {
9:         if (rubber_box) {
10:            arrow = arrow_from_box( rubber_box );
11:            XDrawLines(GxArea), rubber_GC,
12:            XtWindow(GxArea),
13:
14:            arrow->pts, arrow->num_pts,
15:            CoordModeOrigin );
16:
        }
17:
    }
18:    switch (event->type) {
19:        case ButtonPress:
20:            rubber_box = update_box(event, NULL);
21:            set_cursor( EDIT_MODE);
22: 
23:            break;
24: 
25:        case ButtonRelease:
26:            if (rubber_box) {
27:                create_line(NULL, arrow_from_box(rubber_box));
28:                gx_refresh();
29:            }
30:            set_cursor( NORMAL_MODE );
31:            rubber_box = NULL;
32: 
33:            break;
```

```c
34: case MotionNotify:
35: if ( rubber_box ) {
36:   (void)update_box( event, rubber_box );
37:
38:   arrow = arrow_from_box( rubber_box );
39:   XtDrawLines(XtDisplay(GxArea),
40:     XtWindow(GxArea), rubber_GC,
41:     arrow->pts, arrow->num_pts,
42:     CoordModeOrigin );
43:
44:   }
45:   break;
46: 
47: }
48: }
```

`gx_arrow` 函数应该非常熟悉，因为它结构与 `gx_box`（以及之前的）相同。

事实上，`gx_box` 函数和 `gx_arrow` 函数的区别在于以下几行中将 `XRectangle` 结构转换为 `GXLine` 结构的 `line_from_box` 函数：

```c
26: create_line(NULL, arrow_from_box(rubber_box));
38: arrow = arrow_from_box( rubber_box );
```

`line_from_box` 函数在列表 22.5 中定义。

### 列表 22.5 从框创建箭头

```c
1: static GXLinePtr arrow_from_box( XRectangle *box )
2: {
3:   static GLine arrow;
4:   static XPoint pts[10];
5: 
6:   pts[0].x = box->x + (box->width / 10);
7:   pts[0].y = box->y + box->height;
8: 
9:   pts[1].x = box->x + (box->width / 4);
10:  pts[1].y = box->y + box->height - (box->height / 8);
11: 
12:  pts[2].x = box->x + (box->width / 4);
13:  pts[2].y = box->y + (box->height / 2);
14: 
15:  pts[3].x = box->x;
16:  pts[3].y = box->y + (box->height / 2);
17: 
18:  pts[4].x = box->x + (box->width / 2);
19:  pts[4].y = box->y;
20: 
21:  pts[5].x = box->x + box->width;
22:  pts[5].y = box->y + (box->height / 2);
```

# 418 第 V 部分向编辑器添加对象

```c
23: pts[6].x = box->x + ((box->width * 3) / 4);
24: pts[6].y = box->y + (box->height / 2);
25:
26: pts[7].x = box->x + ((box->width * 3) / 4);
27: pts[7].y = box->y + box->height - (box->height / 8);
28:
29: pts[8].x = box->x + box->width - (box->width / 10);
30: pts[8].y = box->y + box->height;
31:
32: arrow_pts = pts;
33: arrow_num_pts = 9;
34:
35: return &arrow
)
```

`arrow_from_function` 定义了足够容纳 10 个 `XPoint` 结构体的空间：

`4: static XPoint pts[10];`

数组中点的排列方式如图 22.3 所示。

### 图 22.3

箭头中点的排列示意图。

![](img/786ba9bd5cd671beb490264fd2e6aae1_440_0.png)

第 63–31 行根据与图 22.3 所示点位置一致的比例和倍率，细致地分配了点值。

> 注意：将一个矩形划分为一系列点以形成箭头的形状，这并没有真正的科学依据。我是通过不断尝试实现的，直到结果符合审美。然而，重要的是，必须使用矩形的比例来创建定义箭头的点，以便使最终生成的 `GXLine` 结构能够尊重纵横比（宽度与高度比例）。

随后，将点数组连同正确的点数赋值给 `GXLine` 结构的 `pts` 值：

```c
33: arrow_pts = pts;
34: arrow_num_pts = 9;
```

并返回 `GXLine` 结构 `arrow` 的地址，用于绘制用户导航的交互对象，或用于创建最终基于点数组的对象：

```c
36: return &arrow;
```

这完成了图形编辑器支持的 `Box`（矩形）和 `Arrow`（箭头）模板对象的介绍。

## 下一步工作

当 `Box` 和 `Arrow` 对象稳妥地留在图形编辑器项目中后，你已经成功添加了总共四个对象。由于它们都是基于点数组的对象，它们能够大量借用核心结构。
