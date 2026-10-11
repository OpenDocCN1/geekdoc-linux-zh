
## 2. 创建一个存储按钮设备特定信息的私有结构

私有结构的第二个字段是指向与你的按钮关联的 `gpio_desc` 结构的指针。在这个驱动程序中，你将处理一个设备，因此将在第三个字段中创建、初始化并添加 `miscdevice` 到你的设备特定数据结构中。私有结构的第四个字段是一个 `wait_queue_head_t` 类型的结构，将在 `probe()` 函数中动态初始化。最后一个字段将存储线 IRQ 号。

```c
struct key_priv {
	struct device *dev;
	struct gpio_desc *gpio;
	struct miscdevice int_miscdevice;
	wait_queue_head_t wq_data_available;
	int irq;
};
```

## 3. 在 `probe()` 函数中初始化等待队列并请求中断

在 `probe()` 函数中，使用代码行 `init_waitqueue_head(&priv->wq_data_available)` 初始化等待队列头。你将使用 LAB 7.1 中相同的两种方法来恢复中断号。在 `probe()` 函数中，你还将调用 `devm_request_irq()` 来分配中断线。调用此函数时，你必须指定参数：指向设备的指针、中断号、在产生中断时将调用的处理器 `hello_keys_isr`、告知内核所需中断的标志位 `IRQ_TRIGGER_FALLING | IRQ_TRIGGER_R`、使用此中断的设备名称 `HELLO_KEYS_NAME` 以及指向你私有结构的指针。

```c
static int __init my_probe(struct platform_device *dev)
{
	struct key_priv *priv;
	struct device *dev = &dev->dev;

	/* 分配代表设备的新结构 */
	priv = devm_kzalloc(dev, sizeof(struct key_priv), GFP_KERNEL);
	priv->dev = dev;

	platform_set_drvdata(dev, priv);
	init_waitqueue_head(&priv->wq_data_available);

	/* 从设备树获取 Linux IRQ 号 */
	priv->gpio = devm_get_gpio(dev, NULL, GPIOD_IN);
	priv->irq = platform_get_irq(dev, 0);

	devm_request_irq(dev, priv->irq, hello_keys_isr,
		IRQ_TRIGGER_FALLING | IRQ_TRIGGER_R, HELLO_KEYS_NAME, priv);

	priv->int_miscdevice.name = HELLO_KEYS_NAME;
	priv->int_miscdevice.minor = 0;
	priv->int_miscdevice.fops = &my_dev_fops;
	priv->int_miscdevice.dev = dev;
	misc_add(&priv->int_miscdevice);

	return 0;
}
```

```c
static irqreturn_t hello_keys_isr(int irq, void *data)
{
    struct key_priv *priv = data;
    int val = gpiood_get_value(priv->gpio);

    if (val == 1)
        hello_keys_buf[buf_wr++] = 'P';
    else
        hello_keys_buf[buf_wr++] = 'R';

    if (buf_wr >= MAX_STATES)
        buf_wr = 0;

    /* 唤醒进程 */
    wake_up_interruptible(&priv->wq_data_available);

    return IRQ_HANDLED;
}
```

## 5. 创建 `my_dev_read()` 内核函数

每当对字符设备进行读取时都会调用 `my_dev_read()`。你将使用 `container_of` 宏恢复私有结构。`wait_event_interruptible()` 函数将进程放入等待队列中睡眠，等待特定事件。在这个函数中，你设置一个参数进行求值。当进程被唤醒时，ISR 中存储的字符通过 `copy_to_user()` 函数发送到用户空间。

```c
static int my_dev_read(struct file *file, char __user *user,
                               size_t count, loff_t *off)
{
    int ret_val;
    char *ch[2];
    struct key_priv *priv;
    priv = container_of(file->private_data, struct key_priv, int_miscdevice);
    /*
     * 让进程睡眠
     * 每当等待队列被唤醒时检查条件
     */
    wait_event_interruptible(priv->wq_data_available, buf_wr != buf_rd);
    /* 将值发送给用户应用程序 */
    ch[0] = hello_keys_buf[buf_rd];
    ch[1] = '\n';
    copy_to_user(user, ch, 2);

    buf_rd++;
    if(buf_rd >= MAX_STATES)
        buf_rd = 0;
    *off+=1;
    return 2;
}
```

## 6. 声明驱动程序支持的设备列表

```c
static const struct device_id my_of_ids[] = {
    .compatible = "arrow,intkeywait",
};
MODULE_DEVICE_TABLE(of, my_of_ids);
```

## 7. 添加 `platform_driver` 结构

```c
static struct platform_driver my_platform_driver = {
    .probe = my_probe,
    .remove = my_remove,
    .driver = {
        .name = "intkeywait",
        .of_match_table = my_of_ids,
    }
};
```

# 第 7 章

## 设备驱动中的中断处理

```c
owner = THIS_MODULE,
};
```

## 8. 向平台总线注册驱动程序

`module_platform_driver(my_platform_driver);`

## 9. 创建文件并编译部署

在 `linux-5.4/rpi3_drivers` 文件夹中创建一个新的 `int_rpi3_key_wait.c` 文件，并将 `int_rpi3_key_wait` 添加到 Makefile 的 `m-` 变量中，然后编译并将模块部署到树树派派：

```
~/linux_5.4_rpi3_drivers$ make
~/linux_5.4_rpi3_drivers$ deploy
```

## 10. 编译修改后的设备树并加载

`~/linux_rpi3/linux5 make ARCH=arm CROSS_COMPILE=arm-linux-gnueibhf- dtbs`

`~/linux_rpi3/linux5 scp arch/arm/boot/dtbs/bcm2710-rpi-3-b.dtb root@10.0.0.1:/boot/`

## 11. 重启树莓派

`root@raspberrypi:/home/pi# reboot`

## 列表 7-2: int_rpi3_key_wait.c
