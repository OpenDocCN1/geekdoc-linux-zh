
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

注意：文档的开头（第 251 页和第 252 页的开头）似乎来自上一个清单或章节，未在提供的片段中完全标题化，但根据流程，第 251 页的内容属于上一个实现示例（可能是清单 4-10 或类似上下文，未完全显示），而第 252 页的代码块完成了该部分。然而，由于提示要求处理提供的文本，且主要标题部分以“Class l3d_world_frustum”开头，我将把第 251-252 页的代码作为导致新类定义的连续代码流的一部分包含进来，或者仅输出主要标题部分。仔细查看第 251 页，它包含的代码片段似乎是上一个清单的结尾部分。第 252 页以该代码的结尾开始，然后开始新部分“# Class l3d_world_frustum”。为了按要求保留所有信息，如果第 251 页和第 252 页开头的代码块是连续的，我将把它们重构为一个代码块；如果是不同的清单，则分开。文本中存在“Listing 4-11”和“Listing 4-12”。第 251/252 页开头的代码在文本中没有清单编号标题，但它确实是代码。我将将其格式化为代码块。然后是新的部分。

**更正：** 指示说“输出处理后的最终文本...”。输入包含带有代码的`[PAGE 251]`，以及更多代码和`# Class l3d_world_frustum`的`[PAGE 252]`。第 251/252 页开头的代码似乎是上一个示例（鉴于 `my_world::~my_world` 和 `main`，可能是与 `my_world` 相关）的结尾。我将将其作为代码块包含。然后是下一个部分。

```cpp
// ...（来自第 251/252 页的前文代码）...
camera->VRP_set(0,0,-50,0);
camera->near_z = float_to_l3d_real(1.0);
camera->far_z = int_to_l3d_real(50);

// 用于 mesa 光栅化器的反向投影
rasterizer_3d_imp->fovx = &(camera->fovx);
rasterizer_3d_imp->fovy = &(camera->fovy);
rasterizer_3d_imp->screen_xsize = &(screen->xsize);
rasterizer_3d_imp->screen_ysize = &(screen->ysize);

int i,j,k,onum=0;

texloader = new l3d_texture_loader_ppm(s1);
scache = new l3d_surface_cache(s1);

for(i=0; i<150; i++) {

    // - 创建一个插件对象
    l3d_object_clipable_boundable *oc;

    objects[onum=objects.next_index()] =
    oc =
        new l3d_object_clipable_boundable(10);
    // - 最多 10 个固定顶点，如果需要，可由插件重写
    // - 通过重新定义顶点列表

    objects[onum]->plugin_loader =
        factory_manager.v_0_2_plugin_loader_factory->create();
    objects[onum]->plugin_loader->load("/../lib/dynamics/plugins/vidmesh/vidmesh.so");
    objects[onum]->plugin_constructor =
        (void (*)(l3d_object*, void *))
        objects[onum]->plugin_loader->find_symbol("constructor");
    objects[onum]->plugin_update =
        (void (*)(l3d_object *))
        objects[onum]->plugin_loader->find_symbol("update");
    objects[onum]->plugin_destructor =
        (void (*)(l3d_object *))
        objects[onum]->plugin_loader->find_symbol("destructor");
    objects[onum]->plugin_copy_data =
        (void (*)(const l3d_object*, l3d_object *))
        objects[onum]->plugin_loader->find_symbol("copy_data");

    texloader = new l3d_texture_loader_ppm(s1);
    scache = new l3d_surface_cache(s1);

    char plugin_params[4096];
    sprintf(plugin_params, "%s\n\n i\n l o o o l t r e e . o b j t r e e . p p m t r e e . u v\n"
            " r a n d ( )"\n200-100,\n0,\n r a n d ( )"\n200-100)";

    l3d_plugin_environment *e = new l3d_plugin_environment
        (texloader, screen->info, scache, plugin_params);

    if(objects[onum]->plugin_constructor)
    {*objects[onum]->plugin_constructor}(objects[onum],e);
}

oc->bounding_sphere.compute_around_object(oc);

		screen->refresh_palette();
	}

	my_world::~my_world(void) {
		delete texloader;
		delete scache;
	}

	main() {
		l3d_dispatcher *d;
		l3d_pipeline_world *p;
		my_world *w;

		factory_manager_v_0_2::choose_factories();
		d = factory_manager_v_0_2::dispatcher_factory->create();

		w = new my_world();
		p = new l3d_pipeline_world(w);
		d->pipeline = p;
		d->event_source = w->screen;

		d->start();

		delete d;
		delete p;
		delete w;
	}
```

#### 类 `l3d_world_frustum`

新的类 `l3d_world_frustum` 将观察体剔除（view frustum culling）整合到世界的绘制行为中。它仅重写了方法 `draw_all`。

### 清单 4-11：`w_vfrustum.h`
