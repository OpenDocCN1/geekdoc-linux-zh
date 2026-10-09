
让我们有一个平移 `T`、一个旋转 `R` 和一个点 `P`。如果我们认为矩阵乘法 `$TR$` 是先进行关于世界坐标系（WC）原点的旋转，然后在 WC 系统中进行平移。我们总是考虑变换相对于包含所有对象的最外层世界坐标系的影响。事实上，我们是相对于 WC 定义了所有变换。

矩阵乘法 `$TR$` 的另一种解释是想象所有的变换都在局部坐标系中进行，并且所有的变换都影响同一个局部坐标系。在在这种解释下，我们必须从左到右考虑矩阵的影响。我们从一个与世界坐标系对应的局部坐标系开始。然后，我们首先通过将局部坐标系移动到某个位置（最左侧的矩阵 `T`）来变换它。接下来，相对于变换后的坐标系，我们相对于变换后的坐标系原点进行旋转。进一步的变换，如缩放、进一步平移或进一步旋转，都被从左解释为改变局部坐标系的尺寸、位置或方向。局部坐标系的每次变换后，下一次变换在这个变换后的坐标系中进行。将变换解释为影响局部坐标系允许（实际上是强制）对矩阵进行从左到右的解释。

矩阵操作的从左到右解释对于思考层次变换（例如手臂层次结构的移动）非常有用。考虑一个手臂模型，其中有上臂、手和手指。层次结构的顶端是上臂。上臂的任何平移或旋转都应该变换连接在手臂上的东西——即层次结构中它下面的所有东西。这意味着当上臂移动时，前臂、手手指应该受到影响。同样，前臂的任何变换都应该变换手和手指；因此层次结构是上臂-前臂-手-手指。相对于世界坐标系，变换是从层次结构的最低级到最高级进行的。要移动手指，我们首先对手指应用所有旋转和平移，以使手指相对于手的变换（`$M_h$`）处于正确的位置，然后相对于前臂-手的变换（`$M_{arm}$`），最后相对于上臂的变换（`$M_u$`）。相对于世界坐标系，我们从右到左解释矩阵，因此手指的变换解释为 `$M_u M_{arm} M_h$`。但是，我们从左到右解释变换序列。首先，参考系是世界坐标。然后，我们使用 `$M_f$` 相对于上臂定义一个新的参考系。相对于新的参考系，我们随后从左到右指定相对于前臂（`$M_f$`）和手（`$M_h$`）的参考系。最后，以手为参考系，通过 `$M_f$` 在该参考系中指定手指的位置。

- 要从右到左解释一系列矩阵 `$ABCD$`，请想所有变换都是在世界坐标系中进行的。从右侧的每个后续矩阵都会导致手指相对于世界坐标的变换：移动到世界坐标系中由 D 指定的位置，然后移动到 C，然后移动到 B，最后进一步到 A。要从左到右解释，请想所有变换都是在一个不断变化的参考系中进行的。首先，从世界坐标系的框架观察世界。通过这个窗口，将 A 应用到你的参考系中，从 A 观察世界。然后应用 B 从 B 观察世界，最后应用 D 从 D 观察世界。最后，使用这个累积的参考系来指定坐标。

总结一下：从右到左的解释将局部坐标系中指定的坐标转换为世界坐标系中的坐标。从左到右的解释将整个世界坐标系转换为局部坐标系。

如果这让你感到困惑，我建议采用矩阵操作的从左到右的解释，即所有变换都是相对于包含所有对象的全局坐标系进行的。

## 第 6 章：矩阵与变换

391

## 总结

在本章中，我们研究了变换和矩阵。我们看到了如何从数学上处理矩阵，以及如何从几何上应用矩阵来实现平移、旋转和缩放。我们看到了如何组合变换来实现复杂的运动，例如关于任意轴的旋转或任意相机移动。示例程序演示了复杂的对象运动以及可以自由放置的相机。

## 第 7 章

3D 中的多边形建模与渲染

## 概述

本章将详细探讨 3D 多边形，它是现代 3D 图形的基础。第 3 章已经涵盖了 2D 多边形图形，第 5 章和第 6 章使用了特殊的结构来存储 3D 多边形数据。在本章中，我们将详细查看 3D 多边形的存储、操作和绘制。我们将涵盖以下主题：

- 使用 3D 多边形的原因
- 3D 多边形的几何结构，包括法线向量、3D 裁剪和平面
- 将多边形分组为 3D 对象，并将对象分组为世界（world）

本章在风格上与之前的章节有所不同。第 5 章和第 6 章侧重于理论，而代码相对较少；本章的第一部分则非常侧重于代码，而理论部分相对容易理解。“将多边形分组以形成 3D 对象”这一描述在理论上足够简单，但在编写用于 3D 对象的 C++ 代码时，必须解决许多实际问题。因此，本章第一部分的重点是理解 3D 多边形的结构和几何属性，并在 I3 库中设计适当且可重用的 C++ 类，用于 3D 多边形的建模和分组。承认设计和实现 3D 多边形对象所需的类确实有些枯燥。这些问题主要是结构性的：决定何时需要临时列表、提供在帧开始时重置列表的方法、避免顶点错误的双重变换、使用链表节省顺序搜索时间等。这项工作通过提供灵活的对象结构得到了回报。

本章介绍了以下示例程序：`clipz` 展示了近裁剪裁剪（near z clipping），`fltsim` 展示了如何创建具有子类和插件行为的多边形 3D 对象，`objcopy` 展示了如何使用对象拷贝构造函数和平面裁剪将一个对象分成两个独立的部分。

## 3D 多边形建模的原因

从第 3 章开始我们一直在使用多边形，在第 3 章中我们定义了 2D 多边形的意义，并开发了绘制多边形的例程。在第 5 章和第 6 章中，我们将多边形的顶点从 3D 投影到 2D，这使得我们能够通过将 3D 多边形投影为 2D 多边形来存储和查看 3D 多边形数据，然后使用第 3 章的例程进行绘制。现在，是时候关注 3D 多边形建模和渲染的细节了。

3D 多边形是在 3D 空间中任意方向和位置的 2D 多边形。这意味着 3D 多边形是 3D 空间中一个平坦的有边界的区域。所谓“平坦”，是指属于多边形的所有点必须位于一个上；我们将在本章稍后用数学方法定义平面的意义。3D 多边形与 2D 多边形的面积由一系列连接的边边界。

![](img/49715b3934121066e59e93823d33ee3a_418_0.png)

通过使用一系列微小且位置略不同的平坦多边形，我们可以描述或至少近似 3D 空间中的任何表面。对于曲面，多边形数量越多，近似效果越好。见图 7-2。

![](img/49715b3934121066e59e93823d33ee3a_418_1.png)

在交互式 3D 图形中，我们通常只对对象的表面进行建模，因为外表面是我们看到不透明对象的所有部分。这意味着当使用 3D 多边形技术时，对象的内部通常不被建模。相反，我们描述的是对象无限薄的外部表面。当我们想要打开或切除对象的部分以查看其内部时，表面建模显示出它的它的局限性。在这种情况下，如果我们只用多边形对对象的表面进行建模，我们将看到一个空空的物体模型，就像这个对象是由纸板制成的但内部是空的。见图 7-3。

## 第 7 章：3D 中的多边形建模与渲染

![](img/49715b3934121066e59e93823d33ee3a_419_0.png)

> 图 7-3：如果一个 3D 多边形对象被切开，就会明显地看出只有表面被建模了，而内部是空的。

尽管有这种局限性，3D 多边形提供了一种相当通用、直接且快速的描述 3D 表面的方法。假设我们只想对表面进行建模——这通常是本书所涉及的交互式 3D 图形应用的情况——多边形通常是最佳选择。它们在数学上描述简单，在概念上容易理解，这使得编写和理解操作及渲染多边形的算法变得相对容易。3D 多边形的简单性允许对 3D 多边形的常用操作进行广泛的硬件加速。现代 3D 加速硬件能够每秒向屏幕绘制惊人数量的多边形，使得可以在可以接受的运行性能下实现高视觉复杂度。

3D 多边形的替代方案包括对曲面建模，或者作为体素（voxels，volume pixels 的缩写）的体积表示，而仅仅是表面表示。图 7-4。使用曲面的数学描述代替平坦多边形可以更准确地表示现实世界的曲面，这些曲面在任何放大倍下看起来仍然是圆的。使用多边形，如果观察者距离对象足够近，多边形固有的扁平性就会变得明显。

## 第 7 章：3D 中的多边形建模与渲染

```cpp
virtual void init_transformed(void);
virtual void transform(const l3d_matrix &m, int count);
virtual void set_transform_stage(int count);
virtual void after_camera_transform(void);

void camera_transform(const l3d_matrix &m, int count) {
    transform(m);
    after_camera_transform();
}
```

```cpp
virtual void clip_segment_to_near_z(l3d_polygon_vertex *vertex, l3d_real zclip, int idx0, int idx1);
virtual void clip_near_z(l3d_real zclip);
virtual void draw(l3d_rasterizer_3d *r);
l3d_polygon_3d(const l3d_polygon_3d &r);
l3d_polygon_2d *clone(void);
```

```cpp
struct l3d_polygon_3d_node {
    l3d_polygon_3d *polygon;
    l3d_polygon_3d *prev = nullptr;
    l3d_polygon_3d *next = nullptr;
};
```

```cpp
#include "../raster/rast3.h";

#endif
```

## 列表 7-2: poly3.cc

```cpp
#include "poly3.h"
#include <string.h>
#include "../tool_os/memman.h"
```

```cpp
void l3d_polygon_3d::init_transformed(void) {
    sfcnormal.reset();
    center.reset();
}
```

```cpp
void l3d_polygon_3d::compute_epsilon() {
    l3d_real collinear_epsilon = float_l3d_real(0.999);
    int found_noncollinear_points = 0;
    int p0, p1, p2;
    for (p0 = 0; p0 < vertices->num_items; p0++) {
        p1 = p0 + 1;
        if (p1 >= vertices->num_items) p1 = 0;
        p2 = p1 + 1;
        if (p2 >= vertices->num_items) p2 = 0;

        l3d_vector v1 = vertices[p1].vertex.original - vertices[p0].vertex.original;
        l3d_vector v2 = vertices[p2].vertex.original - vertices[p0].vertex.original;

        // 如果向量之间的角度接近 0 或 180 度，它们
        // 几乎在同一条直线上，因此我们选择下一个3 个点
        if (l3d_abs(dot(normalized(v1), normalized(v2))) < l3d_real(collinear_epsilon)) {
            sfcnormal.original = center.original + normalized(cross(v1, v2));
            found_noncollinear_points = 1;
        }
    }
}
```

```cpp
void l3d_polygon_3d::compute_center() {
    l3d_real xsum = 0, ysum = 0, zsum = 0;
    int i;

    for (i = 0; i < vertices->num_items; i++) {
        xsum += ((vertex*)vertices[i].vertex).original.X;
        ysum += ((vertex*)vertices[i].vertex).original.Y;
        zsum += ((vertex*)vertices[i].vertex).original.Z;
    }

    center.original_set(
        l3d_divri(xsum, i),
        l3d_divri(ysum, i),
        l3d_divri(zsum, i),
        int_to_l3d_real(1)
    );
}
```

```cpp
void l3d_polygon_3d::clip_segment_to_near_z(
    l3d_polygon_vertex vertex, l3d_real zclip, int idx0, int idx1) {
    l3d_real x0, y0, z0, x1, y1, z1, t, clip_x, clip_y, clip_z;

    if (((vertex*)vertices[idx0].vertex).transformed.Z > zclip) {
        x0 = ((vertex*)vertices[idx0].vertex).transformed.X;
        y0 = ((vertex*)vertices[idx0].vertex).transformed.Y;
        z0 = ((vertex*)vertices[idx0].vertex).transformed.Z;
    }
    if (((vertex*)vertices[idx1].vertex).transformed.Z > zclip) {
        x1 = ((vertex*)vertices[idx1].vertex).transformed.X;
        y1 = ((vertex*)vertices[idx1].vertex).transformed.Y;
        z1 = ((vertex*)vertices[idx1].vertex).transformed.Z;
    } else {
        x0 = ((vertex*)vertices[idx0].vertex).transformed.X;
        y0 = ((vertex*)vertices[idx0].vertex).transformed.Y;
        z0 = ((vertex*)vertices[idx0].vertex).transformed.Z;
    }

    t = l3d_divr(zclip - z0, z1 - z0);
    clip_x = x0 + l3d_mulr(x1 - x0, t);
    clip_y = y0 + l3d_mulr(y1 - y0, t);
    clip_z = z0 + l3d_mulr(z1 - z0, t);

    int new_idx = vertex_index();
    ((vertex*)vertices[new_idx].vertex).transformed.stage = 0;
    ((vertex*)vertices[new_idx].vertex).original.X = clip_x;
    ((vertex*)vertices[new_idx].vertex).original.Y = clip_y;
    ((vertex*)vertices[new_idx].vertex).original.Z = clip_z;
    ((vertex*)vertices[new_idx].vertex).original.W = int_to_l3d_real(1);
    vertex = vertices[new_idx].vertex;
}
```
