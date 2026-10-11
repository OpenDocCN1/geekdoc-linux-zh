
```c
{
    dev_info(&client->dev, "leds_remove enter\n");

    sysfs_remove_group(&client->dev.kobj,&display_cs_group);

    dev_info(&client->dev, "leds_remove exit\n");

    return 0;
}
```

```c
static const struct of_device_id my_of_ids[] = {
    .compatible = "arrow,ltc3206",
};
MODULE_DEVICE_TABLE(of, my_of_ids);

static const struct i2c_device_id ltc3206_id[] = {
    { "ltc3206", 0 },
};
MODULE_DEVICE_TABLE(i2c, ltc3206_id);

static struct i2c_driver ltc3206_driver = {
    .probe = ltc3206_probe,
    .remove = ltc3206_remove,
    .id_table = ltc3206_id,
    .driver = {
        .name = "ltc3206",
        .match_table = my_of_ids,
        .owner = THIS_MODULE,
    }
}
module_i2c_driver(ltc3206_driver);
MODULE_LICENSE("GPL");
MODULE_AUTHOR("Alberto Liberal careral@arroweurope.com");
MODULE_DESCRIPTION("这是一个控制 \ntc3206 I2C 多路显示设备的驱动程序");
```

## `ltc3206_imx_led_class.ko` 演示

将 ENRGB/S 连接到 DVCC

```
root@imx7dsabresd:~# insmod ltc3206_imx_led_class.ko /* 加载模块，probe() function函数被调用了 5 次，且蓝色 LED 开启 */
root@imx7dsabresd:~# ls -1 /sys/class/led /* 查找 led 类下的所有设备 */
root@imx7dsabresd:~# echo 10 /sys/class/leds/red/brightness /* 开启亮度值为为 10 的红色 LED */
root@imx7dsabresd:~# echo 15 /sys/class/leds/red/brightness /* 为红色 LED 设置 最大亮度 */
root@imx7dsabresd:~# echo 0 /sys/class/leds/red/brightness /* 关闭红色 LED */
root@imx7dsabresd:~# echo 10 /sys/class/leds/blue/brightness /* 开启亮度值为为 10 的蓝色 LED */
root@imx7dsabresd:~# echo 15 /sys/class/leds/blue/brightness /* 为蓝色 LED 设置 最大亮度 */
root@imx7dsabresd:~# echo 0 /sys/class/leds/blue/brightness /* 关闭蓝色 LED */
root@imx7dsabresd:~# echo 10 /sys/class/leds/green/brightness /* 开启亮度值为为 10 的绿色 LED */
root@imx7dsabresd:~# echo 15 /sys/class/leds/green/brightness /* 为绿色 LED 设置 最大亮度 */
root@imx7dsabresd:~# echo 0 /sys/class/leds/green/brightness /* 关闭绿色 LED */
root@imx7dsabresd:~# echo 10 /sys/class/leds/main/brightness /* 开启主显示器（DISPLAY MAIN），亮度值为 10 */
root@imx7dsabresd:~# echo 15 /sys/class/leds/main/brightness /* 为主显示器设置 最大亮度 */
root@imx7dsabresd:~# echo 0 /sys/class/leds/main/brightness /* 关闭主显示器 */
root@imx7dsabresd:~# echo 10 /sys/class/leds/sub/brightness /* 开启子显示器（SUB），亮度值为 10 */
root@imx7dsabresd:~# echo 15 /sys/class/leds/sub/brightness /* 为子显示器设置 最大亮度 */
root@imx7dsabresd:~# echo 0 /sys/class/leds/sub/brightness /* 关闭子显示器 */
“混合红、绿、蓝颜色”
root@imx7dsabresd:~# echo 10 /sys/class/leds/red/brightness
root@imx7dsabresd:~# echo 15 /sys/class/leds/blue/brightness
root@imx7dsabresd:~# echo 15 /sys/class/leds/green/brightness
root@imx7dsabresd:~# rmmod ltc3206_imx_led_class.ko /* 移除模块，remove() function函数被调用了 5 次 */
```

关闭板板电源，并将 ENRGB/S 引脚连接到 Mikrob INT 引脚。开启板板电源启动目标处理器。

# 第 6 章

## I2C 客户端驱动

```
root@imx7dsabresd:~# insmod ltc3206_imx_led_class.ko /* 加载模块，probe() function函数被调用了 5 次，且蓝色 LED 关闭 */
root@imx7dsabresd:~# echo 10 /sys/class/leds/sub/brightness /* 开启子显示器，亮度值为 10，此时子显示器为开启 */
root@imx7dsabresd:~# echo 10 /sys/class/leds/red/brightness /* 开启亮度值为 10 的红色 LED，此时红色 LED 为关闭 */
root@imx7dsabresd:~# echo off /sys/class/i2c-dev/2-001b/display_cs/sub /* 关闭子显示器并开启红色 LED */
root@imx7dsabresd:~# echo off /sys/class/i2c-dev/2-001b/display_cs/rgb /* 关闭 RGB LED 并开启子显示器 */
root@imx7dsabresd:~# rmmod ltc3206_imx_led_class.ko
```

# 中断处理

# 第 7 章

# 设备驱动程序中的中断处理

这指的是处理线路流管理的高层函数（`typedef void (*irq_handler_t)(struct irq_desc *desc)`）。每当中断触发时，低层架构代码会通过调用 `irq_desc->handle_irq` 进入通用中断代码。此高层 IRQ 处理函数仅使用分配的芯片描述符所引用的 `irq_desc->irq_data->chip` 原语。
