
请求和释放资源等同于在资源树中添加和删除条目。¹¹ 内核提供了 `request_resource` 函数请求资源区域。¹² 该函数期望一系列参数，包括指向父元素的指针、地址资源的起始地址和结束地址，以及一个用于存储区域名称的字符串。

其目的是分配一个资源实例并填充数据。还会进行检查以检测明显的错误（例如地址大于结束地址），这些错误会使资源无用并中止操作。`request_resource` 只负责锁定。繁重的工作被委托给 `__request_resource`。它会连续扫描现有资源，以便将新资源添加到正确的位置，或者揭示与已分配区域的冲突。它通过扫描现有资源来实现这一点。如果区域空闲，则插入新资源。

## 第 6 章：设备驱动程序

| 名称 | 起 | 结束 | 标志 | 父节点 | 兄弟 |
|---|---|---|---|---|---|
| *pstruc...:parent "PCI bus" | 0 | end=4294967295 | parent=0x00082000 | | |
| 名称 | 起 | 结束 | 标志 | 父节点 | 兄弟 |
|---|---|---|---|---|---|
| *Oacle710 "PCI Bus #1" | 0 | end=4095 | flags=512 | parent=0x002f1234 | sibling=Oacle31c |
| 名称 | 起 | 结束 | 标志 | 父节点 | 兄弟 |
|---|---|---|---|---|---|
| *Oacle825 "Intel Corp. PCI 8215 (Chip Graphics Controller)" | 0 | end=4294967295 | parent=0x002f1234 | sibling=Oacle31c |
| 名称 | 起 | 结束 | 标志 | 父节点 | 兄弟 |
|---|---|---|---|---|---|
| *Oacle31c "Intel Corp. 82N2 (ICNS2) Ethernet Controller" | 0 | end=4095 | flags=512 | parent=0x002f1234 | sibling=Oacle38c |
| 名称 | 起 | 结束 | 标志 | 父节点 | 兄弟 |
|---|---|---|---|---|---|
| *Oacle04c "PCI device 104c:8021 (Texas Instruments)" | 0 | end=4095 | flags=512 | parent=0x002f1234 | sibling=Oacle48c |
| 名称 | 起 | 结束 | 标志 | 父节点 | 兄弟 |
|---|---|---|---|---|---|
| *pstruc...:b-child "exp107" | 0 | end=4294967295 | flags=0x214f8568 | parent=0 | sibling=0 |

图 6-1：PCI 网卡的分配资源。

### 6.6.3 I/O 端口

I/O 端口是与设备和总线通信的常用方式，尤其是在 IA-32 世界。对于 I/O 内存，事实上在驱动程序访问之前必须注册该区域——遗憾的是，资源本身无法检查是否已完成此操作。

来自 `kernel/resource.c` 的 `ioport_resource` 充当元素资源树的根。proc 文件系统中的 `ioports` 文件显示了根端口地址。

```
wolfgang@mitner cat /proc/ioports
0000-01f : dnal
0020-003f : picl
0040-005f : timer
0060-006f : keyboard
```

```
0170-0177 : idel
...
0378-037a : parport0
03C0-03df : vga
...
0CF8-0FFF : PCI conf1
1800-180f : Intel Corp. 82820 8220 (Camino 2) Chipset IDE U100 (-M)
1800-1807 : ideo
1808-180f : idel
1810-181f : Intel Corp. 82820 8220 (Camino 2) Chipset SMBus
1820-183f : Intel Corp. 82820 8220 (Camino 2) Chipset USB (Hub A)
...
3000-3fff : PCI Bus #01
3000-303f : Intel Corp. 82820 (ICH2) Chipset Ethernet Controller
3000-303f : epro1100
```

表 6-3：访问 I/O 内存区域的函数。

| 函数 | 含义 |
|---|---|
| `readb(addr)`<br>`readw(addr)`<br>`readl(addr)` | 从指定的 I/O 地址 `addr` 读取一个字节、字字或长整数。 |
| `writeb(val, addr)`<br>`ritew(val, addr)` | 将 `val` 指定的字节、字字或长整数值写入 I/O 地址 `addr`。 |
| `writel(val, addr)` | 将 `num` 个字节从 I/O 地址移动到普通地址空间中的 `src`。 |
| `memcpy(dest, src, num)` | 从普通空间中的 `dst` 复制字节到 I/O 区域的 `src`。 |
| `memcpy_toio(dest, src, num)`<br>`memset_io(addr, value, count)` | 从位置 `addr` 开始填充 `count` 个 `value`。 |

内核利用缩进来反映父/子/兄弟之间的关系。该列表是在与上方所示 I/O 内存区域相同的系统上生成的。有趣的是，该列表不仅包含键盘和定时器等标准系统组件，还包含了几个 I/O 映射设备，例如以太网控制器——毕竟，没有理由设备不能通过端口和 I/O 内存寻址。

通常，端口必须在汇编层级通过特殊的进程命令进行访问。内核提供了相应的宏，为驱动程序程序员提供与平台相关的接口。它们列在表 6-4 中。

表 6-4：访问 I/O 端口的函数。

| 函数 | 含义 |
|---|---|
| `insb(port)` | 从端口 `port` 读取一个字节。 |
| `insw(port)` | 从端口 `port` 读取一个字字。 |
| `insl(port)` | 从端口 `port` 读取一个长整数。 |
| `outb(val, port)` | 将字节 `val` 写入端口 `port`。 |
| `outw(val, port)` | 将字字 `val` 写入端口 `port`。 |
| `outl(val, port)` | 将长整数 `val` 写入端口 `port`。 |

### 6.7 总线系统

设备通过总线与内核交互。总线是多个组件连接的路径。内核提供了一个抽象层来管理这些总线，驱动程序无需了解硬件细节。

内核使用分级结构来表示总线拓扑。像 PCI 这样的高级总线可以拥有多个子总线。

总线模型负责：

- 发现总线上的设备。
- 管理资源（I/O 端口、内存映射、中断）。
- 为驱动程序提供接口。

### 6.7.1 通用驱动模型

内核使用通用驱动模型来处理支持的各种设备。该模型为驱动程序的注册和管理提供统一的方法。该模型的核心是 `device`、`driver` 和 `bus` 结构。

`device` 代表硬件组件。`driver` 代表控制设备类型的软件。`bus` 代表连接路径。

设备与驱动程序之间的关系通过匹配过程建立。当发现一个设备时，内核会寻找可以处理它的驱动程序。如果找到匹配，将调用驱动程序的探测函数来初始化设备。

通用驱动模型使得内核具有灵性和扩展性。可以在不修改内核的情况下添加新的设备和驱动程序。这对于 Linux 支持的庞大生态系统非常重要。

### 设备表示

驱动模型具有一个特殊结构来表示所有总线的通用设备属性。该结构嵌入在特定的线数据结构中，其（简化）定义如下：
