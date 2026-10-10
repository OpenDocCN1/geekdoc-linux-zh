
```c
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>

#include "../lib/geom/object/sector.h"
#include "../lib/geom/polygon/p3_flat.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/dispatch.h"
#include "../lib/raster/rast3.h"
#include "../lib/tool_2d/scrifin.h"
#include "../lib/geom/world/x_bsp.h"
#include "../lib/system/facto_2.h"
#include "../lib/pipe/line/pi_wor.h"
#include "../lib/dynamics/plugins/plugenv.h"
#include "../lib/geom/texture/t1_ppm.h"
#include "../lib/dynamics/plugins/vidmesh/vidmesh.h"

#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>
#include <stdarg.h>
#include "../lib/geom/bsp/hal_fspace.h"
#include "../lib/geom/bsp/bsp_tree.h"

class my_world : public l3d_world_bsp_tree {
protected:
   l3d_texture_loader *texloader;
   l3d_surface_cache *scache;
public:
   my_world(void);
   virtual ~my_world(void);
};

my_world::my_world(void)
: l3d_world_bsp_tree(320, 240)
{
   l3d_screen_info *si = screen->info;

   camera->VRP_set(0, 0, -50, 0);
   camera->near_z = float_to_l3d_real(1.0);
   camera->far_z = int_to_l3d_real(50);

   // for mesa rasterizer's reverse projection
   rasterizer_3d_imp->focus_x = &camera->fovx;
   rasterizer_3d_imp->focus_y = &camera->fovy;
   rasterizer_3d_imp->screen_xsize = &(screen->xsize);
   rasterizer_3d_imp->screen_ysize = &(screen->ysize);

   int i, j, k;
   texloader = new l3d_texture_loader_ppm(si);
   scache = new l3d_surface_cache(si);

   // create a plugin object
   l3d_object_clipable_boundable *oc;

   oc = new l3d_object_clipable_boundable(10);
   // - max 10 fixed vertices, can be overriden by plug-in if desired
   // - by redefining the vertex list

   oc->plugin_loader = factory_manager_v_0_2_plugin_loader_factory::create();
   oc->plugin_loader->load("../lib/dynamics/plugins/vidmesh/vidmesh.so");
   oc->plugin_constructor =
      (void (*)(l3d_object *, void *))
      oc->plugin_loader->find_symbol("constructor");
   oc->plugin_update =
      (void (*)(l3d_object *))
      oc->plugin_loader->find_symbol("update");
   oc->plugin_destructor =
      (void (*)(l3d_object *))
      oc->plugin_loader->find_symbol("destructor");
   oc->plugin_copy_data =
      (void (*)(const l3d_object *, l3d_object *))
      oc->plugin_loader->find_symbol("copy_data");

   char plugin_params[4096];
   sprintf(plugin_params, "1d %d %d 1 0 0 0 1 0 0 0 1 soup.obj soup.ppm soup.uv", 0, 0, 0);

   l3d_plugin_environment *e =
      new l3d_plugin_environment
      (texloader, screen->info, scache, (void *)plugin_params);

   if (!oc->plugin_constructor) {
      (*oc->plugin_constructor)(oc, e);
   }

   oc->bounding_sphere.compute_around_object(oc);

   l3d_bspTree *tree;
   tree = new l3d_bspTree;
   tree->root = new l3d_halfspace;
   tree->root->bounding_sphere = oc->bounding_sphere;
   tree->root->object = NULL;
   tree->root->children.num_items = 0;
   tree->root->children[tree->root->children.next_index()] = 0;
   tree->root->children[tree->root->children.next_index()] = 0;

   tree->compute_for_object(tree->root, oc);
   tree->print_stats(tree->root);
   tree->push_poly_to_children(tree->root, NULL);
   tree->print_stats(tree->root);
   tree->make_videoscope_meshes(tree->root);

   delete tree;
   screen->refresh_palette();
   exit(0);
}

my_world::~my_world(void) {
   delete texloader;
   delete scache;
}

main() {
   l3d_dispatcher *d;
   l3d_pipeline_world *p;
   my_world *w;

   factory_manager_v_0_2_choose_factories();
   d = factory_manager_v_0_2_dispatcher_factory->create();

   w = new my_world();
   p = new l3d_pipeline_world(w);
   *pipeline = p;
   d->event_source = w->screen;

   d->start();

   delete d;
   delete p;
   delete w;
}
```

##### 该程序读取 VideoScope 文件 `soup.obj`

该程序读取 VideoScope 文件 `soup.obj`。作为输出，它会写入多个 VideoScope 文件，文件名分别为 `vid0.obj`、`vid1.obj`，依此类推。要查看该程序的功能，请按照以下步骤操作。

- 1. 将 `soup.obj` 加载到 Blender 中。请注意，所有多边形都在同一个网格中，且该网格不是凸的（它有凹陷）。

- 2. 运行示例程序。它会在当前目录中创建 `vid0.obj`、`vid1.obj` 等文件。（在运行程序之前，您可能希望删除当前目录中的这些文件。）

- 3. 在 Blender 中，按 `Ctrl+X` 清除所有内容。然后，加载文件 `vid0.obj`。这也会自动加载 `vid1.obj`、`vid2.obj` 等。请注意，几何体的形状与原始 `soup.obj` 文件中的相同，但叶状 BSP 树已自动将几何体划分为凸子集。换句话说，几何体不再是一个网格，而是由几个凸网格组成。在 Blender 中分别右键单击每个网格，以查看其凸形状。

在示例程序 `bsp` 的二进制文件目录中，还有另一个 VideoScope 网格文件，名为 `uglsoup.obj`。该网格包含许多具有完全随机的 3D 位置和朝向的随机多边形，它们通常相互交叉，并说明了“多边形汤”这个词的含义。将此文件重命名为 `soup.ppm`，然后重新运行程序，以查看叶状 BSP 树如何自动从完全随机的多边形选择中创建凸区域。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_316_0.png)

![](img/a19d4e8b1d7eb6387691dc6c865430e6_317_0.png)

图 5-11：程序 `leafbsp` 对网格的自动凸分割。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_317_1.png)

图 5-12：文件 `uglysoup.obj` 中杂乱的凹形、自相交的多边形汤。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_317_2.png)

图 5-13：自动凸分割的一些部分。

注意：程序 `leafybsp` 通常创建大量凸区域，每个区域仅包含少数几个多边形。这样的树效率不高。通过检查，有时可以识别出可能形成的更好的凸区域，但通常，形成更好的凸区域需要我们在选择分割平面时使用一些指导性的启发式方法，如前所述。

### 轴对齐 BSP 树和迷你 BSP 树

我们迄今为止考虑的 BSP 树结构通过从输入集中选择的多边形中的分割平面来划分空间。另一种 BSP 树仅使用轴对齐平面来划分空间 [MOEL99]；换句话说，每个分割平面必须平行于 `x=0`、`y=0` 或 `z=0` 平面之一。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_318_0.png)

图 5-14：轴对齐 BSP 树。

当一个多边形跨越分割平面时，我们可以像之前一样将其拆分为两个部分，使得每个部分最终位于不同的半空间中。或者，我们可以选择将拆分后的多边形视为位于分割平面“上”，并将它们存储在 BSP 树中该分割平面的层级中，或者将该多边形分配给两个半空间 [MOEL99]。

在给定轴对齐这一额外限制的情况下，分割平面的选择是任意的。我们可以选择将空间精确地拆分为两个大小相等的半部分，或者尝试平衡每个半部分中的多边形数量，或者尝试最大化局部性原则，或者尝试最小化拆分数量，或者使用任何其他能降低对 BSP 树执行所需操作之预期成本的启发式方法。

以前，我们从多边形中选择分割平面；当所有多边形都用完后，树就完成了。对于轴对齐 BSP 树，空间的选择是完全任意的，因此我们需要其他标准来决定何时停止划分平面。例如，我们可以当树的深度达到某个最大限制时停止，或者当空间中的多边形数量低于某个最小限制时停止，或者当 BSP 树节点的实际尺寸低于某个限制时停止。

轴对齐 BSP 树与其底层的多边形几何结构之间的联系比我们要看过的 BSP 树更松散。特别是，我们不能遍历轴对齐 BSP 树来确定树内多边形的完全正确的从后到前的排序。同样，我们不能将多边形推送到树叶并期望形成凸子集。我们可以使用轴对齐 BSP 树进行层级视图空间剔除。由轴对齐 BSP 树形成的体积都是轴对齐的盒子：我们可以将盒子本身与视图空间进行比较，如前所述，或者我们可以为每个盒子计算一个包围球，并将球与视图空间进行比较。我们还可以使用轴对齐 BSP 树来确定节点本身的从后到前或从前往后的遍历顺序（但不是其中的多边形），使用我们之前做的相机位置作为参考：首先绘制从相机看远的半空间中的所有节点，然后绘制近半空间中的所有节点。然而，每个节点可能包含一个或多个多边形，我们没有关于这些多边形的排序信息。这意味着为了正确显示，我们必须诉诸于每个节点内的其他可见性机制。例如，我们可以从后到前绘制所有节点，并在绘制每个节点的多边形之前，对节点内的多边形进行 `z` 排序，如简单的画家算法那样。另一种选择是从前到后绘制所有节点，并以任意顺序绘制每个节点中的多边形，使用 `z` 缓冲来解决可见性问题。

在单个节点内解决多边形排序问题的另一种方法是计算该节点的迷你 BSP 树。迷你 BSP 树仅针对轴对齐 BSP 树中特定节点包含的多边形集计算的小型 BSP 树。通常，迷你 BSP 树是针对多边形的某个较小子集计算的多边形对齐（而非轴对齐）BSP 树，其中该子集整体在更高层级上进行排序或排序。在这种情况下，我们遍历轴对齐 BSP 树的高层级节点来确定节点顺序；然后在每个节点内部，我们使用该节点的迷你 BSP 树（它不是轴对齐的，而是使用多边形的分割平面）来找到该节点内正确的多边形顺序。作为一个整体，这将产生一个完整的、正确的可见性顺序。

### 作为多分辨率实体建模表示的 BSP 树

正如我们在讨论 BSP 树开始时提到的，很遗憾我们不能在这里涵盖 BSP 树的所有用途；更多信息请参阅附录中的参考文献。但关于 BSP 树的最后一个话题值得一提：使用 BSP 树作为多面体实体的表示。与其存储定义多面体对象边界的网格多边形，不如将 BSP 树视为同一多面体对象的体积（而非边界）的表示。换句话说，一组多边形和 BSP 树可以用不同的方式表示相同的几何体；多边形勾勒出对象的外表面，但 BSP 树可以被解释为勾勒出对象占据的实际体积。正如我们稍后所见，这有一些有趣的含义。

首先，让我们探讨一下 BSP 树如何表示体积。这需要我们将 BSP 树的概念扩展，将节点分类为我们称为`分割节点`和`非分割节点`的类型。BSP 树中的每个节点都存储一个分割平面（在生成叶状 BSP 树期间在叶子处创建的新节点有一个值得注意的例外——这是一个我们稍后会回到话题）。因此，BSP 树的每个节点将空间分割为前方和后方区域。我们将这些节点称为分割节点。叶分割节点（即没有子节点的节点）代表 BSP 树内空间的最细（最小）划分。对于每个叶分割节点，让我们添加两个子节点：一个左子节点和一个右子节点，每个都没有分割平面。我们将这些称为非分割节点。这些节点代表位于父节点平面的后方和前方的未再被划分的半空间。请记住，由于沿着无限平面的切片，所有半空间因此所有非分割节点都是凸的。

在确保每个叶分割节点都有两个非分割节点作为子节点之后，BSP 树的所有叶节点现在都是非分割节点。所有非分割节点所代表的空间的并集是树根所代表的整个空间；每个非分割节点是整个区域的一个小凸切割。此外，每个非分割节点都可以根据其相对于其父分割平面的位置进行分类。要么非分割节点是左子节点，位于其父节点平面的后方，要么是右子节点，位于其父节点平面的前方。

在基于多边形的 BSP 树中，我们从输入集中的多边形平面中选择分割平面。物体的内部位于所有多边形的某一特定侧（前侧或后侧）；让我们假设多边形法线指向外部，这意味着物体的内部位于所有多边形的后侧。由于所有分割节点都来自多边形，这意味着物体的内部始终位于所有分割平面的后侧。所有分割平面的后侧是所有作为其父节点左子节点的非分割节点的并集。因此，物体的内部（假设法线向外指向）由 BSP 树中所有作为左子节点的非分割节点组成。类似地，物体的外部是所有作为右子节点的非分割节点的并集。

换句话说，BSP 树的分割节点将空间划分为两个区域：前方和后方区域。由分割节点代表的空间区域是非均匀的，因为它被进一步划分为前方和后方。另一方面，非分割节点代表一个未再被划分的均匀空间区域，并且要么完全属于物体的内部（如果是左子节点），要么属于物体的外部（如果是右子节点）。

我们之前看到的叶状 BSP 树强制将多边形从父节点推送到其子节点，在它们向下移动时进行分割。这个过程会导致新树节点的创建；从树较高位置下来的多边形最终会被推送到叶分割节点的一个半空间中，从而创建一个作为子节点的新非分割节点。再次检查程序 `leafbsp` 的文本输出；你会发现，在将多边形推送到叶子之前，多边形存在于树中所有地方的左节点和右节点中；推送之后，多边形仅存在于树的右、叶、非分割节点中。

（它们存在于右侧子节点而非左侧子节点，这是因为示例网格的多边形法线朝内，而我们将平面上的多边形推至后半空间，而非前半空间。如果使用法线朝外的网格，并修改 `l3d_bsptree` 类，将平面上的多边形推至前半空间，则多边形将出现在左侧非分割叶节点中。）

此前，我们将叶状 BSP 树中每个叶节点内的多边形简单地视为原始输入多边形的凸子集。现在我们可以将叶状 BSP 树的每个叶节点重新解释为非分割节点，从而定义沿通往该非分割节点的路径上所有节点中的平面进行空间分割后形成的凸体积空间。叶节点不再仅仅是多边形的容器，它本身就是一个属于（或不属于，尽管我们在示例程序中并未创建“不属于”节点）对象体积的凸空间。
