
/* 选择 GPIO 22，你将把 GPIO 备用选择寄存器 2 的第 18 位 (`FSEL22`) 设置为 `0b111`。GPIO 引脚 22 将控制绿色 LED */

#define `FSEL_22_MASK`      `0x7` << ((`GPIO_22` % `10`) * `3`

/* 选择 GPIO 26，你将把 GPIO 备用选择寄存器 2 的第 20 位 (`FSEL26`) 设置为 `0b111`。GPIO 引脚 26 将控制蓝色 LED */

#define `FSEL_26_MASK`      `0x7` << ((`GPIO_26` % `10`) * `3`

3. 你将创建一个 `led_dev` 私有结构体来存储每个设备的特定信息。
```c

struct led_dev

{

	struct misdevice led_device; /* 为每个 LED 分配设备 */

	u32 led_mask; /* 如果 是 R、G 或 B，则有不同的掩码 */

};

```

# 第 5 章

## 平台驱动

```c

const char *led_name; /* 存储 "Label" 字符串 */

char led_value[8];

```

- 6. 现在，在你的 `probe()` 例程中，声明私有结构体的实例并为每个新探测到的设备分配内存。`probe()` 函数将被调用三次（对于每个与驱动 `compatible` 字段匹配的 `compatible` 属性值的 DT 节点（`ledred`, `ledgreen` 和 `ledblue`）调用一次），并分配相应的设备。

```c

struct led_dev *led_device;

led_device = devm_kzalloc(&pdev->dev, sizeof(struct led_dev), GFP_KERNEL);

```

- 7. 在 `led_init()` 例程中，使用 `ioremap()` 获取寄存地址的虚拟地址，并将它们存储在 `_V` 指针中：

```c

GPFSEL2_V = ioremap(GPFSEL2, sizeof(u32));

GPSET0_V = ioremap(GPSET0, sizeof(u32));

GPCLR0_V = ioremap(GPCLR0, sizeof(u32));

```

- 8. 在 `probe()` 例程中初始化每个 `misdevice` 结构体。正如你在第 4 章看到的，杂设备框架（miscellaneous framework）为没有其他框架连接的设备在字符文件之上提供了一个简单的层。注册到杂设备子系统可以创建字符文件。`of_property_read_string()` 函数将从每个被探测的 DT 设备节点的 `label` 属性中查找并读取字符串。函数的第三个参数是指向 `char` 变量的指针。`of_property_read_string()` 函数将 "label" 存储在 `led_name` 指针变量指向的地址。

```c

of_property_read_string(pdev->dev_of_node, "label", &led_device->led_name);

led_device->led_misc_device.minor = MISC_DYNAMIC_MINOR;

led_device->led_misc_device.name = led_device->led_name;

led_device->led_misc_device.fops = &led_fops;

```

- 9. 当你创建一个字符文件时，需要一个 `file_operations` 结构体来定义用户打开、关闭和写入字符文件时调用哪些驱动函数。该结构将被存储在 `misdevice` 结构体中，并在你将设备注册到它时传递给杂设备系统。需要注意的是，当你使用杂设备系统时，它会自动为你处理 "open" 函数。自动创建的 "open" 函数会将 `misdevice` 结构体绑定到已打开文件的 `private_data` 字段。这对于使用 `container_of()` 宏来访问 `misdevice` 结构体的父结构体非常有用。

```c

static const struct file_operations led_fops = {

    .owner = THIS_MODULE,

    .read = led_read,

    .write = led_write,

};

```

```c

/* 将 file_operations 结构体传递给每个创建的杂设备 */

led_device->led_misc_fops = &led_fops;

```

- 10. 在 `probe()` 例程中，使用 `misc_register()` 函数将每个设备注册到内核。`platform_set_drvdata()` 函数将每个私有结构体附加到每个 `platform_device` 结构体。这允许你在驱动的每个函数中使用私有数据结构。你将在 `remove()` 函数调用中（共三次）通过 `platform_get_drvdata()` 函数恢复私有结构体：

```c

ret_val = misc_register(&led_device->led_misc_device);

platform_set_drvdata(led_device);

```

- 11. 创建 `led_write()` 函数，每当其中一个字符发生写入操作时，该函数会被调用。在你注册每个杂设备时，你并没有指向 `led_dev` 结构体的指针。然而，`misdevice` 结构体可以通过 `file->private_data` 访问，并且它是 `led_dev` 结构体的成员，你可以使用魔术宏 `container_of()` 计算出存储 `misdevice` 的内部结构体（即你的 `led_dev` 结构体）。`copy_from_user()` 函数将从用户空间获取开启/关闭命令，然后你通过 `iowrite32()` 处理器的相应寄存器来开启/关闭。

```c

static ssize_t led_write(struct file *file, const char __user *buff,

    size_t count, loff_t *ppos)

{

    const char *led_on = "on";

    const char *led_off = "off";

    struct led_dev *led_device;

    led_device = container_of(file->private_data,

                 struct led_dev, led_misc_device);

    if(copy_from_user(led_device->led_value, buff, count)) {

        pr_info("Bad copy copied\n");

        return -EFAULT;

    }

    led_device->led_value[count-1] = '\0';

    if(!strcmp(led_device->led_value, led_on)) {

        iowrite32(led_device->led_mask, GPSET0_V);

    } else if (!strcmp(led_device->led_value, led_off)) {

        iowrite32(led_device->led_mask, GPCLR0_V);

    }

    else {

        pr_info("Bad value\n");

        return -EINVAL;

    }

    return count;

}

```

- 12. 创建 `led_read()` 函数，当对一个字符文件发生读取操作时，该函数会被调用。我们将使用 `container_of()` 宏恢复私有结构体，并使用 `copy_to_user()` 函数向用户返回 `led_value` (`on/off`)：

```c

static ssize_t led_read(struct file *file, char __user *buff,

    size_t count, loff_t *ppos)

{

    struct led_dev *led_device;

    led_device = container_of(file->private_data, struct led_dev, led_misc_device);

    if(*ppos == 0) {

        if (copy_to_user(buff, &led_device->led_value,

            sizeof(led_device->led_value))) {
