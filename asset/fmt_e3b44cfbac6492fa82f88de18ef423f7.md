
请注意，位置和方向是直接提取自 Vidoscope 文件的，因此它们是在 Blender 的右手坐标系中指定的，而不是 Id3d 的左手坐标系。`VidscParser.pm` 在将这些坐标写入世界文件之前，会将其转换为左手坐标系。

`VidscParser.pm` 使用 `vidinfo` 从文件中提取 ID。然后，它利用该 ID 尝试查找对应的 `attribXXX.dat` 文件，其中 `XXX` 是提取出的网格 ID。属性文件的内容被读取到内存中的一个数组里。

由于 `TYPE` 和 `NAME` 属性是通用的，因此首先提取它们。根据 `type` 属性，我们将网格作为演员（actor）或扇区（sector）进行处理。

如果 `TYPE` 是 `ACTOR`，则提取所有相关的演员属性，例如插件名称和纹理文件，以便我们在第 5 章规定的格式下创建有效的 `ACTOR` 行。我们将所有这些属性存储在内存中的 `Actor` 对象中。稍后，在生成阶段，`Actor` 的属性会被写入世界文件中的 `ACTOR` 行。

如果 `TYPE` 是其他任何值，我们假设该网格是一个扇区。（通常我们希望针对未知类型显示错误消息，但在这种情况下，该技术允许完全未标记的网格仍被处理为未命名的扇区。）我们之前已经看到了扇区的顶点和多边形是如何创建的。之前没有讨论的是，每个面都是从 Vidoscape 解析到 `World` 结构中的；我们在网格的属性列表中搜索任何 `FACE <X>` 属性。如果我们找到与当前正在处理的面相对应的任何 `FACE <X>` 属性，则使用这些属性来控制内存中 `Facet` 对象的精确属性，进而最终控制写入世界文件的内容。如果该面是一个可见的纹理定义三角形（`IS_TEX_SPACE`），则基于该三角形计算纹理空间，并按名称将纹理空间保存在哈希表中，以便其他多边形将来引用。如果该面是一个不可见的纹理三角形（`IS_TEX_SPACE` 和 `IS_INVISIBLE`），则此外还要将面的标志 `is_invisible` 设置为 `true`，这将在稍后抑制该三角形作为世界文件中的几何多边形的生成。如果该面使用纹理空间（`USES_TEX_SPACE`），则具名纹理直接分配给该 `facet`。如果该面不使用纹理空间（未找到特殊的面属性），则不显式地将纹理分配给该面。稍后，在生成阶段，具有已分配纹理的面将导致创建 `GEOMPLY_TEX` 行，其纹理空间方向和图像由已分配的纹理指定。没有分配纹理的面也会导致创建 `GEOMPLY_TEX` 行，其具有默认的纹理空间方向，并使用世界文件中可用的第一个纹理图像。

`VidscParser.pm` 还将任何演员对象分配给它们的父扇区，这是由演员网格的 `PARENT` 属性确定的。然后，在生成阶段，属于某个扇区的所有演员会立即在该扇区块之后打印出来，以便在加载世界文件时，演员被分配给该扇区。

### blend_at 的程序清单

既然我们已经了解了 `blend_at` 工作的所有细节，现在可以查看该工具的代码清单。

`blend_at` 是使用 Glade GUI 构建工具/环境编写的。“构建工具/环境”这一术语用于表明 Glade 不仅仅是一个单向的 GUI 构建工具，但也不像真正的快速应用程序开发环境那样完全集成。Glade 基于 `GTK` 用户界面小部件工具包，允许你图形化地在窗口内放置小部件，并为小部件上可能发生的各种事件附加代码。就像世界编辑系统让我们无需担心 3D 空间中对象的精确坐标一样，Glade 让我们无需担心窗口内小部件的精确坐标，并允许更快地可视化开发具有现代用户界面的应用程序。

Glade 自动生成代码来创建窗口并在窗口中放置小部件。然后，这些代码被手动扩展以在点击按钮或选择菜单项时执行必要的操作。与其将逻辑嵌入窗口类本身中（这是一个糟糕的主意），不如让代码遵循模型-视图-控制器（MVC）范式，其中数据的视图（窗口）与其上的操作（控制器）是分开的。这个概念在理论上听起来很简单，但就像所有优秀的软件设计原则一样，真正的问题在于你是否能够在代码中坚持这一概念。特别是，在使用 RAD 环境和 GUI 构建工具时，人们很容易受诱惑将应用程序代码直接插入 GUI 构建工具方便提供的空函数体中，但这种方法会毫无选择地将应用程序逻辑分散在代码各处，正如糟糕的 BSP 树毫无选择地将连贯的几何细节分散到树的各个部分一样。复杂应用程序软件的结构应由有能力的决定者确定；没有 GUI 构建工具能为你的应用域提供合适的软件架构建议。

这意味着 `blend_at` 的 GUI 代码大部分是自动生成的，而那些被扩展的部分（例如点击按钮时实际执行的代码）本身并不执行任何逻辑，而是简单地调用控制器对象上的方法，由控制器对象执行实际任务。因此，控制器对象封装了逻辑。所以，我们不会在这里详细讨论 `blend_at` 的 GUI 代码，而是专注于 `blend_at` 中特定领域的类。

为了区分特定领域的文件和 Glade 生成的文件，所有特定领域的文件都以前缀 `n1_` 开头，这个前缀的选择原因印在书的封面上。接下来的章节将介绍 `blend_at` 中使用的每个特定领域的类。

#### 类 `vertex`

类 `vertex` 是三维空间中的一个 `vertex`。成员变量 `x`、`y` 和 `z` 是空间坐标。运算符 `==` 通过比较两个 `vertex` 对象的坐标来测试它们是否相等，并使用一个较小的 `epsilon` 参数，以便将附近的点视为相等。

列表 6-13：`nl_vertex.h`

```cpp
#ifndef __NL_VERTEX_H
#define __NL_VERTEX_H

struct vertex {
    float x, y, z;

    int operator==(const vertex &r) {
        return(
            -0.001 < x-r.x && x-r.x < 0.001 &&
            -0.001 < y-r.y && y-r.y < 0.001 &&
            -0.001 < z-r.z && z-r.z < 0.001
        );
    }
};

#endif
```

#### 类 `blender_config`

类 `blender_config` 存储 Blender 配置数据，`blend_at` 在运行时必须知道这些数据。

- 成员 `blender_path` 是一个字符串，存储 Blender 工作文件所在的目录名称。
- 成员 `blender_work_filename` 是一个字符串，存储 Blender 工作文件的文件名。
- 成员 `db_path` 是一个字符串，存储属性文件将保存所在的目录。
- 成员 `oid_filename` 是一个字符串，存储 `blend_at` 用于记录分配给网格的最后一个 ID 编号的计数器的文件名。每当网格被分配新的 ID 时，该计数器会增加 1，从而确保网格始终拥有唯一的 ID 编号。
- 常量 `BLENDER_MAGIC_X_SIZE` 是一个浮点值，决定插入几何体以编码 ID 的魔法边的空间大小。默认情况下，大小为 `1.0`。
- 常量 `ATTRIB_FNAME` 是一个包含所有属性文件名前缀的字符串。默认情况下，前缀是字符串 `attrib`，因此属性文件名的形式为 `attribXXX.dat`。

列表 6-14：`nl_blender_config.h`

```cpp
#ifndef __BLENDER_CONFIG_H
#define __BLENDER_CONFIG_H

#include <string>

class blender_config {
public:
    string blender_path;
    string blender_work_filename;
    string db_path;
    string oid_filename;

    static float BLENDER_MAGIC_X_SIZE;
    static char ATTRIB_FNAME[];
};

#endif
```

列表 6-15：`nl_blender_config.cc`

```cpp
#include "nl_blender_config.h"

float blender_config::BLENDER_MAGIC_X_SIZE = 1.0;
char blender_config::ATTRIB_FNAME[] = "attrib";
```

#### 类 `blender_controller`

类 `blender_controller` 是用于远程控制 Blender 的抽象接口。

- 成员变量 `blender_config` 指向一个 Blender 配置对象，该对象存储重要的目录名和文件名。
- 成员变量 `current_id` 是一个整数，表示当前在 Blender 中选中网格的 ID。
- 成员变量 `current_prop_filename` 是对应于存储在 `current_id` 中的 ID 的当前属性文件的完整路径。
- 成员变量 `property_lines` 是一个字符串列表，包含当前属性文件的内容。
- 成员变量 `selected_faces` 是一个整数列表，指示当前在 Blender 中选中的面的索引。

纯虚方法 `find_blender_window` 要求控制器查找当前的 Blender 窗口，并以某种方式在内部存储对该窗口的引用，以便后续命令可以引用该 Blender 窗口。控制器具体如何查找和存储窗口引用取决于窗口系统，并在子类中实现。

纯虚方法 `press_key` 要求控制器模拟按键事件并将其发送到 Blender 窗口。

纯虚方法 `release_key` 要求控制器模拟按键释放事件并将其发送到 Blender 窗口。

纯虚方法 `read_properties` 要求控制器提取当前在 Blender 中选中的网格的 ID，然后将该网格的属性（其属性文件的内容）读取到内存中。如果当前选中的网格还没有 ID，则 `read_properties` 应创建新 ID，将该新 ID 嵌入网格中，重新加载网格，创建一个新的属性文件，并将此新的属性文件读取到内存中。

纯虚方法 `determine_selected_face_nums` 要求控制器确定当前在 Blender 中选中的面的索引，并将此列表存储在 `selected_faces` 中。正如我们之前所见，该列表用于“新面属性”按钮，基于当前选中的面创建新的 `<X>` 属性。

列表 6-16：`nl_blender_controller.h`

```cpp
#ifndef _NL_BLENDER_CONTROLLER_H
#define _NL_BLENDER_CONTROLLER_H

#include <vector>

class blender_config;

class blender_controller {
public:
    blender_config *config;

    virtual void find_blender_window(void) = 0;
    virtual void press_key(int code) = 0;
    virtual void release_key(int code) = 0;
    virtual void read_properties(void) = 0;
    virtual void determine_selected_face_nums(void) = 0;

    int current_id;
    char current_prop_filename[4096];
    vector<int> selected_faces;
    vector<string> property_lines;
};

#endif
```

#### 类 `blender_xcontroller`

类 `blender_xcontroller` 是用于 X 窗口系统的 Blender 控制器。

- 成员变量 `dpy` 存储指向 X Display 的指针。
- 成员变量 `blender_w` 以 `Window` 对象的形式存储对 Blender 窗口的引用。

方法 `recursive_find_blender_window` 递归遍历显示中的所有窗口，直到找到一个标题为 Blender 的窗口。然后，它将该窗口存储在变量 `blender_w` 中。

重写的方法 `find_blender_window` 调用 `recursive_find_blender_window` 来执行 X 搜索，以查找 Blender 窗口。

重写的方法 `press_key` 创建一个类型为 `XEvent` 的事件，填充事件结构使其成为具有给定键代码的按键事件，使用 `XSendEvent` 将该事件发送到 Blender 窗口，然后使用 `XFlush` 刷新事件队列以确保事件被发送。

重写的方法 `release_key` 创建一个类型为 `XEvent` 的事件，填充事件结构使其成为具有给定键代码的按键释放事件，使用 `XSendEvent` 将该事件发送到 Blender 窗口，然后使用 `XFlush` 刷新事件队列以确保事件被发送。

重写的方法 `read_properties` 可能是整个 `blend_at` 程序中最显著的方法。该方法向 Blender 发送按键以使其将当前选中的网格保存到工作文件中。然后，读取该文件并扫描以查找 ID，方法是如前所述查找重叠的边。如果未找到 ID，则创建新 ID 并将其编码在网格中；然后，向 Blender 发送相应的按键，使其删除旧网格并重新加载包含嵌入 ID 的新网格。在找到或新分配 ID 后，打开对应于该 ID 的属性文件，并将其内容读取到 `property_lines` 列表中。

重写的方法 `determine_selected_face_nums` 是 `blend_at` 中第二显著的方法。它通过向 Blender 发送按键来分离并保存选中和原始网格，从而确定哪些面被选中；然后，在原始网格中搜索选中的面，并将它们的索引号存储在 `selected_faces` 列表中。

列表 6-17：`nl_blender_xcontroller.h`

```cpp
#ifndef __NL_BLENDER_XCONTROLLER_H
#define __NL_BLENDER_XCONTROLLER_H

#include <X11/X.h>
#include <X11/Intrinsic.h>
#include <unistd.h>
#include <stdio.h>
#include <gtk/gtk.h>
#include <vector>
#include <string>

#include "nl_blender_controller.h"

class blender_config;

class blender_xcontroller : public blender_controller {
protected:
    Display *dpy;
    int recursive_find_blender_window(Window w);

public:
    Window blender_w;

    blender_xcontroller(Display *dpy, blender_config *c);
    virtual ~blender_xcontroller(void);
    void find_blender_window(void);
    void press_key(int code);
    void release_key(int code);
    void read_properties(void);
    void determine_selected_face_nums(void);
};

#endif
```

列表 6-18：`nl_blender_xcontroller.cc`

```cpp
#include "nl_blender_xcontroller.h"
#include "nl_vertex.h"
#include "nl_blender_config.h"

blender_xcontroller::blender_xcontroller(Display *dpy, blender_config *c) {
    this->dpy = dpy;
    config = c;
    find_blender_window();
}

blender_xcontroller::~blender_xcontroller(void) {
    delete config;
}

int blender_xcontroller::recursive_find_blender_window(Window w) {
    Window root_return, parent_return, *children;
    unsigned int nchildren;
```
