
```cpp
#ifdef	W_VFRUST_H
#define	_W_VFRUST_H
#include "../..../tool_os/memman.h"

#include "../..../tool_os/dispatch.h"
#include "../..../view/camera.h"
#include "../..../tool_2d/screen.h"
#include "../object/object3d.h"
#include "world.h"

class l3d_world_frustum : public l3d_world
{

	public:
		l3d_world_frustum(int xsize, int ysize) :
		l3d_world(xsize,ysize) {};
		virtual ~l3d_world_frustum(void);

		/* virtual */ void draw_all(void);
};
#endif
```

## 清单 4-12：`w_vfrust.cc`

```cpp
#include "w_vfrust.h"
#include <stdlib.h>
#include <string.h>

#include "../object/bound.h"
#include "../polygon/polygon.h"
#include "../tool_2d/screen.h"
#include "../tool_os/dispatch.h"
#include "../../raster/rasteriz.h"
#include "../tool_2d/scrinfo.h"
#include "../system/fact0_2.h"
#include "../frustum/vfrust.h"
#include "../tool_os/memman.h"

l3d_world_frustum::l3d_world_frustum() {
}

void l3d_world_frustum::draw_all(void) {
 int i0bj, iFace;

 l3d_polygon_3d *plist[MAX_VISIBLE_FACES]; int pnum=0;

 rasterizer->clear_buffer();

 l3d_viewing_frustum frustum;
 l3d_point top_left, top_right, bot_right, bot_left;
 const int XOFF=2, YOFF=2;

 top_left.set(l3d_mulrr(l3d_divrr(int_to_l3d_real(XOFF - screen->xsize/2),
 camera->near_z),
 l3d_mulri((camera->fovx,screen->xsize)),
 l3d_mulrr(l3d_divrr(int_to_l3d_real(screen->ysize/2 - YOFF),
 l3d_mulri((camera->fovy,screen->ysize)),
 camera->near_z),
 int_to_l3d_real(camera->near_z),
 int_to_l3d_real(1)));
 top_right.set(l3d_mulrr(l3d_divrr(int_to_l3d_real(screen->xsize-XOFF - screen->xsize/2),
 l3d_mulri((camera->fovx,screen->xsize)),
 camera->near_z),
 l3d_mulrr(l3d_divrr(int_to_l3d_real(screen->ysize/2 - YOFF),
 l3d_mulri((camera->fovy,screen->ysize)),
 camera->near_z),
 int_to_l3d_real(camera->near_z),
 int_to_l3d_real(1)));
 bot_right.set(l3d_mulrr(l3d_divrr(int_to_l3d_real(screen->xsize-XOFF - screen->xsize/2),
 l3d_mulri((camera->fovx,screen->xsize)),
 camera->near_z),
 l3d_mulrr(l3d_divrr(int_to_l3d_real(screen->ysize/2 - screen->ysize+YOFF),
 l3d_mulri((camera->fovy,screen->ysize)),
 camera->near_z),
 int_to_l3d_real(camera->near_z),
 int_to_l3d_real(1)));
 bot_left.set(l3d_mulrr(l3d_divrr(int_to_l3d_real(XOFF - screen->xsize/2),
 l3d_mulri((camera->fovx,screen->xsize)),
 camera->near_z),
 l3d_mulrr(l3d_divrr(int_to_l3d_real(screen->ysize/2 - screen->ysize*YOFF),
 l3d_mulri((camera->fovy,screen->ysize)),
 camera->near_z),
 int_to_l3d_real(camera->near_z),
 int_to_l3d_real(1)));

frustum.create_from_points
(top_left, top_right, bot_right, bot_left,
camera->near_z, camera->far_z,
camera->inverse_viewing_xform);

int culled_obj_count;
culled_obj_count =0;
for(i=i0bj; i0bj<objects.num_items; i0bj++) {

objects[i0bj]->reset();  // 同时也重置包围球

if (objects[iobj]->num_xforms) {
l3d_object_clipable_boundable *obj;
if((obj=dynamic_cast<l3d_object_clipable_boundable *>(objects[i0bj])))
{

// 首先，仅仅在世界空间中“定位”包围球
obj->bounding_sphere.transform(objects[iobj]->modeling_xform);

// 现在，检查包围球是否在观察体内
if(! frustum.intersects_sphere(obj->bounding_sphere)) {
culled_obj_count++;
continue;  // 观察体与球不相交->丢弃该对象
} else {
// 球至少部分在观察体内。因此，现在，
// 将对象的*所有*顶点变换到世界空间。

objects[i0bj]->transform(objects[i0bj]->modeling_xform);
}
}
} else {
// 没有可用的包围球。立即
// 变换所有对象顶点。
objects[i0bj]->transform(objects[i0bj]->modeling_xform);
}
}else {
// 未应用对象到世界空间的变换，因此这些坐标
// 是世界坐标；对对象坐标执行观察体测试

l3d_object_clipable_boundable *obj;
if((obj=dynamic_cast<l3d_object_clipable_boundable *>(objects[i0bj])))
{
if(! frustum.intersects_sphere(obj->bounding_sphere)) {
culled_obj_count++;
continue;  // 观察体与球不相交->丢弃该对象
} else {
// 球和对象在（部分）在观察体内；不予剔除
}
}
}

l3d_object_clipable *oc;
oc = dynamic_cast <l3d_object_clipable *>(objects[i0bj]);
if(oc) {
    oc->clip_to_plane(frustum.near);
    oc->clip_to_plane(frustum.far);
    oc->clip_to_plane(frustum.top);
    oc->clip_to_plane(frustum.bottom);
    oc->clip_to_plane(frustum.left);
    oc->clip_to_plane(frustum.right);
}

objects[i0bj]->camera_transform(camera->viewing_xform);

l3d_polygon_3d_node *n;

// - 从面片中心指向相机（位于 0,0,0）的向量，用于背面剔除
l3d_vector facet_to_cam_vec;
//- 面片相对于原点的法线（aFacet.sfc_normal 相对于
//- 面片中心）
l3d_vector N;
n = objects[i0bj]->nonculled_polygon_nodes;
while(n) {
    N = n->polygon->sfcnormal.transformed - n->polygon->center.transformed;

    facet_to_cam_vec.set (0 - n->polygon->center.transformed.X_,
                          0 - n->polygon->center.transformed.Y_,
                          0 - n->polygon->center.transformed.Z_);

    //- 点积被显式公式化以防止定点溢出
    //- (facet_to_cam_vec 非常大)
    //-(使用内联函数 "dot" 使用默认定点精度)

    #include "../../math/fix_lowp.h"
    #define BACKFACE_EPS (float_to_l3d_real(0.1)
    if((l3d_mulr(FX_CVT(N.X_), FX_CVT(facet_to_cam_vec.X_)) +
        l3d_mulr(FX_CVT(N.Y_), FX_CVT(facet_to_cam_vec.Y_)) +
        l3d_mulr(FX_CVT(N.Z_), FX_CVT(facet_to_cam_vec.Z_)) > BACKFACE_EPS)
    //- 等效于: if(N.dot(facet_to_cam_vec) > BACKFACE_EPS ) -
    #include "../../math/fix_prec.h"
{
    //- 多边形未被剔除
} else {
    //- 将此多边形从 nonculled_polygon_nodes 列表中移除
    if(n->prev) {
        n->prev->next = n->next;
    } else {
        objects[i0bj]->nonculled_polygon_nodes = n->next;
    }

    if(n->next) {
        n->next->prev = n->prev;
    }
}

n = n->next;
}
}
```

### 代码示例：多边形排序与渲染

```text
objects[ibj]->apply_perspective_projection(*camera,
    screen->xsize, screen->ysize);

n = objects[ibj]->nonculled_polygon_nodes;

while(n) {

    plist[pnum++] = n->polygon;

    /* Use the average of all z-values for depth sorting */
    l3d_real zsum = int_to_l3d_real(0);
    register int ivtx;

    for(ivtx=0; ivtx<n->polygon->vertices->num_items; ivtx++) {
        zsum += ((*n->polygon->plist)) [ (*n->polygon->vertices)[ivtx].ivertex
            ].transformed_intermediates[1].z; 
    }
    n->polygon->zvisible = l3d_divide(zsum, ivtx);
    n = n->next;
}

/* Sort the visible facets in decreasing order of z-depth */
qsort(plist, pnum, sizeof(l3d_polygon_3d *), compare_facet_zdepth);

/* Display the facets in the sorted z-depth order (painter's algorithm) */
for(int i=0; i<pnum; i++) {
    plist[i]->draw(rasterizer);
}

char msg[256];
sprintf(msg,"%d POLYS DRAWN", pnum);
rasterizer->draw_text(0,16,msg);

sprintf(msg,"%d objects culled",
    culled_obj_count);
rasterizer->draw_text(0,32,msg);
```

在新 `draw_all` 例程中，我们首先计算世界坐标系中的视锥体（view frustum）。我们执行逆投影以获取近平面上的四个角点（使用第 2 章中的公式），然后调用 `l3d_viewing_frustum::create_from_points` 来创建视锥体，并将逆相机变换矩阵作为参数传入，以便视锥体在世界空间中计算，而不是在相机空间中计算。代码中的 `XOFF` 和 `YOFF` 常数是相对于屏幕角点的像素偏移量。在逆投影中，我们没有使用屏幕最上/下/左/右的极端角点，而是使用略微向屏幕中心偏移的点。例如，我们使用 `(2,2)` 而不是左上角的 `(0,0)`。这使得视锥体比实际屏幕略小，以允许裁剪代码中存在的轻微数值误差。正如我们之前指出的，对多边进行裁剪到比其小的视锥体在数学上等效于对视图窗口进行 2D 裁剪。但是，裁剪计算中的较小数值误差可能导致被裁剪的顶点略微位于视锥体外部。通过利用 `XOFF` 和 `YOFF` 常数人为地缩小视锥体，我们可以相对有把握地认为，即使 3D 中被裁剪的顶点略微位于视锥体外部，其在投影后仍会位于 2D 屏幕边界内——如果我们使用 3D 视锥体裁剪来替代 2D 裁剪，这一点至关重要。

然后，我们使用以下代码片段对物体执行视锥体剔除：

```text
l3d_object_clipable_boundable *obj;
if((obj->dynamic_cast<l3d_object_clipable_boundable *>(objects[iObj])))
{
    // -- first, position "ONLY" the bounding sphere in world space
    obj->bounding_sphere.transform(objects[iObj]->modeling_xform);

    // -- now, check if the bounding sphere is in the frustum
    if(! frustum.intersects_sphere(obj->bounding_sphere)) {
        culled_obj_count++;
        continue; // -- frustum does not intersect sphere->discard object
    } else {
        // -- sphere is at least partially in frustum, so, now,
        // -- transform "ALL*" of the object's vertices into world space.
        objects[iObj]->transform(objects[iObj]->modeling_xform);
    }
}
```

首先，我们将物体的包围球（bounding sphere）从物体空间变换到世界空间。然后，我们检查包围球是否位于视锥体外部；如果是，则丢弃该物体并继续处理世界中的下一个物体。否则，如果包围球至少部分位于视锥体内部，我们将球体边界内的几何体变换到世界空间，并像往常一样继续处理该物体。实际的代码有两个主要的 `if` 分支，一个用于物体具有从物体空间到世界空间的变换矩阵的情况，另一个用于物体没有变换的情况（即，物体的坐标已经是世界坐标），但一般逻辑——如果包围球在视锥体内则保留，否则拒绝——在这两种情况下都是相同的。

如果物体的包围球位于视锥体内，则下一步是在 3D 中对物体相对于视锥体平面进行裁剪：
