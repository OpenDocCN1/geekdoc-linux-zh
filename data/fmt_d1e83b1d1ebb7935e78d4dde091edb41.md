
```cpp
#include <string.h>
#include "../tool_os/memman.h"

void I3d_pipeline_world::key_event(int c) {
    switch(c) {
        case 'q': done = 1;
        // world->camera_movement 的默认键 -- 全 360 度移动
        case 'j': if(world->camera->rot_VUP_velocity+int_to_3d_real(-95)) world->camera->rot_VUP_velocity
            ++int_to3d_real(5);
        case 'i': if(world->camera->rot_VUP_velocity+int_to_3d_real(95)) world->camera->rot_VUP_velocity
            ++int_to3d_real(5);
        case 'j': if(world->camera->rot_VFW_velocity+int_to_3d_real(95)) world->camera->rot_VFW_velocity
            ++int_to3d_real(5);
        case 'l': if(world->camera->rot_VFW_velocity+int_to_3d_real(-95)) world->camera->rot_VFW_velocity
            ++int_to3d_real(5);
        case 'm': if(world->camera->rot_VRI_velocity+int_to_3d_real(95)) world->camera->rot_VRI_velocity
            ++int_to3d_real(5);
        case 'k': if(world->camera->rot_VRI_velocity+int_to_3d_real(-95)) world->camera->rot_VRI_velocity
            ++int_to3d_real(5);
        case 'v': if(world->camera->rot_VFW_velocity+int_to_3d_real(-95)) world->camera->rot_VFW_velocity
            ++int_to3d_real(5);
        case 'f': if(world->camera->rot_VFW_velocity+int_to_3d_real(95)) world->camera->rot_VFW_velocity
            ++int_to3d_real(5);
        case 'u': if(world->camera->rot_VRI_velocity+int_to_3d_real(-95)) world->camera->rot_VRI_velocity
            ++int_to3d_real(5);
        case 'h': if(world->camera->rot_VRI_velocity+int_to_3d_real(95)) world->camera->rot_VRI_velocity
            ++int_to3d_real(5);
        case 'd': if(world->camera->rot_VUP_velocity+int_to_3d_real(-95)) world->camera->rot_VUP_velocity
            ++int_to3d_real(5);
        case 'e': if(world->camera->rot_VUP_velocity+int_to_3d_real(95)) world->camera->rot_VUP_velocity
            ++int_to3d_real(5);

        // 视场
        case 'x': world->camera->foxx += int_to_3d_real(0.1);
        case 'a': world->camera->foxx -= int_to_3d_real(0.1);
        case 'y': world->camera->fy += int_to_3d_real(0.1);
        case 's': world->camera->fy -= int_to_3d_real(0.1);

        // 速度
        case 'v':
            world->camera->VUP_thrust += int_to_3d_real(1.0);
            if(world->camera->VUP_thrust > 3.0) {
                world->camera->VUP_thrust -= int_to_3d_real(3.0);
            }
            world->camera->VFW_thrust = world->camera->VUP_thrust;
            world->camera->VRI_thrust = world->camera->VUP_thrust;
            break;

        // 显示
        case 'n': case 'N':
            world->should_display_status = 1-world->should_display_status; // 切换
            break;
    }
}
void I3d_pipeline_world::update_event() {
world->update_all();
}
```

## 第 7 章：3D 中的多边形建模与渲染

`blit` 本身并没有这样做。它本质上是将绘制过程转发给世界对象。在世界对象完成自身的绘制后，该方法执行了一个我们尚未见过的新操作：计算每秒帧数，也称为 `FPS` 或帧率。随着我们的世界复杂性增加，观察应用程序性能如何维持 `FPS` 将是非常有趣的。我们使用 64 帧。为了计算 `FPS`，我们每 64 帧获取一次系统时钟时间。我们使用 64 帧而不是仅 1 帧，是为了获得几帧的平均 `FPS`。然后我们用 64 帧前的时钟时间减去当前时间。这得出了绘制 64 帧所需的经过秒数。因此，我们将 64 帧除以经过秒数即可得到每秒帧数。物理时钟时间是通过函数 `gettimeofday` 获取的，该函数接受时区结构作为输入参数，并用当天的当前时间填充时间结构体。`tv_sec` 和 `tv_use` 字段提供了自 1970 年 1 月 1 日 00:00:00 来的经过秒数和微秒。我们并不关心实际值；我们关心的是当前时间与 64 帧之前的时间差。计算 `FPS` 后，我们使用 3D 栅化器的 `draw_text` 方法将其显示；这会将字符串作为一系列形成字符的像素绘制到栅化器缓冲区（`buffer`）中。

因此，`l3d_pipeline` 类本质上将它的大部分处理工作转发给了世界对象。它调用了世界对象的两个重要函数：`update_all` 和 `draw_all`。这两个函数构成了流水线与世界对象之间的接口。让我们分别查看每一个。

### 更新整个世界

由于一个世界由自主的 3D 对象组成，并且每个对象都知道通过 `l3d_object::update` 方法如何更新自己，因此世界必须允许每个对象通过调用每个对象上的 `update` 来更新自己。这正是 `l3d_world::update_all` 方法所做的。它遍历世界数据库中的所有对象，并对每个对象调用 `update`。它还调用了世界中相机对象的 `update`，因为相机不在世界数据库中，但在对象更新时它也需要被更新。注意，如果世界数据库包含许多对象，我们可能不希望允许所有对象每帧都更新自己；相反，我们可能想根据与相机的距离等某些标准定义世界的“活跃区域”和“非活跃区域”。然后我们就可以每帧更新世界的某些部分——活跃区域——其微的奇特之处在于世界的非活跃区域被“冻结在了时间中”。当相机靠近世界的非活跃区域时，我们可以将它们变为活跃区域，同时让更多遥远的非活跃区域也变为活跃。

### 绘制整个世界

流水线调用 `l3d_world::draw_all` 让世界进行自我绘制。我们通过遍历世界数据库中的所有对象来实现这一点。然后，我们使用其复合 `modeling_xform_array` 将其转换到世界空间，然后将其转换到相机空间。在相机空间中，我们根据 z 裁剪平面（`z-clip plane`）对对象的所有多边形进行剪裁（`clip`），如果一个多边形被完全裁剪掉，则将其从链表中移除。对于所有幸存的多边形，我们应用透视投影，然后将投影后的 2D 多边形裁剪到屏幕上。这一切我们在之前的程序 `clip` 中都见过。

新奇的是对于准备好显示在屏幕上的幸存多边形发生了什么。我们没有像在 `clip` 程序中那样的立即绘制它们，而是将该对象的幸存多边形插入到一个公共的多边形数组中，然后处理下一个对象。……插入到公共数组中而不是立即绘制。以这种方式处理所有对象的多边形。

在处理所有对象之后、绘制任何内容之前，我们得到了一个数组，其中包含所有通过剪裁操作的多边形指针（包括 2D 和 3D），它们已准备好显示在屏幕上。图 7-22。

![](img/49715b3934121066e59e93823d33ee3a_488_0.png)

> 图 7-22：处理所有对象以找到幸存的多边形。所有幸存的多边形在绘制前插入到一个公共列表中。

在绘制多边形之前，我们调用 `qsort` 对多边形列表进行排序。`qsort` 函数可以排序任何同构项的数组，但需要一个辅助函数来告诉它如何比较项以便元素排在前面。但我们应该使用什么标准来对多边形排序，为什么要费力排序多边形呢？这个问题涉及了可见性检测（`visible detection`）或隐藏表面移除（`hidden surface removal`）这一非常广泛的领域，配套书籍《Advanced Linux 3D Graphics Programming》中有更详细的介绍。如果你仔细观察 `clip` 程序，你会发现一些异常的绘制错误。特别是，离你较近的对象有时会被离你较远的较小对象遮挡。实际上，这是不可能的：来自较远对象的光线被较近的对象阻挡，这意味着我们看到较近的对象在较远的对象前面（此处原文应为在前面）。

![](img/49715b3934121066e59e93823d33ee3a_488_1.png)

> 图 7-23：随机顺序绘制多边形意味着物理上更远的多边形可能会阻塞物理上更近的多边形——这在物理上是不可能的。在这里，前景的大金字塔本应遮挡它背后的所有多边形，但由于绘制顺序错误，位于它后面的多边形被绘制了。

### 第 7 章：3D 中的多边形建模与渲染

`clipz` 中绘制异常的原因是我们没有关注多边形的物理距离。每当我们发现投影顶点在屏幕内的多边形时，立即将其绘制到屏幕上，即使那里已经有了内容。我们可以把屏幕比作画家的画布：如果我们在已有内容的地方绘制，就会覆盖掉之前的。`clipz` 的问题在于我们的绘制顺序基本上是随机的。可能我们先了一些近的多边形，随后又处理较远的多边形。由于我们绘制了可见的多边形，后处理的会遮挡近的对象。想象一个画家先画前景的房子，然后在背景画山上。结果是背景物体遮挡了前景物体。

> 图 7-24：如果画家先画前景，然后在上方画背景，结果在物理上是不正确的。

![](img/49715b3934121066e59e93823d33ee3a_489_0.png)

继续这种类比引出了画家算法：先绘制背景，然后在背景上方绘制前景。

> 图 7-25：画家算法。先绘制背景，再绘制前景。

![](img/49715b3934121066e59e93823d33ee3a_489_1.png)

回到我们的多边形数组，我们将背景多边形定义为相机坐标中 z 值最大的。同样，前景多边形是相机坐标中 z 值最小的。这种推理为 `qsort` 例程提供了排序标准：我们按 z 值从大到小对多边形数组进行排序，然后才绘制。结果是从远到近排序，这样最近的最后绘制，不会遮挡任何更远的多边形。

`compare_facet_zdepth` 函数是 `qsort` 的辅助函数，它按 z 减序排序多边形。我们用于排序的 z 值是多边形所有顶点空间 z 值的平均值。方便的是，`l3d_object` 类将其所有多边形的相机坐标保存在变换中间值 1 中。因此，我们现在只需要检索之前保存的变换中间坐标 1 的 z 分量即可。

### 第 7 章：3D 中的多边形建模与渲染

![](img/49715b3934121066e59e93823d33ee3a_490_0.png)

画家算法（`the painter's algorithm`）是可见表面算法中最简单且最易理解的算法之一，它在大多数情况下都能返回基本正确的结果，但在所有情况下都不是理想的。请参阅配套书籍《高级 Linux 3D 图形学编程》以了解对其他技术的讨论。

最后，世界级使用光栅化器 `draw_text` 来显示文本消息，指示发送到光栅化器绘制的多边形数量。通过输入 `n` 可以开启或关闭此显示。

## 示例程序：flitsim

我们已经见过许多用于从 3D 多边形构建世界的类。在最底层，我们有单个多边形 `1d_polygon_3d`。在更高层级上，我们有 3D 多边形对象 `3d_object`。最后，我们完成了 3D 世界 `3d_world`。

现在，让我们来看一个示例程序 `flitsim`，它使用这些类来创建一个 3D 世界。参见代码列表 7-17、7-18 和 7-19。该程序具有与 `camspikes` 程序相同的键盘控制功能。它创建了一个 `1d_world` 并用许多 3D 对象填充该世界，这些对象包括子类 `13d_objects` 和插件 `3d_objects`。你可以在飞行模拟器中自由地穿过场景，这就是 `flitsim` 名称的由来，即使景观有些简单。该程序的目的主要是为了说明 `world`、`object` 和 `polygon` 类的用法。作为一个练习，你可能想尝试编写一个 3D 对象插件，绘制出更有趣的景观。

当你运行程序 `flitsim` 时，你将看到一长排旋转的金字塔。如果你在程序显示 3D 窗口后立即将世界略微向右旋转（按 `I`），你还将看到一个更远的金字塔，它旋转得较慢，并且绕着不同的轴旋转。

注意：要执行此程序，你必须编译插件文件，以便它们可以在运行时加载。在 `$L3D` 目录下执行 `make -f makeall.inx` 来编译所有内容，包括插件文件。详情请参见附录。插件文件位于 `L3D/bin/linux_x/float/app/lib/dynamics/plugins` 目录。

这一长排金字塔都是子类 3D 对象。远处旋转较慢的金字塔是一个 3D 对象。我们将查看每一个。

代码列表 7-17：main.cc，程序 `flitsim` 的主程序文件

```cpp
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <math.h>

#include "../lib/geom/object/object3d.h"
#include "../lib/geom/polygon/p3_flat.h"
#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/dispatch.h"
#include "../lib/raster/raster3.h"
#include "../lib/tool_2d/scinfo.h"
#include "../lib/geom/world/world.h"
#include "../lib/system/facto_2.h"
#include "../lib/pipeline/pi_war.h"
#include "../lib/dynamics/plugins/plugenv.h"

#include "shapes.h"
#include <stdarg.h>
```

```cpp
class my_world:public l3d_world {
public:
    my_world(void);
};

my_world::my_world(void)
    : l3d(640,400)
{
    l3d_screen_info *si = screen_sinfo;

    camera->VRP.set(0,0,-50);
    camera->near_z = float_to_l3d_real(5.5);
    camera->far_z = int_to_l3d_real(500);

    int i,j,k,num=0;

    i=10; j=20; k+=20;
    k=0;

    // 创建一些金字塔对象
    for(i=1; i<=200; i+=20) {
        objects[num_objects.objects.next_index()] = new_pyramid();
        l3d_screen_info_indexed *si_idx;
        l3d_screen_info_rgb *si_rgb;
```
