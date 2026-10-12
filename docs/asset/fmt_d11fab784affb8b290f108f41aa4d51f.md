
`sudo apt-get update`

`sudo apt-get upgrade`

### 01 更新启动文件

在启动树莓派之前，将 Energenie IR 板连接到 GPIO 引脚。该板卡在引脚的顶部，如果未明确设置引脚，默认使用的 GPIO 引脚为：接收红外信号的输入引脚 = `PIN12`/`GPIO18`；发送红外信号的输出引脚 = `PIN11`/`GPIO17`。

然后，向`/boot/config.txt`文件添加一行代码，以启用 LIRC IR 软件，使 IR 模块能够交互。在 LX 终端中输入`sudo nano /boot/config.txt`。这将加载`config.txt`文件。滚动到文本底部，添加以下行：

```
dtoverlay-lirc-rpi-overlay
```

按 `Ctrl+X` 保存文件，然后输入`sudo reboot`重启树莓派。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_69_1.png)

### 你需要什么

- Pi-Mote IR 控制板 [bit.ly/1Mj3FQU](https://bit.ly/1Mj3FQU)
- 遥控机器人

![](img/0fc17bd4c29dc437e3ac28a53f7559db_70_0.png)

# 改装一台机器人

左侧：Pi-Mote 红外控制板功能强大，仅需 £9.99

### 02 安装软件

接下来，安装 LIRC 软件；这是 Linux 红外远程控制（Linux Infrared Remote Control）的缩写，它是让你能够与机器人交互并传输命令的程序。再次打开 LX 终端并输入：

```bash
sudo apt-get install lirc
sudo apt-get install lirc-x
```

安装完成后，你需要使用`sudo reboot`重启你的树莓派。

### 03 编辑硬件文件

接下来，我们需要编辑位于`/etc/lirc/`文件夹中的`lircd.hw.conf`文件，并进行如下所示的更改。在终端窗口中，输入：

```bash
sudo nano /etc/lirc/hardware.conf
```

在文件中找到`DRIVER`、`DEVICE`和`MODULES`行，然后进行以下更改：

```
DRIVER = "default"
DEVICE = "/dev/lirc0"
MODULES = "lirc_rpi"
```

按`Ctrl+X`保存文件，不要重命名它，按`Y`然后按`return`。使用命令`sudo /etc/init.d/lirc restart`重启 LIRC 守护进程。

### 04 测试红外接收器是否正常工作

为了测试红外接收器已正确安装并正常工作，你需要前往 LX 终端，然后停止 LIRC 守护进程（第 1 行），启用测试模式（第 2 行），然后启动模式 2 测试（第 3 行）：

```bash
sudo /etc/init.d/lirc stop
sudo modprobe lirc_rpi
sudo mode2 -d /dev/lirc0
```

这将运行一个程序来输出红外信号的占空比。它测量红外信号的脉冲和空档长度，并将值返回到终端。拿起机器人的遥控器，将其指向红外接收器，然后按下一些按钮。你应该会看到类似以下内容：

```
space 16300
pulse 95
space 28794
pulse 80
space 19395
space 28794
pulse 80
```

### 05 创建 lircd.conf 文件：第一部分

`lircd.conf`文件包含控制你设备的代码或指令。虽然你可以在网上找到这些文件，但你可能不得不从头创建一个。这需要运行`irrecord`程序，将遥控器对准红外板，然后按下按钮！这会记录来自你遥控器的信号，然后你为每个信号分配`KEYS`，以将信号传输给机器人。在终端中输入以下命令停止 LIRC 软件：

```bash
sudo /etc/init.d/lirc stop
```

### 06 创建 lircd.conf 文件：第二部分

接下来，创建你的新`lircd.conf`配置文件并保存输出。在 LX 终端中，输入：

```bash
irrecord -d /dev/lirc0 ~/lircd.conf
```

这将打开一个程序，该程序会提示你如何记录来自遥控器的信号的操作说明。第一部分需要你反复按下遥控器上的按钮，直到屏幕上出现两行点。这会测量并记录遥控器发送的信号。请按照逻辑顺序进行操作，从遥控器的顶部开始向下进行。一旦两行点完成，你的遥控器就被识别了。

### Pygame 按钮

Pygame 允许你创建按钮并为其分配操作。这意味着你可以为 Pygame 窗口创建并分配按钮。你可以使用按钮而不是按键来控制机器人。这里有一个简单的教程：`pygame.org/project-ButtonDrawer-2541.html`，涵盖了如何创建按钮并为各种按钮分配交互。

# 教程

![](img/0fc17bd4c29dc437e3ac28a53f7559db_71_0.png)

上方：你机器人上的红外接收器看起来大概是这样

### 机器人变体

- 你可以使用多种不同的机器人配合本教程，例如图中所示的 Makeblock 或作者使用的 WowWee Roboquad。请注意代码中的事件键设置——不同的机器人具有不同的原生功能。
- 例如，Roboquad 有一个“Dance”（跳舞）命令，你可以在对面页面上的代码列表中间部分看到它。

### 07 创建 lircd.conf 文件：第三部分

程序的第二部分要求你输入已记录的每个信号对应的键名。遵循每个屏幕提示，为每个遥控器按钮/键输入一个合适的名称。例如，输入“`KEY_UP`”，然后按下遥控器上对应的向上键。接下来你会被提示输入下一个键的名称——例如，“`KEY_BACK`”，在这种情况下，你需要按下遥控器上的返回键，以此类推。不断重复此过程，直到你为每个记录的键都输入了名称。

### 08 重命名遥控器

保存后，在`/home/pi`文件夹中找到新的`lirc.conf`文件。默认情况下，第 14 行的遥控器名称可能命名为`/home/pi/lirc.conf`。更改这一点：在“`begin remote`”标题下，找到“`name`”标签并将`/home/pi/lirc.conf`重命名为更合适的名称，例如“`Robot`”。这样做有助于确保在程序中调用移动指令或键名时，引用它变得更加容易。

### 09 传输 lircd.conf 文件

现在你的`lircd.conf`文件准备好传输到`/etc/lirc`文件夹；这是存放硬件和 lirc 文件的文件夹。最简单的方法是打开你的新`lircd.conf`（它保存在`/pi/home`文件夹中），然后复制并粘贴覆盖你刚刚创建的代码。但是，这会覆盖你现有的任何旧配置文件设置。要保存以前的文件，请参见下一步。在 LX 终端中，输入：

```bash
sudo nano /etc/lirc/lircd.conf
```

### 10 传输文件而不覆盖

如果你已经设置了`lircd.conf`文件，或者想使用新的但保留旧的，请创建一个新的配置文件。这保存在`/home/pi`文件夹中，并可以复制到`/etc/lirc`。通过创建一个副本并将另存为`lircd_original.conf`来备份原始的`lircd.conf`文件。在 LX 终端中，输入：

```bash
sudo cp /etc/init.d/lirc_start
sudo mv /etc/lirc/lircd.conf /etc/lirc/lircd_original.conf
```

然后复制你的新配置文件：

```bash
sudo cp ~/lircd.conf /etc/lirc/lircd.conf
```
