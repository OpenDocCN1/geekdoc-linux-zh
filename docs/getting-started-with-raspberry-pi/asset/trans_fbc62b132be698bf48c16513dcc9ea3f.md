
## 7.2 输入子系统（续）

```c
vms_cleanup(void)
{

/* Unregister from the input subsystem */
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

让我们更仔细地查看代码清单 7.2。在初始化期间，vms 驱动程序将自己注册为输入设备驱动程序。为此，它首先使用核心 API `input_allocate_device()` 分配一个 `input_dev` 结构：

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

第一条语句生成一个 REL_X 事件，即在 X 方向上的相对设备移动。第二条语句生成一个 REL_Y 事件，即在 Y 方向上的相对移动。`input_sync()` 表示该事件已完成。因此，输入子系统将这两个事件收集到一个 evdev 数据包中，并通过 `/dev/input/eventX` 发送出去，其中 X 是分配给 vms 驱动程序的接口号。读取此文件的应用程序将接收到以前描述过的 input_event 格式的事件数据包。要让 gpm 附加到此事件接口，并相应地在你的屏幕上追踪光标，请执行以下操作：

```bash
bash> gpm -m /dev/input/eventX -t evdev
```

稍后在“触摸控制器”和“加速度计”章节中讨论的 ADS7846 触摸控制器驱动程序和加速度计驱动程序，也是 evdev 的用户。

## 更多事件接口

vms 驱动程序利用通用的 evdev 事件接口，但键盘、鼠标和触摸控制器等输入设备具有自定义事件驱动程序。当我们讨论相应的设备驱动程序时，我们将介绍它们。

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

查看 mousedev（`drivers/input/mousedev.c`）的实现，以获取完整的示例。

## 输入设备驱动程序

让我们把注意力转向键盘、鼠标和触摸屏等常见输入设备的驱动程序。但首先，让我们快速查看一下可供输入驱动程序使用的现成硬件访问设施。

### 串口（Serio）

*serio* 层提供了访问传统输入硬件（如 i8042 兼容的键盘控制器和串口）的库例程。PS/2 键盘和鼠标与前者进行接口，而串口触摸控制器则连接到后者。为了与 *serio* 服务的硬件进行通信，例如向 PS/2 鼠标发送命令，请使用 `serio_register_driver()` 将预定的回调例程注册到 *serio*。

要将新驱动程序作为 *serio* 的一部分添加，请使用 `serio_register_port()` 注册 `open()` / `close()` / `start()` / `stop()` / `write()` 入口点。请查看 `drivers/input/serio/serport.c` 以获取示例。

如图 7.1 所示，*serio* 只是访问底层硬件的一条路径。许多输入设备驱动程序依赖于 USB 或 SPI 等总线层提供的底层支持。

### 键盘

键盘有不同的类型——传统 PS/2、USB、蓝牙、红外等。每种类型都有其特定的输入设备驱动程序，但它们都使用相同的键盘事件驱动程序，从而确保对其用户的一致性接口。然而，与其他事件驱动程序相比，键盘事件驱动程序有一个独特特征：它将数据传递给另一个内核子系统（*tty* 层），而不是通过 `/dev` 节点传递到用户空间。

#### PC 键盘

PC 键盘（也称为 PS/2 键盘或 AT 键盘）通过 i8042 兼容的键盘控制器与处理器进行接口。台式机通常有专用的键盘控制器，但在笔记本电脑上，键盘接口是通用嵌入式控制器（参见第 20 章“更多设备和驱动程序”中的“嵌入式控制器”部分）的职责之一。当你按下 PC 键盘上的一个键时，它遵循的路径如下：

1.  键盘控制器（或嵌入式控制器）扫描并解码键盘矩阵，并处理按键去抖动等细微差别。

2.  键盘设备驱动程序在 *serio* 的帮助下，为每次按键和释放从键盘控制器读取原始*扫描码*。按键和释放之间的区别在于最高有效位，后者会将此位设置为 1。例如，按下“a”键会产生一对扫描码，`0x1e` 和 `0x9e`。特殊键使用 `0xE0` 进行转义，因此按下右箭头键会产生序列 (`0xE0 0x4D 0xE0 0xCD`)。你可以使用 `showkey` 实用程序来观察来自控制器的扫描码（`-->` 符号附加了解释）：

   ```bash
   bash> showkey -s
   kb mode was UNICODE
   [ if you are trying this under X, it might not work since
     the X server is also reading /dev/console ]

   press any key (program terminates 10s after last
   keypress)...
   ```

   ```c
   0x1e 0x9e --> A push of the "a" key
   ```

3.  键盘设备驱动程序根据输入模式将接收到的扫描码转换为键码。要查看与 "a" 键对应的键码：

   ```bash
   bash> showkey
   ```

   ```c
   keycode 30 press --> A push of the "a" key
   keycode 30 release --> Release of the "a" key
   ```

   为了将键码向上游报告，驱动程序生成一个输入事件，该事件将控制权传递给键盘事件驱动程序。

4.  键盘事件驱动程序根据加载的键映射执行键码转换。（参见 `loadkeys` 的手册页和 `/lib/kbd/keymaps/` 中存在的映射文件）。它检查转换后的键码是否绑定到切换虚拟控制台或重新启动系统等操作。为了响应 Ctrl+Alt+Del 按键组合时点亮 `CAPSLOCK` 和 `NUMLOCK` LED 指示灯而不是重新启动系统，请将以下内容添加到键盘事件驱动程序 `drivers/char/keyboard.c` 的 Ctrl+Alt+Del 处理器中：

   ```c
   static void fn_boot_it(struct vc_data *vc,
                          struct pt_regs *regs)
   {
   +   set_vc_kbd_led(kbd, VC_CAPSLOCK);
   +   set_vc_kbd_led(kbd, VC_NUMLOCK);
   -   ctrl_alt_del();
   }
   ```

5.  对于常规键，转换后的键码会被发送到关联的虚拟终端和 `N_TTY` 行规程。（我们在第 6 章“串行驱动程序”中讨论了虚拟终端和行规程。）`drivers/char/keyboard.c` 按以下方式完成此操作：

   ```c
   /* Add the keycode to flip buffer */
   tty_insert_flip_char(tty, keycode, 0);
   /* Schedule */
   con_schedule_flip(tty);
   ```

`N_TTY` 行规程处理从键盘接收到的输入，将其回显到虚拟控制台，并允许用户空间应用程序从连接到虚拟终端的 `/dev/ttyX` 节点读取字符。

图 7.3 展示了从你按下键盘上的一个键到该键在你的虚拟控制台上回显的数据流。图的左半部分是特定于硬件的，右半部分是通用的。按照输入子系统的设计目标，底层硬件接口对键盘事件驱动程序和 tty 层是透明的。输入核心和明确定义的事件接口因此将输入用户与硬件的复杂性隔离开来。

**图 7.3。来自 PS/2 兼容键盘的数据流。**

![](img/07cc6f9c8c74622020874f66bfb53dc4_201_0.png)
