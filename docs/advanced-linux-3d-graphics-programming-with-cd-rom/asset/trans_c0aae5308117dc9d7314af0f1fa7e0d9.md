
## 代码示例：多边形排序与渲染

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

在新 `draw_all` 例程中，我们首先计算世界坐标系中的视锥体（view frustum）。我们执行逆投影以获取近平面上的四个角点（使用第 2 章中的公式），然后调用 `l3d_viewing_frustum::create_from_points` 来创建视锥体，并将逆相机变换矩阵作为参数传入，以便视锥体在世界空间中计算，而不是在相机空间中计算。代码中的 `XOFF` 和 `YOFF` 常数是相对于屏幕角点的像素偏移量。在逆投影中，我们没有使用屏幕最上/下/左/右的极端角点，而是使用略微向屏幕中心偏移的点。例如，我们使用 (2,2) 而不是左上角的 (0,0)。这使得视锥体比实际屏幕略小，以允许裁剪代码中存在的轻微数值误差。正如我们之前指出的，对多边进行裁剪到比其小的视锥体在数学上等效于对视图窗口进行 2D 裁剪。但是，裁剪计算中的较小数值误差可能导致被裁剪的顶点略微位于视锥体外部。通过利用 `XOFF` 和 `YOFF` 常数人为地缩小视锥体，我们可以相对有把握地认为，即使 3D 中被裁剪的顶点略微位于视锥体外部，其在投影后仍会位于 2D 屏幕边界内——如果我们使用 3D 视锥体裁剪来替代 2D 裁剪，这一点至关重要。

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

```text
l3d_object_clipable *oc;
oc = dynamic_cast <l3d_object_clipable *>(objects[iObj]);
if(oc) {
    oc->clip_to_plane(frustum.near);
    oc->clip_to_plane(frustum.far);
    oc->clip_to_plane(frustum.top);
    oc->clip_to_plane(frustum.bottom);
    oc->clip_to_plane(frustum.left);
    oc->clip_to_plane(frustum.right);
}
```

物体处理的其余部分与我们之前看到的完全相同：变换到相机空间、背面剔除、透视投影、多边形排序以及光栅化。（下一节关于画家算法的部分将更详细地涵盖多边形排序的主题。）请注意，在这种情况下，我们不将多边形在 2D 中裁剪到视图窗口；3D 视锥体裁剪意味着任何投影多边形都将位于视图窗口内（除了之前提到的数值误差情况除外）。最后，新的 `draw_all` 例程还将文本字符串绘制到显示器上，指示被剔除的物体数量。

然而，此处实现的视锥体剔除在物体数量增加时仍存在问题。我们在物体级别执行剔除，没有进一步的层级结构。这意味着随着物体数量的增加，我们必须线性地搜索越来越多的物体，测试每个物体是否在视锥体内。即使我们能够通过不进一步处理物体来节省工作，检查更多物体所花费的时间仍然会越来越多。正如我们之前看到的，通过分层将物体分组为越来越大的组，并首先针对这些大组检查视锥体，我们可以通过丢弃大型组而不需要遍历层级结构中的每个节点来节省时间。

如何生成这种层级结构的问题仍然存在。您可以将层级结构硬编码到程序中，但这将非常难以维护。您可以使用 3D 建模软件的 3D 功能来为场景强加层级结构，假设您可以导出此信息供 3D 程序读取。这仍然存在问题，即对场景的任何更改都需要在 3D 建模器内更改或更新层级结构。一个非常有吸引力的选项是使用 BSP 树为任意多边形集合自动生成包围体层级，正如下一章所讨论的那样。

但在讨论 BSP 树之前，让我们继续查看一些更简单的 VSD（可见性排序深度）算法。接下来，我们介绍一种简单且流行的算法，我们已经见过并使用过：画家算法。

## 画家算法

画家算法是一种 VSD 算法，依赖于多边形排序，它解决了正确性问题但忽略了效率问题。我们知道，按随机顺序将多边形绘制到屏幕上有时会导致显示不正确，因为较远的多边形会遮挡较近的多边形。原始 `l3d_world` 类中采用的解决方案是所谓的画家算法，其中我们按从后到前的顺序将多边形绘制到帧缓冲区。通过最后绘制最近的多边形，最近多边形的像素将覆盖同一位置可能已经存在于帧缓冲区中的较远多边形的像素。这意味着较近的多边形总是遮挡较远的多边形。

由于使用 `l3d_world` 类的示例程序已经使用了画家算法，因此这里没有额外的示例程序。画家算法非常简单，并且在大多数情况下产生基本正确的结果。然而，关于画家算法有一些重要的缺点和观察结果值得注意。

-   排序。画家算法要求我们根据多边形到观察者的距离对多边形进行排序。排序需要时间。对于大量多边形，画家算法可能将大部分时间花在排序多边形上。一种避免这种排序的技术是创建一个大的多边形列表，例如足够容纳 4096 个多边形。该列表中的每个条目代表一个 z 深度。然后，在绘制多边形之前，我们将它的 z 深度缩放以落在列表的范围内。我们将这个缩放后的 z 深度四舍五入为整数，并将其用作多边形在列表中的插入位置。如果两个多边形的 z 深度足够接近，它们将被分配到同一个槽中，这可能会导致小规模的排序错误。然后，为了绘制多边形，我们从后向前遍历列表

