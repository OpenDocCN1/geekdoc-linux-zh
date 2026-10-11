
```c
static int led_probe(struct usb_interface *intf, const struct usb_device_id *id) {
    struct usb_device *udev = interface_to_usbdev(intf);

    /* 获取 USB 接口的当前备设置 */
    struct usb_host_interface *altsetting = intf->cur_altsetting;
    struct usb_endpoint_descriptor *endpoint;
    struct usb_led *dev = NULL;
    int ep;
    int ep_in, ep_out;
    int size;

/*
* 找到最后一个中断端点描述符
* 以检查其编号和大小。
* 仅用于教学目的
*/
usb_fnd_last_int_out_endpoint(altsetting, &endpoint);

/* 获取端点编号 */
ep = usb_endpoint_num(endpoint); /* * 值从 0 到 15，此处为 1 */
size = usb_endpoint_max(endpoint);
/* 验证端点及其大小 */
if (size < 0) {
    dev_info(&intf->dev, "invalid size (%d)", size);
    return -ENODEV;
}
dev_info(&intf->dev, "endpoint size is (%d)", size);
dev_info(&intf->dev, "endpoint number is (%d)", ep);

/* 获取 Endpoint 1 的两个地址 (IN 和 OUT) */
ep_in = altsetting->endpoint[0].desc.bEndpointAddress;
ep_out = altsetting->endpoint[1].desc.bEndpointAddress;

/* 将值存储在数据中 */
dev->dev_in = ep_in;
dev->dev_out = ep_out;
dev->udev = usb_get_dev(udev);
dev->intf = intf;

/* 分配 interrupt_out_urb */
dev->interrupt_out_urb = usb_alloc_urb(0, GFP_KERNEL);
/* 初始化 interrupt_out_urb */
usb_fill_urb(dev->interrupt_out_urb,
    dev->udev,
    usb_sndpipe(dev->udev, ep_out),
    (void *)&dev->irq_data,
    1,
    led_out_callback, dev, 1);

/* 分配 interrupt_in_urb */
dev->interrupt_in_urb = usb_alloc_urb(0, GFP_KERNEL);
if (!dev->interrupt_in_urb) {
    goto error_out;
}
/* 初始化 interrupt_in_urb */
usb_fill_urb(dev->interrupt_in_urb,
    dev->udev,
    usb_rcvpipe(dev->udev, ep_in),
    (void *)&dev->buffer,
    1,
    led_in_callback, dev, 1);

/* 将设备数据附加接口 */
usb_set_intfdata(intf, dev);

/* 创建与用户空间交互的 sysfs 条目 */
device_create_file(&intf->dev, &dev_attr);

/* 提交中断 URB */
usb_submit(dev->interrupt_in_urb, GFP_KERNEL);

return 0;
```

### 5. 写 `led_store()` 函数
每当用户应用程序写入 USB 设备下的 sysfs 条目 (`sys/bus/usb/devices/1-1.3:led`) 时，就会调用驱动程序的 `led_store()` 函数。通过 `usb_getfdata()` 恢复与 USB 设备关联的 `led_store` 结构。写入 sysfs 条目的命令存储在 `irq_data` 变量中。最后，通过 `usb_submit_urb()` 函数通过 USB 查看命令值。

此处是 `led_store()` 例程的提取：

```c
static ssize_t led_store(struct device *dev, struct device_attribute *attr,
const char *buf, size_t count)
{
    struct usb_interface *intf = to_usb_interface(dev);
    struct usb_led *led = usb_getintfdata(intf);
    u8 val;
    int retval;

    /* 将字符数组转换为 u8 值 */
    kstrtoub(buf, 10, &val);

    led->irq_data = val;

    /* 发送数据 */
    retval = usb_submit_urb(led->interrupt_out_urb, GFP_KERNEL);

    return count;
}
static DEVICE_ATTR_RW(led);
```

### 6. 创建 OUT 和 IN URB 的回调
中断 OUT 回调检查 URB 状态并返回。中断 IN 回调检查 URB 状态，然后使用 `buffer` 获取 PIC32MX 板上 S1 开关的状态，最后重新提交中断 URB。

```c
static void led_urb_out_callback(struct urb *urb)
{
    struct usb_led *dev;
    dev = urb->context;
    /* 同步/异步取消不是错误 */
    if (urb->status) {
        if ((urb->status == -ENOTENT ||
            urb->status == -ECONRESET ||
            urb->status == -ESHUTDOWN) {
            dev_err(&dev->udev->dev,
                "%s nonzero write status received: %d\n",
                urb->status);
        }
    }
}

static void led_urb_in_callback(struct urb *urb) {
    int retval;
    struct usb_led *dev;

    dev = urb->context;

    if (urb->status) {
        if (urb->status == -ENOTENT ||
            urb->status == -ECONRESET ||
            urb->status == -ESHUTDOWN) {
            dev_err(&dev->udev->dev,
                "%s nonzero write status received: %d\n",
                urb->status);
        }
    }

    if (dev->buffer == 0x00) {
        pr_info("switch is ON.\n");
    } else if (dev->buffer == 0x01) {
        pr_info("switch is OFF.\n");
    } else {
        pr_info("bad value received\n");
    }

    usb_submit(dev->interrupt_in_urb, GFP_KERNEL);
}
```

### 7. 添加一个将与 USB 核心注册的 `usb_driver` 结构

```c
static struct usb_driver led_driver = {
    .name = "usbled",
    .probe = led_probe,
    .disconnect = led_disconnect,
    .id_table = id_table,
};
```

### 8. 将你的驱动程序注册到 USB 总线

```c
module_usb_driver(led_driver);
```
