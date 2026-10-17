
```cpp
void *data)

{
    texture = loader;
    this->sinfo = sinfo;
    this->scache = scache;
    this->data = data;
}

virtual 13d_plugin_environment *clone(void *e) {
    13d_plugin_environment *e = new 13d_plugin_environment(
        (loader, sinfo, scache, NULL);
    return e;
}
};

#endif
```

## 3D 中的平面

到目前为止，我们对 3D 平面的概念处理得相当随意。我们见过近 `z` 裁剪平面和投影平面，它们都是完全垂直的，位于沿 `z` 轴正方向的特定距离。现在，让我们看看如何泛化平面的概念，以包含任意方向。我们需要平面来针对任意平面执行 3D 多边形裁剪、碰撞检测以及 3D 图形学中的其他若干操作。

## 定义平面

从几何角度来说，正如我们之前提到的，你可以将平面认为在 3D 空间中任意方向的无限宽无限高、平坦且无限薄的 2D 表面。我们可以通过法向量和一个点来定义平面。法向量指定了平面的方向。具有特定方向的平面有无限多个。这就是点的目的：指定平面上的一个特定点，以将其与其他具有相同法向量的所有平面区分开。

> 图 7-27：法向量指定了平面的方向。

![](img/49715b3934121066e59e93823d33ee3a_500_0.png)

> 图 7-28：对于给定的法向量有无限多个平面。因此，我们必须指定一个法向量和一个平面上的点来唯一确定一个特定的平面。

![](img/49715b3934121066e59e93823d33ee3a_500_1.png)

在数学上，3D 平面的方程如下：

$$
Ax + By + Cz + D = 0
$$

该方程源于向量形式的形式：

$$
N \cdot P = N \cdot P_0
$$

在该方程中，$N$ 是平面的已知法向量 $[A,B,C]^T$，$P$ 是形式为 $[x,y,z]^T$ 的点，$P_0$ 是平面上的已知点 $[x_0,y_0,z_0]^T$。将法向量与点点积可以看作是法向量与从原点到点的向量的点积（回想第 5 章中点和向量之间关系的讨论）。此外，请记住两个向量的点积在几何上可以解释为第二个向量在第一个向量上的投影。因此，方程的向量形式表示，所有位于平面上的点都必须满足一个约束：从原点到点的向量在法向量上的投影必须是一个常数——具体来说，就是从原点到点的向量投影到法向量上得到的常数。

另一种方法，在平面的非向量形式中，$A, B, C$ 项是法向量。假设法向量已归一化，$D$ 是平面到原点沿法向量方向的符号距离。$D$ 的正值意味着沿法向量方向移动 $D$ 个单位到达原点；$D$ 的负值意味着沿法向量相反方向移动 $D$ 个单位到达原点。

![](img/49715b3934121066e59e93823d33ee3a_501_0.png)

> 图 7-29：平面方程中 A, B 和 D 的含义。

注意，如果你展开方程的向量形式，将所有项移到左侧并将常数标记为 $D$，就会得到非向量形式。

## 平面的面

平面有两个面：正面和背面。由于平面具有无限的宽高，它将整个 3D 空间分为两个区域：平面正面和背面。平面的正面是法向量指向侧；背面是另一侧。

通常我们有一个点，并希望确定该点是在平面正面还是背面。为了做到，我们只需对该点求平面方程。如果点是 $(x_p, y_p, z_p)$，我们计算 $Ax_p+By_p+Cz_p+D$。结果是一个标量。该标量的正负告诉我们点相对于平面的位置。如果是正数，则在平面正面；如果是负数，则在背面；如果恰好为零，则在平面上。

![](img/49715b3934121066e59e93823d33ee3a_502_0.png)

> 图 7-30：通过平面方程求出的平面正反。

这种方法有效的原因可以通过方程的向量形式来理解。对于平面上的所有点，从原点到点的向量在平面法向量上的投影会比平面上对应的投影长。同样，对于平面背面的所有点，投影会更短。$Ax_p+By_p+Cz_p$ 项是测试点的投影；通过加上 $D$，我们实际上减去了平面所有点的常数投影。如果减法结果为正，则点在平面正面；如果结果为负，则投影较短，点在背面。

## 13d_plane 类

我们使用 `13d_plane` 来表示任意方向的平面。

代码列表 7-22：`plane.h`

```cpp
#ifndef _PLANE_H
#define _PLANE_H

#include "../os/memman.h"
#include "../../system/sys_dep.h"
#include "../../math/vector.h"
#include "../point/point.h"
#include "../dynamics/collide.h"

#define EPSILON_PLANE float_to_13d_real(0.001)
#define CROSS_FRONT_TO_BACK 1
#define CROSS_BACK_TO_FRONT -1

class 13d_plane {
  public:
    13d_real a,b,c,d;

    void align_with_point_normal(const 13d_point&,
                               const 13d_vector&);
    void align_with_points(const 13d_point& p0,
                           const 13d_point& p1,
                           const 13d_point& p2);

    13d_real side_of_point(const 13d_point& p) const {
      return (13d_mulrr(a,p.X) +
              13d_mulrr(b,p.Y) +
              13d_mulrr(c,p.Z) +
              d);
    }

    13d_real intersection_t;
    13d_point intersection;

    int intersect_with_segment(const 13d_point& p0,
                                 const 13d_point& p1);
}

#endif
```

代码列表 7-23：`plane.cc`

```cpp
#include "plane.h"
#include "../tool_os/memman.h"

void 13d_plane::align_with_point_normal(const 13d_point&,
                                      const 13d_vector& normal) {
    a = normal.a[0];
    b = normal.a[1];
    c = normal.a[2];
    d = -a * p0.X - b * p0.Y - c * p0.Z;
}

void 13d_plane::align_with_points(const 13d_point& p0,
                                   const 13d_point& p1,
                                   const 13d_point& p2) {
    align_with_point_normal(p0, normalized(cross(p1-p0, p2-p0)));
}
```

# 480 第 7 章：3D 中的多边形建模与渲染

```cpp
dx, dy, dz;
```

```cpp
t_bottom = (13d_mulrr(a,(dx=p1_X_ - p0_X_)) + 
            13d_mulrr(b,(dy=p1_Y_ - p0_Y_)) +
            13d_mulrr(c,(dz=p1_Z_ - p0_Z_));
            
if(13d_abs(t_bottom) < 0) {
  return 0;
}

t_top = -1*(d + 
            13d_mulrr(a,p0_X_) + 
            13d_mulrr(b,p0_Y_) + 
            13d_mulrr(c,p0_Z_));
```

```cpp
intersection_t = 13d_divrrr(t_top, t_bottom);
intersection_X = 13d_mulrr(dx,intersection_t) + p0_X_;
intersection_Y = 13d_mulrr(dy,intersection_t) + p0_Y_;
intersection_Z = 13d_mulrr(dz,intersection_t) + p0_Z;
intersection_W = -int_to_13d_real(1);
```

```cpp
return (t_top>0 ? CROSS_BACK_TO_FRONT : CROSS_FRONT_TO_BACK);
```

变量 `a`, `b`, `c` 和 `d` 允许我们访问并修改平面中所见平面的系数。`align_with_normal` 方法接收平面上的一个点和一个法向量，并计算 `a`, `b`, `c` 和 `d` 系数。同样，`align_with_points` 接收三个平面上的点作为参数，其工作原理是将这三个点解释为顺时针方向的多边形顶点规格，通过叉积计算该多边形的法向量，并使用计算出的法向量和指定的点之一调用 `align_with_point_normal` 方法。

`side_of_point` 方法接收一个点作为参数，并使用给定点计算平面方程。如果点在平面前方，则返回正值；如果点在平面后面或在平面上，则返回负值。

> 注意：由于计算机精度计算的固有不准确性，当使用 `side_of_point` 评估时，平面上的点可能会返回接近非零的值。这种不准确性对于引入一个 `epsilon` 参数很有用，它的效果是让平面变得稍微“厚一点”。所有 `side_of_point` 返回值在 -epsilon 和 epsilon 之间的点都被认为在平面上。

`intersect_with_segment` 方法将平面与由两点 `p0` 和 `p1` 指定的直线相交。如果没有找到交点，如果找到了交点且 `p0` 在平面正面，则返回 1；如果找到了交点且 `p0` 在平面背面，则返回 -1。交点存储在变量 `intersection` 中。交点时间（一个范围从 0 到 1 的参数，代表从 `p0` 到 `p1` 的位移百分比）存储在变量 `intersection_t` 中。直线相交对于相对于任意平面的多边形裁剪（下文将介绍）以及碰撞检测（在伴随书籍《Advanced Linux 3D Graphics Programming》中介绍）非常有用。

## 第 7 章：3D 中的多边形建模与渲染

让我们来看 `intersect_with_segment` 方法是如何工作的。首先，我们考虑从 $p_0=(x_0, y_0, z_0)$ 到 $p_1=(x_1, y_1, z_1)$ 的直线的参数 $t_0$。

```cpp
x = x_0 + t(x_1 - x_0)
y = y_0 + t(y_1 - y_0)
z = z_0 + t(z_1 - z_0)
```

随着参数 $t$ 从 0 变化到 1，坐标从 $p_0$ 移动到 $p_1$。在这个范围之外，坐标移动到 $p_0$ 之前或超出 $p_1$ 之后。

接下来，我们将直线的 $x, y, z$ 值代入平面方程。这给出了与参数化定义的直线相交时的平面方程表达式。

$$
A(x_0 + t(x_1 - x_0)) + B(y_0 + t(y_1 - y_0)) + C(z_0 + t(z_1 - z_0))
$$

解方程求 $t$：

$$
t = -(D + Ax_0 + By_0 + Cz_0) / (A(x_1 - x_0) + B(y_1 - y_0) + C(z_1 - z_0))
$$

注意，如果 $t$ 的分母为 0，则参数化直线与平面不相交；直线“平行”于平面。计算 $t$ 后，我们可以将其代入直线的参数形式，以获得直线与平面之间的精确交点。

此方法计算由端点定义的无限直线与平面之间的交点。要计算有限线段与平面之间的交点，我们只需要检查计算出的 $t$ 值是否在 0 到 1 之间；如果不是，则交点位于无限直线的某处，在线段之外。`intersect_with_segment` 方法没有进行此测试，而是存储了交时间 $t$，以便调用程序决定做什么——某些情况下我们只想与线段相交；而在其他情况下则是整条直线。

## 任意 3D 平面的多边形裁剪

凭借与任意方向平面相交的能力，我们现在可以相对于任意 3D 平裁剪多边形。我们已经见过如何相对于由单个标量定义的近 `z` 平裁剪多边形。现在我们知道如何表示直线以及如何使线段（即多边形边）与这些平面相交。有了这些知识，任意平面裁剪多边形是一个简单的实现。

## l3d_polygon_clipable

`l3d_polygon_clipable` 类是一个可以相对于 3D 平裁剪的 3D 对象。成员变量 `plane` 存储多边形的 3D 平，并通过重写的 `init_transformed` 和 `transform` 方法更新。`clip_to_plane` 根据指定的 `clip_plane` 裁剪多边形的几何。此方法与我们看到的近 `z` 裁剪类似。我们使用平面的 `side_of_point` 方法寻找交叉边。使用 `intersect_with_segment` 方法与平面相交。然后按照惯例创建一个裁剪后的顶点列表并与主列表交换。平面的“内部”被定义为平面正面；正面内容被保留，其余的裁剪掉。

> 注意：将平面的某侧定义为“内部”并不适用于所有情况；这只是我们在实体建模（在《3D Graphics Programming》书中讨论）中倾向于将正面视为“外部”。当你看到平面的“内部””术语时，请记住该术语的含义。

注意 `clip_to_plane` 方法是虚函数，因为多边形类可能需要裁剪其他信息。在 3D 中裁剪纹理多边形需要像《3D Graphics Programming》书中描述的那样也裁剪坐标。在这种情况下，继承自多边形的纹理多边形类覆盖此方法。

### 列表 7-24: p3_clip.h

```cpp
#ifndef P3_CLIP_H
#define P3_CLIP_H
#include "../os/memman.h"
#define __ACTIVE_P3_CLIP_H
#include "poly3.h"
#include "../plane/plane.h"
#include "../dynamics/collide.h"

class l3d_polygonal_clipable {
    virtual l3d_polygonal_3d;
public:
    l3d_polygonal_clipable(void) :
    l3d_polygonal_clipable(int num_pts),
        l3d_polygonal_3d(num_pts),
        l3d_polygonal_2d(num_pts)
    {}
    virtual ~l3d_polygonal_clipable(void) {};
    l3d_plane;
    virtual int clip_to_plane(l3d_plane& clip_plane);
    void init_transformed(void);
    void transform(const l3d_matrix& m, int count);
    l3d_polygonal_clipable(const l3d_polygonal_clipable& r);
    l3d_polygonal_2d *clone(void);
};

#endif // __ACTIVE_P3_CLIP_H
#endif
```

### 列表 7-25: p3_clip.cc

```cpp
#include "p3_clip.h"
#include "../tool_os/memman.h"

int l3d_polygon_3dclip::clip_to_plane(l3d_plane& clip_plane) {
    int idx0, idx1;
    int crossededge0, crossededge1, crossededge1_idx0, crossededge1_idx1;
    int newvertex0, newvertex1;
    int i;
    int dir;

    idx0=0;
    idx1=next_clipidx_right(idx0, clip_ivertex->num_items);
    temp_clip_ivertex->num_items = 0;
    extends_behind_plane = 0;

    while (1) {
        if ((clip_plane.side_of_point((*vlist)[idx0].vertex.transformed) > 
            EPSILON_PLANE
            && clip_plane.side_of_point((*vlist)[idx1].vertex.transformed) < 
            -EPSILON_PLANE)
```
