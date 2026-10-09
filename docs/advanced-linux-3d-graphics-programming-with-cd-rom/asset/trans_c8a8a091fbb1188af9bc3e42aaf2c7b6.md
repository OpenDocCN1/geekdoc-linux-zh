
# 第 4 章：可见表面确定 I：通用技术

## 列表 4-16：sc_zmesa.cc

```cpp
#include "sc_zmesa.h"
#include "../tool_os/memman.h"

l3d_screen_zbuf_mesa::l3d_screen_zbuf_mesa (int xsize, int ysize) :
 l3d_screen (xsize, ysize)
{
 int argc=1;
 char *argv[1];
 argv[0] = "a";

 Visual *vis;
 int depth=0, bytespp=0, scan_line_pad=0;
 Display *dpy;
 XPixmapFormatValues *pixmap_formats;
 int i, count;

 dpy = XopenDisplay(NULL);

 pixmap_formats = XListPixmapFormats(dpy, &count);
 for(i=0, depth=0; i<count; i++) {
 if (pixmap_formats[i].depth > depth)
 depth = pixmap_formats[i].depth;
 bytespp = pixmap_formats[i].bits_per_pixel / BITS_PER_BYTE;
 scan_line_pad = pixmap_formats[i].scan_line_pad;
 }
 Xfree(pixmap_formats);
 printf("max depth of display id", depth);
 printf("bytes per pixel: %d", bytespp);

 bufsize = xsize * ysize * bytespp;
 vis = DefaultVisual(dpy,0);

 switch(vis->c_class) {

 case PseudoColor:
 sino = new l3d_screen_info_indexed_mesa(255, 65535, 65535, 65535);
 glutInit(&argc, argv);
 glutInitDisplayMode(GLUT_DOUBLE|GLUT_INDEX|GLUT_DEPTH);
 glutInitWindowSize(xsize, ysize);
 glutInitWindowPosition(100,100);
 glutCreateWindow("l3d");

 glClearColor(0.0,0.0,0.0,0.0);
 glMatrixMode(GL_PROJECTION);
 glLoadIdentity();
 gluOrtho2D(0, xsize, ysize, 0);
 glMatrixMode(GL_MODELVIEW);
 glLoadIdentity();
 glTranslatef(0.375, 0.375, 0.0);
 glViewport(0,0,xsize,ysize);
 break;
 case TrueColor:
 sino = new l3d_screen_info_rgb_mesa(vis->red_mask, vis->green_mask,
 vis->blue_mask, bytespp);
      glutInit(&argc, argv);
      glutInitDisplayMode(GLUT_DOUBLE|GLUT_RGB|GLUT_DEPTH);
      glutInitWindowSize(xsize, ysize);
      glutInitWindowPosition(100,100);
      glutCreateWindow("l3d");

      glClearColor(0.0,0.0,0.0,0.0);
      glMatrixMode(GL_PROJECTION);
      glLoadIdentity();
      gluOrtho2D(0, xsize, ysize, 0);
      glMatrixMode(GL_MODELVIEW);
      glLoadIdentity();
      glTranslatef(0.375, 0.375, 0.0);
      glViewport(0,0,xsize,ysize);

      }

      case StaticColor: printf("unsupported visual StaticColor");break;
      case GrayScale:    printf("unsupported visual GrayScale");break;
      case StaticGray:   printf("unsupported visual StaticGray");break;
      case DirectColor:  printf("unsupported visual DirectColor");break;
      }

      }

      l3d_screen_zbuf_mesa::~l3d_screen_zbuf_mesa(void) {
      }

      inline void l3d_screen_zbuf_mesa::blit_screen(void) {
         glutSwapBuffers();
         glFlush();
      }

      void l3d_screen_zbuf_mesa::open_screen(void) {
      }
```

## 列表 4-17：ras3z_mesa.h

```cpp
#ifndef _RAS3Z_MESA_H
#define _RAS3Z_MESA_H

#include "../tool_os/memman.h"
#include "ras3z_mesa.h"

class l3d_rasterizer_3d_zbuf_mesa_imp {
    public:
        l3d_rasterizer_3d_zbuf_mesa_imp(int xs, int ys, l3d_screen_info *si);
        virtual ~l3d_rasterizer_3d_zbuf_mesa_imp(void);
        void clear_buffer(void);
};

class l3d_rasterizer_3d_zbuf_mesa_imp_factory :
    public l3d_rasterizer_3d_imp_factory {
    public:
        l3d_rasterizer_3d_imp *create(int xs, int ys, l3d_screen_info *si);
};

#endif
```

## 列表 4-18：ras3z_mesa.cc

```cpp
#include "ras3z_mesa.h"
#include "GL/gl.h"
#include "GL/glu.h"
#include "GL/glut.h"
#include "../tool_os/memman.h"

l3d_rasterizer_3d_imp *l3d_rasterizer_3d_zbuf_mesa_imp_factory::create (int xs, int ys, l3d_screen_info *si) {
    return new l3d_rasterizer_3d_zbuf_mesa_imp(xs, ys, si);
}

l3d_rasterizer_3d_zbuf_mesa_imp::
l3d_rasterizer_3d_zbuf_mesa_imp(int xs, int ys, l3d_screen_info *si) :
    l3d_rasterizer_3d_imp(xs, ys, si),
    l3d_rasterizer_2d_mesa_imp(xs, ys, si) {
    glEnable(GL_DEPTH_TEST);
}

l3d_rasterizer_3d_zbuf_mesa_imp::~l3d_rasterizer_3d_zbuf_mesa_imp(void) {
}

void l3d_rasterizer_3d_zbuf_mesa_imp::clear_buffer(void) {
    l3d_rasterizer_2d_mesa_imp::clear_buffer();
    glClear(GL_DEPTH_BUFFER_BIT);
}
```

## Z 缓存光栅器的工厂管理器

为了使 13d 程序能够使用光栅器的 z 缓存版本，我们需要提供一个新的工厂管理器，允许选择生成新光栅器的工厂。`l3d_factory_manager_v_0_3` 类正是这样做的。它在初始工厂选择菜单中增加了三个新选项，这些选项分别是前三项选择的 z 缓存版本。

## 列表 4-19：fact0_3.h

```cpp
#ifndef FACTO_3_H
#define FACTO_3_H

#include "../tool_os/memman.h"
#include "fact0_2.h"

class l3d_factory_manager_v_0_3 : public l3d_factory_manager_v_0_2 {
    public:
        l3d_factory_manager_v_0_3(void);
        virtual ~l3d_factory_manager_v_0_3(void);
        int choose_factories(void);
};

extern l3d_factory_manager_v_0_3 factory_manager_v_0_3;

#endif
```

## 列表 4-20：fact0_3.cc

```cpp
#include "fact0_3.h"

#include <stdio.h>

#include "../tool_os/dis_x11.h"
#include "../tool_os/dis_mesa.h"
#include "../tool_2d/sc_x11shm.h"
#include "../tool_2d/sc_mesa.h"
#include "../raster/ras3_sw.h"
#include "../raster/ras3_mesa.h"
#include "../raster/ras3z_gl_linux.h"
#include "../raster/ras3z_sw.h"
#include "../raster/ras3z_mesa.h"
#include "../tool_2d/sc_zmesa.h"
#include "../tool_os/memman.h"

l3d_factory_manager_v_0_3 factory_manager_v_0_3;

l3d_factory_manager_v_0_3::l3d_factory_manager_v_0_3(void) :
    l3d_factory_manager_v_0_2()
{
}

l3d_factory_manager_v_0_3::~l3d_factory_manager_v_0_3(void)
{
}

int l3d_factory_manager_v_0_3::choose_factories(void) {

    char input[80];
    int i;

    printf("which configuration?");
    printf("(1. Software X11)");
    printf("(2. Software X11 with SHM extension)");
    printf("(3. Mesa (with 3DFX h/w accel if installed with Mesa))");
    printf("(4. Software X11 with z buffer and fog)");
    printf("(5. Software X11 with SHM, z buffer, and fog)");
    printf("(6. Mesa with z buffer");
    gets(input);
    i = atoi(input);
    switch(i) {

    case 1:
        screen_factory = new l3d_screen_factory_x11;
        ras_2d_imp_factory = new l3d_rasterizer_2d_sw_imp_factory;
        dispatcher_factory = new l3d_dispatcher_factory_x11;
        ras_3d_imp_factory = new l3d_rasterizer_3d_sw_imp_factory;
        plugin_loader_factory = new l3d_plugin_loader_linux_factory;
        break;

    case 2:
        screen_factory = new l3d_screen_factory_x11_shm;
        ras_2d_imp_factory = new l3d_rasterizer_2d_sw_imp_factory;
        dispatcher_factory = new l3d_dispatcher_factory_x11;
        ras_3d_imp_factory = new l3d_rasterizer_3d_sw_imp_factory;
        plugin_loader_factory = new l3d_plugin_loader_linux_factory;
        break;

    case 3:
        screen_factory = new l3d_screen_factory_mesa;
        ras_2d_imp_factory = new l3d_rasterizer_2d_mesa_imp_factory;
        dispatcher_factory = new l3d_dispatcher_factory_mesa;
        ras_3d_imp_factory = new l3d_rasterizer_3d_mesa_imp_factory;
        plugin_loader_factory = new l3d_plugin_loader_linux_factory;
        break;

    case 4:
        screen_factory = new l3d_screen_factory_x11;
        ras_2d_imp_factory = new l3d_rasterizer_2d_sw_imp_factory;
        dispatcher_factory = new l3d_dispatcher_factory_x11;
        ras_3d_imp_factory = new l3d_rasterizer_3d_zbuf_sw_imp_factory;
        plugin_loader_factory = new l3d_plugin_loader_x11_factory;
        break;

    case 5:
        screen_factory = new l3d_screen_factory_x11_shm;
        ras_2d_imp_factory = new l3d_rasterizer_2d_sw_imp_factory;
        dispatcher_factory = new l3d_dispatcher_factory_x11;
        ras_3d_imp_factory = new l3d_rasterizer_3d_zbuf_sw_imp_factory;
        plugin_loader_factory = new l3d_plugin_loader_linux_factory;
        break;

    case 6:
        screen_factory = new l3d_screen_factory_zbuf_mesa;
        ras_2d_imp_factory = new l3d_rasterizer_2d_mesa_imp_factory;
        dispatcher_factory = new l3d_dispatcher_factory_mesa;
        ras_3d_imp_factory = new l3d_rasterizer_3d_zbuf_mesa_imp_factory;
        plugin_loader_factory = new l3d_plugin_loader_linux_factory;
        break;
    }

    factory_manager_v_0_2 = *this;
    factory_manager_v_0_2.should_delete_factories = 0;
    return 1;
}
```

## 示例程序：texzbuf

示例程序 `texzbuf` 与示例程序 `textest` 相同，只是主程序文件更改为使用新的工厂管理器。它显示两个相交的金字塔，一个是静态的，另一个是旋转的。运行该程序，并选择工厂 4、5 或 6 之一，即可看到 z 缓存的效果。仔细观察两个金字塔对象相交的区域。在之前的程序 `textest` 中（以及在程序 `texzbuf` 中，如果你选择了工厂 1、2 或 3），贯穿多边形会立即从被贯穿多边形的翻转到其后方，这是使用简单画家算法的结果。在使用新程序 `texzbuf` 以及新的 z 缓存工厂 4、5 或 6 之一时，金字塔对象之间的相交区域被正确绘制。注意，一个金字塔的尖端看起来确实贯穿了另一个金字塔的面，金字塔对象之间存在一条清晰的交线，反映了每个多边形每个像素的真实 3D 位置。再次强调，这是 z 缓存算法的优势之一：它对像素级是精确的，即使对于相交的多边形也是如此，并且无需分割多边形即可产生正确的显示。

