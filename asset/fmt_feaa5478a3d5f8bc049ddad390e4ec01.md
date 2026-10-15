
```c
input_unregister_device(vms_input_dev);

/* Cleanup sysfs node */

sysfs_remove_group(&vms_dev->dev.kobj, &vms_attr_group);

/* Unregister driver */

platform_device_unregister(vms_dev);

return;

}

module_init(vms_init);

module_exit(vms_cleanup);
```

让我们更仔细地查看代码清单 7.2。在初始化期间，`vms` 驱动程序将自己注册为输入设备驱动程序。为此，它首先使用核心 API `input_allocate_device()` 分配一个 `input_dev` 结构：

```c
vms_input_dev = input_allocate_device();
```

然后，它声明虚拟鼠标产生相对事件：

```c
set_bit(EV_REL, vms_input_dev->evbit);  /* Event Type is EV_REL */
```

接下来，它声明虚拟鼠标产生的事件代码：

```c
set_bit(REL_X, vms_input_dev->relbit); /* Relative 'X' movement */
set_bit(REL_Y, vms_input_dev->relbit); /* Relative 'Y' movement */
```

如果你的虚拟鼠标还能够产生按钮点击，你需要将此添加到 `vms_init()` 中：

```c
set_bit(EV_KEY, vms_input_dev->evbit);  /* Event Type is EV_KEY */
set_bit(BTN_0, vms_input_dev->keybit);  /* Event Code is BTN_0 */
```

最后是注册：

```c
input_register_device(vms_input_dev);
```

`write_vms()` 是连接到 `/sys/devices/platform/vms/coordinates` 的 `sysfs store()` 方法。当 `coord.c` 向此文件写入 X/Y 对时，`write_vms()` 执行以下操作：

```c
input_report_rel(vms_input_dev, REL_X, x);
input_report_rel(vms_input_dev, REL_Y, y);
input_sync(vms_input_dev);
```

第一条语句生成一个 `REL_X` 事件，即在 X 方向上的相对设备移动。第二条语句生成一个 `REL_Y` 事件，即在 Y 方向上的相对移动。`input_sync()` 表示该事件已完成。因此，输入子系统将这两个事件收集到一个 evdev 数据包中，并通过 `/dev/input/eventX` 发送出去，其中 X 是分配给 `vms` 驱动程序的接口号。读取此文件的应用程序将接收到以前描述过的 `input_event` 格式的事件数据包。要让 `gpm` 附加到此事件接口，并相应地在你的屏幕上追踪光标，请执行以下操作：

```bash
bash> gpm -m /dev/input/eventX -t evdev
```

稍后在“触摸控制器”和“加速度计”章节中讨论的 ADS7846 触摸控制器驱动程序和加速度计驱动程序，也是 evdev 的用户。

### 更多事件接口

`vms` 驱动程序利用通用的 evdev 事件接口，但键盘、鼠标和触摸控制器等输入设备具有自定义事件驱动程序。当我们讨论相应的设备驱动程序时，我们将介绍它们。

要编写自己的事件驱动程序并通过 `/dev/input/mydev` 将其导出到用户空间，你需要填充一个名为 `input_handler` 的结构，并按照以下方式将其注册到输入核心：

```c
static struct input_handler my_event_handler = {  
    .event      = mydev_event,             /* Handle event reports sent by
                                               input device drivers that use
                                               this event driver's services */
    .fops       = &mydev_fops,            /* Methods to manage
                                               /dev/input/mydev */
    .minor      = MYDEV_MINOR_BASE,       /* Minor number of
                                               /dev/input/mydev */
    .name       = "mydev",                /* Event driver name */
    .id_table   = mydev_ids,              /* This event driver can handle
                                               requests from these IDs */
    .connect    = mydev_connect,          /* Invoked if there is an
                                               ID match */
    .disconnect = mydev_disconnect,       /* Called when the driver unregisters */
};

/* Driver Initialization */
static int __init
mydev_init(void)
{
    /* ... */
    input_register_handler(&my_event_handler);
    /* ... */
    return 0;
}
```
