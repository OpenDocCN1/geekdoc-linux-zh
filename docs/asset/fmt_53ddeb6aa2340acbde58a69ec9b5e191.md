
`dev_link_t` 结构的字段指向一个 `dev_node_t` 结构链表。在 `dev_node_t` 中，`dev_name` 字段由驱动程序填充，包含用于访问该设备的设备文件名，例如，`serial_cs` 驱动程序使用如“`ttyS1`”之类的名称。访问此设备的主设备和次设备号。`Driver Services` 通过 `DS_GET_DEVICE_INFO` `ioctl` 将这些字段传递给用户态程序。

在 `dev_link_t` 中，`state` 字段用于跟踪当前设备状态。以下是标志位：

- `DEV_PRESENT`: 表示卡存在。此位应设置。
- `DEV_CONFIG`: 表示卡已配置。
- `DEV_CONFIG_PENDING`: 表示配置正在进行。
- `DEV_SUSPEND`: 表示卡已挂起。
- `DEV_BUSY`: 表示操作正在进行。
- `DEV_STALE_CONFIG`: 表示配置已过期。
- `DEV_STALE_LINK`: 表示链接已失效。

## 7. 驱动服务接口

### 7.2.3 driver_operations 入口

`attach()` 入口点用于配置单个设备，其参数是一个描述设备查找位置的“设备定位器”（device locator）结构。

`dev_locator_t` 结构如下：

```c
typedef struct dev_locator_t {
    enum { LOC_ISA, LOC_PCI } bus;
    union {
        struct {
            u_short io_base_1, io_base_2;
            u_long mem_base;
            u_char irq, dma;
        } isa;
        struct {
            u_char bus;
            u_char devfn;
        } pci;
    } b;
} dev_locator_t;
```

`attach()` 函数应返回 `NULL` 或一个描述新设备的有效 `dev_node_t` 结构。所有其他入口点都使用此指针来识别要操作的设备。`cb_enabler` 模块会根据卡的插入和拔出事件调用 `attach()` 和 `detach()` 入口。`suspend()` 和 `resume()` 入口则会在响应电源管理事件时调用。

没有办法拒绝 `suspend()` 或 `detach()`。当接收到 `detach()` 事件时，驱动程序应该阻塞任何对指定设备的后续 `IO` 操作，但在内核设备实际关闭之前，可以保留内部数据结构。

### 7.3 访问用户态实用工具的接口

`Driver Services` 创建了一个伪设备，用于与用户态 `PC` 卡进行通信。设备的主设备号是动态选择的，`PC` 卡通过 `/proc/devices` 确定它。次设备号对应套接字号，从 `0` 开始。

只允许一个进程打开读写套接字。其他进程可以只读模式打开套接字。到 `Driver Services` 的只读连接可以执行部分 `ioctl` 操作。读写连接可以发出所有 `ioctl`，还可以接收 `Card Services` 事件通知。

#### 7.3.1 Card Services 事件通知

`Driver Services` 为事件通知实现了 `read()` 和 `select()` 函数。从 `PC` 卡设备读取数据将返回一个无符号值，其中包含了 `Driver Services` 自上一次 `read()` 以来收到的所有事件。如果没有收到任何事件，调用将阻塞直到下一个事件发生。可以使用 `select()` 来监控多个套接字是否有新事件。

`Driver Services` 监控以下事件：`CS_EVENT_CARD_INSERTION`、`CS_EVENT_CARD_REMOVAL`、`CS_EVENT_RESET_PHYSICAL`、`CS_EVENT_CARD_RESET` 以及 `CS_EVENT_RESET_COMPLETE`。

#### 7.3.2 Ioctl 描述

大多数 `Driver Services` `ioctl` 操作直接映射到 `Card Services` 函数。`ioctl` 调用形式如下：

```c
int ioctl(int fd, int cmd, ds_ioctl_arg *arg);
```

`ds_ioctl_arg_t` 结构如下：

```c
typedef union ds_ioctl_arg_t {
	servino_t		servino;
	adjust_t		adjust;
	config_info_t		config;
	tuple_t		tuple;
	tuple_parse_t	tuple_parse;
	client_req_t		client_req;
	status_t		status;
	conf_reg_t		conf_reg;
	cisinfo_t		cisinfo;
	region_info_t		region;
	bind_info_t		bind_info;
	mtd_info_t		mtd_info;
	cidump_t;cidump;
} ds_ioctl_arg_t;
```

以下 `ioctl` 命令执行相应的 `Card Services` 函数：

- `DS_GET_CARD_SERVICES_INFO`: 调用 `CardServices(GetServicesInfo, ..., &arg->servino)`。
- `DS_ADJUST_RESOURCE_INFO`: 调用 `CardServices(AdjustResourceInfo, ..., &arg->adjust)`。
- `DS_GET_CONFIGURATION_INFO`: 调用 `CardServices(GetConfigurationInfo, ..., &arg->config)`。
- `DS_GET_FIRST_TUPLE`: 调用 `CardServices(GetFirstTuple, ..., &arg->tuple)`。
- `DS_GET_NEXT_TUPLE`: 调用 `CardServices(GetNextTuple, ..., &arg->tuple_parse.data)`。
- `DS_GET_TUPLE_DATA`: 调用 `CardServices(GetTupleData, ..., &arg->tuple_parse.tuple)`。元组数据返回在 `arg->tuple_parse.data` 中。
- `DS_PARSE_TUPLE`: 调用 `CardServices(ParseTuple, ..., &arg->tuple_parse.tuple, &arg->tuple_parse.parse)`。
- `DS_RESET_CARD`: 调用 `CardServices(ResetCard, ...)`。
- `DS_GET_STATUS`: 调用 `CardServices(GetStatus, ..., &arg->status)`。
- `DS_ACCESS_CONFIGURATION_REGISTER`: 调用 `CardServices(AccessConfigurationRegister, ..., &arg->conf_reg)`。
- `DS_VALIDATE_CIS`: 调用 `CardServices(ValidateCIS, ..., &arg->cisinfo)`。
- `DS_SUSPEND_CARD`: 调用 `CardServices(SuspendCard, ...)`。
- `DS_RESUME_CARD`: 调用 `CardServices(ResumeCard, ...)`。
- `DS_EJECT_CARD`: 调用 `CardServices(EjectCard, ...)`。
- `DS_INSERT_CARD`: 调用 `CardServices(InsertCard, ...)`。
- `DS_GET_FIRST_REGION`: 调用 `CardServices(GetFirstRegion, ..., &arg->region)`。
- `DS_GET_NEXT_REGION`: 调用 `CardServices(GetNextRegion, ..., &arg->region)`。
- `DS_REPLACE_CIS`: 调用 `CardServices(ReplaceCIS, ..., &arg->cisump)`。

以下 `ioctl` 触发 `Driver Services` 函数。它们作用于 `bind_info_t` 结构：

```c
typedef struct bind_info_t {
    dev_info;
    dev_info_t;
    u_char function;
    struct dev_info_t *instance;
    char name[DEV_NAME_LEN];
    u_char major, minor;
    void *next;
} bind_info_t;
```
