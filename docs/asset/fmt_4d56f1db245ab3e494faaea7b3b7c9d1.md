
```c
static int led_probe(struct usb_interface *intf, const struct usb_device_id *id) {
    struct usb_led *dev;
    struct endpoint_descriptor *endpoint;
    struct usb_interface *altsetting = intf;
    struct usb_device *udev = usb_to_dev(intf);
    struct usb_host *host;
    int i, ep_in, ep_out;
    int retval, size;

    dev_info(&intf->dev, "led_probe() is called.\n");
    dev = kzalloc(sizeof(struct usb_led), GFP_KERNEL);
    if (!dev)
        return -ENOMEM;

dev->udev = udev;
    dev->intf = intf;

    /* 获取端点 */
    for (i = 0; i < altsetting->cur_desc->desc_endpoints; i++) {
        endpoint = &altsetting->cur_desc->b_endpoint[i];
        if (usb_endpoint_direction(endpoint->bm_attributes) == USB_ENDPOINT_IN) {
            dev->interrupt_in_endpoint = endpoint;
            ep_in = endpoint->b_EndpointAddress;
        } else if (usb_endpoint_direction(endpoint->bm_attributes) == USB_ENDPOINT_OUT) {
            dev->interrupt_out_endpoint = endpoint;
            ep_out = endpoint->b_EndpointAddress;
        }
    }

    if (!dev->interrupt_in_endpoint || !dev->interrupt_out_endpoint) {
        dev_err(&intf->dev, "could not find required endpoints\n");
        retval = -ENOENT;
        goto error_free;
    }

    dev->ep_in = ep_in;
    dev->ep_out = ep_out;

    /* 分配 URB */
    dev->interrupt_in_urb = usb_alloc_urb(0, GFP_KERNEL);
    if (!dev->interrupt_in_urb) {
        retval = -ENOMEM;
        goto error_free;
    }
    dev->interrupt_out_urb = usb_alloc_urb(0, GFP_KERNEL);
    if (!dev->interrupt_out_urb) {
        retval = -ENOMEM;
        goto error_free_in;
    }

    /* 初始化 URB */
    usb_fill_int_urb(dev->interrupt_in_urb, udev, ep_in,
        dev->ibuffer, 64, led_urb_in_callback, dev, 0);
    usb_fill_int_urb(dev->interrupt_out_urb, udev, ep_out,
        dev->ibuffer, 64, led_urb_out_callback, dev, 0);

    usb_set_intdata(intf, dev);
    retval = device_create_file(&intf->dev, &dev->led);
    if (retval)
        goto error_create_file;
    }

    dev_info(&intf->dev, "USB LED driver initialized\n");
    return 0;

error_create_file:
    usb_free_urb(dev->interrupt_out_urb);
error_free_in:
    usb_free_urb(dev->interrupt_in_urb);
error_free:
    kfree(dev);
    return retval;
}
```

# USB 设备驱动程序

## 第13章

开关已开启。

释放 PIC32MX Curiosity 开发板上的 S1 开关并获取开关状态：

```
root@raspberry:/sys/usb/bus/devices/1-1.3:1.0# echo 0 > led
usbled 1-1.3:1.0: led_store() function is called.
usb 1-1.3: read status
usb 1.1.3: led_urb_out_callback() function is called.
usb 1-1.3: led_urb_in_callback() function is called.
switch is OFF.
```

移除模块：

```
root@raspberry:/home# rmod usb_urb_int_led.ko
usbcore: deregistering interfacing driver usbled
usb 1-1.3: led_urb_in_callback() function is called.
switch is OFF.
usb 1-1.3: Couldn't submit interrupt_in_urb -1
usbled 1-1.3:1.0: USB led now disconnected
```

### 实验 13.4：“I2C 转 USB 多显示 LED 模块”

在本书的实验 6.2 中，你实现了一个 I2C Linux 驱动来控制 LTC3206 多显示 LED 控制器（https://www.analog.com/en/products/ltc3206.html）。在实验 13.4 中，你将编写一个 USB 驱动，使用 Linux I2C 工具从用户空间控制 LTC3206；为了完成此任务，你需要在你的 Linux USB 驱动创建一个新的 I2C 适配器。

驱动模型是递归的。在下面的图中，你可以看到通过集成了 USB 转 I2C 转换器的 PCI 板控制 I2C 设备所需的所有驱动。创建此递归驱动模型的主要步骤如下：

- 首先，你必须开发一个 PCI 设备驱动，它将创建一个 USB 适配器（PCI 设备驱动是 USB 适配器的父节点）。
- 第二，你必须开发一个 USB 设备驱动，通过 USB 核心将 USB 数据发送到 USB 适配器。该 USB 设备驱动还将创建一个 I2C 适配器驱动（USB 设备驱动是 I2C 适配器的父节点）。
- 最后，你将创建一个 I2C 设备驱动，它通过 I2C 核心向 I2C 适配器发送数据，并创建一个 `file_operations` 结构来定义当 Linux 用户读写字符设备时调用的驱动函数。

这种递归模型将在之前提到的三个驱动程序中的被简化，你只需要执行这三个步骤中的第二步。在该驱动程序中，主机与设备之间的通信是通过使用中断 OUT URB 异步完成的。

在开发开发 Linux 驱动程序之前，你必须首先向之前的项目添加新的 Harmony 配置。你必须在 Harmony Framework 配置内部选择 I2C Drivers 选项：

![](img/eebd1e8dc8b2bd72a2e2142ef70e7c33_618_1.png)

在 MPLAB Harmony Configurator 的引脚表（Pin Table）中，激活 I2C1 控制器的 SCL1 和 SDA1 引脚：

| Output - USB_I2C (Clean, Build, ...) | MPLAB® Harmony Configurator |
|---|---|
| Output: QFN | |
