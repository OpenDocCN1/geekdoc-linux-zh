
C:* #Ifs= 1 Cfg#= 1 Atr=80 MxPwr=  0mA

I*:  If#= 0 Alt= 0 #EPs= 2 Cls=08(stor.) Sub=06 Prot=50 Driver=usb-storage

T:  Bus=04 Lev=02 Prnt=02 Port=01 Cnt=02 Dev#=  5 Spd=480 MxCh=  0

N:  Device=sr0(CDROM)

D:  Ver= 2.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS=64 #Cfgs=  1

P:  Vendor=0bf6 ProdID=a002 Rev= 3.00

S:  Manufacturer=Addonics

S:  Product=USB to IDE Cable

S:  SerialNumber=1301011002A9AF9

C:* #Ifs= 1 Cfg#= 2 Atr=c0 MxPwr= 98mA

I*:  If#= 0 Alt= 0 #EPs= 3 Cls=08(stor.) Sub=06 Prot=50 Driver=usb-storage

E:  Ad=01(O) Atr=02(Bulk) MxPS= 512 Ivl=125us

E:  Ad=82(I) Atr=02(Bulk) MxPS= 512 Ivl=0ms

E:  Ad=83(I) Atr=03(Int.) MxPS=   2 Ivl=32ms

T:  Bus=04 Lev=02 Prnt=02 Port=02 Cnt=03 Dev#=  4 Spd=480 MxCh= 0

N:  Device=sdb(Disk)

D:  Ver= 2.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS= 64 #Cfg= 1

P:  Vendor=0bc2 ProdID=0501 Rev= 0.01

S:  Manufacturer=Seagate

S:  Product=USB Mass Storage

S:  SerialNumber=000000062459

C:* #Ifs= 1 Cfg#= 1 Atr=c0 MxPwr= 0mA

I*:  If#= 0 Alt= 0 #EPs= 2 Cls=08(stor.) Sub=06 Prot=50 Driver=usb-storage

E:  Ad=02(O) Atr=02(Bulk) MxPS= 512 Ivl=0ms

E:  Ad=88(I) Atr=02(Bulk) MxPS= 512 Ivl=0ms

...
```

如你所见，SCSI 子系统将 `sda` 分配给闪存盘，`sr0` 分配给 CD-ROM，`sdb` 分配给硬盘。用户空间应用程序通过操作这些节点与相应设备通信。如你在第 4 章中所学到的，随着 `udev` 的出现，然而，你有一个选择，可以创建更高级别的抽象来标识每个设备，而无需依赖 SCSI 子系统分配的 `/dev` 名称的身份。

## USB-串口

USB 转串口转换器通过 USB 为你的计算机提供串行端口功能。例如，你可以使用 USB 转串口转换器，从没有串行端口的开发笔记本电脑上的嵌入式设备获取串行调试控制台。

在第 6 章“串行驱动”中，你学习了内核分层串行架构的好处。图 11.5 说明了 USB-串口层如何融入内核的串行框架。

![](img/07cc6f9c8c74622020874f66bfb53dc4_320_0.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_320_1.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_321_0.png)

USB-串口驱动与其他 USB 客户端驱动类似，除了它还利用了 USB-串口核心服务，而不仅仅是 USB 核心。USB-串口核心提供以下内容：

- 一个 tty 驱动，将低层级的 USB 转串口驱动与更高层级的串行层（如行规程）隔离开来。
- 通用的 `probe()` 和 `disconnect()` 例程，供各个 USB-串口驱动使用。
- 用于从用户空间访问 USB-串口端口的设备节点。应用程序通过 `/dev/ttyUSBX` 操作 USB-串口端口，其中 X 是串口号。如 `minicom` 这样的终端仿真器和如 `PPP` 这样的协议可以在这些接口上无改动地运行。

低层级的 USB 转串口转换器驱动本质上执行以下操作：

1. 使用 `usb_serial_register()` 向 USB-串口核心注册一个 `usb_serial_driver` 结构体。作为 `usb_serial_driver` 一部分提供的入口点构成了驱动的核心。
2. 填充一个 `usb_driver` 结构体，并使用 `usb_register()` 将其注册到 USB 核心。这与示例遥测驱动所做的类似，只不过串口转换器驱动可以依赖 USB-串口核心提供的通用 `probe()` 和 `disconnect()` 例程。

### 列表 11.7. FTDI 驱动片段

```c
/* The usb_driver structure */

static struct usb_driver ftdi_driver = {
    .name           = "ftdi_sio",     /* Name */
    .probe          = usb_serial_probe, /* Provided by the USB-Serial core */
    .disconnect     = usb_serial_disconnect, /* Provided by the USB-Serial core */
    .id_table       = id_table_combined, /* List of supported devices built around the FTDI chip */
    .no_dynamic_id = 1,              /* Supported ids cannot be added dynamically */
};

/* The usb_serial_driver structure */

static struct usb_serial_driver ftdi_sio_device = {
    /* ... */
    .num_ports        = 1,
    .probe            = ftdi_sio_probe,
    .port_probe       = ftdi_sio_port_probe,
    .port_remove      = ftdi_sio_port_remove,
    .open             = ftdi_open,
    .close            = ftdi_close,
    .throttle         = ftdi_throttle,
    .unthrottle       = ftdi_unthrottle,
    .write            = ftdi_write,
    .write_room       = ftdi_write_room,
    .chars_in_buffer  = ftdi_chars_in_buffer,
    .read_bulk_callback = ftdi_read_bulk_callback,
    .write_bulk_callback = ftdi_write_bulk_callback,
    /* ... */
};

/* Driver Initialization */

static int __init ftdi_init(void)
{
    /* ... */
    /* Register with the USB-Serial core */
    retval = usb_serial_register(&ftdi_sio_device);
    /* ... */
    /* Register with the USB core */
    retval = usb_register(&ftdi_driver);
    /* ... */
}
```
