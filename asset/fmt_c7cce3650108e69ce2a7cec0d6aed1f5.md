
首先，确定从正 x 轴（3 点钟位置）相对于向量 (`ex`, `ey`), (`cx`, `cy`) 以度为单位测量的角度：

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

接下来，考虑 `X` 用于决定的 `angle1` 和 `angle2` 测量值。正如你从第 7 章第 19 页“`XDrawArc`”节关于 `XDrawArc` 的信息中所记得的，`Y` 将这些角度以“度 × 64”的形式保持为整数。

```
45: angle1 = (double)angle_data->angle / 64.0;
46: angle2 = (double)arc_data->angle2 / 64.0;
```

最后，应用收集到的信息并查看弧是否被选中。

判断标准是：事件点到焦点的距离之和是否比主轴大了 `TOLERANCE`。如果是，则未选中弧。

分别考虑每种情况。首先 (`f1x`, `f1y`)：

```
48: if (sqrt(f1x - ex) + sqrt(f1y - ey) ) +
49: sqrt(f2x - ex) + sqrt(f2y - ey) > 2 * (hmaj + TOLERANCE)
50: return( False );
```

![](img/786ba9bd5cd671beb490264fd2e6aae1_244_0.png)

然后 (`f2x`, `f2y`)：

```
51: if (sqrt(f1x - ex) + sqrt(f1y - ey)) +
52:     sqrt(f2x - ex) + sqrt(f2y - ey)) < 2 * hmaj - TOLERANCE
53:     return( False );
```

如果差之和不大于，函数返回 `true`，表示事件点成功绘制了弧。

```
54: return( True );
```

## 拓展

### X 窗口系统的局限

`X` 窗口系统的局限性是无法绘制主轴和短轴不与 `x` 轴和 `y` 轴平行的椭圆。图 10.4 展示了这样一个椭圆。

## 图 10.4

在 `X` 中无法表示的椭圆。

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

无论类型如何，移动对象都需要应用光标移动的增量。在 Graphics Editor 中移动对象，首先选择对象并在移动光标时按住鼠标右键。光标移动的距离应用于对象的位置。对于数组对象，对象的位置是包含在数组中的点。然而，弧有一个显式的 `x`, `y` 值描述它们在画布中的位置。

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

应用于局部变量时，`static` 关键字确保它们的值在函数调用之间是残留（保持）的。这对 `line_move` 函数至关重要，因为它必须保留驱动移动对象位置的 `PointerMotion` 事件的 (`x`, `y`) 值。

然而，应用于函数声明时，`static` 仅限制了函数的可见性范围在该文件中。

静态变量 `x`, `y` 保留了 `X PointerMotion` 事件的坐标，允许将光标移动距离的增量应用于定义的点。

很快就会发现，赋值给 `x` 和 `y` 的值 `0` 对于判断何时开始移动很重要。

## 228 第三部分 回到学校

`x` 和 `y` 的非零值表示这不是移动动作的第一次迭代，这是一个重要点，因为必须从屏幕上擦除橡皮筋对象（`rubber-banding object`）。

```
9: XDrawLines( XtDisplay(GxDrawArea), XtWindow(GxDrawArea), rubberGC,
10: line_data->_pts, line_data->num_pts, CoordModeOrigin );
```

在 Graphics Editor 项目中，对象创建和变换期间使用的橡皮筋效果是指以交互模式绘制对象。允许用户在屏幕上移动对象时，画布上存在的其他对象不会因为交互模式下对象的绘制和擦除而消失。

- 复习第 4 章“窗口概念”中关于“Expose”节（第 122 页）讨论的 `X` 的即时图形特性。
- 为了防止误擦除画布上的其他对象，在第 7 章“Xlib 图形原语”节“GC 函数”（第 182 页）引入的 GC 函数 `gXxor` 被赋值为全局 GC `rubbergc`。

> `rubbergc` 图形内容将在第一次请求 `X` 原语时绘制对象，并在第二次请求时擦除，而不会损坏底层的背景或对象。

对使用 `GCFunction` 设置为 `gXxor` 的 GC 进行原语的调用次数必须非常小心（并进行仔细管理），因为调用奇数次会导致屏幕上显示生成的橡皮筋对象。
