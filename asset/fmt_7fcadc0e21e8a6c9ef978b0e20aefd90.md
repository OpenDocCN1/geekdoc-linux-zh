
```cpp
#include <stdlib.h>
#include <stdio.h>

#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/dispatch.h"
#include "../lib/raster/rasterizer.h"
#include "../lib/tool_2d/scrinfo.h"
#include "../lib/system/factories.h"

#include "../lib/geom/point/point.h"
#include "../lib/math/vector.h"
#include "../lib/math/matrix.h"

#define MAXSPIKES 150
#define PI 3.14159265

unsigned long red_color;
unsigned long green_color;
unsigned long blue_color;

// STEP 1: 选择工厂
void choose_factories(void) {
    factory_manager_v_0.choose_factories();
}

// STEP 2: 声明一个流水线子类
13d_real fovx, fovy;
int xsize, ysize;

class spike {
public:
    13d_two_part_list<13d_coordinate>* vlist;
    13d_polygon_2d_flatshaded *faces[3];
    13d_vector displacement;

    int rx, ry, rz, drx, dry, drz;
    13d_vector velocity;

    spike(void) {
        // 为所有多边形声明公共顶点列表
        vlist = new 13d_two_part_list<13d_coordinate>(4);
        int i = 0;
        (*vlist[i]).original.set(int_to_3d_real(0),
            int_to_3d_real(0),
            int_to_3d_real(100),
            int_to_3d_real(1));
        (*vlist[i++]).original.set(int_to_3d_real(10),
            int_to_3d_real(10),
            int_to_3d_real(100),
            int_to_3d_real(1));
        (*vlist[i++]).original.set(int_to_3d_real(10),
            int_to_3d_real(0),
            int_to_3d_real(100),
            int_to_3d_real(1));
        (*vlist[i++]).original.set(int_to_3d_real(0),
            int_to_3d_real(0),
            int_to_3d_real(0),
            int_to_3d_real(1));

        // 使用顶点列表的索引定义多边形
        faces[0] = new 13d_polygon_flatshaded(3);
        faces[0]->vlist = vlist; // 共享顶点列表
        faces[0]->vertices[0].vertex = 3;
        faces[0]->vertices[1].vertex = 0;
        faces[0]->vertices[2].vertex = 1;

        faces[1] = new 13d_polygon_flatshaded(3);
        faces[1]->vlist = vlist; // 共享顶点列表
        faces[1]->vertices[0].vertex = 3;
        faces[1]->vertices[1].vertex = 1;
        faces[1]->vertices[2].vertex = 2;

        faces[2] = new 13d_polygon_flatshaded(3);
        faces[2]->vlist = vlist; // 共享顶点列表
        faces[2]->vertices[0].vertex = 3;
        faces[2]->vertices[1].vertex = 2;
        faces[2]->vertices[2].vertex = 0;
    }

    ~spike(void) {
        delete faces[0];
        delete faces[1];
        delete faces[2];
        delete vlist;
    }

    void spike(void) {
        displacement.set(int_to_3d_real(rand() % 2000),
            int_to_3d_real(rand() % 2000),
            int_to_3d_real(100 + rand() % 1000),
            int_to_3d_real(1));
        velocity.set(int_to_3d_real(rand() % 10 - 5),
            int_to_3d_real(rand() % 10 - 5),
            int_to_3d_real(rand() % 10 - 5));

        rx = ry = rz = 0;
        drx = (rand() % 16 - 8);
        dry = (rand() % 16 - 8);
        drz = (rand() % 16 - 8);
    }

    void move_spike(void) {
        displacement = displacement + velocity;
        rx = rx + drx;
        if (rx < 0) rx += 360;
        if (rx >= 360) rx -= 360;
        ry = ry + dry;
        if (ry < 0) ry += 360;
        if (ry >= 360) ry -= 360;
        rz = rz + drz;
        if (rz < 0) rz += 360;
        if (rz >= 360) rz -= 360;
    }

    void transform(void) {
        matrix t = 13d_mat_translate(displacement.a[0], displacement.a[1], displacement.a[2]) |
            13d_mat_rotz(rz) | 13d_mat_rotx(ry) | 13d_mat_rotx(rx);
        for (int q = 0; q < vlist->num_fixed_items; q++) {
            (*vlist[q]).reset();
            (*vlist[q]).transformed = t * (*vlist[q]).transformed;
        }
    }

    void project_spike() {
        for (int v = 0; v < vlist->num_fixed_items; v++) {
            (*vlist[v]).transformed.X_ = 13d_mulri(13d_mulrr_divrr(*(*vlist)[v].transformed.X_), (*(*vlist)[v].transformed.Y_), (*(*vlist)[v].transformed.Z_));
        }
    }
};
```

# 346 第 6 章：矩阵与变换

```cpp
void my_pipeline::key_event(int ch) {
  switch(ch) {
    case 'q':
      exit(0);
    }
}

void my_pipeline::update_event() {
  int i;
  for(i=0;i<numspikes;i++) {
    spikes[i].move_spike();
    if(out_of_wc_bounds(spikes[i].vlist[0].transformed)) {
      // out_of_wc_bounds(spikes[i].vlist[1].transformed)
      // out_of_wc_bounds(spikes[i].vlist[2].transformed)
      // out_of_wc_bounds(spikes[i].vlist[3].transformed)
      // 我们必须检查尖刺的所有顶点，因为它的方向
      // 不是任意的，任何一个点都可能是最先
      // 越出边界的前端点
      spikes[i].place_spike();
    }
  }
}

void my_pipeline::draw_event(void) {
  int i;
  r->clear_buffer();

  for(i=0;i<numspikes;i++) {
    for(int f=0;f<3; f++) {
      spikes[i].faces[f]->init_clip_vertices();
      spikes[i].faces[f]->clip_to_polygon_2d(s->win_win);
      r->draw_polygon_fragmented(spikes[i].faces[f]);
    }
  }
  s->blit_screen();
}

int my_pipeline::out_of_wc_bounds(l3d_point const &p) {
  return(p.z<int_to_l3d_real(1));
}

int main(int argc, char **argv) {
  choose_factories();

  l3d_dispatcher *d;
  my_pipeline *p;

  // 步骤 3：创建一个分发器

  d = factory_manager_v_0_1.dispatcher_factory->create();

  // 步骤 4：创建一个流水线
```

# 第 6 章：矩阵与变换

```cpp
// 将我们的自定义行为流水线接入分发器
p = new_my_pipeline();
```

```cpp
// 步骤 5：启动分发器
d->pipeline = p; // 多态赋值
d->event_source = p->s;
d->start();
```

```cpp
delete d;
delete p;
}
```

![](img/49715b3934121066e59e93823d33ee3a_371_0.png)

让我们看看相对于第 5 章原始尖刺（`spikes`）程序的变化。首先，我们声明了一些变量来存储每个尖刺的旋转角度以及旋转速度。

`int rx, ry, rz, drx, dry, drz;`

接下来，在 `place_spike` 和 `move_spike` 中，我们分别初始化和更新旋转变量。然后，我们使用代表旋转的旋转角度和代表平移的位移向量，使用 `d3d_mat_` 函数构建适当变换矩阵。我们使用矩阵乘运算符 `|` 将所有这些旋转矩阵相乘，并将结果存储在复合矩阵变量 `transform` 中。

```cpp
transform =
d3d_mat_translate(displacement.a[0],
displacement.a[1],
displacement.a[2]);
```

```cpp
d3d_mat_rotz(rz) | d3d_mat_rotx(ry) | d3d_mat_rotx(rx);
```

在计算出包含三个旋转的组合变换矩阵后，我们通过将矩阵与点相乘，将变换矩阵应用于尖刺中的每个点。在第 5 章的原始尖刺程序中，我们只是为尖刺的位置加上位移向量。在这里，我们将通用变换矩阵与尖刺的位置相乘，一次性应用多个变换。

```cpp
for(q=0; q<vlist->num_fixed_items; q++) {
  (*vlist)[q].reset();
  (*vlist)[q].transformed = transform | (*vlist)[q].transformed;
}
```

# 第 6 章：矩阵与变换

最后，我们还必须更改尖刺的越界检查。在第 5 章中，我们只是检查了三号顶点来判断它是否越界。这是因为顶点具有固定的方向，我们知道三号顶点始终是最靠近相机的前端顶点（记得，相机位于原点）。此外，由于尖刺只能向前移动，我们在第 5 章中知道该顶点将是第一个越出边界的。然而，在新的 `rotspikes` 程序中，这些假设不再成立了。尖刺可能具有任意的方向；尖刺的四个顶点中的任何一个都可能是前端，因此，需要对四个顶点中的任何一个进行扩展，以检查尖刺的所有顶点，从而确定尖刺是否需要重新定位。

```cpp
spikes[i].move_spike();
if(out_of_wc_bounds(spikes[i].vlist[0].transformed) ||
    out_of_wc_bounds(spikes[i].vlist[1].transformed) ||
    out_of_wc_bounds(spikes[i].vlist[2].transformed) ||
    out_of_wc_bounds(spikes[i].vlist[3].transformed)) {
    spikes[i].place_spike();
}
```

通过变换矩阵，我们现在学会了如何组合。

## 组合变换

最后，我们还必须更改尖刺的越界检查。在第 5 章中，我们只是检查了三号顶点来判断它是否越界。这是因为顶点具有固定的方向，我们知道三号顶点始终是最靠近相机的前端顶点（记得，相机位于原点）。此外，由于尖刺只能向前移动，我们在第 5 章中知道该顶点将是第一个越出边界的。然而，在新的 `rotspikes` 程序中，这些假设不再成立了。尖刺可能具有任意的方向；尖刺的四个顶点中的任何一个都可能是前端，因此，需要对四个顶点中的任何一个进行扩展，以检查尖刺的所有顶点，从而确定尖刺是否需要重新定位。

那么我们从中中学到，变换的应用顺序非常重要。代表变换的矩阵也必须按照特定的顺序相乘；改变乘法顺序通常会改变结果，就像改变变换的顺序会改变结果一样。

## 顺序变换

最简单的例子就是当我们应用一个变换，然后应用另一个。参见图 17。

## 关于任意点的旋转或缩放

之前开发的旋转和缩放公式是相对于原点定义的。这意味着如果我们旋转一组点（定义一个物体），该物体不仅被旋转了，还获得了一个新的位置。同样，当我们缩一个物体时，它不仅变小了，而且更靠近原点；如果我们放大它，它就会远离原点。

# 第 6 章：矩阵与变换

通常，我们希望围绕物体自身的中心进行旋转或缩放。这样，物体的中心在空间中的位置保持不变，物体的其余部分改变其取向或大小。图 6-19 和 6-20 展示了这些局部旋转和局部缩放的思想。

![](img/49715b3934121066e59e93823d33ee3a_375_0.png)

![](img/49715b3934121066e59e93823d33ee3a_375_1.png)

该问题的解决方法很简单：我们首先平移物体的所有点，将所需的旋转或缩放中心移动到世界坐标系中的原点。然后，我们使用标准的旋转或缩放矩阵绕原点进行旋转或缩放。最后，我们通过与初始平移完全相反的量将物体的所有点移回去。

记住一系列矩阵乘法表示从右到左执行的几何操作，我们可以写出局部旋转的方程如下：

```
6-26 T(x,y,z) = RT(-x,-y,-z)
```

考虑我们将此矩阵与属于物体的一系列点相乘会发生什么。假设物体的中心位于 `(x,y,z)`。最右侧的矩阵 `T(-x,-y,-z)` 在几何上首先应用，它平移了物体的所有点，使得物体中心正好位于原点。从右到左的下一个矩阵是所需的矩阵或旋转矩阵系列。由于平移矩阵已经应用，物体的所有点在世界坐标系中以原点为中心。因此，我们可以使用之前推导的标准旋转矩阵绕原点旋转。最后，在旋转完成后，我们应用相反的平移 `$T(x,y,z)$` 将物体移回原始位置。见图 6-21。

图 6-21：作为系列变换的局部旋转。

![](img/49715b3934121066e59e93823d33ee3a_376_0.png)

同样，我们可以将局部缩放表示为系列变换，这些变换将物体的点平移到原点，相对于原点缩放点，并将点移回。数学上为：

`$T(x,y,z)S(s_x, s_y, s_z)T(-x, -y, -z)$`

## 任意相机位置和朝向

变换矩阵最重要的应用之一是将任意相机位置和朝向转换为之前讨论的标准相机位置和朝向（相机位于原点，直直面向 z 轴，完全正立）。我们需要这样做是因为第 5 章开发的透视投影方程均假设相机处于标准位置和朝向，但我们希望允许虚拟相机能够位于任意位置。
