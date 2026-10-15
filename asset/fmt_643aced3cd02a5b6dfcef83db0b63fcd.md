
关于队列规则（`queue disciplines`）的更多细节请参阅第 5 章，关于队列规则如何用于路由和流量分类调度请参阅第 8 章。

## 通知链与网络接口设备状态通知

`Notifier` 提供了一种用于设备状态变化通知的机制，称为通知链（`notifier chains`）。它基于一个通用的通知设施，该设施可以被内核中的任何模块用于各种目的。在 `TCP/IP` 栈中，通知链用于将网络设备状态的变化或其他事件传递给任何向该设施注册了自身的协议、模块或设备。通知链用于是将将状态变化传递给任何在通知设施中注册的函数。表 3.7 显示了目前 Linux 内核中使用的预定义通知事件。这些值定义在 `linux/include/linux/notifier.h` 文件中。通知链实际上是一个非常简单的结构，无非比一个用于事件通知的函数链表而已。

### 表 3.7 预定义的网络设备通知事件

| 名称 | 值 | 用途 |
| --- | --- | --- |
| `NETDEV_UP` | `0x001` | 网络设备启动通知 |
| `NETDEV_DOWN` | `0x002` | 网络设备关闭通知 |
| `NETDEV_REBOOT` | `0x003` | 通知协议网络接口发生崩溃并重启 |
| `NETDEV_CHANGE` | `0x004` | 设备状态变化通知 |
| `NETDEV_REGISTER` | `0x005` | 网络设备注册事件 |
| `NETDEV_UNREGISTER` | `0x006` | 网络设备注销事件 |
| `NETDEV_CHANTU` | `0x007` | `MTU` 更改通知 |
| `NETDEV_CHANGEADDR` | `0x008` | 网络地址更改通知 |
| `NETDEV_GOING_DOWN` | `0x009` | 网络设备正在关闭 |
| `NETDEV_CHANGENAME` | `0x00A` | 网络设备名称更改 |
| `NETDEV_FEAT_CHANGE` | `0x00B` | 网络设备功能变更 |

通知链中的每个位置都由 `notifier_block` 结构实例定义。该结构通常由想要使用通知设施的代码在编译时初始化。

该结构中的第一个字段 `notifier_call` 是事件通知函数。该字段是静态初始化的。

## 第 3 章 Linux 网络接口驱动程序 105

```c
int (*notifier_call)(struct notifier_block *self, unsigned long, void *);
```

`next` 不是静态分配的。期望接收事件通知的模块必须一个 `notifier_block` 实例并将 `next` 字段设置为 `NULL`，以便在注册通知块时填充该字段。

```c
struct notifier_block *next;

int priority;
```

## 通用事件通知函数

Linux 提供了一组通用的事件通知函数。这些函数供网络接口驱动编写者和协议使用者使用，以便处理表 3.7 中的各种设备状态变化事件。

### `register_notifier`

要在链中注册，我们调用注册函数 `register_notifier` 并传入 `notifier_block` 的指针。

```c
int register_notifier(struct notifier_block *nb);
```

函数的调用者并不挑选它将看到哪些事件。

### `unregister_notifier`

要从网络设备通知链中注销，我们调用 `unregister_notifier` 从链中移除 `notifier_block`。

```c
int unregister_notifier(struct notifier_block *nb);
```

### `notifier_call`

通知函数将通过 `nb` 中的 `notifier_call` 字段被调用，对应表 3.7 中的所有事件类型。

```c
int (*notifier_call)(struct notifier_block *self, unsigned long, void *);
```
