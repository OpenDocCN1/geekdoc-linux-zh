
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

虽然并不常需要这样做，但如果你确实希望看到表面的两面，要么使用两个多边形来分别建模表面的正面和背面，要么跳过背面剔除操作。请注意，如果你跳过背面剔除操作并希望绘制背面多边形，你需要对`l3d`中的光栅化例程进行修改，因为它们都期望多边形顶点遵循特定的顺序，即顺时针方向。背面多边形具有反向朝向，因此其顶点顺序为逆时针，这需要由光栅化器来处理。从某种意义上说，光栅化器不绘制具有反向朝向多边形的事实，本身也是一种形式的背面剔除（实际上也是OpenGL使用的屏幕空间方法），但通过利用表面法向量执行背面判定，从而完全避免将多边形发送给光栅化器，可能会更高效。

### 视锥剔除

视锥剔除是另一种可见表面判定（VSD）算法，与背面剔除类似，它侧重于VSD的效率方面。通过视锥剔除，我们剔除完全位于视锥（view frustum）之外的多边形或多边形组。视锥，也称为观察体积（view volume），是三维空间中虚拟观察者可见的区域。观察者看不到世界中的所有内容；涉及显示窗口大小的水平和垂直视野项限制了可以看到的世界范围。窗口边界之外的任何内容都不可见。此外，比近`z`平面更近或比远`z`平面更远的对象也看不到。从几何上讲，观察体积是一个截锥体，其顶点位于摄像头处。观察体积内的对象是可见的；观察体积外的对象是不可见的。

视锥剔除背后的思想是在三维空间中用数学方法表示视锥，然后测试对象是否位于视锥内。如果在视锥内，则进一步处理。如果不在，则立即从后续处理中丢弃。显然，我们越早执行观察体积包含测试，潜在节省的工作就越多。

#### 定义视锥

视锥可以用六个平面表示。视锥本身则是所有六个平面相交内部区域。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_235_0.png)

图 4-7：视锥体（view frustum）可以由六个平面定义：近面（near）、远面（far）、左面（left）、右面（right）、上面（top）和下面（bottom）。角点是通过反向投影屏幕空间角点计算得出的，用于计算左、右、上、下平面的方程。

视锥体的近面（near）和远面（far）分别是近`z`裁剪平面和远`z`裁剪平面，每个平面都由形式为`z=k`的平面方程定义，其中`k`是该平面（近或远）与眼点（eye）之间的距离。到目前为止，我们实际上还没有针对远`z`平面进行裁剪，但其原理与近`z`平面相同，唯一的区别在于：远`z`平面的法线方向与近`z`平面的法线方向相反。这是因为我们在近平面的近侧进行裁剪，而在远平面的远侧进行裁剪。

视锥体剩余的四个平面定义起来稍微棘手一些。它们代表了由于投影窗口尺寸有限而导致的视野左、右、下、上限制。回想一下，知道位于平面上的三个点即可定义该平面；我们只需使用这三个点构造两个唯一向量，通过计算叉积找到平面法线（即平面方程中的$A$、$B$和$C$项），然后使用这三个点中的一个来求解平面方程中的$D$项。方法`l3d_plane::align_with_points`根据给定的三个点计算平面系数；请记住，传入该方法的点的顺序很重要，因为它决定了平面的正面/背面朝向。

为了定义视锥体剩余的四个平面，我们首先计算近平面上四个角点的相机空间坐标，这些点在从3D投影到2D时，会产生屏幕空间的四个角点。换句话说，我们对2D屏幕空间中的四个屏幕角点进行反向投影，从而得到位于3D相机空间近平面上的四个相机空间点。视锥体的每个平面都经过其中两个点。

例如，对于一个`320x240`的窗口，`(0,0)`、`(319,0)`、`(319,239)`、`(0,239)`将是屏幕空间的角点坐标；我们将使用第2章中的反向投影公式将这些点反向投影到近`z`平面上。回想一下，反向投影首先使用3D点必须所在的平面的平面方程找到投影点的`z`值，然后将投影的$x$和$y$乘以计算出的3D$z$值，以获得3D的$x$和$y$值，从而逆转由$z$引起的透视除法。完整的方程涉及视野（field of view）项和屏幕尺寸，请参阅第2章。请注意，在这种情况下，我们实际上不需要使用平面方程来计算$z$值；由于我们是在近$z$平面上进行反向投影，而该平面的$z$是常数，因此我们已经知道要在第2章反向投影公式中使用的$z$值。

然后，我们使用这些反向投影角点中的连续对，以及相机自身的相机空间坐标（在相机空间中恰好是`(0,0,0)`），并根据这三个点计算平面，因为这三个点恰好位于视锥体的各侧上。假设我们将屏幕的反向投影角点称为“左上”、“右上”、“右下”和“左下”，以下列表展示了用于计算特定视锥体平面的点。

- 顶部视锥体平面：相机位置`(0,0,0)`、右上 和 左上。
- 右侧视锥体平面：相机位置`(0,0,0)`、右下 和 右上。
- 底部视锥体平面：相机位置`(0,0,0)`、左下 和 右下。
- 左侧视锥体平面：相机位置`(0,0,0)`、左上 和 左下。

> 注意：在上述列表中，点的顺序是精心选择的，目的是将平面的内侧定义为视锥体内部；换句话说，从视锥体内部观看时，指定的点看起来是顺时针排列的。这对于前文提到的方法`l3d_plane::align_with_points`至关重要。

#### 在世界坐标系中计算视锥体

上述步骤为我们提供了定义在相机空间中的视锥体平面，以平面方程系数的形式表示。我们也可以通过使用世界空间位置来执行相同的步骤，即在将点用于计算视锥体平面之前，将每个点乘以逆相机变换矩阵。这将给出世界坐标系下的视锥体平面，而不是相机坐标系下的。这很有用，因为它允许我们在世界空间而不是相机空间中进行视锥体剔除（frustum culling），从而允许我们在将物体变换到相机空间之前先剔除物体。请注意，这种世界空间剔除只有在用于剔除目的的几何体表示使用简化的包围体时，才能节省计算工作量；参见标题为“包围球和视锥体”的部分。

例如，要计算世界坐标系中的顶部视锥体平面，我们将相机位置`(0,0,0)`乘以逆相机变换矩阵，以获得相机在世界空间中的位置。同样，我们将右上角点和左上角点乘以逆相机矩阵，以获得这些点在世界空间而非相机空间中的坐标。然后使用这些世界空间坐标计算平面方程。

在世界空间计算近面和远面视锥体平面也需要我们在世界空间而不是相机空间使用三个点创建平面。这也是很直接的：近面和远面在相机空间中由形式为$z = k$的方程定义，其中$k$是定义从眼点到平面距离的常数。因此，在相机空间中，形式为$(x,y,k)$的任何点，其中$x$和$y$是任意的，都位于该平面上。我们可以选择任意三个不共线的点$(x_i,y_i,k)$来定义相机空间中的平面；然后，我们将这些相机空间点乘以逆相机矩阵，以获得世界空间点，从而计算世界空间平面。对于近平面，选择共线（不位于一条直线上）点的一个方便选择是`(0,0,k)`、`(1,0,k)`和`(0,1,k)`；对于远平面，使用相同的点但顺序相反：`(0,1,k)`、`(1,0,k)`、`(0,0,k)`。远平面的法线必须指向与近平面法线相反的方向，以便每个平面的内侧位于视锥体的内部——这就是近面和远面点顺序反转的原因。例如，如果近平面在相机空间中定义为`z=1.5`，我们将取点`(0,0,1.5)`、`(1,0,1.5)`和`(0,1,1.5)`作为已知位于相机空间近平面上的点。然后我们将这些点乘以逆相机矩阵以获得世界空间点。最后，我们使用这三个点计算平面。

#### 类 l3d_viewing_frustum

类`l3d_viewing_frustum`表示一个视锥体。它通过成员变量`top`、`bottom`、`left`、`right`、`near`和`far`存储视锥体六个侧面的六个平面。

方法`create_from_points`给定四个反向投影角点（如前所述）、一个近平面、一个远平面和一个变换矩阵，创建一个视锥体。该例程使用上一节描述的布局对齐视锥体的六个平面：顶、底、左、右平面使用眼点和四个角点中的两个创建。前/后平面使用位于近/远平面上的简单非共线三点集创建。所有平面的创建（或对齐，取决于如何看待）都通过方法`l3d_plane::align_with_points`完成。在所有点传递给该方法之前，它们会乘以作为参数传递的变换矩阵`xform`。默认情况下，视锥体的创建在相机坐标中进行，并产生代表视锥体在相机坐标中位置的一组平面。通过传递一个将相机坐标变换为世界坐标的变换矩阵，我们可以计算世界坐标中的视锥体，这通常是更期望的结果。这意味着我们传递从相机到世界坐标的逆视图矩阵作为`xform`参数，以获得世界空间中的视锥体平面。要在相机空间中获取视锥体，请传递单位矩阵作为`xform`参数。

方法`intersect_with_sphere`测试球体是否在视锥体内部。接下来的部分将详细介绍该方法和这一思想。

> 代码清单 4-6: `vfrust.h`
