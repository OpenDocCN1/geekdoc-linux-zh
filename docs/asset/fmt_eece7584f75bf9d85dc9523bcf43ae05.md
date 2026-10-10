
### 将各部分串联起来

正如你在图 9.3 中看到的，PCMCIA 层由各种组件组成。组件之间的数据流路径有时可能会变得复杂。让我们追踪代码路径，从你插入 PCMCIA 卡开始，直到应用程序开始向卡传输数据。假设在一个具有 82365 兼容 PCMCIA 宿主控制器的笔记本电脑上插入了一张思科 Aironet PCMCIA 卡：

1. PCMCIA 宿主控制器驱动程序（`drivers/pcmcia/yenta_socket.c`）通过其中断服务例程检测到插入事件，并使用适当的数据结构对此进行记录。
2. 作为 Card Services 一部分的 `pcicard` 内核线程（`drivers/pcmcia/cs.c`）在一个等待队列上休眠，直到宿主控制器驱动程序在第 1 步检测到卡插入时将其唤醒。
3. Card Services 将插入事件分发给 Driver Services（`drivers/pcmcia/ds.c`）。这会触发 Driver Services 在初始化期间注册的事件处理程序执行。
4. Driver Services 验证卡的 CIS 空间，确定有关插入设备的信息，例如制造商 ID 和卡 ID，并将该设备注册到内核中。随后加载相应的客户端设备驱动程序（`drivers/net/wireless/airo_cs.c`）。回顾我们之前关于 `MODULE_DEVICE_TABLE()` 的讨论，以了解这是如何实现的。
5. 在第 4 步中加载的客户端驱动程序（`airo_cs.c`）使用 `pcmcia_register_driver()` 进行初始化和注册，如列表 9.1 所示。此注册接口内部将设备的总线类型设置为 `pcmcia_bus_type`。由 Driver Services（`ds.c`）定义的 PCMCIA 总线操作，如 `probe()` 和 `remove()`，也在内部进行了注册。
6. 内核调用 Driver Services 在第 5 步中注册的总线 `probe()` 操作。这进而调用属于匹配客户端驱动程序（`airo_probe()`）的 `probe()` 方法，该也是在第 5 步中注册的。客户端 `probe()` 例程填充设置（例如 I/O 窗口和中断线），并配置通用的芯片组特定驱动程序（`drivers/net/wireless/airo.c`），如列表 9.2 所示。
7. 芯片组驱动程序（`airo.c`）创建一个网络接口（`ethX`），并负责从此刻起的常规操作。该驱动程序负责处理由卡响应数据报接收和传输完成而生成中断。设备的外形（例如，它是 PCMCIA 卡还是 PCI 卡）对于芯片组驱动程序以及通过 `ethX` 运行的应用程序都是透明的。

### PCMCIA 存储

当今的 PCMCIA/CF 存储支持千兆字节级别的数据密度。存储卡有不同的形式：

- 微型 IDE 磁盘驱动器或微驱动器。这些是机械硬盘的微型版本，使用磁性介质。其数据传输速率通常高于固态内存设备，但在数据传输之前，IDE 驱动器具有启动和寻道延迟。IDE Card Services 驱动程序 `ide_cs` 与传统 IDE 驱动程序配合使用，用于与这类存储卡通信。
- 模拟 IDE 的固态存储卡。这类卡没有运动部件，通常基于闪存，由于 IDE 模拟，对操作系统是透明的。由于这些驱动器实际上是基于 IDE 的，可以使用相同的 IDE Card Services 驱动程序（`ide_cs`）与其通信。
- 使用闪存但没有 IDE 模拟的存储卡。`memory_cs` Card Services 驱动程序为这类卡提供块和字符接口。块接口用于在卡内存上放置文件系统，而字符接口用于访问原始数据。你还可以使用 `memory_cs` 读取任何 PCMCIA 卡的属性内存空间。

### 串行 PCMCIA

许多网络技术，如通用分组无线业务（GPRS）、全球移动通信系统（GSM）、全球定位系统（GPS）和蓝牙，使用串行传输机制与主机系统通信。在本节中，让我们找出 PCMCIA 层如何处理具有此类技术的卡。请注意，本节仅旨在帮助你理解具有 PCMCIA/CF 外形尺寸的 GPRS、GSM 和蓝牙卡的总线接口部分。这些技术本身在第 16 章“无线 Linux”中详细讨论。

通用的串行 Card Services 驱动程序 `serial_cs` 允许操作系统的其余部分将 PCMCIA/CF 卡视为串行设备。第一个未使用的串行设备 `/dev/ttySX` 分配给该卡。因此，`serial_cs` 在 GPRS、GSM 和 GPS 卡上模拟串行端口。它还允许使用串行传输的蓝牙 PCMCIA/CF 卡将主机控制接口（HCI）数据包传输到蓝牙协议层。

图 9.5 说明了实现不同网络技术的内核模块如何与 `serial_cs` 交互以与其各自的卡通信。

![](img/07cc6f9c8c74622020874f66bfb53dc4_256_0.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_257_0.png)

*点对点协议*（PPP）允许 TCP/IP 等网络协议在串行链路上运行。在图 9.5 的上下文中，PPP 使 TCP/IP 应用程序能够运行在 GPRS 和 GSM 拨号上。PPP 守护进程 `pppd` 附着在由 `serial_cs` 模拟的虚拟串行端口上。为了 `pppd` 正常工作，必须加载 PPP 内核模块——`ppp_generic`、`ppp_async` 和 `slhc`。按如下方式调用 `pppd`：

```bash
pppd ttySx call connection-script
```
