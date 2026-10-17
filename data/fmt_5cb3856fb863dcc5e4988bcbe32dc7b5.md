
```c
1: void gx_line(XEvent *event)
2: {
3:     static GXLine *rubber_line = NULL;
4:
5:     if (event == NULL) {
6:         rubber_line = NULL;
7:     } else {
8:         /* 移除当前的橡皮筋线（如果有的话） */
9:         GxRubberLine(rubber_line);
10:
11:         switch (event->type) {
12:             case ButtonPress:
13:                 if (rubber_line == NULL) set_cursor (LINE_MODE);
14:
15:             /*
16:                 * 检查是否是“双击”并完成了点选择
17:             */
18:             if (point_event(rubber_line, event) == True) {
19:
20:                 /* 擦除我们的临时线 * */
21:                 XtDisplay(GxDrawArea), XtWindow(GxDrawArea),
22:                 rubberGC, rubber_line->pts,
23:                 rubber_line->num_pts, CoordModeOrigin);
24:
25:
26:                 create_line(NULL, rubber_line);
27:                 gx_refresh();
28:
29:                 set_cursor(NORMAL_MODE);
30:                 rubber_line = NULL;
31:             } else {
32:             /*
33:                 * 初始化一个 GXLine 结构来管理我们的创建
34:             */
35:                 GxRubberLine(rubber_line);
36:                 rubber_line = update_line(event, rubber_line);
37:
38:             break;
39:  case ButtonRelease:
40:  case MotionNotify:
41:    /*
42:    * 根据新点和鼠标的当前位置
43:    * 更新 GXLine 结构
44:    */
45:    if( rubber_line ) {
46:      /*
47:      * 将最后一个点替换为当前事件位置
48:      * 如果我们有超过一个点
49:      */
50:      if( rubber_line->num_pts > 1 ) {
51:        rubber_line->pts[rubber_line->num_pts-1].x =
52:          event->xbutton.x;
53:        rubber_line->pts[rubber_line->num_pts-1].y =
54:          event->xbutton.y;
55:
56:    } else {
57:      (void)update_line(event, rubber_line);
58:      /*
59:      * 重新绘制橡皮筋线
60:      */
61:      GXRubberLine(rubber_line);
62:    }
63:  }
64:  }
```

在 `gx_line` 函数的定义中，你可以立即看到该函数是完全由事件驱动的——意味着根据指定的事件，`gx_line` 函数会采取适当的操作。

可以预期的每个事件的操作可以概括如下：

- 当接收到 `ButtonPress` 事件时，开始创建过程。
- 随后的 `ButtonPress` 事件会将事件点添加到 `rubber_line` 结构中包含的点数组中。
- 如果 `ButtonPress` 事件点与插入 `rubber_line` 结构中的上一个点相等，则表示发生了双击并结束创建。
- 当发生 `ButtonRelease` 或 `MotionNotify` 事件时，事件点将连接到点数组中最近添加的点上，并使用橡皮筋线进行绘制，以提供 Latex 行的交互式创建。

`gx_line` 函数首先测试作为函数唯一参数的事件引用的有效性：

![](img/786ba9bd5cd671beb490264fd2e6aae1_403_0.png)

## 第五部分 向编辑器添加对象

```c
5: if( event == NULL ) {
6:   rubber_line = NULL;
7: } else {
```

向 `gx_line` 函数传递 `NULL` 指针可以使局部变量 `rubber_line` 被重置，从而终止创建模式。这对于消除用户在启动另一个创建过程之前未能结束上一个过程的可能性是必要的。当为任何类型的对象启动新的创建过程时，传递 `NULL` 指针给 `gx_line` 函数能够让 `rubber_line` 被重置，从而终止创建模式。当 `ButtonPress` 事件发生时，如果 `rubber_line` 为 `NULL`，则将光标设置为 `LINE_MODE`（第 13 行所示）。

`point_event` 函数指示了这些点是否相等（第 18 行所示）。如果 `point_equal_event` 函数返回 `True`，表示点相等，通过擦除交互橡皮筋线并调用 `create_line` 函数（第 21-25 行）来结束创建过程。

然而，如果 `point_equal_event` 返回 `False`，表示点与上一个点不相等，则进入 `else` 分支，通过 `GXRubberLine` 重新绘制橡皮筋线（第 35 行所示）。

`gx_line` 函数随后将光标恢复为正常模式并清除 `rubber_line`（第 29-30 行所示）。

正如你可能记得的，光标控制函数在第 17 章“实用与工具”的“使用光标作为状态”中被引入。

当 `ButtonPress` 事件发生时，`gx_line` 函数会根据其指定的事件类型执行相应的操作（第 11 行所示）。

如果 `rubber_line` 为 `NULL`，则将光标设置为 `LINE_MODE`（第 13 行所示）。

![](img/786ba9bd5cd671beb490264fd2e6aae1_404.png)

在 `MotionNotify` 事件发生时，根据新点和鼠标的当前位置更新 `GXLine` 结构（第 42 行所示）。

如果 `rubber_line` 中有超过一个点，则将最后一个点替换为当前事件位置（第 50-54 行所示）。

如果 `rubber_line` 只有一个点，则调用 `update_line`（第 57 行所示）并重新绘制橡皮筋线（第 61 行所示）。

# Latex 线对象 第20章 385

```
5:
6: xe_x = event->xbutton.x;
7: xe_y = event->xbutton.y;
8:
/*
* 最后一个点将始终是当前的运动事件
* 所以检查上一个点以消除冗余（等同于
* 双击以结束动作） 
* */
13: if (line && line->num_pts > 2) {
14:     int num = line->num_pts - 2;
16:

17: if (abs(line->pts[num].x - xe_x) <= TOLERANCE) &&
18:     abs(line->pts[num].y - xe_y) <= TOLERANCE) {
19:

20:     pts_equal = True;
21: }
22:
23:     return pts_equal;
24: }
```

`point_equal` 函数必须在确定是否发生双击之前，确保数组中至少有三个点：

`14: if (line && line->num_pts > 2 ) {`

这是必要的，因为设置数组中最后一个点的不是 `ButtonRelease` 或 `MotionNotify`，而是用户。为了使线条创建有效，数组中必须至少有两个用户指定的点。

当数组中存在点数时，会将最后一个用户定义的点与事件点进行比较。如果它们之间差值的绝对值小于 `gxGraphics.h` 头文件中定义的 `TOLERANCE` (3)，则认为它们是等等的。

![](img/786ba9bd5cd671beb490264fd2e6aae1_407_0.png)
