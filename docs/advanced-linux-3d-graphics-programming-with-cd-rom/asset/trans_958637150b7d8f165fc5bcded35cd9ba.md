
在世界坐标系中。通过反转表示坐标系的矩阵，我们可获得逆向变换。因此，矩阵乘积 $M^{-1}P$ 给出的就是该点（在世界坐标系中定义）相对于 $M$ 的坐标。

当你看到矩阵乘积 $MP$ 时，请将其理解为回答这样一个问题：“$P$ 是相对于 $M$ 定义的，它在世界坐标系中的位置在哪里？” 当你看到 $M^{-1}P$ 时，请将其理解为回答这样一个问题：“$P$ 是在世界坐标系中定义的，它相对于 $M$ 的位置在哪里？”

## I3d 库类

本书依赖于一系列 C++ 库类的使用，这些类实现了前述章节中描述的所有二维和三维图形概念。该库被称为 I3d 库。它在配套的介绍性书籍 *Linux 3D Graphics Programming*（Linux 三维图形编程）中逐步开发而来。在本书中，我们使用第一本书中介绍的类，并在此基础上继续构建，以阐述更新、更高级的概念。I3d 类位于 CD-ROM 中，也可在互联网上的 `http://www.linux3dgraphicsprogramming.org` 处下载。

### I3d 示例程序

在查看 I3d 类本身之前，让我们先看一下一个使用 I3d 的示例程序。这将让你在深入了解后续章节中关于特定 I3d 类的详细内容之前，先从实际角度了解 I3d。

下面的示例程序名为 `drawdot`，它演示了如何使用 I3d 库类在屏幕上移动一个绿点，从而形成一个简单的绘图程序。该程序适用于任意色深的显示窗口，既支持 TrueColor（真彩色）模式，也支持索引颜色（indexed color）模式。请注意，该程序相当简短，且只声明了一个类。这是因为 I3d 库已经声明了几个有用的类来简化应用程序。

![](img/a19d4e8b1d7eb6387691dc6c865430e6_24_0.png)

**列表 1-1: drawdot.cc**

```cpp
#include <stdlib.h>
#include <stdio.h>

#include "../lib/tool_2d/screen.h"
#include "../lib/tool_os/dispatch.h"
#include "../lib/raster/rasteriz.h"
#include "../lib/tool_2d/scriinfo.h"
#include "../lib/system/factorys.h"

// ------------------------------------------------
//
//  STEP 1: CHOOSE THE FACTORIES
// ------------------------------------------------
void choose_factories(void) {
  factory_manager_v_0_1.choose_factories();
}

// ------------------------------------------------
//
//  STEP 2: DECLARE A PIPELINE SUBCLASS
// ------------------------------------------------
class my_pipeline : public l3d_pipeline {
protected:
  l3d_rasterizer_2d *ri;
  l3d_rasterizer_2d *rr;

  int x, y, dx, dy;
  unsigned long color;

public:
  l3d_screen *s;
  my_pipeline(void);
  virtual ~my_pipeline(void);

  void key_event(int ch);  // from dispatcher
  void update_event(void); // from dispatcher
  void draw_event(void);   // from dispatcher
};

my_pipeline::my_pipeline(void) {
  s = factory_manager_v_0_1.screen_factory->create(320, 200);
  ri = factory_manager_v_0_1.ras_2d_imp_factory->create(320, 200, &sinfo);
  r = new l3d_rasterizer_2d(ri);

  s->sinfo->next_max_red =
    s->sinfo->next_max_green =
    s->sinfo->next_max_blue = 255;

  s->sinfo->next_to_native(0, 0, 0); // allocate background color
  color = s->sinfo->next_to_native(0, 255, 128);
  s->refresh_palette();

  x = y = dx = dy = 0;
}

my_pipeline::~my_pipeline(void) {
  delete s;
  delete ri;
  delete rr;
}

void my_pipeline::key_event(int ch) {
  switch(ch) {
  case 'h': dx = -1; dy = 0; break;
  case 'l': dx = 1; dy = 0; break;
  case 'j': dx = 0; dy = 1; break;
  case 'k': dx = 0; dy = -1; break;
  case ' ': dx = 0; dy = 0; break;
  case 'q': {
    exit(0);
  }
  }
}

void my_pipeline::update_event() {
  x += dx;
  y += dy;

  if(x < 0) x = 0;
  if(x > s->xsize - 1) x = s->xsize - 1;
  if(y < 0) y = 0;
  if(y > s->ysize - 1) y = s->ysize - 1;
}

void my_pipeline::draw_event(void) {
  rr->draw_point(x, y, color);
  s->blit_screen();
}

int main() {
  choose_factories();

  l3d_dispatcher *d;
  my_pipeline *p;

  //----------------------------------------------------
  //
  // STEP 3: CREATE A DISPATCHER
  //
  //----------------------------------------------------

  d = factory_manager_v_0_1.dispatcher_factory->create();

  //----------------------------------------------------
  //
  // STEP 4: CREATE A PIPELINE
  //
  //----------------------------------------------------

  // plug our custom behavior pipeline into the dispatcher
  p = new my_pipeline();

  //----------------------------------------------------
  //
  // STEP 5: START DISPATCHER
  //
  //----------------------------------------------------

  d->pipeline = p; // polymorphic assignment
  d->event_source = p->s;
  d->start();

  delete d;
  delete p;
  return 0;
}
```

> **注意** 以下操作假设你已经按照附录中的说明安装了源代码。特别是，安装说明要求你设置 `$L3D` 环境变量指向安装目录。此外，你应该在 X 窗口系统的 shell 窗口中执行这些命令。有关源代码初始安装和配置的具体细节，请参阅附录。

首先，让我们看看如何编译该程序。然后，我们查看程序本身的结构。最后，我们讨论 l3d 类。

示例程序的源代码位于目录 `$L3D/source/app/drawdot` 中。源文件和二进制文件位于不同的目录树中；下一节将详细讨论此问题。目前，请按照以下步骤编译和运行程序：

- 1. 要编译 l3d 库，请输入 `cd $L3D/source/app/lib`，按 Enter 键，输入 `make -f makeall.lnx`，然后按 Enter 键。请注意，此 makefile 的文件名不同于标准的 `Makefile`；因此，我们指定 `-f` 标志以告知 `make` 命令哪个文件是 makefile。
- 2. 通过在 shell 中输入 `cd $L3D/source/app/drawdot` 更改到 `drawdot` 的源目录，并按 Enter 键。编译 `drawdot`：输入 `make -f makeall.lnx` 并按 Enter 键。
- 3. 输入 `cd $L3D/binaries/linux_x/float/app/drawdot` 更改到二进制文件目录，并按 Enter 键。
- 4. 注意，编译过程产生的对象文件和可执行文件被放置在对应的二进制目录中。输入 `drawdot` 并按 Enter 键以运行程序。
- 5. 注意会询问“Which configuration?”（选择哪种配置？）。目前请选择 1 以选择普通的 X11 窗口，然后按 Enter 键。
- 6. 注意会出现一个空的黑色窗口。按 1 键。注意绿色线条在显示屏的最顶部从左向右移动，并且在你松开按键后线条继续移动。
- 7. 输入 `j`。注意绿色线条向下移动。
- 8. 使用以下按键控制线条的移动：`h` 向左移动，`l` 向右移动，`j` 向下移动，`k` 向上移动，空格键停止移动。
- 9. 输入 `q` 结束程序。

既然现在已经成功运行了程序，让我们接下来查看 l3d 目录结构的组织方式，然后检查 drawdot 程序本身。

## l3d 目录结构

库类和使用该库类的应用程序被拆分到单独的源目录树和二进制目录树中。我们将源文件和二进制文件拆分为两棵独立目录树的原因是，相同的源代码可以在多个不同的平台上编译。由于二进制文件因平台而异，而源文件保持一致，如果将二者放在同一目录中，会导致相当混乱的组织方式。虽然混沌论（chaos theory）是一个丰富且引人入胜的科学研究领域，但我们并不一定希望基于这种混乱来组织目录结构。拆分源目录和二进制目录可以形成更整洁的多平台目录结构。

具体而言，使用的目录结构如下：

- `$L3D/source/`：所有源文件。
- `$L3D/source/util/`：非 C++ 源文件（预处理脚本等）。
- `$L3D/source/app/`：与三维应用直接相关的 C++ 源文件。
- `$L3D/source/app/lib/`：l3d 库类的 C++ 源代码。
- `$L3D/source/app/[program_name]`：示例程序的 C++ 源代码。少数简单程序将二进制文件放在源目录中，但大多数程序将它们放在二进制目录中。
- `$L3D/binaries/linux_x/`：为 X 窗口系统编译的 Linux 二进制文件。
- `$L3D/binaries/linux_x/fixed/`：使用定点数数学编译的 Linux 二进制文件。定点数可执行文件目前支持并不完善，且并非总能正确工作。子目录结构与 float 子目录下的相同。
- `$L3D/binaries/linux_x/float/`：使用浮点数数学编译的 Linux 二进制文件。这是二进制文件的主要输出目录。
- `$L3D/binaries/linux_x/float/bin/`：l3d 库的 Linux 浮点数二进制文件。
- `$L3D/binaries/linux_x/float/app/[program_name]`：示例程序的 Linux 浮点数二进制文件。

makefiles 会自动将二进制文件放置在对应的二进制目录中。通常，你需要在应用程序的源目录中调用 **make -f makeall.lnx**，然后编译所有 Linux 二进制文件并将其放置在适当的二进制目录中。

> **注意** 请记住，附录提供了如何一次性编译所有示例程序的说明。前面的讨论主要是为了让你了解目录结构及其背后的逻辑。

综上所述，l3d 库的源文件位于 `$L3D/source/app/lib`，而示例程序的源文件都位于 `$L3D/source/app`。主要的二进制文件位于 `$L3D/binaries/linux_x/float/app`。

