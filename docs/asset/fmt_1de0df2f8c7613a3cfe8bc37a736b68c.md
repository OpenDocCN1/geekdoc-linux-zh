
```
block
  loop0 -> ../devices/virtual/block/loop0
  md0 -> ../devices/virtual/block/md0
  nbd0 -> ../devices/virtual/block/nbd0
  ram0 -> ../devices/virtual/block/ram0
  xvda -> ../devices/vbd-51712/block/xvda
bus
  platform
  serio
class
  bdi
  block
  input
  mem
  misc
  net
  ppp
  rtc
  tty
  vc
  vtconsole
dev
  block
  char
devices
  console-0
  platform
  system
  vbd-S1712
  vbd-S1728
  vir0
  virtual
firmware
fs
  encryptfs
  ext4
  fuse
  gfs2
kernel
  config
  dim
  mem
  notes
  uevent_helper
  uevent_seqnum
  uids
module
  ext4
  i8042
  kernel
  keyboard
  mousedev
  nbd
  printk
  psmouse
  sch_htb
  tcp_cubic
  vt
  xt_recent
```

图 17.2 `/sys` 树的部分视图。

`sysfs` 的根包含至少 10 个目录：`block`, `bus`, `class`, `dev`, `devices`, `firmware`, `fs`, `kernel`, `module`, `power`。`block` 目录为系统上每个注册的块设备包含一个目录。这些目录中的每一个包含了该块设备上的所有分区。`bus` 目录提供了系统总线的视图。`class` 目录包含了按高层功能组织的设备视图。`dev` 目录是系统设备拓扑的视图。它直接映射到内核内部设备结构体的层级结构。`firmware` 目录包含一个特定于系统的低级子系统树，如 `ACPI`、`EDD`、`EFI` 等。`fs` 目录包含已注册文件系统的视图。`kernel` 目录包含内核配置选项和状态信息，而 `module` 目录包含了系统已加载模块的视图。`power` 目录包含系统级的电源管理数据。并非所有系统都拥有所有目录，其他系统还存在此处未提到的目录。

最重要的目录是 `devices`，它向外界导出设备模型。设备结构是系统的实际设备拓扑。其他许多目录是 `devices` 目录中数据的简单组织替代方案。例如，`/sys/class/net/` 根据注册接口的高层概念来组织设备。该目录内部有一个子目录 `eth0`，它包含一个指向 `devices` 中实际设备目录的符号链接设备。

查看具有访问权限的 Linux 系统上的 `/sys`。一个如此精确的系统设备结构非常整洁，看到 `class` 中的高层概念与 `devices` 中的低级物理设备以及 `bus` 中的实际驱动程序之间的互连是非常获益匪浅的。当你意识到数据作为内核维护设备层级结构的副作用而被免费提供的，并且这些数据是内核内部维护的系统表示时，整个体验会变得更有成就感。

## 从 sysfs 中添加和删除对象

初始化的对象不会自动导出到 `sysfs`。要将一个 `kobject` 表示于 `sysfs`，你使用 `kobject_add()`：

```
int kobject_add(struct kobject *kobj, struct kobject *parent, const char *fmt, ...);
```

给定的 `kobject` 在 `sysfs` 中的位置取决于它在对象层级结构中的位置。如果没有设置父指针，则 `kobject` 将映射到 `sysfs` 中其父目录下的子目录。

> 如果你觉得 `sysfs` 有趣，你可能对 `HAL` 感兴趣，这是一个硬件抽象层，可以在 `http://www.freedesktop.org/wiki/Software/hal` 找到。`HAL` 基于 `sysfs` 中的数据构建一个内存数据库，将类、设备和驱动器的概念连接在一起。在此数据之上，`HAL` 提供了丰富的 `API`，能够实现更智能的、硬件感知的应用程序。

`kset->kobj`。如果在给定的 `kset` 中既没有设置 `parent` 也没有设置 `kset`，则假设对象没有父节点，并映射到 `sysfs` 中的根级目录。在大多数情况下，在调用 `kobj_add()` 之前，应该适当地设置 `parent` 和 `kset` 的一个或两者。无论如何，`sysfs` 中表示 `kobj` 的目录名称由 `fmt` 指定，它使用 `printf()` 风格的格式字符串。

辅助函数 `kobj_create_and_add()` 将 `kobj_create()` 和 `kobj_add()` 的工作合并为一个函数：

```
struct kobj *kobj_create_and_add(const char *name, struct kobj *parent);
```

注意 `kobj_create_and_add()` 接收 `kobj` 目录名称的指针指针，而 `kobj_add()` 使用 `printf()` 风格的格式。删除 `kobj` 的表示通过 `kobj_del()` 完成：

```
void kobj_del(struct kobject *kobj);
```

所有这些函数都定义在 `lib/kobj.c` 中，并在 `<linux/kobj.h>` 中声明。

## 向 sysfs 中添加文件

`Kobjects` 映射到目录，完整的对象层级结构可以很好地映射到 `sysfs` 目录结构，但文件呢？`sysfs` 仅仅是对象的视图。

## 默认属性

与 `kobject` 关联的 `ktype` 提供的默认属性已经足够了。类型的目的是为 `ktypes` 提供通用操作。与 `kobjects` 共享 `ktypes` 不仅简化了编程，还为相关对象的 `sysfs` 提供了整合性和统一的视觉感受。

```c
/* 属性结构体 */
struct attribute {
    const char *name;          /* 属性名称 */
    struct module *owner;       /* 所有者模块，如果有 */
    mode_t mode;               /* 权限 */
};
```

`name` 成员提供了 `sysfs` 中的文件名称。`owner` 成员指向一个模块，如果有。如果模块不拥有此属性，则 `owner` 为 `NULL`。`mode` 成员是一个 `mode_t` 类型，指定了文件的权限。只读属性如果是全局可读的，可能希望设置为 `S_IRGO`；如果仅所有者可读，则希望设置为 `S_IRUSR`。可写属性可能希望设置为 `S_IRGO | S_IWUSR`。所有文件都归 `uid` 和 `gid` 0 所有。

```c
struct sysfs_ops {
    /* 在读取 sysfs 文件时调用的方法 */
    ssize_t (*show) (struct kobject *kobj, struct attribute *attr, char *buffer);

    /* 在写入 sysfs 文件时调用的方法 */
    ssize_t (*store) (struct kobject *kobj, struct attribute *attr, const char *buffer, size_t size);
};
```

`show()` 方法在用户空间读取 `sysfs` 时被调用。它必须将 `attr` 给出的属性值拷贝到提供的 `buffer` 中。`buffer` 的长度为 `PAGE_SIZE`；在 `x86` 上，`PAGE_SIZE` 是 4096。该函数在成功时返回实际写入 `buffer` 的字节数，失败时返回负错误代码。

`store()` 方法在写入时被调用。它必须从 `buffer` 中读取 `size` 字节到 `attr` 指向的变量中。`buffer` 的大小总是 `PAGE_SIZE` 或更小。该函数在成功时返回从 `buffer` 读取的字节数，失败时返回负错误代码。

由于这些函数必须处理所有属性的 I/O 请求，它们通常需要维护某种通用映射，以调用特定于每个属性的处理程序。

## 创建新属性

通常，与 `kobject` 关联的 `ktype` 提供的默认属性已经足够了。类型的目的是为类型提供通用操作。与 `kobjects` 共享 `ktypes` 不仅简化了编程，还为相关对象的 `sysfs` 提供了整合性和统一的视觉感受。

然而，某些 `kobject` 实例可能是特殊的。它想要甚至需要自己的属性——也许是为了提供通用类型不共享的数据或功能。内核提供了 `sysfs_create_file()` 接口在默认集合之上添加新属性：

```
int sysfs_create_file(struct kobject *kobj, const struct attribute *attr);
```

该函数将 `attr` 指向的属性结构与 `kobj` 指向的 `kobject` 关联。在调用它之前，应该填充给定的属性。该函数在成功时返回零，否则返回负错误代码。

# 第 17 章 设备与模块
