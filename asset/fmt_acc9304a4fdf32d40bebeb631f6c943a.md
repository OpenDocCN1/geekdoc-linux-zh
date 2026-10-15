
`pci_driver` 结构体中的字段之一 `probe` 指向一个包含驱动程序初始化入口的函数，该函数在 PCI 设备配置空间与驱动程序 ID 结构之间检测到匹配后被调用。`e100` 驱动程序的一个 PCI ID 匹配示例如表 4.3 所示。此初始化的事件序列如图 4.2 所示。另一种查看工作原理的方法是查看 Linux 中以太网驱动的代码。例如，我们查看 `e100` 驱动程序。一旦该序列完成，PCI 就会匹配到其设备，驱动程序初始化就可以继续。

PCI 驱动程序模块静态定义了 `pci_driver` 结构体的一个实例。

```c
struct pci_driver {
```

第一个字段 `node` 是所有 PCI 驱动程序列表的头节点。

```c
struct list_head      node;
```

`name` 是驱动程序名称。`id_table` 指向要调用的函数指针。我们的 `e100` 驱动程序支持的一个以太网芯片的 `id_table` 条目示例如图 4.2 所示。`probe` 指向在发现匹配设备时或如果设备是热插拔的、在插入时调用的函数。对于热插拔设备，`remove` 不得为 `NULL`。

```c
char                *name;
const struct pci_device_id *id_table;
int             (*probe) (struct pci_dev *dev, const struct pci_device_id *id);
```

下一个函数 `remove` 在热插拔设备从 PCI 总线移除时被调用。`suspend` 在设备挂起时被调用，`resume` 在设备被唤醒时被调用。

```c
void (*remove) (struct pci_dev *dev);
int (*suspend) (struct pci_dev *dev, u32 state);
int (*resume) (struct pci_dev *dev, u32 state);
```

下一个字段 `enable_wake` 指向启用或禁用 `wake_up` 事件的函数。

```c
int (*enable_wake) (struct pci_dev *dev, u32 state, int enable);
struct device_driver      driver;
struct pci_dynids         dynids;
```

PCI 驱动程序被初始化为一个静态结构。在这里展示了 `e100` 模块如何初始化 `pci_driver` 结构中的字段。这在 `linux/drivers/net/e100/e100_main.c` 文件中完成。

```c
MODULE_DEVICE_TABLE(pci, e100_id_table);
static struct pci_driver e100_driver = {
    name: "e100",
    id_table: e100_id_table,
```

`id_table` 指向要调用的函数指针。我们的 `e100` 驱动程序支持的一个以太网芯片的 `id_table` 条目示例如图 4.2 所示。`probe` 指向在发现匹配设备时或如果设备是热插拔的、在插入时调用的函数。`remove` 不得为 `NULL`。

```c
probe: e100_found1
remove: __devexit(e100_remove)
#ifdef CONFIG_PM
suspend: e100_suspend,
resume: e100_resume,
#endif
```

## 4.6 网络接口注册

初始化 `pci_driver` 结构中的字段后，私有数据可以注册为网络设备。这在 `linux/drivers/net/e100/e100_main.c` 文件中完成。网络设备注册包括将驱动网络设备放在链表中。`linux/net/core/dev.c` 和 `linux/net/net_init.c` 提供了注册所需的工具函数。网络设备注册使用 `net_dev` 结构中的 `name` 字段。为了执行网络接口注册的最后一步，驱动程序初始化调用 `net_init.c` 中的 `register_netdev`。

```c
int register_netdev(struct net_device *dev)
{
    int err;
```

通过获取网络内核锁来锁定。

```c
rtnl_lock();
```

`dev_alloc_name` 被调用将字符串 `%d` 设备名称替换为数字。所选数字是到目前为止的设备数。例如，第一个设备将是 `eth0`，第二个将是 `eth1`，依此类推。

```c
if (strchr(dev->name, '%'))
{
    err = dev_alloc_name(dev, dev->name);
    if (err < 0)
        goto out;
}
```

这是一个所有以太网设备的后兼容钩子，可能会被弃用。在调用此之前，`net_dev` 结构中的 `name` 字段应该初始化为基础名称加上格式字符。

```c
if (dev->name[0]==0 || dev->name[0]=='')
{
    err = dev_alloc_name(dev, "eth%d");
    if (err < 0)
        goto out;
}
```

我们将 `register_netdev` 用于与网络接口注册相关的繁重工作。如果调用者知道设备名称已设置正确，可以直接调用 `register_netdev`，但前提是先获取网络内核锁。

```c
err = register_netdev(dev);
```

我们在返回前必须解锁。

```c
rtnl_unlock();
return err;
```

在初始化网络设备结构时，`qdisc` 和 `qdisc_sleeping` 字段应该指向一个默认队列规则。

### 4.6.1 网络设备注册实用函数

本节中的所有函数都声明在 `linux/include/linux/netdevice.h` 文件中。第一个函数 `dev_get_by_name` 通过名称查找设备。可以在任何上下文中调用，因为它拥有自己的锁机制。它根据字符串返回一个指向 `net_device` 的指针。在函数返回之前，`net_device` 中的引用计数字段会增加。

```c
struct net_device *dev_get_by_name(const char *name);
```

第一个函数 `register_netdev` 用于注册网络接口驱动程序。此版本的函数会获取调用者。如果 `register_netdev` 返回时调用者已持有了 `rtnl` 锁，则也可以使用该函数。

```c
int      register_netdev(struct net_device *dev);
```

`register_netdev` 的一个重要职责是将网络设备结构放置在 Linux 内核的网络设备驱动程序列表中。在此之前，它会初始化设备的队列和 `xmit_list` 字段。它在编译时检查一个全局变量 `dev_boot_phase` 以指示设备已初始化。如果 `dev_boot_phase` 被设置，则会调用 `netdev_init` 函数，该函数会初始化队列层——这会在第一个设备初始化时发生一次，因为 `netdev_init` 退出时会被重置为 0。（有关队列层的更多细节，请参见第 6 章）。设备被分配了一个唯一的 `ifindex`，该数字被设置在 `netdevice` 的 `ifindex` 字段中。接下来，`state` 字段被设置为 `_LINK_STATE_PRESENT`，表示设备存在并已准备好调度。

```c
int      register_netdev(struct net_device *dev);
```

接下来的函数 `register_netdev` 和 `unregister_netdev` 从设备列表中移除设备。其中第一个函数 `unregister_netdev` 是“安全”版本。在例程中，我们获取 `rtn` 信号量并调用内部例程 `unregister_netdev`。

```c
void     unregister_netdev(struct net_device *dev);
```

下一个函数也用于注销 `net_device`。在该函数中，我们要求调用者在调用之前获取 `rtn` 信号量。

```c
int unregister_netdev(struct net_device *dev)
{
    struct net_device *d, **dp;
    BUG_ON(dev_boot_phase);
    ASSERT_RTNL();
```

我们还防止在从未注册过的设备上进行调用。
