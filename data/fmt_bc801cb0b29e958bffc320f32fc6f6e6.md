
```c
led_device->brightness = 4;
} else if (strcmp(cdev->name, "green") == 0) {
    led_device->brightness = 0;
}
dev_led_classdev_register(cdev);
}
private->num_leds++;
dev_info(dev, "probe finished\n");
return 0;
}
```

- 6. 编写亮度函数。每当用户应用程序向 `/sys/class/led>/brightness` 写入 "0" 到 "15" 时，`led_device` 结构都会处理这些复杂性。使用 `container_of()` 函数来获取 `led_device`。

- 7. 在 `probe()` 函数中，你通过编写代码 `sysfs_create_group()` 添加了一组 sysfs 文件来控制 ENGB/S 引脚。现在，你将创建两个名为 'rgb' 和 'sub' 的 `device_attribute` 类型结构，并将这些属性组织在一起：

```c
static DEVICE_ATTR(rgb, S_IWRUS, NULL);
static DEVICE_ATTR(sub, S_IWRUS, NULL);
static struct attribute *display_cs_attrs[] = {
    &dev_attr_rgb.attr,
    &dev_attr_sub.attr,
    NULL,
};
static struct attribute_group display_cs_group = {
    .name = "display_cs",
    .attrs = display_cs_attrs,
};
```

- 8. 编写 `rgb_select()` 和 `select()` 函数，当用户应用程序写入 "rgb" 和 "sub" sysfs 条目时，这些函数会被调用。在这些函数内部，使用 `to_i2c_client()` 函数恢复 `i2c_client` 结构，然后使用 `i2c_get_clientdata()` 函数恢复 `led_priv` 全局结构。`i2c_get_clientdata()` 函数接收之前恢复的 `i2c_client` 结构作为参数。一旦获取了全局结构，你可以使用 `CMD_SUB_SHIFT` 更新 `command[0]` 的 A2 位，然后使用 `Ltc3206_led_write()` 函数将新命令值发送给 LTC3206 设备。根据所选的 "on" 或 "off" 值，使用 `gpio_set_value()` 函数将 GPIO 物理线从“低到高”或“高到低”，该函数以你 `led_priv` 全局结构中的 GPIO 描述符作为参数。

- 9. 定义驱动程序支持的设备列表：

```c
static const struct device_id my_of_ids[] = {
    {.compatible = "arrow,ltc3206"},
    {}
};
MODULE_DEVICE_TABLE(of, my_of_ids);
```

- 10. 定义 `i2c_device_id` 结构数组：

```c
static const struct i2c_device_id ltc3206_id[] = {
    {"ltc3206", 0},
};
MODULE_DEVICE_TABLE(i2c, ltc3206_id);
```

# 第6 章

## I2C 客户端驱动

```c
{ }
MODULE_DEVICE_TABLE(i2c, ltc3206_id);
```

11. 添加一个注册到 I2C 总线的 `i2c_driver` 结构体：

```c
static struct i2c_driver ltc3206_driver = {
    .probe = ltc3206_probe,
    .remove = ltc3206_remove,
    .id_table = ltc3206_id,
    .driver = {
        .name = "ltc3206",
        .of_match_table = my_of_ids,
        .owner = THIS_MODULE,
    }
}
```

12. 将你的驱动注册到 I2C 总线：

```c
module_i2c_driver(ltc3206_driver);
```

13. 在 `linux_5.4_rpi3_drivers` 文件夹中创建一个新的 `ltc3206_rpi3_led_class.c` 文件，并将 `ltc3206_rpi3_led_class.o` 添加到 Makefile 的 `obj-m` 变量中，然后编译并将模块部署到树莓派：

```bash
~linux_5.4_rpi3_drivers$ make
~linux_5.4_rpi3_drivers$ make deploy
```

14. 编译修改后的设备树并将其加载到目标处理器：

```bash
~linux_rpi3/linux$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- dts
~linux_rpi3/linux$ scp arch/arm/boot/bcm2710-rpi-3-b.dtb root@10.0.0.10:/boot/
```

15. 重启树莓派：

```bash
root@raspberrypi:~/home/pi# reboot
```

## 列表 6-2: ltc3206_rpi3_led_class.c

```c
#include <linux/module.h>
#include <linux/i2c.h>
#include <linux/led.h>
#include <linux/gpio/consumer.h>
#include <linux/delay.h>
#define LED_NAME_LEN      32
#define CMD_RED_SHIFT    4
#define CMD_BLUE_SHIFT   4
#define CMD_GREEN_SHIFT  0
#define CMD_MAIN_SHIFT   4
#define CMD_SUB_SHIFT    0
#define EN_CS_SHIFT      (1 << 2)
/* 为 5 个 LED 设备中的每一个设置 led 设备结构体 / */
struct led_device {
    u8 brightness;
    struct led_class cdev;
    struct led_priv *private;
};
/*
* 存储 5 个 LED 设备共享的全局参数。
* 这些参数在每次调用 led_control() 后都会更新
*/
struct led_priv {
    u32 num_leds;
    u8 command[3];
    struct gpio_desc *display_cs;
    struct i2c_client *client;
};
/* 向 I2C 设备写入数据的函数 / */
static int ltc3206_led_write(struct i2c_client *client, u8 *command)
{
    int ret = i2c_master_send(client, command, 3);
    if (ret < 0)
        return 0;
    return ret;
}
/* sysfs 函数 / */
static ssize_t sub_select(struct device *dev, struct device_attribute *attr,
    const char *buf, size_t count)
{
    char *buffer;
    struct i2c_client *client;
    struct led_priv *private;
    buffer = buf;
static size_t rgb_select(struct device *dev, struct device_attribute *attr,
const char *buf, size_t count)
{
    char *buffer;
    struct i2c_client *client = to_i2c_client(dev);
```
