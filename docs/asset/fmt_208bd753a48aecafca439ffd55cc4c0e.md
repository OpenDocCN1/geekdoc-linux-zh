
```c
static int led_probe(struct usb_interface *interface,
               struct usb_device_id *id)
{
    /* 从 usb_interface 中获取 usb_device 结构体 */
    struct usb_device *dev = interface_to_usbdev(interface);
    struct usb_led *led = NULL;
    int retval = -ENOMEM;

    dev_info(&interface->dev, "led_probe() function is called.\n");

    /* 分配我们的私有数据结构 */
    dev = kmalloc(sizeof(struct usb_led), GFP_KERNEL);

    /* 将 USB 设备数据存储在我们的数据结构中 */
    dev->udev = usb_get_dev(dev);

    /* 将 USB 设备数据附加到 USB 接口 */
    usb_set_intfdata(interface, dev);

    /* 创建 led sysfs 条目以与用户空间交互 */
    device_create_file(&interface->dev, &dev_attr_led);

    return 0;
}
```

### 5. 编写 `led_store()` 函数
每当用户空间写入 sysfs 条目（`/sys/bus/usb/devices/1-1.3:0/led`）时，驱动的 `led_store()` 函数会被调用。通过 `usb_get_intfdata()` 函数恢复与 USB 设备关联的结构体。写入 sysfs 条目的命令存储在 `val` 变量中。内核提供了 `usb_bulk_msg()` 和 `usb_control_msg()` 辅助函数，允许在无需创建 `urb` 结构的情况下初始化、提交并等待批量和控制消息的完成。这些函数是同步的，你不能在中断上下文中或持有自旋锁的情况下调用它们。

```c
int usb_bulk_msg(struct usb_device *usb_dev, unsigned int pipe, void *data,
                int len, int *actual_length, int timeout);
```

下面是 `usb_bulk_msg()` 参数的简要描述：

- `usb_dev`: 用于发送消息的 USB 设备。
- `pipe`: 端点。
- `len`: 要发送的数据长度（字节）。
- `actual_length`: 实际传输长度的指针。
- `timeout`: 等待消息完成的毫秒数。

下面是 `led_store()` 例程的提取：

```c
static size_t led_store(struct device *dev, struct device_attribute *attr,
               const char *buf, size_t count)
{
    struct usb_interface *int = to_usb_interface(dev);
    struct usb_led *led = usb_get_intfdata(int);
    u8 val;
    int retval;

    /* 将字符数组转换为 u8 */
    strtou8(buf, &val);

    led->led_number = val;

    /* 切换 led */
    retval = usb_bulk_msg(led->udev, usb_pipe(led->udev, 1),
        &led->led_number,
        1,
        NULL,
        0);

    if (retval)
      retval = -EFAULT;
    return count;
}
static DEVICE_ATTR_RW(led);
```

### 添加到 USB 核心的 `usb_driver` 结构

```c
struct usb_driver led_driver = {
    .name = "usbled",
    .probe = led_probe,
    .disconnect = led_disconnect,
    .id_table = id_table,
};
```

### 在 USB 总线上注册你的驱动

```bash
module_usb_driver(led_driver);
```

### 创建 `usb_drivers` 文件夹

```bash
mkdir usb_drivers
```

### 在 `usb_drivers` 文件夹中创建新的 `usb_led.c` 和 `Makefile`，并将 `usb_led.o` 添加 `Makefile` 变量，然后编译并部署模块到树莓派

```c
# 列表 13-1: usb_led.c
#include <linux/slab.h>
#include <linux/module.h>
#include <linux/usb.h>

#define USB_VENDOR_ID 0x04D8
#define USB_PRODUCT_ID 0x003F

/* 使用此驱动的设备表 */
static const struct usb_device_id id_table[] = {
    { USB_DEVICE(USB_VENDOR_ID, USB_PRODUCT_ID) },
};

static int led_probe(struct usb_interface *interface, struct usb_device_id *id)
{
  struct usb_device *udev = interface_to_usbdev(interface);
  struct usb_led *dev = NULL;
  int retval = -ENOMEM;

  dev_info(&interface->dev, "led_probe() function is called.\n");
  dev = kmalloc(sizeof(struct usb_led), GFP_KERNEL);
  if (!dev) {
    dev_err(&interface->dev, "out of memory\n");
    retval = -ENOMEM;
    goto error;
  }

  dev->udev = usb_get_dev(udev);
  usb_set_intfdata(interface, dev);
  retval = device_create_file(&interface->dev, &dev_attr_led);
  if (retval) {
    goto error_create_file;
  }

  return 0;

error_create_file:
  usb_put_dev(udev);
  usb_set_intfdata(interface, NULL);
error:
  kfree(dev);
  return retval;
}

static void led_disconnect(struct usb_interface *interface)
{
  struct usb_led *dev;

  dev = usb_get_intfdata(interface);
  device_remove_file(&interface->dev, &dev_attr_led);

  usb_set_intfdata(interface, NULL);
  usb_put_dev(dev->udev);
  kfree(dev);

  dev_info(&interface->dev, "USB led disconnected\n");
}

static struct usb_driver led_driver = {
    .name = "usbled",
    .probe = led_probe,
    .disconnect = led_disconnect,
    .id_table = id_table,
};

module_usb_driver(led_driver);

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Alberto aliberal@arroweurope.com");
MODULE_DESCRIPTION("这是一个同步 led 控制模块");
```

# `usb_led.ko`

将 PIK32MX470 Curiosity 开发板的 Micro-B 端口 (`J12`) 连接到树莓派板的四个 USB Host-A 连接之一。为树莓派板供电启动处理器。PIK32MX470 板处于关电状态。
