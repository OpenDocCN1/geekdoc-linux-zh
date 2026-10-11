
# 第 7 章
# 设备驱动中处理中断

```c
GPIO_ASIS, label_name);

            gpiod_direction_input(keyd);

        }

    }

    return 0;

error:

    for (i = 0; i < priv->num_leds; i++) {

        device_destroy(priv->led_class, MKDEV(MAJOR(priv->devt), i));

    }

    class_destroy(priv->led_class);

    return ret;

}
```

```c
fnode_property_read_string(child, "trigger", &trigger);

if (strcmp(trigger, "falling") == 0)
    flags = IRQ_TRIGGER_FALLING;
else if (strcmp(trigger, "rising") == 0)
    flags = IRQ_TRIGGER_RISING;
else if (strcmp(trigger, "both") == 0)
    flags = IRQ_TRIGGER_RISING | IRQ_TRIGGER_FALLING;
else
    return -EINVAL;

irq = gpio_to_irq(keyd);
if (irq < 0)
    return irq;

ret = dev_request_irq(dev, irq, KEY_ISR1, flags, "ISR1", priv);
if (ret) {
    dev_err(dev, "Failed to request interrupt %d, error %d\n", irq, ret);
    return ret;
}

dev_info(dev, "IRQ number: %d\n", irq);
} else if (strcmp(label_name, "MIKROBUS_KEY_2") == 0) {
    keyd = dev_fwnode_get_gpio_from_child(dev, NULL, child);
    gpiod_direction_input(keyd);
    fwnode_property_read_string(child, "trigger", &trigger);
    if (strcmp(trigger, "falling") == 0)
        flags = IRQ_TRIGGER_FALLING;
    else if (strcmp(trigger, "rising") == 0)
        flags = IRQ_TRIGGER_RISING;
    else if (strcmp(trigger, "both") == 0)
        flags = IRQ_TRIGGER_RISING | IRQ_TRIGGER_FALLING;
    else
        return -EINVAL;
    irq = gpio_to_irq(keyd);
    if (irq < 0)
        return irq;
    ret = dev_request_irq(dev, irq, KEY_ISR2, flags, "ISR2", priv);
    if (ret < 0) {
    dev_err(dev, "Failed to request interrupt %d, error %d\n", irq, ret);
        goto error;
    }
    dev_info(dev, "IRQ number: %d\n", irq);
} else {
    dev_info(dev, "Bad device tree value\n");
    ret = -EINVAL;
    goto error;
}
```

```c
}
dev_info(dev, "i am out of the device tree\n");
/* 将周期重置为 10 */
priv->period = 10;
dev_info(dev, "the led period is %d\n", priv->period);
platform_set_drvdata(pdev, priv);
dev_info(dev, "my_probe() function exited.\n");
return 0;
error:
/* 如果发生错误时注销所有内容 */
for (i = 0; i < priv->num_leds; i++) {
    device_destroy(priv->led_class, MKDEV(priv->led_devt, i));
}
class_destroy(priv->led_class);
unregister_chrdev_region(priv->led_devt, priv->num_leds);
return ret;
}

static int my_remove(struct platform_device *pdev)
{
    int i;
    struct led_dev *led_count;
    struct keyed_led *priv = platform_get_drvdata(pdev);
    dev_info(&pdev->dev, "my_remove() function exited.\n");
if (priv->task_flag == 1) {
    kthread_stop(priv->task);
    priv->task_flag = 0;
}
if (priv->led_flag == 1) {
    for (i = 0; i < priv->num_leds; i++) {
        led_count = priv->leds[i];
        gpiod_set_value(led_count->ledd, i);
    }
}
for (i = 0; i < priv->num_leds; i++) {
    device_destroy(priv->led_class, MKDEV(MAJOR(priv->led_devt), i));
}
class_destroy(priv->led_class);
unregister_chrdev_region(priv->led_devt, priv->num_leds);
dev_info(&pdev->dev, "my_remove() function exited.\n");
return 0;
}

static const struct device_id my_dev_of_ids[] = {
```

```c
{ .compatible = "arrow, ledpwm", },
};

MODULE_DEVICE_TABLE(of, my_of_ids);

static struct platform_driver my_platform_driver = {
  .probe = my_probe,
  .remove = my_remove,
  .driver = {
    .name = "ledpwm",
    .match_table = my_of_ids,
    .owner = THIS_MODULE,
  },
};

module_platform_driver(my_platform_driver);

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Alberto Liberal liberal@arrow.com");
MODULE_DESCRIPTION("这是一个可以减少和增加 LED 周期的按键类驱动程序");
```

# keyed_rpi3_class.ko 演示

加载模块：

```
root@raspberrypi:~# insmod keyed_rpi3_class.ko
ledpwm:ledpwm: my_probe() function is called.
ledpwm:ledpwm: there are 5 nodes
ledpwm:ledpwm: the major number is 238
ledpwm:ledpwm: IRQ number: 166
ledpwm:ledpwm: IRQ number: 167
keyed red: the major number is 238, the minor number is 0, red
```
