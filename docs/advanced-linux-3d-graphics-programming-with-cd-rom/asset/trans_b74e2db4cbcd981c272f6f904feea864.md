

# 第 4 章：可见表面判定 I：通用技术

首先，我们计算从多边形中心指向摄像头的向量。由于该计算是在相机坐标系下进行的，因此摄像头位于 $(0,0,0)$ 位置。然后，我们计算多边形表面法向量与所计算的多边形到摄像头向量之间的点积，并利用符号来确定多边形是正面还是背面朝向。请注意，点积被显式地表示为乘积之和，而不是使用 $\mathbf{dot}$ 运算符，以控制在使用定点数学进行计算时的精度（即用于小数部分和整数部分的位数）。否则，点积计算可能会溢出，并导致在使用定点数学时错误地计算多边形的朝向。此外，请注意使用了一个 epsilon 参数，以允许计算中存在一定的不准确性；多边形必须是面向前方的程度大于 epsilon 参数，才会被接受为面向前方。（多边形“面向前方”的“程度”是点积计算返回的标量值，即两个向量之间夹角的余弦值。）由于我们在相机坐标系中执行背面计算，实际上只需检查法向量的 z 分量符号就足够了。然而，本例展示了更通用的基于点积的背面计算方法，该方法也可以在将顶点变换到相机空间之前，在世界坐标系中执行，从而避免在变换顶点后才发现这些顶点属于背面多边形、因此不需要被处理的计算开销。

类 $l3d\_world\_backface$ 还显示了发送给光栅化器的多边形数量计数。请注意，对于相同的场景，程序 $backface$ 的这个数值比程序 $flsim$ 的要低；背面剔除减少了发送给光栅化器的多边形数量。

**列表 4-4**：$w\_back.h$，用于执行背面剔除的新世界类的声明

```cpp
#ifndef W_BACK_H
#define W_BACK_H

#include "../../tool_os/neuman.h"
#include "../../tool_os/dispatch.h"
#include "../../view/camera.h"
#include "../../tool_2d/screen.h"
#include "../object/object3d.h"
#include "world.h"

class l3d_world_backface : public l3d_world
{
public:
    l3d_world_backface(int xsizel, int ysizel) :
        l3d_world(xsizel, ysizel) {}
    virtual ~l3d_world_backface(void);

    /* virtual */ void draw_all(void);
};

#endif
```

**列表 4-5**：$w\_back.cc$，用于执行背面剔除的新世界类的代码

```cpp
#include "w_back.h"
#include <stdlib.h>
#include <string.h>

#include "../object/object3d.h"
#include "../polygon/polygon.h"
#include "../tool_2d/screen.h"
#include "../tool_os/dispatch.h"
#include "../raster/rasteriz.h"
#include "../tool_2d/scrinfo.h"
#include "../system/fact0_2.h"
#include "../tool_os/hemmai.h"

l3d_world_backface l3d_world_backface() {
}

void l3d_world_backface::draw_all(void) {

    int iObj, iFace;
    l3d_polygon_3d *plist[MAX_VISIBLE_FACETS]; int nNum=0;

    rasterizer->clear_buffer();

    for(iObj=0; iObj<objects.num_items; iObj++) {

        objects[iObj]->reset();

        if (objects[iObj]->num_xforms) {
            objects[iObj]->transform(objects[iObj]->modeling_xform);
        }

        objects[iObj]->camera_transform(camera->viewing_xform);

        l3d_polygon_3d_node *n;

        // vector from facet center to camera (at 0,0,0), for backface culling
        l3d_vector facet_to_cam_vec;

        // 'Facet's sfc normal relative to origin (aFacet.sfc_normal is relative
        // to facet center)
        l3d_vector N;

        n=objects[iObj]->nonculled_polygon_nodes;
        while(n) {
            N = n->polygon->sfc_normal.transformed - n->polygon->center.transformed;

            facet_to_cam_vec.set(0 - n->polygon->center.transformed_X_,
                                0 - n->polygon->center.transformed_Y_,
                                0 - n->polygon->center.transformed_Z_,
                                int_to_l3d_real(0));

            // - dot product explicitly formulated so no fixed point overflow
            // (facet_to_cam_vec is very large)
            // (use of the inline function "dot" uses default fixed precision)
            #include <../math_fix_func.h>
            #define backface_eps float_to_l3d_real(0.1)

            if((l3d_mulrr(FX_CVT(N,X_), FX_CVT(facet_to_cam_vec, X_)) +
               l3d_mulrr(FX_CVT(N,Y_), FX_CVT(facet_to_cam_vec,Y_)) +
               l3d_mulrr(FX_CVT(N,Z_), FX_CVT(facet_to_cam_vec,Z_)) > backface_eps)
            // equivalent to: if(dot(facet_to_cam_vec)*backface_eps)

            #include "../math/fix_prec.h"

            &&
            n->polygon->clip_near_z(camera->near_z)
            {
                // polygon is not culled
            } else {
                // take this polygon out of the list of nonculled_polygon_nodes
                if(n->prev) {
                    n->prev->next = n->next;
                } else {
                    objects[iObj]->nonculled_polygon_nodes = n->next;
                }
                if(n->next) {
                    n->next->prev = n->prev;
                }
                n = n->next;
            }

        objects[iObj]->apply_perspective_projection(*camera, screen->wsize, screen->ysize);

        n = objects[iObj]->nonculled_polygon_nodes;

        while(n) {
            if ( n->polygon->clip_to_polygon_2d(screen->view_win)) {
                plist[nNum++] = n->polygon;
            }
            /* Use the average of all z-values for depth sorting */
            l3d_real zsum = int_to_l3d_real(0);
            register int ivtx;
            for(ivtx=0; ivtx<n->polygon->ivertices->num_items; ivtx++) {
                zsum += ((*(*n->polygon->vlist[ivtx]))[ (*n->polygon->ivertices)[ivtx].ivertex ]
                         ).transformed_intermediates[1],Z ;
            }
            n->polygon->zvisible = l3d_divrf(zsum, ivtx);
            n = n->next;
        }

        /* Sort the visible facets in decreasing order of z-depth */
        qsort(plist, nNum, sizeof(l3d_polygon_3d *), compare_facet_zdepth);

        /* Display the facets in the sorted z-depth order (painter's algorithm) */
        for(int i=0; i<nNum; i++) {
            plist[i]->draw(rasterizer);
        }

        char msg[256];
        sprintf(msg,"%d POLYS DRAWN\n", nNum);
        rasterizer->draw_text(0,16,msg);
    }
}
```

虽然并不常需要这样做，但如果你确实希望看到表面的两面，要么使用两个多边形来分别建模表面的正面和背面，要么跳过背面剔除操作。请注意，如果你跳过背面剔除操作并希望绘制背面多边形，你需要对 $l3d$ 中的光栅化例程进行修改，因为它们都期望多边形顶点遵循特定的顺序，即顺时针方向。背面多边形具有反向朝向，因此其顶点顺序为逆时针，这需要由光栅化器来处理。从某种意义上说，光栅化器不绘制具有反向朝向多边形的事实，本身也是一种形式的背面剔除（实际上也是 OpenGL 使用的屏幕空间方法），但通过利用表面法向量执行背面判定，从而完全避免将多边形发送给光栅化器，可能会更高效。

## 视锥剔除

*视锥剔除* 是另一种可见表面判定（VSD）算法，与背面剔除类似，它侧重于 VSD 的效率方面。通过视锥剔除，我们剔除完全位于*视锥*（view frustum）之外的多边形或多边形组。视锥，也称为*观察体积*（view volume），是三维空间中虚拟观察者可见的区域。观察者看不到世界中的所有内容；涉及显示窗口大小的水平和垂直视野项限制了可以看到的世界范围。窗口边界之外的任何内容都不可见。此外，比近* z* 平面更近或比远* z* 平面更远的对象也看不到。从几何上讲，观察体积是一个截锥体，其顶点位于摄像头处。观察体积内的对象是可见的；观察体积外的对象是不可见的。

视锥剔除背后的思想是在三维空间中用数学方法表示视锥，然后测试对象是否位于视锥内。如果在视锥内，则进一步处理。如果不在，则立即从后续处理中丢弃。显然，我们越早执行观察体积包含测试，潜在节省的工作就越多。

### 定义视锥

视锥可以用六个平面表示。视锥本身则是所有六个平面相交内部区域。

