
```c
priv = devm_kzalloc(dev, sizeof_keyed_priv(count), GFP_KERNEL);

if (!priv)
    return -ENOMEM;

/* 分配设备号 */
alloc_chrdev_region(&priv->led_dev, 0, COUNT_INT_NUMBER, "keyed_class");
major = MAJOR(priv->led_dev);
dev_info(dev, "主设备号为 %d\n", major);

/* 创建 LED 类 */
priv->led_class = class_create(THIS_MODULE, "keyed");
if (!priv->led_class) {
    dev_info(dev, "分配类失败\n");
    return -ENOMEM;
}

/* 设置该类的属性 */
priv->led_class->dev->groups = led_groups;

/* 解析所有 DT 节点 */
device_for_each_child_node(dev, child) {
    fwnode_property_read_string(child, "label", &label_name);
    /* 解析 DT led 节点 */
    if (strcmp(label_name, "led") == 0) {
        fwnode_property_read_string(child, "colour", &colour_name);
        /*
         * 在 keyed 类下创建设备
         * priv->num_leds 在第一次迭代时为 0
         * 用于设置每个设备的次设备号
         * 直增加到迭代末尾
         */
        new_led = led_device_register(colour_name, priv->num_leds, dev,
            priv->led_dev, priv->led_class);
        if (!new_led) {
            ret = PTR_ERR(new_led);
            goto error;
        }
        priv->num_leds++;
    }
    /* 解析中断节点 */
    if (strcmp(label_name, "KEY_1") == 0) {
        keyd = devm_get_gpio_from(child, NULL);
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
    }
        irq = gpiod_to_irq(keyd);
        if (irq < 0)
            return irq;
        ret = devm_request_irq(dev, irq, KEY_ISR1,
            flags, "ISR1", priv);
        if (ret) {
            dev_err(dev, "请求中断 %d 失败，错误 %d\n",
                irq, ret);
            return ret;
        }
        dev_info(dev, "IRQ 号: %d\n", irq);
    } else if (strcmp(label_name, "KEY_2") == 0) {
        keyd = devm_get_gpio_from(child, NULL);
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
    }
        irq = gpiod_to_irq(keyd);
        if (irq < 0)
            return irq;
        ret = devm_request_irq(dev, irq, KEY_ISR2,
            flags, "ISR2", priv);
        if (ret) {
            dev_err(dev, "请求中断 %d 失败，错误 %d\n",
                irq, ret);
            return ret;
        }
        dev_info(dev, "IRQ 号: %d\n", irq);
    }
}
return 0;
error:
return ret;
}
```

# 第7章

## 设备驱动程序中的中断处理

```c
ret = devm_request_irq(dev, irq, KEY_ISR2,
    flags, "ISR2", priv);
if (ret < 0) {
    dev_err(dev,
        "Failed to request interrupt %d, error %d\n",
        irq, ret);
    goto error;
}
dev_info(dev, "IRQ number: %d\n", irq);
} else {
    dev_info(dev, "Bad device tree value\n");
    ret = -EINVAL;
    goto error;
}
dev_info(dev, "i am out of the device tree\n");
/* reset period to 10 * */
priv->period = 10;
dev_info(dev, "the led period is %d\n", priv->period);
platform_set_drvdata(pdev, priv);
dev_info(dev, "my_probe() function is exited.\n");
return 0;
error:
/* Register everything in case of errors */
```
