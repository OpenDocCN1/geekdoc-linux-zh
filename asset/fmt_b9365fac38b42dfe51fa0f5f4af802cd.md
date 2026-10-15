
## FDDI 设备初始化

### 参数

- `dev`: 要填充的 FDDI 设备结构，或者如果应该分配新的 `struct` 则为 `NULL`。
- `sizeof_priv`: 分配额外的私有结构的大小

### 描述

填充以太网设备结构的值。

如果传递了设备结构，则创建一个大小为 `sizeof_priv` 的私有区域。对于该私有区域执行 32 字节对齐。

## alloc_fddidev — 分配 FDDI 设备

### 签名

```
struct net_device * alloc_fddidev (int sizeof_priv);
```

### 参数

- `sizeof_priv`: 分配私有结构的大小

### 描述

填充以太网设备结构的值。

## init_hippi_dev — 注册 HIPPI 设备

### 签名

```
struct net_device * init_hippi_dev (struct net_device * dev, int sizeof_priv);
```

### 参数

- `dev`: 要填充的 HIPPI 设备结构，或者如果应该分配新的 `struct` 则为 `NULL`。
- `sizeof_priv`: 分配额外的私有结构的大小

### 描述

填充以太网设备结构的值。

如果传递了设备结构，则创建一个大小为 `sizeof_priv` 的私有区域。对于该私有区域执行 32 字节对齐。

## alloc_hippi_dev — 分配并设置 HIPPI 设备

### 签名

```
struct net_device * alloc_hippi_dev (int sizeof_priv);
```

### 参数

- `sizeof_priv`: 分配私有结构的大小

### 描述

填充以太网设备结构的值。

## 光纤通道设备初始化

### 参数

- `dev`: 一个待填充的光纤通道设备结构，如果需要分配新结构体则为 `NULL`。
- `sizeof_priv`: 为此以太网设备分配的额外驱动私有结构的大小。

### 描述

使用光纤通道通用值填充设备结构中的字段。

如果没有传递设备结构，则会构造一个新的结构体，并包含一个大小为 `sizeof_priv` 的私有数据区域。该私有数据区域强制执行 32 字节（而非位）对齐。

如果传递的 `dev->name` 为空字符串区域或创建了新结构，则将构造一个新的字符串。

## alloc_fcdev — 注册光纤通道设备

### 签名

```
struct net_device * alloc_fcdev (int sizeof_priv);
```

### 参数

- `sizeof_priv`: 为此以光纤通道设备分配的额外驱动私有结构的大小。

### 描述

使用光纤通道通用值填充设备结构中的字段。

构造一个新的网络设备，并包含一个大小为 `sizeof_priv` 的私有数据区域。该私有数据区域强制执行 32 字节（而非位）对齐。

## dev_add_pack — 添加数据包处理器

### 签名

```
void dev_add_pack (struct packet_type * pt);
```

### 参数

- `pt`: 数据包类型声明

### 描述

向网络栈添加一个协议处理程序。传递的 `&packet_type` 被链接到内核列表中，在它从内核列表中移除之前可能被释放。

## dev_remove_pack — 移除数据包处理器

### 签名

```
void dev_remove_pack (struct packet_type * pt);
```

### 参数

- `pt`: 数据包类型声明

### 描述

移除之前通过 `dev_add_pack` 添加到内核协议处理器的协议处理程序。传递的 `&packet_type` 将从内核列表中移除，并在此函数返回后可以释放或重用。

## __dev_get_by_name — 通过名称查找设备

### 签名

```
struct net_device * __dev_get_by_name (const char * name);
```

### 参数

- `name`: 要查找的内容

### 描述

通过名称查找接口。必须在 RTNL 信号量或 `dev_base_lock` 下调用。如果找到名称，则返回设备指针。如果未找到，则返回 `NULL`。引用计数不会增加，因此调用者必须小心处理锁。

## dev_get_by_name — 通过名称查找设备

### 签名

```
struct net_device * dev_get_by_name (const char * name);
```

### 参数

- `name`: 要查找的名称

### 描述

通过名称查找接口。这可以在任何上下文中调用，并处理自己的锁。返回的句柄使用计数已增加，调用者在不再需要它时必须使用 `dev_put` 来释放它。如果没有找到匹配的设备，则返回 `NULL`。

## dev_get — 测试设备是否存在

### 签名

```
int dev_get (const char * name);
```

### 参数

- `name`: 要测试的名称

### 描述

测试名称是否存在。如果找到名称，则返回 true。为了确保名称在测试期间未被分配或移除，调用者必须持有 rtnl 信号量。

此函数主要存在是为了与旧驱动程序兼容。

## __dev_get_by_index — 通过 ifindex 查找设备

### 签名

```
struct net_device * __dev_get_by_index(int ifindex);
```

### 参数

- `ifindex`: 设备的索引

### 描述

通过索引搜索接口。如果未找到设备，则返回 `NULL` 或返回设备指针。设备的引用计数未增加，因此调用者必须小心处理锁。调用者必须持有 RTNL 信号量或 `dev_base_lock`。

## dev_get_by_index — 通过 ifindex 查找设备

### 签名

```
struct net_device * dev_get_by_index (int ifindex);
```

### 参数

- `ifindex`: 设备的索引

### 描述

通过索引搜索接口。如果未找到设备，则返回 `NULL` 或返回设备指针。返回的设备已增加引用，在用户调用 `dev_put` 表明已完成操作之前，该指针是安全的。

## dev_alloc_name — 为设备分配名称

### 签名

```
int dev_alloc_name (struct net_device * dev, const char * name);
```

### 参数

- `dev`: 设备
- `name`: 名称格式字符串

### 描述

传递一个格式字符串——例如 `"%s"`——它将尝试寻找一个合适的 ID。对于许多设备来说效率不高，且调用并不频繁。调用者在分配名称和添加设备时必须持有 `dev_base` 或 `rtl` 锁，以避免重复。返回分配的单元号或负 errno 错误码。

## dev_alloc — 分配网络设备和名称

### 签名

```
struct net_device * dev_alloc (const char * name, int * err);
```

### 参数

- `name`: 名称格式字符串
- `err`: 错误返回指针

### 描述

传递格式字符串，例如 `"ltd"`，它将分配一个网络设备和名称空间。如果没有可用内存，则返回 `NULL`。如果分配成功，则会分配名称并返回设备指针。如果名称分配失败，则返回 `NULL`。错误原因将作为负 errno 错误码通过 `err` 指向的变量返回。

调用者在执行此操作时必须持有 `dev_base` 或 RTNL 锁，以避免重复分配名称。

## netdev_state_change — 设备状态变更

### 签名

```
void netdev_state_change (struct net_device * dev);
```
