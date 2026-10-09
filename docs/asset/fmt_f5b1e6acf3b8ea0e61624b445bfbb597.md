
每当应用程序窗口中按下键时，`key_event` 函数就会自动调用。调用时传入的参数表示按键的 ASCII 值，从而允许应用程序响应特定的按键。

## 第二2章：访问屏幕

当应用程序允许更新自身时，`update_event` 函数会被自动调用。你可以将你的程序想象成一个巨大的时钟装置，一切都在时钟的每一次滴答中发生。这个函数代表了你程序中的一次“滴答”。通过此点，你可以更新存储各种对象位置的内部变量、更新速度、检查碰撞等。

> 提示：`update_event` 的频率并不保证是恒定的。这意味着，连续调用之间流逝的时间可能会略有不同。对于精确的物理模拟（即需要根据时间更新速度或其他物理量），我们可以存储一个内部变量，记录上一次调用 `update_event` 时的系统时钟时间。然后，我们可以比较当前系统时钟与该变量的值，以确定经过了多少物理时间，并更新与时间相关的变量。配套书籍《高级 Linux 3D 图形编程》中包含了此类代码的示例。

当应用程序允许绘制屏幕时，`draw_event` 函数会被调用。该函数通常在 `update_event` 之后立即被调用，但并非一定如此。换句话说，虚拟世界的更新和虚拟世界的绘制可以被视为两个独立的控制线程，它们是有用的但并不一定同步。

在对流水线结构（屏幕创建、变量存储和事件响应）有了通用的理解后，我们可以更仔细一下 `drawdot` 程序中流水线的具体细节。

`drawdot` 流水线的构造函数负责 `l3d_pipeline` 类的第一个职责：创建屏幕、光栅化器实现和光栅化器对象。在构造函数中，我们首先请求屏幕工厂创建一个屏幕，并请求光栅化器实现因子创建一个使用所创建的光栅化器实现的类。成员变量 `s`、`ri` 和 `r` 分别代表屏幕、光栅化器和光栅化器。

构造函数还负责 `l3d_pipeline` 类的第二个职责：代表我们虚拟世界的数据管理。在我们的案例中，虚拟世界由单个像素组成（一个谦虚的开始）。声明并初始化了以下成员变量以跟踪点的状态：`color`、`x`、`y`、`dx` 和 `dy`。我们更新点的颜色、水平和垂直位置以及速度，它们都已初始化为零。变量 `color` 代表点的颜色，绿色和蓝色值为 255。然后，如果我们指定颜色为 `(0, 255, 128)`，这意味着红色强度为 0，绿色强度为 255，蓝色强度为 128，所有值都是相对于我们刚刚设置的 255 逻辑最大值衡量的。最后，我们将此 RGB 转换为适用于当前颜色深度和颜色模型的“原生”颜色。该转换通过类型为 `l3d_screen_info` 的对象完成，该对象封装了之前讨论的颜色计算。颜色转换函数为 `ext_to_native`，因为它将颜色从“外部”RGB 格式转换为 XImage 的“原生”格式。

## 第二2章：评估屏幕

`drawdot` 流水线重写了 `key_event`、`update_event` 和 `draw_event` 方法以响应事件。这完成了 `l3d_pipeline` 类的第三也是也是最后一个职责：响应事件。

`drawdot` 流水线的 `key_event` 检查是否有任何一个方向键被按下，并相应更新代表水平和垂直速度的 `dx` 和 `dy` 变量。

`drawdot` 流水线的 `update_event` 将速度添加到位置变量中，并确保位置保持在屏幕范围内。换句话说，`x += dx` 和 `y += dy`。

`drawdot` 流水线的 `draw_event` 首先调用光栅化器的 `draw_point` 例，然后将请求转发给光栅化器实现，以特定的颜色在特定的点绘制像素。记住，绘制是离屏的（双缓冲）。像素颜色必须指定为当前深度和颜色的“原生”格式。我们之前已经使用 `l3d_screen_info:ext_to_native` 函数计算并存储了这种颜色。在绘制该点之后，我们可以使用 `blit_screen` 将离屏图形拷贝到屏幕上。

让我们总结一下流水线背的核心思想。流水线代表了应用程序的主要功能，并派生自 `l3d_pipeline`。`l3d_pipeline` 子类有三个职责：
- 创建屏幕访问对象（屏幕、光栅化器实现和光栅化器），允许访问屏幕和屏幕绘制函数。
- 声明世界数据，允许程序能够跟踪虚拟世界中所有对象的状态。
- 响应事件是流水线响应输入（通过 `key_event`）、更新虚拟世界（通过 `update_event`）以及绘制到屏幕（通过 `draw_event`）的方式，使用之前创建的屏幕访问对象。

流水线不需要担心事件何时以及如何发生；它只需做出响应。因此，流水线的虚拟事件函数从外部源调用。这个源就是分发器。

## 第 3 步：创建分发器

编写 `l3d` 应用程序的第三步是创建一个事件分发对象。事件分发器作为事件源和事件接收者之间的接口。在我们的案例中，事件接收者是流水线。事件源是在特定事件驱动窗口系统下创建的窗口。分发器的作用是从特定系统的窗口接收事件，并调用相应的流水线函数来响应事件。

整个核心思想是将流水线（即你的应用程序逻辑）与底层事件系统的细节隔离开。

# 第 2 章：评估屏幕

接下来的章节将从视角进行介绍。再次，这些类并没有引入任何我们尚未涵盖过的概念。然而，它们将这些概念重新组织为通用的、可用的抽象类。

主应用程序由 `l3d_pipeline` 派生。`l3d_dispatcher` 从 `l3d_event_source` 获取事件，并自动调用 `l3d_pipeline` 中相应的事件处理例程。`l3d_dispatcher_x11` 类是 X 分发器。

`l3d_screen` 类派生自 `l3d_event_source`，表示一个输出设备，`l3d_rasterizer_2_imp` 可以在其中绘图。在这一模型下，屏幕还必须向其他对象提供事件通知，这是父类 `l3d_event_source` 的职责。`l3d_screen_x11` 类是 X 下的一个子类，形式为包含一个 `Ximage` 的 X 窗口。

`l3d_rasterizer2` 类表示 2D 栅格化概念的高级接口；`l3d_rasterizer_2_imp` 表示使用软件或硬件进行 2D 栅格化的低级实现。`l3d_users` 使用 `l3d_rasterizer_2_imp` 执行工作。`l3d_rasterizer_2_sw_imp` 是软件栅格器实现。

`l3d_screen_info` 类为栅格器实现提供关于屏幕的信息，这些信息对于执行栅格化是必要的。`ext_to_native` 函数透明地将 RGB 颜色转换为屏幕所需的原生位格式——无论深度和色彩模型如何。`light_native` 和 `fog_native` 方法对原生格式的特定颜色应用光照或雾，从而适当更改颜色。`l3d_screen_info_rgb` 类处理基于 RGB 颜色规范的屏幕信息，而 `l3d_screen_indexed` 类处理基于索引颜色模型的屏幕信息。`l3d_screen_indexed` 管理 RGB 颜色调色板，这是一个包含类型 `l3d_rgb` 条目的动态分配数组。

`l3d_factory_manager_v_0_1` 类是工厂管理器，用于集中管理程序中的所有工厂。该类的一个全局实例会被自动创建，名称为 `factory_l3d_factory_manager_v_0_1`。应用程序通过变量 `factory_manager_y_v_0_1` 选择其工厂。

使用 `l3d` 的应用程序将遵循 `drawdot` 所示的五步过程：选择工厂、声明派生类、创建分发器、创建启动分发器。工厂是通过调用 `l3d_factory_manager_v_0_1_factories` 来选择的。目前，所选的工厂类型为 `l3d_dispatcher_factory_x11` 和 `l3d_rasterizer_2_sw_imp_factory`。这意味着分发器（`l3d_dispatcher_x11`）知道如何处理 X 事件，且屏幕（`l3d_screen_x11`）知道如何与显示 `Ximages` 通信；离屏缓冲区是使用 2D 软件栅格器实现（`l3d_rasterizer_2_sw_imp`）绘制的。

注意：稍后，我们必须使用硬件加速的栅格器实现和共享内存屏幕工厂。因此，上一个段并不是规定使用 `l3d` 的 X 应用程序始终使用哪些类的硬性规则；它仅仅阐明了基于我们目前为止所见概念的典型结构。

# 13d 类源码走读

在对 `13d` 类进行了上述述述概述后，我们现在可以深入研究类本身的源代码。请记住，你已经看过了即将呈现的所有内容，只是以不那么通用的形式。

接下来的章节将详细描述在本章中使用的每个 `13d` 类。我们首先描述该类所表示的数据的通用类型，并提到我们在之前的讨论中首次遇到该概念的地方。然后，我们列出类中每个成员变量和函数的含义。每个类都以其完整的源代码形式呈现。当多个类协同工作时，在最后一个类的描述之后将展示类图，说明类与类之间的关系。最后，将为到目前为止讨论的所有 `13d` 类提供一张类图。

在阅读后续章节时，你可能会发现参考之前的 `13d` 类概述以及结论的类图将很有帮助，这有助于保持全局视角。

# 抽象事件驱动的图形应用程序：13d_pipeline

`13d_pipeline` 类是一个表示你的应用程序的抽象类。正如我们之前看到的，你从 `13d_pipeline` 派生以创建应用程序，并且必须履行三个职责：创建屏幕访问对象、声明世界数据以及响应事件。

我们首先在示例程序 `hello_oo` 中看到了这个概念，它使用了一个抽象类。

成员变量 `done` 是一个标志，指示流水线已完全完成处理；换句话说，应用程序应该退出。该变量初始化为零，通常在 `key_event` 某处被设置，以响应用户按键退出应用程序流水线。该变量的值由事件分发器对象检查。

列表 2-24：pipeline.h

```
#ifndef __PIPELINE_H

#define __PIPELINE_H

#include "../tool_os/memman.h"

class 13d_pipeline {

public:

    int done;

    virtual void draw() = 0;

    virtual void update() = 0;

    virtual void key(int event) = 0;

};
```

# 抽象事件生成：13d_event_source

`13d_event_source` 类是一个空类，其唯一目的是指示任何派自它的类都能生成事件。我们首先在示例程序 `hello_oo` 中看到这个概念。在我们的案例中，`13d_event_source` 是一个与屏幕相关的对象。

列表 2-25：ev_src.h

```
#ifndef EV_SRC_H

#define EV_SRC_H

#include "../tool_os/memman.h"

class 13d_event_source {

};
```

# 抽象调度循环：13d_dispatcher

`13d_dispatcher` 类是一个表示分发机制的抽象类。我们首先在程序 `hello_oo` 中看到这个概念。在我们的案例中，`13d_dispatcher` 是事件循环的子类。

列表 2-26：dispatch.h

```
#ifndef _DISPATCH_H

#define _DISPATCH_H

#include "../tool_os/memman.h"

#include "../tool_2/screen.h"

#include "../pipeline/pipeline.h"

class 13d_dispatcher {

public:

    13d_pipeline *pipeline;

    13d_event_source *event_source;

    virtual void start() = 0;

};
```

# 访问屏幕

变量 `pipeline` 指向在事件发生时应调用的流水线。变量 `event_source` 指向以系统特定方式生成事件的对象。在我们的案例中，`event_source` 是一个屏幕对象。

`start` 方法启动事件循环，在来自事件源的相关事件发生时控制相应的流水线虚函数。

图 2-21 展示了抽象类 `13d_pipeline`、`13d_dispatcher` 和 `13d_event_source` 之间的关系。

（注：此处原文为类图描述，由于 Markdown 无法直接渲染复杂类图，译文保持了描述文字的逻辑对应）

图 2-21：事件相关类的类图。

# X 的分发器：13d_dispatcher_x11

`13d_dispatcher_x11` 类派生自 `13d_dispatcher`，表示特定于 X 窗口系统的分发器。与父类 `13d_dispatcher` 一样，我们首先在程序 `hello_oo` 中看到这个概念。

列表 2-27：dis_13d_x.h

```
#ifndef _13D_X11_H

#define _13D_X11_H

#include "./tool/os/memman.h"

#include <X11/Intrinsic.h>

#include <X11/Xlib.h>

#include "dispatch.h"

#include "../tool_2/sc_x11.h"

class 13d_dispatcher_x11 : public 13d_dispatcher {

public:

  void start(void);

};

class 13d_dispatcher_factory_x11 : public 13d_dispatcher_factory {
public:
  virtual 13d_dispatcher *create(void) = 0;
};
```

# 第2章：访问屏幕

```cpp
public:

    3d_dispatcher *create(void) {

        return new 3d_dispatcher_x11;

    }

#endif
```

**列表 2-28: dis_x11.cc**

```cpp
#include "3d_x11.h"

#include "../Tool/os/memman.h"

void 3d_dispatcher_x11::start(void) {

    XEvent event;

    char ch;

    KeySym keysym;

    XStatus status;

    3d_screen_x11 *screen;

    screen = (3d_screen_x11 *)event_source;

    while (pipeline->done) {

        if (XCheckWindowEvent(screen->dpy, screen->screen->w, KeyPressMask, &event)) {

            XLookupString(&event.xkey.key_code, &ch, 1, &keysym, xcompat);

            pipeline->event_key(ch);

        }

        pipeline->update_event();

        pipeline->draw_event();

        XSync(screen->dpy, false);

    }

}
```

方法 `start` 被重写并拦截了类型为 `3d_screen_x11` 的对象的 `event_source`。它从 X11 屏幕中提取显示器和窗口变量，使用 `XCheckWindowEvent` 检查键盘事件，并将这些事件翻译为流水线（`pipeline`）上的虚拟调用。每次遍历事件循环都会执行此操作，请注意这些事件发生的频率取决于操作系统允许的最快。最后，我们调用 `Sync` 以确保输出确实显示在屏幕上；否则，X 服务器可能会将事件（包括显示请求）排队，导致输出在 X 窗口内真正可见之前产生不定的延迟。调用 `Sync` 可以保证输出是立即可见的。

## 抽象屏幕控制：3d_screen

`3d_screen` 和 `3d_screen_info` 类紧密配合，以控制并提供对显示硬件的访问。

`3d_screen` 是显示设备的抽象接口。屏幕负责对已绘制到屏幕上的数据进行创建、设置和显示。屏幕本身并不负责绘图。换句话说，屏幕是一个“哑”显示设备。它可以显示自己、初始化调色板等，但它不知道如何绘制多边形、线、点或任何其他内容。屏幕仅仅是一个被动显示设备，其他对象可以将其作为目标。特别是，`3d_rasterizer` 类处理绘图（栅格化）任务，操作屏幕内部的数据。

我们首先在 `hello_image` 中看到了这个概念，它直接使用 `XImage` 作为屏幕来显示点图案。`3d_screen` 类是对是对“屏幕作为输出设备”这一更通用概念的识别——它不只是一个 X 窗口。应用程序通过抽象的 `3d_screen` 接口使用屏幕，并且不受限于任何特定的显示器。

### 列表 2-29: screen.h

```cpp
#ifndef _SCREEN_H

#define _SCREEN_H

#include "../tool_os/memman.h"

#include "../geom/polygon.h"

#include "screen.h"

#include "idx.h"

#include "../tool_os/event_source.h"

class 3d_screen : public 3d_event_source {

protected:

    virtual void wait_trace(void);

    virtual void close_screen(void);

    3d_list<3d_coordinate> *vwin_list;

    int bufsize;

public:

    3d_screen(int xsize, int ysize);

    virtual ~3d_screen(void);
```
