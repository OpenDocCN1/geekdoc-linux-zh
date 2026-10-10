

Bus=03 Lev=01 Prnt=01 Port=01 Cnt=01 Dev#= 5 Spd=12 MxCh= 0
Ver=1.10 Cls=00(>ifc) Sub=00 Prot=00 MxPS=64 #Cfgs= 1
Vendor=04b0 ProdID=0205 Rev=1.00
Manufacturer=Nikon
Product=Nikon Dsc E5200
SerialNumber=2507597
#Ifs= 1 Cfg#= 1 Atr=c0 MxPwr= 2mA
I: If#= 0 Alt= 0 #EPS= 2 Cls=08(stor.) Sub=06 Prot=50
 Driver=usb-storage
Ad=01(O) Attr=02(Bulk) MxPS= 64 Ivl=0ms
Ad=82(I) Attr=02(Bulk) MxPS= 64 Ivl=0ms

Bus=01 Lev=01 Prnt=01 Port=02 Cnt=01 Dev#= 12 Spd=480 MxCh= 0
Ver=2.00 Cls=00(>ifc) Sub=00 Prot=00 MxPS=64 #Cfgs= 1
Vendor=0bc2 ProdID=0501 Rev=0.01
Manufacturer=Seagate
Product=USB Mass Storage
SerialNumber=00000062459
#Ifs= 1 Cfg#= 1 Atr=e00 MxPwr=0mA
I: If#= 0 Alt= 0 #EPS= 2 Cls=08(stor.) Sub=06 Prot=50
 Driver=usb-storage
Ad=02(0) Attr=02(Bulk) MxPS= 512 Ivl=0ms
Ad=88(I) Attr=02(Bulk) MxPS= 512 Ivl=0ms

查看上述输出中的 **T:** 行，它们显示了拓扑结构。如预期那样，硬盘已连接到 **EHCI** 总线（**bus1**），而相机则出现在 **UHCI** 总线（**bus3**）上。这是当前 **usbfs** 树的外观：

# 代码视图：

```bash
ls -lR /proc/bus/usb
/proc/bus/usb:
total 0
dr-xr-xr-x 2 root root 0 Dec 2 12:44 001
dr-xr-xr-x 2 root root 0 Dec 2 12:44 002
dr-xr-xr-x 2 root root 0 Dec 2 12:44 003
dr-xr-xr-x 2 root root 0 Dec 2 12:44 004
-r--r----- 1 root root 0 Dec 2 19:51 devices

/proc/bus/usb/001:
total 0
-rw-r----- 1 root root 43 Dec 2 12:44 001
-rw-r----- 1 root root 50 Dec 2 19:51 007

/proc/bus/usb/002:
total 0
-rw-r----- 1 root root 43 Dec 2 12:44 001

/proc/bus/usb/003:
total 0
-rw-r----- 1 root root 43 Dec 2 12:44 001
-rw-r----- 1 root root 50 Dec 2 19:16 003

/proc/bus/usb/004:
total 0
-rw-r--r-- 1 root root 43 Dec 2 12:44 001
```

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_0.png)

**EHCI**: **bus1**

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_1.png)

高速硬盘

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_2.png)

**UHCI**: **bus2**

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_3.png)

**UHCI**: **bus3**

![](img/07cc6f9c8c74622020874f66bfb53dc4_528_4.png)

全速相机

与插入设备相对应的 **usbfs** 文件包含相关的 **USB** 设备描述符和配置描述符。在上面的示例中，读取 `/proc/bus/usb/003/003` 可以获取相机的描述符信息，读取 `/proc/bus/usb/001/007` 可以获取与硬盘相关的描述符。然而，管理 **usbfs** 文件并不简单，因为设备拔出后，设备文件名会被重用。解决方案是使用 **libusb** 库，该库在底层使用 **usbfs**。与直接操作 **usbfs** 相比，使用 **libusb** 还有另一个好处：你的驱动程序很可能在其他支持该库的操作系统上无需修改即可运行。如果你的发行版没有附带 **libusb**，可以从 [http://libusb.sourceforge.net/](http://libusb.sourceforge.net/) 下载其源代码。该库提供的 **USB** 访问功能完整列表可以在 **libusb** 源代码的 `doc/` 目录下找到。

**Listing 19.6** 实现了一个使用常用 **libusb** 编程模板的数码相机用户空间骨架驱动程序。相机的供应商 ID (**0x04b0**) 和设备 ID (**0x0205**) 是从之前显示的 `/proc/bus/usb/devices` 输出中获取的。

# Listing 19.6. 使用 libusb 的用户空间 USB 骨架驱动程序

```c
#include <usb.h>

/* From the libusb package */
#define DIGICAM_VENDOR_ID 0x04b0 /* From /proc/bus/usb/devices */
#define DIGICAM_PRODUCT_ID 0x0205 /* From /proc/bus/usb/devices */

int main(int argc, char *argv[]) {
    struct usb_dev_handle *mydevice_handle;
    struct usb_bus *usb_bus;
    struct usb_device *mydevice;

    /* Initialize libusb */
    usb_init();
    usb_find_buses();
    usb_find_devices();

    /* Walk the bus */
    for (usb_bus = usb_buses; usb_bus; usb_bus = usb_bus->next) {
        for (mydevice = usb_bus->devices; mydevice;
             mydevice = mydevice->next) {
            if ((mydevice->descriptor.idVendor == DIGICAM_VENDOR_ID) &&
                (mydevice->descriptor.idProduct == DIGICAM_PRODUCT_ID)) {

                /* Open the device */
                mydevice_handle = usb_open(mydevice);

                /* Send commands to the camera. This is the heart of the
                   driver. Getting information about the USB control
                   messages to which your device responds is often a
                   challenge since many vendors do not readily divulge
                   hardware details */
                usb_control_msg(mydevice_handle, ...);
                /* ... */

                /* Close the device */
                usb_close(mydevice_handle);
            }
        }
    }
}
```

# 用户模式 I²C

在第 8 章“**I²C（集成电路间互连）协议**”中，你学习了如何为 **I²C** 设备开发内核模式驱动程序；但有时，当需要支持大量慢速 **I²C** 设备时，从用户空间驱动这些设备是合理的。`i2c-dev` 模块允许开发用户模式 **I²C/SMBus** 设备驱动程序。用户空间代码可以通过设备节点访问 **I²C** 主机适配器。为了操作第 $n$ 个适配器，打开 `/dev/i2c-n`。一旦你获得了与主机适配器设备节点关联的文件描述符，你就可以通过 `ioctl` 命令它连接到附加到它的特定从设备。然后，你可以使用一系列数据访问例程的服务与从设备交换数据。

**Listing 19.7** 是一个简单的用户模式驱动程序，用于在用户空间对 **I²C EEPROM** 执行常见操作。该 **EEPROM** 与第 8 章中讨论的是同一个，它有两个存储库，每个存储库对应一个从地址。该列表使用来自 `i2c-dev.h` 的内联函数来操作与存储库关联的设备节点。从可下载的 [www.im-sensors.org](https://www.im-sensors.org) 的 **Im-sensors** 软件包（也在第 8 章中讨论过）中获取此头文件。该文件包含了第 8 章表 8.1 中列出的所有内核空间 **I²C** 访问函数的用户空间等效项。

# Listing 19.7. 用户空间 I²C/SMBus 驱动程序

```c
#include <linux/i2c.h>
#include <linux/i2c-dev.h>

/* Bus addresses of the memory banks */
#define SLAVE_ADDR1 0x60
#define SLAVE_ADDR2 0x61

int main(int argc, char *argv[])
{
    /* Open the host adapter */
    if ((smbus_fp = open("/dev/i2c-0", O_RDWR)) < 0) {
        exit(1);
    }

    /* Connect to the first bank */
    if (ioctl(smbus_fp, I2C_SLAVE, EEPROM_SLAVE_ADDR1) < 0) {
        exit(1);
    }

    /* ... */

    /* Dump data from the device */
    for (reg=0; reg < length; reg++) {
        /* See i2c-dev.h from the Im-sensors package for the
           implementation of the following inline function */
        res = i2c_smbus_read_byte_data(smbus_fp, (unsigned char) reg);
        if (res < 0) {
            exit(1);
        }

        /* Dump data */
        /* ... */
    }

    /* Switch to bank 2 */
    if (ioctl(smbus_fp, I2C_SLAVE, SLAVE_ADDR2) < 0) {
        exit(1);
    }

    /* Clear bank 2 */
    for (reg=0; reg < length; reg+=2){
        i2c_smbus_write_word_data(smbus_fp, (unsigned char) reg, 0x0);
    }

    /* ... */

    close(smbus_fp);
}
```

# UIO

从 **2.6.23** 版本开始，内核包含一个名为 **UIO**（*用户空间 I/O*）的子系统，它简化了一些用户空间驱动程序的实现。**UIO** 的目的是允许开发用于中断处理等任务的最小化内核驱动程序，并将大多数设备 **I/O** 逻辑推送到用户空间。**UIO** 对于某些类别的工业 **I/O** 卡特别相关。

在 `drivers/uio/` 内部查找 **UIO** 源代码。用户指南位于 `Documentation/DocBook/uio-howto.tmpl` 下。探索 **UIO** 超出了本章的范围。

# 查看源代码

Linux 调度程序位于 `kernel/sched.c`。SCSI 通用实现位于 `drivers/scsi/sg.c`，而 `drivers/usb/core/devio.c` 负责支持用户空间 **USB** 驱动程序。启用用户模式 **I²C** 编程支持的 `i2c-dev` 驱动程序位于 `drivers/i2c/i2c-dev.c`。

表 19.1 包含本章使用的主要数据结构，表 19.2 列出了用于辅助用户模式驱动程序开发的函数。

**表 19.1. 数据结构摘要**

| 数据结构 | 位置 (用户空间) | 描述 |
|---|---|---|
| *sched_param* | */usr/include/bits/sched.h* | 与调度优先级相关的信息。 |
| *fb_var_screeninfo* | */usr/include/linux/fb.h* | 用于操作帧缓冲区。包含可变屏幕信息，如分辨率和像素时钟。更多细节请参见第 11 章。 |
| *sg_io_hdr_t* | */usr/include/scsi/sg.h* | 用于管理 SCSI 通用设备的信息。 |
| *usb_dev_handle* | libusb 软件包中的头文件。 | 用于从用户空间操作 USB 设备的结构。 |
| *usb_bus* | libusb 软件包中的头文件。 | 用于从用户空间操作 USB 设备的结构。 |

**表 19.2. 用户空间函数摘要**

| 用户空间函数 | 描述 |
|---|---|
| *sched_getparam()* | 获取与给定进程相关的调度参数 |
| *sched_setscheduler()* | 设置与给定进程相关的调度参数 |
| *mlockall()* | 将调用进程的页面锁定在内存中，从而避免缺页中断 |
| *ioperm()* | 控制对前 0x3FF 个 I/O 端口的访问权限 |
| *iopl()* | 控制对所有 I/O 端口的访问权限 |
| *outb() / outw() / outl()* | 向指定端口输出字节/字/长整型 |
| *inb() / inw() / inl()* | 从指定端口输入字节/字/长整型 |
| *mmap()* | 将文件或设备地址区域与用户虚拟内存块关联 |
| *msync()* | 刷新对 mmap 内存区域所做的更改 |
| *munmap()* | mmap() 的逆操作 |
| *usb_init()* | libusb 库提供的用于帮助操作 usbfs 的函数 |
| *usb_find_buses()* | libusb 库提供的用于帮助操作 usbfs 的函数 |

