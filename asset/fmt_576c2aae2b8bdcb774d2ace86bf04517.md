
```bash
~/linux_5.4_rpi3_drivers/linux_5.4_USB_drivers$ make
~/linux_5.4_rpi3_drivers/linux_5.4_USB_drivers$ make deploy
```

# 列表 13-2: usb_urb_int_led.c

```c
#include <linux/slab.h>
#include <linux/module.h>
#include <linux/usb.h>

#define USBLED_VENDOR_ID    0x04D8
#define USBLED_PRODUCT_ID  0x003F

static void led_urb_out_callback(struct urb *urb);
static void led_urb_in_callback(struct urb *urb);

/* 与此驱动程序工作的设备表 */
static const struct usb_device_id id_table[] = {
    USB_DEVICE(USBLED_VENDOR_ID, USBLED_PRODUCT_ID),
};
MODULE_DEVICE_TABLE(usb, id_table);

struct usb_led {
    struct usb_device *udev;
    struct usb_interface *intf;
    struct urb *interrupt_out_urb;
    struct urb *interrupt_in_urb;
    struct endpoint_descriptor *interrupt_out_endpoint;
    u8 *endpoint_descriptor *interrupt_in_endpoint;
    u8 irq_data;
    u8 led_number;
    u8 ibuffer;
    int interrupt_out_interval;
    int ep_in;
    int ep_out;
};

static ssize_t led_show(struct device *dev, struct device_attribute *attr, char *buf)
{
    struct usb_interface *intf = to_usb_interface(dev);
    struct usb_led *led = usb_get_intdata(intf);

    return sprintf(buf, "%d\n", led->led_number);
}

static ssize_t led_store(struct device *dev, struct device_attribute *attr,
    const char *buf, size_t count)
{
    struct usb_interface *intf = to_usb_interface(dev);
    struct usb_led *led = usb_get_intdata(intf);
    u8 val;
    int error, retval;

dev_info(&intf->dev, "led_store() function is called.\n");

/* 将字符数组转换为为 u8 值 */
error = ktou8(buf, 10, &val);
if (error)
    return error;

led->led_number = val;
led->irq_data = val;

if (val == 0)
    dev_info(&led->udev->dev, "read status\n");
else if (val == 1 || val == 2 || val == 3)
    dev_info(&led->udev->dev, "led %d\n", led->led_number);
else {
    dev_info(&led->udev->dev, "unknown value %d\n", val);
    retval = -EINVAL;
    return retval;
}

/* 发送数据出去 */
retval = usb_submit_urb(led->interrupt_out_urb, GFP_KERNEL);
if (retval)
    dev_err(&led->udev->dev, "Couldn't submit interrupt_out_urb %d\n", retval);
    return retval;

return count;
static DEVICE_ATTR_RW(led);

static void led_urb_out_callback(struct urb *urb)
{
    struct usb_led *dev;
    dev = urb->context;

dev_info(&dev->udev->dev, "led_urb_out_callback() function is called.\n");

/* 同步/异步取消链的故障不是错误 */
if (urb->status)
    if (!(urb->status == -ENOTIFYED ||
          urb->status == -ECONNRESET ||
          urb->status == -ESHUTDOWN))
        dev_err(&dev->udev->dev, "%s nonzero status received: %d\n",
        __func__, urb->status);

static void led_urb_in_callback(struct urb *urb)
{
    int retval;
    struct usb_led *dev;

dev_info(&dev->udev->dev, "led_urb_in_callback() function is called.\n");

if (urb->status) {
    if (!(urb->status == -ENOENT ||
        urb->status == -ECONNRESET ||
        urb->status == -ESHUTDOWN))
        dev_err(&dev->udev->dev,
            "%s nonzero write status received: %d\n",
            __func__, urb->status);
}
if (dev->ibuffer == 0x00) {
    pr_info("switch is ON.\n");
} else if (dev->ibuffer == 0x01) {
    pr_info("switch is OFF.\n");
} else {
    pr_info("bad value received\n");

retval = usb_submit_urb(dev->interrupt_in_urb, GFP_KERNEL);
if (retval) {
    dev_err(&dev->udev->dev,
        "Couldn't submit interrupt_in_urb %d\n", retval);
}
```
