
## 类 `vertex`

类 `vertex` 是三维空间中的一个 `vertex`。成员变量 `x`、`y` 和 `z` 是空间坐标。运算符 `==` 通过比较两个 `vertex` 对象的坐标来测试它们是否相等，并使用一个较小的 epsilon 参数，以便将附近的点视为相等。

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

## 类 `blender_config`

类 `blender_config` 存储 Blender 配置数据，`blend_at` 在运行时必须知道这些数据。

- 成员 `blender_path` 是一个字符串，存储 Blender 工作文件所在的目录名称。
- 成员 `blender_work_filename` 是一个字符串，存储 Blender 工作文件的文件名。
- 成员 `db_path` 是一个字符串，存储属性文件将保存所在的目录。
- 成员 `oid_filename` 是一个字符串，存储 `blend_at` 用于记录分配给网格的最后一个 ID 编号的计数器的文件名。每当网格被分配新的 ID 时，该计数器会增加 1，从而确保网格始终拥有唯一的 ID 编号。
- 常量 `BLENDER_MAGIC_X_SIZE` 是一个浮点值，决定插入几何体以编码 ID 的魔法边的空间大小。默认情况下，大小为 1.0。
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

## 类 `blender_controller`

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

## 类 `blender_xcontroller`

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

