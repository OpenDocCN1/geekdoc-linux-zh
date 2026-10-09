

## 类 13d_pipeline_world_lightmapped

类 `13d_pipeline_world_lightmapped` 是一个流水线类，用于处理光照贴图源世界对象所需的新键盘输入。两个新按键是 `p` 和 `r`。按下 `p` 键可在当前摄像机位置放置一个灯。按下 `r` 键可重置表面缓存，从而显示新计算出的光照贴图。

```cpp
List 5-16: pi_lwcr.h

#ifndef PI_LWOR_H
#define _PI_LWOR_H
#include "../tool_os/memman.h"
#include "pi_wor.h"
#include "../geom/world/world.h"

class 13d_pipeline_world_lightmapped: public 13d_pipeline_world {
public:
    13d_pipeline_world_lightmapped(13d_world *w);
    ~13d_pipeline_world();
    void key_event(int ch);
};

#endif
```

```cpp
List 5-17: pi_lwcr.cc

#include "pi_wor.h"
#include <sys/time.h>
#include <unistd.h>
#include <string.h>
#include "../tool_os/memman.h"

void 13d_pipeline_world::key_event(int c) {
    switch(c) {
    case 'q': done = 1;

    // default keys for world->camera movement -- full 360 degree movement
    case 'j': if(world->camera->rot_VUP_velocity<int_to_13d_real(-95)) world->camera->rot_VUP_velocity += int_to_13d_real(5); break;
    case 'l': if(world->camera->rot_VUP_velocity>int_to_13d_real(95)) world->camera->rot_VUP_velocity += int_to_13d_real(5); break;
    case 'J': if(world->camera->rot_VFM_velocity<int_to_13d_real(95)) world->camera->rot_VFM_velocity += int_to_13d_real(5); break;
    case 'L': if(world->camera->rot_VFM_velocity>int_to_13d_real(-95)) world->camera->rot_VFM_velocity += int_to_13d_real(5); break;
    case '1': if(world->camera->rot_VRI_velocity<int_to_13d_real(95)) world->camera->rot_VRI_velocity += int_to_13d_real(5); break;
    case 'K': if(world->camera->rot_VRI_velocity>int_to_13d_real(-95)) world->camera->rot_VRI_velocity += int_to_13d_real(5); break;
    case 's': if(world->camera->VFM_velocity >int_to_13d_real(-90)) world->camera->VFM_velocity -= world->camera->VFM_thrust; break;
    case 'i': if(world->camera->VFM_velocity <int_to_13d_real(90)) world->camera->VFM_velocity += world->camera->VFM_thrust; break;
    case '5': if(world->camera->VRI_velocity <int_to_13d_real(-90)) world->camera->VRI_velocity += world->camera->VRI_thrust; break;
    case 'f': if(world->camera->VRI_velocity >int_to_13d_real(90)) world->camera->VRI_velocity -= world->camera->VRI_thrust; break;
    case 'd': if(world->camera->VUP_velocity >int_to_13d_real(-90)) world->camera->VUP_velocity -= world->camera->VUP_thrust; break;
    case 'v': if(world->camera->VUP_velocity <int_to_13d_real(90)) world->camera->VUP_velocity += world->camera->VUP_thrust; break;

    // field-of-view modification
    case 'X': world->camera->fov = world->camera->fov * float_to_13d_real(0.1); break;
    case 'x': world->camera->fov = world->camera->fov * float_to_13d_real(0.1); break;
    case 'Y': world->camera->fov = world->camera->fov * float_to_13d_real(0.1); break;
    case 'y': world->camera->fov = world->camera->fov * float_to_13d_real(0.1); break;

    // speed
    case 'w': case 'W':
        world->camera->VUP_thrust += int_to_13d_real(1.0);
        if(world->camera->VUP_thrust > 3.0) {
            world->camera->VUP_thrust -= int_to_13d_real(3.0);
        }
        world->camera->VFM_thrust = world->camera->VUP_thrust;
        world->camera->VRI_thrust = world->camera->VUP_thrust;
        break;

    // display
    case 'n': case 'N':
        world->should_display_status = 1-world->should_display_status; // toggle
        break;
    }
}

void 13d_pipeline_world::update_event() {
    world->update_all();
}

void 13d_pipeline_world::draw_event(void) {
    static int frame=0;
    static long last_sec, last_usec;
    long sec, usec;
    static float fps;
    static char str[80];

    struct timeval tv;
    struct timezone tz;
    tz.tz_minuteswest = -60;

    world->rasterizer->clear_buffer();
    world->draw_all();

    frame++;
    if((frame & 0x3F) == 0) {
        gettimeofday(&tv,&tz);
        fps = 64 * 1.0 / ( (tv.tv_sec + tv.tv_usec/1000000.0) - (last_sec + last_usec/1000000.0) );
        last_sec = tv.tv_sec;
        last_usec = tv.tv_usec;
    }
    if(world->should_display_status) {
        sprintf(str,"FPS: %f", fps);
        world->rasterizer->draw_text(0, 0, str);
    }
    world->screen->blit_screen();
}
```

## 示例程序：portlex

本章最后一个示例程序 portlex 是一个简单的例子，使用上述传送门类创建一个室内传送门世界，其中包含完整的对象、灯光和阴影。利用上述用于处理传送门和扇区的类，主程序仅需创建基于新传送门的世界类的一个实例，并请求世界类从文件加载世界数据库，在本例中该文件为 world.dat。

world.dat 的平面图如*图 5-28* 所示。启动程序后，您将位于图中指示的摄像机位置。初始时，场景会相当昏暗。按下 `p` 键可在当前摄像机位置放置一个灯；按下 `r` 键可重置表面缓存并查看新计算出的光照贴图。从起始位置开始，尝试在当前摄像机位置放置几个灯，然后移动到前方较大的房间，以观察传送门光照贴图计算产生的阴影效果。请注意，我们在平面图左下角的房间里放置了三个视频显微镜插件对象。它们的网格从文件 torch.obj 加载。扇区内支持任意对象意味着我们可以自由地在房间内放置道具来布置场景，就像舞台设计师所做的那样。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_370_0.png)

*图 5-28*：程序 *portlex* 的世界数据库平面图。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_370_1.png)

*图 5-29*：程序 *portlex* 中由传送门生成的阴影。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_370_2.png)

*图 5-30*：程序 *portlex* 还可以将任意网格（例如这些火炬）加载到传送门世界中。

