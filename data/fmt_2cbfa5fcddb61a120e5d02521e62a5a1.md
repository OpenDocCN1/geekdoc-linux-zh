
# stat valimer-2.6-rc

```
File: valimer-2.6-rc
Size: 2489
Blocks: 5592
Device: 805h/2053d
Inode: 2209
Links: 1
Access: (0644)-rw-r--
Root: (root)
Modified: 2008-06-07 12:31:50.000
Change: 2008-06-07 12:31:50.000
```

![](img/4e539a55ab31f2c9df39e648783d8023_31_0.png) 显示磁盘上主设备号为 8 次设备号为 5 的文件 (`/dev/sda`)，它列在 `805h`（十六进制）或 `2053d`（十进制）。

- 在 2.4 内核中，只有主设备号可用，用于注册和注销的函数：

```
#include <linux/fs.h>
register_chdev(unsigned int major, const char *name);
unregister_chdev(unsigned int major, const char *name);
```

- 动态分配是通过...（此处原文逻辑不完整）

- 在 2.6 内核中，存在一个次设备号范围是可以全部可用的，且独立并发加载的驱动程序可以具有相同的主设备号，只要它们具有不同的次设备号范围。

## 4.4 分配主/次设备号

（注：原文此段存在较多断句和重复，翻译已根据语意尽量对齐）

42

# 第4章 字符设备

## 4.6 UDEV 与 HAL

```c
struct cdev_alloc(void)
struct cdev *cdev = udev_alloc(), struct file_operations *fops;
cdev_put(struct cdev *cdev);
struct kobject *kobj = (struct kobject *)cdev->kobj;
int cdev_add(struct cdev *cdev, dev_t dev, unsigned count)
cdev_del(struct cdev *cdev);
```

`udev` 负责设备节点的生成，但不处理设备的发现。这需要硬件抽象层（HAL），它由 freedktop (`https://www.freedesktop.org/wiki/Solutions/`) 提供。

HAL 使用 HAL 提供的 D-BUS（设备总线）接口。它维护一个所有连接硬件设备的动态数据库，并与宿主机设施耦合。主守护进程会将 HAL 当前拥有的信息输出到 `/usr/share/hal` 和 `/etc/hal`。

这些结构是动态分配的，然后使用如下代码进行初始化：

```c
struct cdev *mydev = cdev_alloc(0);
cdev_init(mydev, &fops);
```

此 `cdev` 为结构分配了内存，初始化了所有者和 dev 字段，并指向当前模式。

当执行以下操作时将调用驱动程序：

```c
cdev_add(mydev, dev, count);
```

使用 `udev` 的优雅方法是保持系统纯净；设备条目在内核启动之前是空的，并在需要时填充设备节点。当使用这种方法时，不会创建或删除设备节点，这可能会导致在 `udev` 程序运行时产生初步设备节点的痕迹。

在驱动程序准备好处理任何传发给它的请求之前，不应调用此函数。

其逆函数是

当设备通过热插拔从系统中添加和移除时，`udev` 会创建事件。创建和移除设备节点、主号和次号、权限等信息是从信息源（在 `/sys` 监控）收集的，并设置为配置文件。

```c
cdev_del(struct cdev *cdev);
```

在设备从系统移除后，在此之后永远不应再次访问该 `cdev` 结构。

主配置文件是 `/etc/udev/rules.d`。它包含了关于设备放置位置和所有权的信息。默认情况下，设备命名的规则位于 `/etc/udev/rules.d`。通过阅读 `udev` 的主页，你可以获得大量关于如何设置 `udev` 的信息。

## 4.6 udev 和 HAL

在 Linux 进化之前，管理设备节点的方法变得非常笨拙。`/dev` 及其子目录中的设备节点数量达到了 15 个。

通过使用以下函数在驱动程序内部动态创建和移除设备节点是可能的：

```c
#include <linux/class.h>
```

```c
struct class {struct module *owner; const char *name};
struct device {struct class *class; struct device *parent, dev_t devt};
dev_create(struct class *cls, dev_t devt)
dev_destroy(struct class *cls, dev_t devt);
```

如今许多开发者和系统管理员受限于实际所需的需求，特别是当必须创建和销毁设备节点时，但这是一种手动且潜在易出错的方法。

通常，在层级结构的顶层创建类是比较好的。类片段似乎用于这些函数之一：

```c
static struct class *class_class;
```

```c
// 在初始化函数中创建节点
class_class = class_create(THIS_MODULE, "my_class");
dev_create(class_class, NULL, "Xdev", "mydev");
```

```c
// 在退出函数中移除节点
dev_destroy(class_class, "Xdev");
class_destroy(class_class);
```

请注意，设备节点不是普通文件，不占用文件系统空间，驱动程序可以直接访问设备节点，特别是在第一次使用时。此外，主号和次号可用性的耗尽需要一种更现代、动态的方法来创建和管理设备节点。

理想情况下，人们希望通过名称注册设备，然而，主号和次号无法完全消除，因为 `udev` 仍然需要它们。

`udev` 方法创建了可能永远需要的设备。`udev` 中的 `u` 代表用户（user），它表示创建、移除和修改设备节点的大部分工作是在用户空间完成的。

必须小心在设备节点创建之前使设备可用哪些操作是必要的，以避免竞态条件。

## 4.7 operations 结构

`file_operations` 结构定义在 `/usr/src/include/linux/fs.h` 中，如下：
