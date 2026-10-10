
*其中 `usb_dev` 是关联的 `usb_device` 结构体的指针，`endpointAddress` 是分配的端点地址，介于 1 和 127 之间。例如，要创建 OUT 方向的批量管道，请调用 `usb_sndbulkpipe()`。对于 IN 方向的控制管道，请调用 `usb_rcvctrlpipe()`。*

提到 URB 时，它通常由关联管道的传输类型来限定。例如，如果 URB 附加到批量管道，则称为*批量 URB*。

## 描述符结构

USB 规范定义了一系列*描述符*以保存设备信息。Linux-USB 核心定义了与每个描述符对应的数据结构。描述符有四种类型：

- **设备描述符**包含设备的通用信息，例如产品 ID 和供应商 ID。`usb_device_descriptor` 是对应设备描述符的结构。
- **配置描述符**用于描述不同的配置模式，例如总线供电和自供电操作。`usb_config_descriptor` 是与配置描述符关联的数据结构。
- **接口描述符**允许 USB 设备支持多个功能。`usb_interface_descriptor` 定义接口描述符。
- **端点描述符**携带与设备最终端点关联的信息。`usb_endpoint_descriptor` 就是相关的结构。

这些描述符格式在 USB 规范的第 9 章中定义，而相应的结构定义在 `include/linux/usb/ch9.h` 中。**清单 11.1** 展示了描述符的层次拓扑，并打印出与 USB 设备关联的所有端点地址。为此，它遍历了由前述四种类型描述符组成的树。**清单 11.1** 为 USB 光驱生成的输出如下：

```
Endpoint Address = 1

Endpoint Address = 82

Endpoint Address = 83
```

第一个地址属于批量 `IN` 端点，第二个地址由批量 `OUT` 端点拥有，第三个地址指向中断 `IN` 端点。

还有更多与 USB 客户端驱动程序关联的数据结构，例如 `usb_device_id`、`usb_driver` 和 `usb_class_driver`。当我们进行“**设备示例：遥测卡**.”一节的实践开发时，将会遇到它们。

### 清单 11.1. 打印设备上的所有 USB 端点地址

![](img/07cc6f9c8c74622020874f66bfb53dc4_301_0.png)

```c
/* ... */
/* USB device */
struct usb_device *udevce;
/* ... */
struct usb_device_descriptor u_d_desc = udevice->descriptor;
/* Device's active configuration */
struct usb_host_config *uconfig;
struct usb_config_descriptor u_c_desc;
/* Interfaces in the active configuration */
struct usb_interface *uinterface;
/* Alternate Setting for this interface */
struct usb_host_interface *ualtsetting;
struct usb_interface_descriptor u_i_desc;
/* Endpoints for this altsetting */
struct usb_host_endpoint *uendpoint;
struct usb_endpoint_descriptor u_e_desc;
uconfig = udevice->actconfig;
u_c_desc = uconfig->desc;
for (i = 0; i < u_c_desc->bNumInterfaces; i++) {
    uinterface = udevice->actconfig->interface[i];
    for (j = 0; j < uinterface->num_altsetting; j++) {
        ualtsetting = &uinterface->altsetting[j];
        u_i_desc = ualtsetting->desc;
        for (k = 0; k < u_i_desc->bNumEndpoints; k++) {
            uendpoint = &ualtsetting->endpoint[k];
            u_e_desc = uendpoint->desc;
            printk("Endpoint Address = %d\n",
                   u_e_desc->EndpointAddress);
        }
    }
}
/* ... */
```

![](img/07cc6f9c8c74622020874f66bfb53dc4_302_0.png)

## 枚举

热插拔 USB 设备的生命周期始于一个称为枚举的过程，在此过程中，主机了解设备的能力并对其进行配置。集线器驱动程序是 Linux-USB 子系统中负责枚举的组件。让我们看一下当您将 USB 闪存驱动器插入主机计算机时，实现设备枚举的步骤序列：

1. 根集线器报告端口电流因设备连接而变化。集线器驱动程序检测到此状态变化，在 Linux-USB 术语中称为 `USB_PORT_STAT_C_CONNECTION`，并唤醒 `khubd`。
2. `khubd` 破译发生状态变化的 USB 端口的身份。在这种情况下，它是您插入闪存驱动器的端口。
3. 接下来，`khubd` 在 1 和 127 之间选择一个设备地址，并使用附加到端点 0 的控制 URB 将其分配给闪存驱动器的批量端点。
4. `khubd` 使用上述附加到端点 0 的控制 URB 从闪存驱动器获取设备描述符。然后，它请求设备的配置描述符并选择一个合适的配置。对于闪存驱动器，只提供了一个配置描述符。
5. `khubd` 请求 USB 核心将匹配的客户端驱动程序绑定到插入的设备。

当枚举完成且设备已绑定到驱动程序时，`khubd` 调用关联客户端驱动程序的 `probe()` 方法。在这种情况下，`khubd` 调用在 `drivers/usb/storage/usb.c` 中定义的 `storage_probe()`。从这一点开始，大容量存储驱动程序负责正常的设备操作。

## 设备示例：遥测卡

既然你已经了解了 Linux-USB 的基础知识，是时候来看看一个示例设备了。考虑一个配备遥测卡的系统，该卡通过内部 USB 连接到处理器，如图 11.2 中的总线 2 所示。该卡从远程设备获取数据，并通过 USB 将其传输到处理器。一个遥测卡的例子是医疗级主板，它用于监控或编程植入式设备。

假设我们的示例遥测卡具有以下端点，其语义如表 11.2 中所述：

- 连接到板载配置寄存器的控制端点
- 将卡片收集的远程遥测信息传递给处理器的批量 IN 端点
- 以相反方向传输数据的批量 OUT 端点

### 表 11.2. 遥测卡中的寄存器空间

| 寄存器 | 关联端点 |
| :--- | :--- |
| 遥测配置寄存器 | 控制端点 0（寄存器偏移 0x8）。 |
| 遥测数据输入寄存器 | 批量 IN 端点。端点地址在设备枚举过程中分配。 |
| 遥测数据输出寄存器 | 批量 OUT 端点。端点地址在设备枚举过程中分配。 |

让我们构建一个针对此卡片的最小驱动程序，该驱动程序部分基于 USB 骨架驱动程序，`drivers/usb/usb-skeleton.c`。

由于 PCMCIA、PCI 和 USB 设备具有相似的特性，例如对热插拔的支持，这些子系统中的一些驱动程序方法和数据结构彼此相似。这对于负责初始化和探测的部分尤其如此。随着我们深入研究遥测驱动程序，并注意到我们在第 10 章中学到的 PCI 驱动程序中的相似之处，我们将暂停并加以记录。

### 初始化与探测

与 PCI 和 PCMCIA 驱动程序类似，USB 驱动程序具有支持热插拔的 `probe()`/`disconnect()` [2] 方法，以及一个包含其所支持设备标识的表。USB 设备由定义在 `include/linux/mod_devicetable.h` 中的 `usb_device_id` 结构体识别。你可能记得，前一章中定义在同一头文件中的 `pci_device_id` 结构体用于识别 PCI 设备。

> [2] `disconnect()` 在 PCI 和 PCMCIA 术语中称为 `remove()`。

```c
struct usb_device_id {
    /* ... */
    __u16 idVendor;       /* Vendor ID */
    __u16 idProduct;      /* Device ID */
    /* ... */
```
