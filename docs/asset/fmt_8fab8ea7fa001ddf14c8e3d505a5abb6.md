
# 第7章

## 设备驱动程序中的中断处理

```
if(!strcmp(buffer, "on")) {

    if (led->private->led_num_leds == 1) {

        for (i = 0; i < led->private->num_leds; i++) {

            led_count = led->private->leds[i];

            gpiod_set_value(led_count->ledd, 1);

        }

        gpiod_set_value(led->ledd, 0);

    } else {

        gpiod_set_value(led->ledd, 0);

        led->private->led_flag = 1;

    }

  } else if (!strcmp(buffer, "off")) {

    gpiod_set_value(led->ledd, 1);

  } else {

    dev_info(led->dev, "Bad led value.\n");

    return -EINVAL;

  }

return count;

static DEVICE_ATTR_WO(set_led);
```

/* 通过运行线程让 LED 闪烁 */

```
static ssize_t blink_on_led_store(struct device_attribute *attr,

                               const char *buf, size_t count)

{

    int i;

    char *buffer = buf;

    struct led_device *led_count = count;

    struct led_device *led = dev_get_drvdata(dev);

    /* 将终端添加 \n 替换为 \0 */

    *(buffer+(count-1)) = '\0';

    if (led->private->led_flag == 1) {

        for (i = 0; i < led->private->num_leds; i++) {

            led_count = led->private->leds[i];

            gpiod_set_value(led_count->ledd, 1);

        }

    }

  if(!strcmp(buffer, "on")) {

    if (led->private->task_flag == 0) {

        led->private->task = kthread_run(led->flash, led, "Led_flash_thread");

        if(IS_ERR(led->private->task)) {

            dev_info(led->dev, "Failed to create the task\n");

            return PTR_ERR(led->private->task);

        }

    }

  }

}
```

## 设备驱动程序中的中断处理

# 第7章

```c
else
    return -EBUSY;
} else {
    dev_info(led->dev, "Bad led value.\n");
    return -EINVAL;
}
led->private->task_flag = 1;
dev_info(led->dev, "Blink_on_led exited\n");
    return count;

static DEVICE_ATTR_WO(blink_on_led);
```

/* 关闭 LED 闪烁 */

```
static size_t blink_off_led_store(struct device *dev,

    struct device_attribute *attr,

    const char *buf, size_t count)

{

    int i;

    char *buffer = buf;

    struct led_device *led = dev_get_drvdata(dev);

    struct led_device *led_count;

/* 将终端的 \n 替换为 \0 */

(buffer+(count-1)) = '\0';

if(!strcmp(buffer, "off")) {

    if (led->private->task_flag == 1) {

        kthread_stop(led->private->task);

        for (i = 0; i < led->private->num_leds; i++) {

            led_count = led->private->leds[i];

            gpiod_set_value(led_count->ledd, 1);

        }

    } else {

        return 0;

    }

} else {

    dev_info(led->dev, "Bad led value.\n");

    return -EINVAL;

}

led->private->task_flag = 0;

    return count;

static DEVICE_ATTR_WO(blink_off_led);
```

/* 设置闪烁周期 */

```
static size_t set_period_store(struct device *dev,

    struct device_attribute *attr,

    const char *buf, size_t count)

{
```

# 第7章

## 设备驱动程序中的中断处理

```
unsigned long flags;
int ret, period;
struct led_device *led = dev_get_drvdata(dev);
dev_info(led->dev,"Enter set_period\n");
```

```c
ret = scanf(buf,"%u", &period);

if (ret < 1 || period < 10 || period > 10000) {

    dev_err(dev,"invalid value\n");

    return -EINVAL;

}
```

```c
spin_lock_irqsave(&led->private->period_lock, flags);

led->private->period = period;

spin_unlock_irq(&led->private->period_lock, flags);
```

```c
dev_info(led->dev,"period is set\n");

return count;

static DEVICE_ATTR_WO(set_period);
```

```c
/* 声明 sysfs 结构 */
static struct led_attrs[] = {
&dev_attr_set_led_attr,
&dev_attr_blink_on_led_attr,
&dev_attr_blink_off_led_attr,
&dev_attr_set_period_attr,
NULL,
};
```

```c
static const struct attribute_group led_group = {
    .attrs = led_attrs,
};
```

```c
static const struct attribute_group *led_groups[] = {
    &led_group,
    NULL,
};
```

```c
/* 为全局私有结构和三个 LED 结构体分配空间 */
static inline int size_of(struct keyed_priv)(int num_leds)
{
    return sizeof(struct keyed_priv) + (sizeof(struct led_device) * num_leds);
}
```

```c
/* 第一个中断处理程序 */
static irqreturn_t ISR1(int irq, void *data)
{
    struct keyed_priv *priv = data;
dev_info(priv->dev,"Interrupt1 received: %s\n", LED_NAME);
```
