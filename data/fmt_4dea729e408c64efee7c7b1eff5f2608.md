
```
atan2( cy - ey, ex - cx ) * 180/M_PI
```

> 注意
>
> 常数 `M_PI` 定义为
>
> `#define M_PI 3.1415926535897923846`
>
> 它在计算由椭圆中心点和事件点定义的向量角度时，作用是将 `atan2` 返回的弧度值转换为 `-M_PI` 到 `M_PI` 范围内的度。

```
41: angle = atan2( cy - ey, ex - cx ) * 180/M_PI;
```

如果角度小于零，则旋转 360 度：

```
42: if (angle < 0)
43: angle += 360;
```

接下来，考虑 X 用于决定的 `angle1` 和 `angle2` 测量值。正如你从第 7 章第 19 页“XDrawArc”节关于 `XDrawArc` 的信息中所记得的，Y 将这些角度以“度 × 64”的形式保持为整数。

```
45: angle1 = (double)angle_data->angle / 64.0;
46: angle2 = (double)arc_data->angle2 / 64.0;
```

最后，应用收集到的信息并查看弧是否被选中。

判断标准是：事件点到焦点的距离之和是否比主轴大了 `TOLERANCE`。如果是，则未选中弧。

分别考虑每种情况。首先 `(f1x, f1y)`：

```
48: if (sqrt(f1x - ex) + sqrt(f1y - ey) ) +
49: sqrt(f2x - ex) + sqrt(f2y - ey) > 2 * (hmaj + TOLERANCE)
50: return( False );
```

![](img/786ba9bd5cd671beb490264fd2e6aae1_244_0.png)

然后 `(f2x, f2y)`：

```
51: if (sqrt(f1x - ex) + sqrt(f1y - ey)) +
52:     sqrt(f2x - ex) + sqrt(f2y - ey)) < 2 * hmaj - TOLERANCE
53:     return( False );
```

如果差之和不大于，函数返回 true，表示事件点成功绘制了弧。

```
54: return( True );
```

## 拓展

### X 窗口系统的局限

X 窗口系统的局限性是无法绘制主轴和短轴不与 x 轴和 y 轴平行的椭圆。图 10.4 展示了这样一个椭圆。

## 图 10.4

在 X 中无法表示的椭圆。

![](img/786ba9bd5cd671beb490264fd2e6aae1_244.png)

一种解决方案是使用 Bézier 算法将椭圆转换为线段，然后像数组对象一样处理它。通过选择数组对象和弧对象的这种方法，你准备好执行几何操作。

## 后续步骤

第 11 章“图形变换”引入并满足了移动、缩放和旋转操作的要求。理解这些操作（称为几何变换）将带你完成最后几章精心设计的布局。

## 第 11 章：

- 移动
- 缩放
- 旋转
- 后续步骤

## 图形变换

我们已经学习了准确判断 Graphics Editor 中画布上被选中对象的计算，现在我们将注意力转移到应用于已选中对象的操作。

图形变换，如术语所示，是改变图形的操作。编辑器支持修改对象的 `move`、`scale` 和 `rotate` 函数。这些将在接下来的章节中讨论。正如分析正确选择时所需的，对数组对象和弧进行单独考虑。

## 移动

无论类型如何，移动对象都需要应用光标移动的增量。在 Graphics Editor 中移动对象，首先选择对象并在移动光标时按住鼠标右键。光标移动的距离应用于对象的位置。对于数组对象，对象的位置是包含在数组中的点。然而，弧有一个显式的 `x, y` 值描述它们在画布中的位置。

### 移动线条

列表 11.1 展示了 Graphics Editor 如何跟踪并应用光标的距离。虽然 `GXObj` 尚未定义，但你从第 9 章“Object Bounds”中的列表 9.2 中知道 `GXLine` 结构的定义。该结构为类型为 `line` 的 `GXObj` 提供唯一的数据字段。`GX` 结构见第 9 章第 204 页“Point-Array-Based Object Bounds”。

#### 列表 11.1 `line_move` 函数

```
static void line_move(GXObjPtr line, XEvent * event )
{
    int x = 0, y = 0;
    GXLinePtr line_data = (GXLinePtr)line->data; int i;
    if(x && y) {
        XDrawLines(XtDisplay(GxDrawArea), XtWindow(GxDrawArea), rubberGC,
            line_data->pts, num_pts, CoordOrigin);
    } else {
        /* 第一次执行 */
        (*line->erase)( line);
        x = event ? event->button.x : 0;
        y = event ? event->button.y : 0;
    }
    if ( event ) {
        for(i = 0; i < line_data->num_pts; i++) {
            line_data->pts[i].x += (event->button.x - x);
            line_data->pts[i].y += (event->button.y - y);
        }
    }
    /** 绘制橡皮筋 */
    XDrawLines(XtDisplay(GxDrawArea), XtWindow(GxDrawArea), rubberGC,
        line_data->pts, num_pts, CoordOrigin);
    x = event->button.x;
    y = event->button.y;
} else {
    x = 0;
    y = 0;
}
}
```

列表 11.1 中的 `line_move` 函数首先声明了局部静态变量：

```
3:    static int x = 0, y = 0;
```

## 拓展

### `static` 关键字有多种用途

对比 `static` 关键字应用于局部变量与在 `line_move` 函数声明中的用法：

```
1:    static void line_move
```

请参第 3 章第 103 页关于 `static` 关键字的讨论。

应用于局部变量时，`static` 关键字确保它们的值在函数调用之间是残留（保持）的。这对 `line_move` 函数至关重要，因为它必须保留驱动移动对象位置的 `PointerMotion` 事件的 `(x, y)` 值。

然而，应用于函数声明时，`static` 仅限制了函数的可见性范围在该文件中。

静态变量 `x, y` 保留了 X `PointerMotion` 事件的坐标，允许将光标移动距离的增量应用于定义的点。

很快就会发现，赋值给 `x` 和 `y` 的值 `0` 对于判断何时开始移动很重要。

### 228 第三部分 回到学校

`x` 和 `y` 的非零值表示这不是移动动作的第一次迭代，这是一个重要点，因为必须从屏幕上擦除橡皮筋对象（rubber-banding object）。

```
9: XDrawLines( XtDisplay(GxDrawArea), XtWindow(GxDrawArea), rubberGC,
10: line_data->_pts, line_data->num_pts, CoordModeOrigin );
```

在 Graphics Editor 项目中，对象创建和变换期间使用的橡皮筋效果是指以交互模式绘制对象。允许用户在屏幕上移动对象时，画布上存在的其他对象不会因为交互模式下对象的绘制和擦除而消失。

- 复习第 4 章“窗口概念”中关于“Expose”节（第 122 页）讨论的 X 的即时图形特性。
- 为了防止误擦除画布上的其他对象，在第 7 章“Xlib 图形原语”节“GC 函数”（第 182 页）引入的 GC 函数 `gXxor` 被赋值为全局 GC `rubbergc`。

> `rubbergc` 图形内容将在第一次请求 X 原语时绘制对象，并在第二次请求时擦除，而不会损坏底层的背景或对象。

对使用 `GCFunction` 设置为 `gXxor` 的 GC 进行原语的调用次数必须非常小心（并进行仔细管理），因为调用奇数次会导致屏幕上显示生成的橡皮筋对象。

如果 `x` 和 `y` 的值为 `0`，则这是移动请求的第一次迭代，此时会进入 `else` 分支。在 `else` 体中，调用了 `GXobj` 的 `erase` 方法将对象从画布上清除。它会立即使用 `rubbergc` 在交互（非破坏性）模式下重新绘制。

```
11: else {
12: /* 我们的第一次通过 /
13: (*line->erase) ( line );
14:
15: x = event ? event->button.x : 0;
16: y = event ? event->button.y : 0;
17: }
```

在 `else` 体中，调用对象的 `erase` 方法会将对象从画布上移除，如果存在 `PointerMotion` 事件，则将 `x` 和 `y` 的值设置为该事件的坐标。

## 图形变换 第11 章 229

虽然直到第 15 章“通用对象定义”才介绍具体的 `Gxobj` 定义，但可以说，一个对象将具有方法（内部函数），用于完成与其对象类型相关的所有自我管理任务。

对象方法包括绘制、擦除、移动、缩放、旋转、复制、保存、恢复和删除的函数。

也许第 15 章的标题可以叫作“驴不对马嘴”。

对象的擦除方法与用于管理橡皮筋效果的 X 原语 `XDrawLine` 调用不兼容。

这种不兼容性源于在屏幕上绘制对象时使用的 GC 函数的差异。

所有用于绘制的 `Gxobj` 方法例如 `GCcopy` 函数，该函数无法通过 `GCxor` 函数进行擦除或撤销。

- 如第 20 章“后期 Latex 对象”所示，第 7 章“X Lib 图形原语”节“GCTile”（第 188 页）引入的，使用 `GCcopy` 放置在屏幕上的对象的擦除方法是：对当前擦除对象所在的画布背景进行平铺填充（tile）。

## 游离

### 一种新的 if then else 结构形式

C 语言语法

```
var = test ? value1 : value2;
```

等同于

```
if( test )
  var = value1;
  else
  var = value2;
```

虽然这种写法并不清晰或易读，但它在 C 程序员中非常常见。

测试 `event` 的隐式非空值的必要性是为了考虑到变换函数 `line_move` 可能会被中断或擦除。

为了终止或移动动作，会将空事件指针传递给 `line_move` 函数，允许它将 `x` 和 `y` 的值重置为 `0`，以便另一个对象重新开始变换。

## 230 第三部分 回到学校

非空事件的隐式测试紧随 `x` 和 `y` 值为 `0` 时进入的 `else` 体之后。

隐式测试的形式如下：

```
if( variablePtr )
```

C 将此解释为对非零值的测试。`NULL` 在 C 中定义为 `#define NULL (unsigned long)` 或 `#define NULL (0)`。该测试与指针变量及非指针变量兼容。

显式测试明显优于隐式测试，因为可以防止语义错误并使测试更具可读性。如短语所示，显式测试显式地测试预期值。上述示例的等效显式测试为：

```
if( variablePtr != NULL )
```

如所述，发送空事件指针会导致函数重置 `x` 和 `y` 的值，以便动作可以：

```
19: if ( event ) {
20: for( i = 0; i < line_data->num_pts; i++) {
21: line_data->pts[i].x += (event->button.x - x);
22: line_data->pts[i].y += (event->button.y - y);
23: }
```

如果存在有效的事件指针，则当前事件位置的差异应用到 `line_data->pts` 数组中的每个点。在更新所有点后，对象被隐式地放置在新位置，并使用全局变量 `rubberGC` 在屏幕上绘制橡皮筋对象。

```
28: XDrawLines(XtDisplay(GxDrawArea), XtWindow(GxDrawArea), rubberGC,
29: line_data->pts, line_data->num_pts, CoordModeOrigin );
```

随着橡皮筋对象的绘制到屏幕上，必须保留其位置，以便后续调用可以擦除它。

```
31: x = event->button.x;
32: y = event->button.y;
```

当 `line_move` 函数被调用时，通过增加差值来更新位置。

## 移动圆弧

移动对象的方法比基于点的对象更简单，因为它是通过 `x` 和 `y` 字段显式赋值的。示例 11.2 显示了对圆弧进行变换。

### 11.2 `arc_move` 函数

```
1: /*
   * arc_move
   */
4: static void arc_move(GxPtr, XEvent *event)
5: {
6:     static int x = 0, y = 0;
7:     XArc *arc_data = (XArc *)arc;
8: 
9:     if (x && y) {
10:         /*
11:          erase the rubberband arc
12:         */
13:         XDrawLines(XtDisplay(GxDrawArea), XtWindow(GxDrawArea), rubberGC,
14:             arc_data->x, arc_data->y,
15:             arc_data->width, arc_data->height,
16:             arc_data->angle1, arc_data->angle2);
17:     }
18:     } else {
19:         /*
20:          * 我们的第一次通过 / erase actual arc
21:         */
22:         (arc->erase)(arc);
23: 
24:         /*
25:          * store the event location
26:         */
27:         x = event ? event->button.x : 0;
28:         y = event ? event->button.y : 0;
29:     }
30: 
31:     if (event) {
32:         /*
33:          * get the x,y delta
34:         */
35:         arc_data->x += (event->button.x - x);
36:         arc_data->y += (event->button.y - y);
37: 
38:         /*
39:          * draw a rubberband arc
40:         */
```

### 11.2 XArc 延续

```
41: XDrawArc(XtDisplay(GxDrawArea), XtWindow(GxDrawArea), rubberGC,
42:     arc_data->x, arc_data->y,
43:     arc_data->width, arc_data->height,
44:     arc_data->angle1, arc_data->angle2 );
45:
46:     x = event->button.x;
47:     y = event->button.y;
48:  } else {
49:      x = 0;
50:      y = 0;
51:  }
52: }
```

示例 11.2 中的 `arc_move` 函数除了这几行外，与 `line_move` 函数完全相同，只是管理的数据类型是 `XArc` 而不是 `GXLine`。

## 缩放

缩放变换是指改变对象的高度和宽度。

对于许多对象，宽度高度值仅引用对象边界定义的值。更改对象边界的宽度会影响组成对象的每个部分，因为它们必须按比例调整以完成或获得新的边界。

缩放对象的挑战在于，`x` 和 `y` 差值（与移动变换一样，通过计算当前与之前的差值来确定）

（之前的事件位置）并不是线性地应用到对象上的。相反，必须考虑缩放操作的方向，并将增量（delta）的大部分应用于与缩放方向对应的一侧，而不是对立侧。

图形编辑器对通过选择过程创建的对象应用了八个句柄。

图 11.1 和图 11.2 展示了句柄分别放置在直线（Line）和弧（Arc）对象上。

## 图 11.1

插图直线对象的句柄。

![](img/786ba9bd5cd671beb490264fd2e6aae1_255_0.png)

## 图 11.2

插图弧对象的句柄。

![](img/786ba9bd5cd671beb490264fd2e6aae1_255_1.png)

当用户选择对象时，对象句柄的放置如图 11.1 和 11.2 所示，对应于对象的每一个角和每一边。

当用户选择对象显示其句柄、将鼠标光标置于所需的句柄上并按下左鼠标键选择句柄时，就会触发缩放操作。

只要按住左鼠标键，后续的 `PointerMotion` 事件将以相对于所选句柄的方式改变对象的宽度或高度。

当释放鼠标键时，对象将根据新尺寸重新绘制。
