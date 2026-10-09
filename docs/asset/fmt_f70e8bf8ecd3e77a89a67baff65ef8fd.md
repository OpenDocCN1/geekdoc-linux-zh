
## 第 2 章：访问屏幕

让我们看看这些数字在二进制中是什么。为了做到这一点，我们可以使用命令行计算器 `bc`，操作如下：

1. 输入 `bc` 并按回车。
2. 注意欢迎信息。输入 `obase=2` 并按回车，设置输出基数为 2（二进制）。
3. 输入 `63488`（红掩码的十进制值），并按回车。
4. 注意输出 `11111100000000000`。
5. 输入 `2016`（绿掩码的十进制值），并按回车。
6. 注意输出 `111111100000`。
7. 输入 `31`（蓝掩码的十进制值），并按回车。
8. 注意输出 `111111`。
9. 按 `Ctrl+D` 退出。

注意，这些掩码假设的是高位字节优先（MSFirst），而 `X`（在 Linux x86 系统上）以低位字节优先（LSBFirst）顺序存储字节。为了正确解释位掩码，我们必须交换字节序。

### 颜色表与像素映射

然而，在运行 `XFree86` 的基于 x86 的 Linux 机器上，可以确定字节序是小端序（little endian）。

每个像素的最终值随后被用颜色表（`colormap`）的索引。颜色表本质上是一个包含每个索引对应特定颜色的表格。在使用它之前，我们需要创建一个颜色表并用颜色填充。在 `X` 系统中，创建颜色表的一般过程如下：

1. 使用 `XCreateColormap` 函数创建一个颜色表。
2. 使用 `XAllColorCells` 函数为颜色表分配空的颜色单元格。
3. 对于颜色表中的每个空条目，声明一个类型为 `XColor` 的临时变量，赋予该 `XColor` 变量合适的 RGB 值，并使用 `XStoreColor` 将此颜色存入颜色表。
4. 在初始化颜色表中的所有条目后，使用 `XSetWindowColormap` 将其分配给你的窗口。

![](img/49715b3934121066e59e93823d33ee3a_113_0.png)

图 2-18：索引颜色表的位解释。图像中的这些颜色表是通过取对应一个像素的所有字节并使用低位优先（LSBFirst）规则计算的。在颜色表中查找这些颜色表索引以确定最终的红色、绿色和蓝色颜色值。

> 注意：`XColor` 结构中的红、绿、蓝值始终指定在 0（最低强度）到 65535（最高强度）的范围内；`X` 服务器会将这些 RGB 值转换为视频硬件所需的实际红、绿、蓝值。

在“开发可重用图形类”节中介绍的 `l13d_screen_x11` 类源码说明了这一过程。

### 真色彩（TrueColor）与直接色彩（DirectColor）

对于 `TrueColor` 和 `DirectColor` 视觉，每个像素的位被分为红、绿、蓝组件。我们确定哪些位负责红、绿、蓝。不幸的是，由于逻辑和物理位顺序，这是一个相当混乱的问题。让我们来看看它是如何工作的。

`X` 提供 `XMatchVisualInfo` 函数来查找并返回关于特定视觉（visual）的额外信息。这些信息在 `XVisualInfo` 结构中返回。对于 `TrueColor` 和 `DirectColor` 视觉，`XVisualInfo` 结构包含三个成员：`red_mask`、`green_mask` 和 `blue_mask`，每个类型均为 `unsigned long`。对于匹配的视觉结构，这些字段包含了访问像素红色部分、像素绿色部分和蓝色部分所需的位掩码。

令人混乱的地方在于，这些掩码假设的是高位字节优先（MSFirst）顺序，而 `X`（在 Linux x86 系统上）以低位字节优先（LSBFirst）顺序存储字节。为了正确解释位掩码，我们必须交换字节序。

一个例子将使这一点变得清晰。假设你的 `X` 服务器以每像素 16 位的速度运行。在用 `XMatchVisualInfo` 查询视觉后，我们将获得如下所示的值：

```
red_mask = 63488
green_mask = 2016
blue_mask = 31
```

让我们看看这些数字在二进制中是什么。为了做到这一点，我们可以使用命令行计算器 `bc`，操作如下：

1. 输入 `bc` 并按回车。
2. 注意欢迎信息。输入 `obase=2` 并按回车，设置输出基数为 2（二进制）。
3. 输入 `63488`（红掩码的十进制值），并按回车。
4. 注意输出 `11111100000000000`。
5. 输入 `2016`（绿掩码的十进制值），并按回车。
6. 注意输出 `111111100000`。
7. 输入 `31`（蓝掩码的十进制值），并按回车。
8. 注意输出 `111111`。
9. 按 `Ctrl+D` 退出。

### 架构概述

派生类、具体类以及 `X` 实现的具体类。不同的派生具体类可以使用硬件加速（在第 3 章中说明）或不同的操作系统（见附录）来实现相同的抽象。

### 使用 I3d 的示例程序

在查看 `I3d` 代码本身之前，让我们先看一个使用 `I3d` 的示例程序。这将让你在查看随后详细介绍类内部工作机制的章节之前，对代码有一个实践性的直观认识。在大多数情况下，该库类并没有引入许多新概念；我们已经涵盖了大多数与 `X` 和 Linux 之上的 2D 编程相关的重要技术问题。

下一个示例程序称为 `drawdot`，它演示了如何使用 `I3d` 库类在屏幕上移动点，形成一个简单的图形程序。意义在于，这是我们第一次在特定位置以特定颜色绘制像素点。该程序适用于任何色深以及真色彩（`TrueColor`）或索引颜色模式。这并非易事——正如我们之前说的，由于可能的颜色深度和颜色模型非常多，像素位置和内容的计算都非常复杂。复杂的计算已全部封装在易于使用的类中。顺便提一下，正如我们稍后看到的，该程序不仅适用于“普通”窗口，还可以使用共享内存或硬件加速的输出设备。

图 2-20：示例程序 `drawdot` 的输出。

列表 2-23：`drawdot.cc`

```cpp
#include <stdlib.h>
#include <stdio.h>
#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/dispatch.h"
#include "../lib/raster/rasterizer.h"
#include "../lib/tool_2d/scrinfo.h"
#include "../lib/system/factorys.h"

// 步骤 1: 选择工厂
void choose_factories(void) {
    factory_manager_v_0_1.choose_factories();
}

// 步骤 2: 声明流水线子类
class my_pipeline : public i3d_pipeline {
protected:
    i3d_rasterizer_2d_imp *ri;
    i3d_rasterizer_2d *r;
    int x, y, dx, dy;
    unsigned long color;
public:
    i3d_pipeline *s;
    my_pipeline(void);
    virtual ~my_pipeline(void);
    void key_event(int ch); // 来自调度器
    void update_event(void); // 来自调度器
    void draw_event(void); // 来自调度器
};

my_pipeline::my_pipeline(void) {
    s = factory_manager_v_0_1.screen_factory->create(320, 200);
    ri = factory_manager_v_0_1.ras_2d_imp_factory->create(320, 200, s->infoinfo);
    r = new i3d_rasterizer_2d(ri);
    
    s->infoinfo->ext_max_red = 255;
    s->infoinfo->ext_max_blue = 255;
    s->infoinfo->to_native(0, 0, 0); // 分配背景颜色
    color = s->infoinfo->to_native(0, 255, 128);
    s->refresh_palette();
    
    x = y = dx = dy = 0;
}

my_pipeline::~my_pipeline(void) {
    delete s;
    delete ri;
    delete r;
}

my_pipeline::key_event(int ch) {
    switch(ch) {
        case 'h': dx-=1; dy=0; break;
        case 'l': dx+=1; dy=0; break;
        case 'j': dx+=0; dy=1; break;
        case 'k': dx+=0; dy-=1; break;
        case ' ': dx=0; dy=0; break;
        case 'q': exit(0);
    }
}

void my_pipeline::update_event() {
    x += dx;
    y += dy;
    if(x < 0) x = 0;
    if(x > s->xsize-1) x = s->xsize-1;
    if(y < 0) y = 0;
    if(y > s->ysize-1) y = s->ysize-1;
}

void my_pipeline::draw_event(void) {
    r->draw_point(x, y, color);
    s->blit_screen();
}

int main() {
    choose_factories();
    i3d_dispatcher *d;
    
    // 步骤 3: 创建调度器
    d = factory_manager_v_0_1.dispatcher_factory->create();
    
    // 步骤 4: 创建流水线
    // 将我们的自定义行为插入调度器
    my_pipeline *p = new my_pipeline();
    
    // 步骤 5: 启动调度器
    d->pipeline = p; // 多态赋值
    d->start();
    
    delete d;
    delete p;
    return 0;
}
```
