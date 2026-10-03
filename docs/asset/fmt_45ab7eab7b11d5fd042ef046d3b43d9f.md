
在上一节中，你学习了 D-Bus 有多强大以及如何使用它。但很自然，应用程序需要对发送的信号和消息进行标准化。本节将介绍什么是硬件抽象层（HAL），它如何与 D-Bus 关联，以及如何在你的应用程序中使用 HAL。

## 让硬件即插即用

Linux 的长期用户还记得，过去获取新硬件时曾是相当麻烦的。人们必须花时间尝试弄清楚设备工作需要存在哪些内核模块。如果设备是可热插拔的（例如 USB 设备），当设备空闲时可能不需要加载模块。在许多设备之间切换时，很容易对应该加载哪个模块而感到困惑。

当然，即使过程进行得很顺利，这个操作也是枯燥的。当普通电脑用户发现相机插入电脑后没有按预期工作，或者他们无法立即访问 USB 硬盘，又可能是打印机时，他们可能会感到沮丧。应用程序无法关心硬件的具体细节，否则作者将不得不为每个想要支持的新硬件都更新他们的软件。

最终，红帽公司的 Havoc Pennington 编写了一篇名为《让硬件即插即用》（http://ometer.com/hardware.html）的论文，文中概述了他认为的一系列问题，并提出了使用硬件抽象层（HAL）来解决这些问题的想法。几个月后，第一批代码被提交到了 CVS 仓库中。今天，HAL 能够发现存储设备、网络设备、打印机、像 iPod 这样的媒体播放器、数字相机等。

HAL 是一个监控系统当前硬件的系统守护进程。它通过在 `/etc/dev.d` 中安装脚本来监听硬件设备从系统添加或移除时触发的热插拔事件，每当 `dev` 在启动时请求系统上所有设备列表时，该脚本就会运行。除了设备信息外，HAL 还可以执行某些任务，例如锁定硬件设备以进行独占访问。

HAL API 完全基于 D-Bus，但它是一个相当大的 API，而许多程序是用 C 语言编写的；存在一个名为 `libhal` 的 C 辅助库。使用 HAL 非常简单。让我们先创建一个应用程序，它只需监听系统中下一个被添加或移除的设备，打印一条短消息，然后退出。

```c
#include <libhal.h>
#include <dbus/dbus.h>
#include <dbus/dbus-glib.h>
#include <glib.h>
#include <stdlib.h>
#include <stdio.h>
```

我们先完成应用的核心部分，稍后再考虑回调函数。为了等待事件，让我们使用 Glib 提供的 `GMainLoop`。我们必须打开一个到系统总线的 D-Bus 连接。

```c
int main (int argc, char *argv[])
{
    GMainLoop *mainloop;

    DBusConnection *dbconn;
    DBError dberr;

    LibHalContext *hal_ctx;

    mainloop = g_main_loop_new(NULL, FALSE);
    if (mainloop == NULL) {
        fprintf(stderr, "Can't get a mainloop");
        return EXIT_FAILURE;
    }

    dbus_error_init(&dberr);
    dbconn = dbus_bus_get(DBUS_BUS_SYSTEM, &dberr);
    if (dbus_error_is_set(&dberr)) {
        fprintf(stderr, "Can't get D-Bus system bus!");
        return EXIT_FAILURE;
    }

    dbus_connection_setup_with_g_main (dbconn, NULL);
```

处理好这些事务后，现在可以创建一个 `LibHalContext` 并告诉它回调应该处理哪些事件。注意，执行顺序很重要。首先，必须使用 `libhal_ctx_new()` 创建一个 `LibHalContext`，然后在调用 `libhal_ctx_init()` 之前，必须注册所有的回调、D-Bus 连接等。

```c
hal_ctx = libhal_ctx_new();
if (hal_ctx == NULL) {
    printf(stderr, "Can't create a LibHalContext!");
    return EXIT_FAILURE;
}
```

```c
/* 将 HAL 与我们建立的 D-Bus 连接关联 */
libhal_ctx_set_connection(hal_ctx, dbconn);
/* 注册回调 */
libhal_ctx_register_added(hal_ctx, my_device_added);
libhal_ctx_register_removed(hal_ctx, my_device_removed);
/* 我们将在主循环上阻塞 */
libhal_ctx_set_main_loop(hal_ctx, mainloop);
libhal_ctx_init(hal_ctx);

g_main_loop_run(mainloop);

libhal_ctx_unref(hal_ctx);
g_main_loop_unref(mainloop);
dbus_connection_unref(dbconn);
dbus_error_clear(&dberr);

return 0;
}
```

*(注：原文中的代码块存在严重碎片/损坏。我根据标准的 D-Bus/libhal 模式和提供的片段重建了逻辑流，因为原始文本代码中包含了错误的字符串和页码。)*

等等，上一节向你展示了连接 HAL 以及让它在设备添加和移除时通知你的基础。现在，是探索 HAL 设备对象的细节了。

HAL 设备对象由部分内容组成。每个 HAL 设备都有一个唯一设备标识符（UDI），两个设备在同一时间共享它。UDI 是通过总线信息计算的，并且在设备插入期间保持静态。对于不提供序列号的设备，HAL 将无法完全实现。在这种情况下，HAL 将提供设备的物理位置信息（例如总线 42 上的 PCI 插槽 0）来生成 UDI。

HAL 设备对象还带有关联的键值属性。键是 ASCII 字符串。值可以是以下类型之一：

- `int`（32 位有符号整数）
- `uint64`
- `string`（UTF-8 字符串）
- `strlist`（排序的 UTF-8 字符串列表）
- `double`

属性键使用点（.）字符分隔的命名空间，例如 `info.linux.driver` 和 `net.80211.mac_address`。

# 第 12 章：FreeDesktop 项目

HAL 属性键可以分为四类：

- **元数据属性**（Metadata properties）由 HAL 设置，用于描述设备之间互连连接的关系以及设备的类型。
- **物理属性**（Physical properties）由 HAL 从设备本身或包含产品 ID 和供应商 ID 等信息的设备信息文件中定义。
- **功能属性**（Functional properties）提供有关设备当前状态信息的属性。例如：链接状态、文件系统挂载、笔记本电脑电池电量等。
- **策略属性**（Policy properties）定义了用户如何使用设备，通常由系统管理员在设备信息文件中设置。

HAL 还提供了关于设备能力的信息。这些信息包含在 `info.capabilities` 属性中，该属性提供了关于设备可以做什么的信息。例如，一个便携音乐播放器（如 iPod）也可以作为存储设备使用。在这种情况下，`info.capabilities` 将是一个包含 `portable_music_player` 和 `storage.disk` 的字符串列表。`info.capabilities` 键表示主类型，并将被设置为 `portable_music_player`。

最后，需要注意的是，HAL 设备对象并不一定映射到一个物理设备。例如，一个打印机可能有三个 HAL 设备对象，分别用于打印、扫描和存储。其他具有多用途的设备可能仅有一个 HAL 设备接口。主设备将有一个列出所有能力的单一列表，并且在其树下会有三个设备，每个设备对应一种能力。

现在你已经基本了解了 HAL 设备对象的工作原理，让我们写一个程序来查找系统上的光驱驱动器并打印关于它们的一些细节。我们需要向 HAL 请求 `storage.cdrom` 能力，这就是应该请求的内容。要确定驱动器是否也支持读取 DVD，请向 HAL 查询 `storage.cdrom.dvd` 属性的值。查找驱动器的最大读取速度也是很有用的，而且这由 `storage.cdrom.read_speed` 属性决定。

HAL 的初始化方式与之前的程序类似。注意，由于我们只需要获取已连接设备的列表，因此不需要进行事件监听或主循环（`mainloop`），不再需要 Glib 库。

```c
#include <libhal.h>
#include <stdlib.h>
#include <stdio.h>

int main (int argc, char *argv[])
{
    DBusConnection *dbconn;
    DBusError derr;

    LibHALContext *hal_ctx;
    LibHALPropertyType property_type;
    char *property_key;
    dbus_bool_t bool_value;
    int int_value;
    char **udis;
    int num_udis;
    int i;
```

```c
dbus_error_init(&dberr);
dbconn = dbus_bus_get(DBUS_BUS_SYSTEM, &dberr);
if (dbus_error_is_set(&dberr)) {
    fprintf(stderr, "Can't create D-Bus system bus!\n");
    return EXIT_FAILURE;
}
```

```c
hal_ctx = libhal_ctx_new();
if (hal_ctx == NULL) {
    fprintf(stderr, "Can't create a LibHalContext!\n");
    return EXIT_FAILURE;
}
```

```c
/* 将 HAL 与我们建立的 D-Bus 连接关联 */
libhal_ctx_set_dbus_connection(hal_ctx, dbconn);
```

```c
dbus_error_init(&dberr);
libhal_ctx_init(hal_ctx, &dberr);
if (dbus_error_is_set(&dberr)) {
    fprintf(stderr, "libhal_ctx_init() failed: %s. Is hal running?\n", dberr.message);
    dbus_error_free(&dberr);
    libhal_ctx_free(hal_ctx);
    return EXIT_FAILURE;
}
```

HAL 初始化完成后，现在是时候寻找具有 `storage.cdrom` 能力设备设备。

```c
/* 查找光驱设备：storage.cdrom */
udis = libhal_find_device_by_capability(hal_ctx, "storage.cdrom", &num_udis);
if (dbus_error_is_set(&dberr)) {
    fprintf(stderr, "libhal_find_device_by_capability error: %s\n", dberr.message);
    dbus_error_free(&dberr);
    libhal_ctx_free(hal_ctx);
    return EXIT_FAILURE;
}
```

`udis` 变量现在包含一个匹配 `storage.cdrom` 能力的 `udis` 数组。下一步是过滤这些设备，以便可以获取每个独立设备的属性。我们首先使用 `libhal_device_get_property_type` 来确保每个属性的类型都是我们预期的类型。

```c
printf("%d Optical Device(s)\n", num_udis);
for (int i = 0; i < num_udis; i++) {
    /* 确保我们的属性是预期的类型 */
    property_type = libhal_device_get_property_type(hal_ctx,
        udis[i],
        "storage.cdrom.dvd",
        &dberr);

    if (dbus_error_is_set(&dberr) ||
        property_type != LIBHAL_PROPERTY_TYPE_BOOLEAN) {
        fprintf(stderr, "error checking storage.cdrom.dvd");
        dbus_error_free(&dberr);
        libhal_ctx_free(hal_ctx);
        return EXIT_FAILURE;
    }

    property_type = libhal_device_get_property_type(hal_ctx,
        udis[i],
        "storage.cdrom.read_speed",
        &dberr);

    if (dbus_error_is_set(&dberr) ||
        property_type != LIBHAL_PROPERTY_TYPE_INTEGER) {
        fprintf(stderr, "error checking storage.cdrom.read_speed");
        dbus_error_free(&dberr);
        libhal_ctx_free(hal_ctx);
        return EXIT_FAILURE;
    }

    bool_value = libhal_device_get_bool(hal_ctx,
        udis[i],
        "storage.cdrom.dvd",
        &dberr);
    if (dbus_error_is_set(&dberr)) {
        fprintf(stderr, "error getting storage.cdrom.dvd");
        dbus_error_free(&dberr);
        libhal_ctx_free(hal_ctx);
        return EXIT_FAILURE;
    }

    int_value = libhal_device_get_int(hal_ctx,
        udis[i],
        "storage.cdrom.read_speed",
        &dberr);
    if (dbus_error_is_set(&dberr)) {
        fprintf(stderr, "error getting storage.cdrom.read_speed");
        dbus_error_free(&dberr);
        libhal_ctx_free(hal_ctx);
        return EXIT_FAILURE;
    }
}
return EXIT_SUCCESS;
```

编译程序并运行。输出应该类似于：

```text
$ ./optical-test
Found 2 Optical Device(s)
Device /org/freedesktop/hal/devices/model_HL_STVD_ROM has a maximum read speed of 8467 kb/s and can read DVDs
Device /org/freedesktop/hal/devices/model_HL_STVD_ROM has a maximum read speed of 8467 kb/s and cannot read DVDs.
```

为了更好地列出 HAL 感知的属性，查看 `listhal` 程序。它列出了 HAL 知道的所有设备及其属性。输出将类似于：
