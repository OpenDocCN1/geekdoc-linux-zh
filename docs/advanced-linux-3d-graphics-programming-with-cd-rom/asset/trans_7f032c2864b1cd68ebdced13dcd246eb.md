

# 清单 2-2：shapes.h，程序 morph3d 中 3D 对象的头文件

```cpp
#include "../lib/geom/object/object3d.h"
#include "geom/vertex/vertex.h"

class pyramid : public l3d_object {
  static const int num_keyframes = 2;
  int keyframe_no;
  l3d_two_part_list<l3d_coordinate>* keyframes[2];
  l3d_vertex_interpolator interp;
  bool currently_interpolating;

public:
  pyramid(void);
  virtual ~pyramid(void);
  int update(void);
};
```

# 清单 2-3：shapes.cc，程序 morph3d 中 3D 对象的实现文件

```cpp
#include "shapes.h"
#include <stdlib.h>
#include <string.h>

pyramid::pyramid(void) :
  l3d_object(4)
{
  keyframes[0] = new l3d_two_part_list<l3d_coordinate>(4);
  (*keyframes[0])[0].original.set(
    float_to_l3d_real(0.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(1.0));
  (*keyframes[0])[1].original.set(
    float_to_l3d_real(10.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(1.0));
  (*keyframes[0])[2].original.set(
    float_to_l3d_real(0.0),
    float_to_l3d_real(10.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(1.0));
  (*keyframes[0])[3].original.set(
    float_to_l3d_real(0.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(10.0),
    float_to_l3d_real(1.0));

  keyframes[1] = new l3d_two_part_list<l3d_coordinate>(4);
  (*keyframes[1])[0].original.set(
    float_to_l3d_real(5.0),
    float_to_l3d_real(5.0),
    float_to_l3d_real(5.0),
    float_to_l3d_real(1.0));
  (*keyframes[1])[1].original.set(
    float_to_l3d_real(-10.0),
    float_to_l3d_real(10.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(1.0));
  (*keyframes[1])[2].original.set(
    float_to_l3d_real(10.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(1.0));
  (*keyframes[1])[3].original.set(
    float_to_l3d_real(10.0),
    float_to_l3d_real(15.0),
    float_to_l3d_real(0.0),
    float_to_l3d_real(1.0));

  int pi;
  pi = polygons.next_index();
  polygons[pi] = new l3d_polygon_3d_flatshaded(3);
  printf("before: %p", polygons[pi]->vlist);
  polygons[pi]->vlist = &vertices;
  printf("after: %p", polygons[pi]->vlist);
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 0;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 1;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 3;
  polygons[pi]->compute_center();
  polygons[pi]->compute_sfcolorn();

  pi = polygons.next_index();
  polygons[pi] = new l3d_polygon_3d_flatshaded(3);
  polygons[pi]->vlist = &vertices;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 2;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 3;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 1;
  polygons[pi]->compute_center();
  polygons[pi]->compute_sfcolorn();

  pi = polygons.next_index();
  polygons[pi] = new l3d_polygon_3d_flatshaded(3);
  polygons[pi]->vlist = &vertices;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 0;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 1;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 2;
  polygons[pi]->compute_center();
  polygons[pi]->compute_sfcolorn();

  pi = polygons.next_index();
  polygons[pi] = new l3d_polygon_3d_flatshaded(3);
  polygons[pi]->vlist = &vertices;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 3;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 2;
  (*polygons[pi]->ivertices)[polygons[pi]->ivertices->next_index()].ivertex = 0;
  polygons[pi]->compute_center();
  polygons[pi]->compute_sfcolorn();

  num_xforms = 2;
  modeling_xforms[0] = l3d_mat_rotx(0);
  modeling_xforms[1].set(
    float_to_l3d_real(1.0), float_to_l3d_real(0.0), float_to_l3d_real(0.0), float_to_l3d_real(0.0),
    float_to_l3d_real(0.0), float_to_l3d_real(1.0), float_to_l3d_real(0.0), float_to_l3d_real(0.0),
    float_to_l3d_real(0.0), float_to_l3d_real(0.0), float_to_l3d_real(1.0), float_to_l3d_real(1.0),
    float_to_l3d_real(0.0), float_to_l3d_real(0.0), float_to_l3d_real(0.0), float_to_l3d_real(1.0));

  modeling_xform = modeling_xforms[1] | modeling_xforms[0];
  currently_interpolating = false;
  keyframe_no = 0;
  vertices = keyframes[keyframe_no];
}

pyramid::~pyramid(void) {
  for (register int i = 0; i < polygons.num_items; i++) { delete polygons[i]; }
  for (int i = 0; i < num_keyframes; i++) {
    delete keyframes[i];
  }
}

int pyramid::update(void) {
  if (currently_interpolating) {
    vertices = interp.list;
    if (interp.interpolate()) {
      currently_interpolating = false;
    }
  } else {
    keyframe_no++;
    if (keyframe_no >= num_keyframes) { keyframe_no = 0; }
    int next_keyframe = keyframe_no + 1;
    if (next_keyframe >= num_keyframes) { next_keyframe = 0; }

    vertices = keyframes[keyframe_no];
    interp.start(*keyframes[keyframe_no], *keyframes[next_keyframe],
                 rand() % 100 + 50, 3);

    currently_interpolating = true;
  }
  return 0;
}
```

程序 morph3d 使用 `l3d_world` 和 `l3d_object` 类来存储虚拟世界。`main.cc` 文件非常简单：它声明了一个 world 的子类，该类创建一些 pyramid 对象。

pyramid 类是一个变形的 3D 金字塔。它在紧凑型和细长型金字塔形状之间进行变换。为了实现这一点，我们在 pyramid 类中添加了以下行：

```cpp
class pyramid : public l3d_object {
  static const int num_keyframes = 2;
  int keyframe_no;
  l3d_two_part_list<l3d_coordinate>* keyframes[2];
  l3d_vertex_interpolator interp;
  bool currently_interpolating;
};
```

`keyframes` 变量持有两个独立的、不同的顶点列表。每个列表都是一组完整的顶点位置，定义了 3D 对象的一个形状。我们在 `pyramid` 构造函数中创建并填充这些列表。

现在，给定存储在两个独立顶点列表中的对象的两种不同形状，我们使用 `l3d_vertex_interpolator` 类，正如我们在之前的程序 morph2d 中所做的那样，在两个顶点列表之间插值顶点的位置。这发生在方法 `pyramid::update` 中。顶点插值器的使用方式与之前完全相同：我们指定起始顶点列表、结束顶点列表、插值步骤的总数，以及一个维度（2D 或 3D），该维度决定了插值顶点元素中的哪些元素。顶点插值器拥有自己内部的、独立的顶点列表，其中包含指定的起始顶点列表和结束顶点列表之间插值的“中间”位置。我们通过调用 `interp.step` 在顶点列表之间进行插值，并将插值后的顶点列表赋值给金字塔的顶点列表。

